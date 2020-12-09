# 代码高亮工具[```highlight.js```](https://highlightjs.org/)
> [API文档](https://highlightjs.readthedocs.io/en/latest/index.html)
--------------------

# 目录
- [如何使用Highlight.js](#如何使用Highlight.js)
- [与Vue.js一起使用](#与Vue.js一起使用)
- [在vue中的应用](#在vue中的应用)

--------------------

# 如何使用Highlight.js
## 入门
在网页上使用```highlight.js```的最基本要求是链接到库以及其中一种样式并调用```initHighlightingOnLoad```：
```html
<link rel="stylesheet" href="/path/to/styles/default.css">
<script src="/path/to/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>
```
这将在```<pre><code>```标签内查找并突出显示代码；它会尝试自动检测语言。如果自动检测对您不起作用，则可以在```class```属性中指定语言：
```html
<pre><code class="html">...</code></pre>
```
```class```也可以以```language-```或前缀```lang-```。
```html
<pre><code class="language-html">...</code></pre>
```

## 纯文本和禁用突出显示
要设置任意文本的样式，例如代码，但不突出显示，```class```属性请使用 ```plaintext```：
```html
<pre><code class="plaintext">...</code></pre>
```
要完全禁用标签的突出显示，```class``请使用```nohighlight```类：
```html
<pre><code class="nohighlight">...</code></pre>
```
## 支持的语言
```Highlight.js```在核心库中支持超过180种不同的语言。也有第三方语言插件可用于其他语言。您可以在[```SUPPORTED_LANGUAGES.md```](https://github.com/highlightjs/highlight.js/blob/master/SUPPORTED_LANGUAGES.md)中找到支持的语言的完整列表。

# 自定义初始化
当需要对```Highlight.js```的初始化进行更多控制时，可以使用[```highlightBlock```](https://highlightjs.readthedocs.io/en/latest/api.html#highlightblock-block)和[```configure```](https://highlightjs.readthedocs.io/en/latest/api.html#configure-options) 函数。这可以让你控制什么突出和时。

这是[```initHighlightingOnLoad```](https://highlightjs.readthedocs.io/en/latest/api.html#inithighlightingonload)使用普通```JS```调用的等效方法：
```js
document.addEventListener('DOMContentLoaded', (event) => {
  document.querySelectorAll('pre code').forEach((block) => {
    hljs.highlightBlock(block);
  });
});
```
您可以使用任何标签代替```<pre><code>```标记代码。如果您不使用保留换行符的容器，则需要配置```highlight.js```以使用```<br>```标记：
```js
hljs.configure({useBR: true});

document.querySelectorAll('div.code').forEach((block) => {
  hljs.highlightBlock(block);
});
```
有关其他选项，请参阅的文档[```configure```](https://highlightjs.readthedocs.io/en/latest/api.html#configure-options)。

# 与Vue.js一起使用
只需在Vue中注册插件：
```js
Vue.use(hljs.vuePlugin);
```
您将获得一个```highlightjs```可在模板中使用的组件：
```html
  <div id="app">
    <!-- bind to a data property named `code` -->
    <highlightjs autodetect :code="code" />
    <!-- or literal code works as well -->
    <highlightjs language='javascript' code="var x = 5;" />
  </div>
```
# 网络工作者
您可以在网络工作者中运行突出显示功能，以避免在处理非常大的代码块时冻结浏览器窗口。

在您的主脚本中：
```js
addEventListener('load', () => {
  const code = document.querySelector('#code');
  const worker = new Worker('worker.js');
  worker.onmessage = (event) => { code.innerHTML = event.data; }
  worker.postMessage(code.textContent);
});
```
在```worker.js```中：
```js
onmessage = (event) => {
  importScripts('<path>/highlight.min.js');
  const result = self.hljs.highlightAuto(event.data);
  postMessage(result.value);
};
```
# Node.js
您可以在节点上使用```highlight.js```突出显示内容，然后再将其发送到浏览器。确保使用该```.value```属性获取格式化的html。有关返回的对象的更多信息，请参阅```api docs``` https://highlightjs.readthedocs.io/en/latest/api.html
```js
// require the highlight.js library, including all languages
const hljs = require('./highlight.js');
const highlightedCode = hljs.highlightAuto('<span>Hello World!</span>').value
```
或者占用较小的空间...仅加载所需的语言。
```js
const hljs = require("highlight.js/lib/core");  // require only the core library
// separately require languages
hljs.registerLanguage('xml', require('highlight.js/lib/languages/xml'));

const highlightedCode = hljs.highlight('xml', '<span>Hello World!</span>').value
```

# ES6模块
首先，您可能会通过```npm```或```yarn```-安装，请参阅下面的[获取库](https://highlightjs.org/usage/#getting-the-library)。

在您的应用程序中：
```js
import hljs from 'highlight.js';
```
默认导入将导入所有语言。因此，仅导入所需的库和语言可能会更有效：
```js
import hljs from 'highlight.js/lib/core';
import javascript from 'highlight.js/lib/languages/javascript';
hljs.registerLanguage('javascript', javascript);
```
要设置语法突出显示样式，如果构建工具从JavaScript入口点处理CSS，则还可以将样式表直接导入为模块：
```js
import hljs from 'highlight.js/lib/core';
import 'highlight.js/styles/github.css';
```

# 获取Library
您可以将```Highlight.js```作为托管或自定义构建的浏览器脚本或作为服务器模块来获取。即开即用的浏览器脚本同时支持```AMD```和```CommonJS```，因此，如果您希望可以使用```RequireJS```或```Browserify```，而无需从源代码进行构建。服务器模块也可以与```Browserify```完美配合，但是可以选择使用特定于浏览器的版本，而不是用于服务器的版本。

**不要直接链接到```GitHub```。**该库不应该直接从源头工作，它需要构建。如果没有任何预包装的选项对您有效，请参考建筑文档。

**在```Almond```上**。您需要使用优化器为模块命名。例如：
```sh
r.js -o name=hljs paths.hljs=/path/to/highlight out=highlight.js
```

## CDN托管
以下CDN托管了与许多常用语言捆绑在一起的highlight.js的预构建版本：

### [cdnjs](https://cdnjs.com/libraries/highlight.js)
```html
<link rel="stylesheet"
      href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/10.4.1/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/10.4.1/highlight.min.js"></script>
<!-- and it's easy to individually load additional languages -->
<script charset="UTF-8"
 src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/10.4.1/languages/go.min.js"></script>
```
### [jsdelivr](https://www.jsdelivr.com/package/gh/highlightjs/cdn-release)
```html
<link rel="stylesheet"
      href="//cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.4.1/build/styles/default.min.css">
<script src="//cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.4.1/build/highlight.min.js"></script>
```
### [unpkg](https://unpkg.com/browse/@highlightjs/cdn-assets@10.4.1/)
```html
<link rel="stylesheet" href="https://unpkg.com/@highlightjs/cdn-assets@10.4.1/styles/default.min.css">
<script src="https://unpkg.com/@highlightjs/cdn-assets@10.4.1/highlight.min.js"></script>
```
> **注意**： ```CDN```托管的```highlight.min.js```软件包不会捆绑所有语言。会很大。您可以在下载页面上找到默认情况下捆绑的列表“常用”语言。

## 自托管
该下载页面可以快速生成仅包括您所需要的语言定制的捆绑。

或者，您可以从源代码构建浏览器程序包：
```sh
node tools/build.js -t browser :common
```
有关更多信息，请参见我们的[构建文档](http://highlightjs.readthedocs.io/en/latest/building-testing.html)。

> **注意**：从源代码构建应始终导致最小的构建。网站下载页面针对速度而非大小进行了优化。

## 预建CDN资产
您还可以下载并通过我们自己的```CDN```自托管我们提供的相同资产。我们将这些构建发布到[```cdn-release```](https://github.com/highlightjs/cdn-release) ```GitHub```存储库中。您可以使用等轻松地将单个文件从```CDN```端点中拉出```curl```。如果说您只需要```highlight.min.js```一个```CSS```文件。

还有一个```npm```包[```@ highlightjs / cdn-assets```](https://www.npmjs.com/package/@highlightjs/cdn-assets)，如果通过```via```提取资产，```npm```或者```yarn```对于您的构建过程来说更容易。

## NPM / Node.js服务器模块
```Highlight.js```也可以在服务器上使用。可以从```NPM```或```Yarn```安装具有所有受支持语言的软件包：
```sh
npm install highlight.js
# or
yarn add highlight.js
```
或者，您可以从源代码构建它：
```sh
node tools/build.js -t node
```
有关更多信息，请参见我们的[构建文档](https://highlightjs.readthedocs.io/en/latest/building-testing.html)。

## 资源
[当前源](https://github.com/highlightjs/)始终在```GitHub```上可用。

## 执照
```Highlight.js```是在```BSD```许可下发布的。有关详细信息，请参见[LICENSE](https://github.com/highlightjs/highlight.js/blob/master/LICENSE)文件。

## 链接
该库的官方网站是https://highlightjs.org/。

有关API和其他主题的更多深入文档，请 参见http://highlightjs.readthedocs.io/。

作者和贡献者列在[AUTHORS.txt](https://github.com/highlightjs/highlight.js/blob/master/AUTHORS.txt)文件中。


---------

# 在vue中的应用
> https://www.jianshu.com/p/e35f6d62b3bd
在 ```vue-cli3``` 项目中，通过```highlight.js```，实现页面中代码高亮。

请先了解```highlight.js```官网中的使用说明。

### **安装**
```sh
npm install highlight.js --save
```
### **封装成vue插件**

[官方文档---自定义插件](https://cn.vuejs.org/v2/guide/plugins.html)

[官方文档---自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

新建```highlight.js```文件，并添加：
```js
// src/utils/highlight.js 文件路径，纯属自定义

// highlight.js  代码高亮指令
import Hljs from 'highlight.js';
import 'highlight.js/styles/tomorrow-night.css'; // 代码高亮风格，选择更多风格需导入 node_modules/hightlight.js/styles/ 目录下其它css文件

let Highlight = {};
// 自定义插件
Highlight.install = function (Vue) {
    // 自定义指令 v-highlight
    Vue.directive('highlight', {
        // 被绑定元素插入父节点时调用
        inserted: function(el) {
            let blocks = el.querySelectorAll('pre code');
            for (let i = 0; i < blocks.length; i++) {
                Hljs.highlightBlock(blocks[i]);
            }
        },
        // 指令所在组件的 VNode 及其子 VNode 全部更新后调用
        componentUpdated: function(el) {
            let blocks = el.querySelectorAll('pre code');
            for (let i = 0; i < blocks.length; i++) {
                Hljs.highlightBlock(blocks[i]);
            }
        }
    })
};

export default Highlight;
```
### **全局引入自定义插件**
在```src/main.js```中：
```js
// highlight.js代码高亮插件
import Highlight from './utils/highlight'; // from 路径是highlight.js的路径，纯属自定义
Vue.use(Highlight);
```
### **使用**
```html
<div id="codeView" v-highlight>
    <pre><code v-html="code"></code></pre>
</div>
```
```code```是代码的字符串形式，比如：
```js
"0x0000000000400da0 <+0>:\tpush\t%rbx\n0x0000000000400da1 <+1>:\tcmp\t$0x1,%edi\n0x0000000000400da4 <+4>:\tjne\t0x400db6 <main+22>\n"
```
更换更多的代码高亮风格，需要切换```highlight.js```中导入的```css```文件。

