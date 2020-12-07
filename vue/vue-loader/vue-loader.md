# [Vue Loader](https://vue-loader.vuejs.org/zh/)

# 起步
## Vue CLI
如果你不想手动设置 ```webpack```，我们推荐使用 ```Vue CLI``` 直接创建一个项目的脚手架。通过 ```Vue CLI``` 创建的项目会针对多数常见的开发需求进行预先配置，做到开箱即用。

如果 ```Vue CLI``` 提供的内建没有满足你的需求，或者你乐于从零开始创建你自己的 ```webpack``` 配置，那么请继续阅读这篇指南。

## 手动设置
### 安装
你应该将 ```vue-loader``` 和 ```vue-template-compiler``` 一起安装——除非你是使用自行 fork 版本的 Vue 模板编译器的高阶用户：
```
npm install -D vue-loader vue-template-compiler
```

```vue-template-compiler``` 需要独立安装的原因是你可以单独指定其版本。

每个 ```vue``` 包的新版本发布时，一个相应版本的 ```vue-template-compiler``` 也会随之发布。编译器的版本必须和基本的 ```vue``` 包保持同步，这样 ```vue-loader``` 就会生成兼容运行时的代码。这意味着**你每次升级项目中的 ```vue``` 包时，也应该匹配升级 ```vue-template-compiler``` 。**

### webpack 配置
```Vue Loader``` 的配置和其它的 loader 不太一样。除了通过一条规则将 vue-loader 应用到所有扩展名为 .vue 的文件上之外，请确保在你的 ```webpack``` 配置中添加 ```Vue Loader``` 的插件：
```
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  module: {
    rules: [
      // ... 其它规则
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      }
    ]
  },
  plugins: [
    // 请确保引入这个插件！
    new VueLoaderPlugin()
  ]
}
```
**这个插件是必须的！** 它的职责是将你定义过的其它规则复制并应用到 ```.vue``` 文件里相应语言的块。例如，如果你有一条匹配``` /\.js$/ ```的规则，那么它会应用到``` .vue ```文件里的``` <script> ```块。
一个更完整的 webpack 配置示例看起来像这样：
```javascript
// webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')

module.exports = {
  mode: 'development',
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader'
      },
      // 它会应用到普通的 `.js` 文件
      // 以及 `.vue` 文件中的 `<script>` 块
      {
        test: /\.js$/,
        loader: 'babel-loader'
      },
      // 它会应用到普通的 `.css` 文件
      // 以及 `.vue` 文件中的 `<style>` 块
      {
        test: /\.css$/,
        use: [
          'vue-style-loader',
          'css-loader'
        ]
      }
    ]
  },
  plugins: [
    // 请确保引入这个插件来施展魔法
    new VueLoaderPlugin()
  ]
}
```
你也可以在选项参考查阅所有可用的 ```loader``` 选项。

> **警告**    
如果你在开发一个库或多项目仓库 (```monorepo```)，请注意导入 ```CSS``` **是具有副作用的**。请确保在 ```package.json``` 中**移除** ```"sideEffects": false```，否则 ```CSS ```代码块会在生产环境构建时被 ```webpack``` 丢掉。

-----------------------------------

# 处理资源路径
当 ```Vue Loader``` 编译单文件组件中的 ```<template>``` 块时，它也会将所有遇到的资源 ```URL``` 转换为 ```webpack``` **模块请求**。

例如，下面的模板代码片段：
```html
<img src="../image.png">
```
将会被编译成为：
```javascript
createElement('img', {
  attrs: {
    src: require('../image.png') // 现在这是一个模块的请求了
  }
})
```
默认下列标签/特性的组合会被转换，且这些组合时可以使用 ```transformAssetUrls``` 选项进行配置的。
```js
{
  video: ['src', 'poster'],
  source: 'src',
  img: 'src',
  image: ['xlink:href', 'href'],
  use: ['xlink:href', 'href']
}
```
此外，如果你配置了为``` <style>``` 块使用 ```css-loader```，则你的 ```CSS``` 中的资源 ```URL``` 也会被同等处理。

## 转换规则
资源 ```URL``` 转换会遵循如下规则：

- 如果路径是绝对路径 (例如 ```/images/foo.png```)，会原样保留。

- 如果路径以 ```.``` 开头，将会被看作相对的模块依赖，并按照你的本地文件系统上的目录结构进行解析。

- 如果路径以 ```~``` 开头，其后的部分将会被看作模块依赖。这意味着你可以用该特性来引用一个 ```Node``` 依赖中的资源：
```html
<img src="~some-npm-package/foo.png">
```
- 如果路径以 ```@``` 开头，也会被看作模块依赖。如果你的 ```webpack``` 配置中给 ```@``` 配置了 ```alias```，这就很有用了。所有 ```vue-cli``` 创建的项目都默认配置了将 ```@``` 指向 ```/src```。

## 相关的 Loader
因为像 ```.png``` 这样的文件不是一个 ```JavaScript``` 模块，你需要配置 ```webpack``` 使用 ```file-loader``` 或者 ```url-loader``` 去合理地处理它们。通过 ```Vue CLI``` 创建的项目已经把这些预配置好了。

## 为什么
转换资源 ```URL``` 的好处是：

```file-loader``` 可以指定要复制和放置资源文件的位置，以及如何使用版本哈希命名以获得更好的缓存。此外，这意味着 **你可以就近管理图片文件，可以使用相对路径而不用担心部署时 ```URL``` 的问题**。使用正确的配置，```webpack``` 将会在打包输出中自动重写文件路径为正确的 ```URL```。

```url-loader ```允许你有条件地将文件转换为内联的 ```base-64 URL``` (当文件小于给定的阈值)，这会减少小文件的 ```HTTP``` 请求数。如果文件大于该阈值，会自动的交给 ```file-loader``` 处理。

-------------------------------------

# Scoped CSS
当 ```<style>``` 标签有 ```scoped``` 属性时，它的 ```CSS``` 只作用于当前组件中的元素。这类似于 ```Shadow DOM``` 中的样式封装。它有一些注意事项，但不需要任何 ```polyfill```。它通过使用 ```PostCSS``` 来实现以下转换：
```html
<style scoped>
.example {
  color: red;
}
</style>

<template>
  <div class="example">hi</div>
</template>
```
转换结果：
```html
<style>
.example[data-v-f3f3eg9] {
  color: red;
}
</style>

<template>
  <div class="example" data-v-f3f3eg9>hi</div>
</template>
```
## 混用本地和全局样式
你可以在一个组件中同时使用有``` scoped``` 和非 ```scoped``` 样式：
```html
<style>
/* 全局样式 */
</style>

<style scoped>
/* 本地样式 */
</style>
```
## 子组件的根元素
使用 ```scoped``` 后，父组件的样式将不会渗透到子组件中。**不过一个子组件的根节点会同时受其父组件的 ```scoped CSS``` 和子组件的 ```scoped CSS``` 的影响**。这样设计是为了让父组件可以从布局的角度出发，调整其子组件根元素的样式。

## 深度作用选择器
如果你希望 ```scoped``` 样式中的一个选择器能够作用得“更深”，例如影响子组件，你可以使用 ```>>>``` 操作符：
```html
<style scoped>
.a >>> .b { /* ... */ }
</style>
```
上述代码将会编译成：
```css
.a[data-v-f3f3eg9] .b { /* ... */ }
```
有些像 ```Sass``` 之类的预处理器无法正确解析 ```>>>```。这种情况下你可以使用 ```/deep/``` 或 ```::v-deep``` 操作符取而代之——两者都是 ```>>>``` 的别名，同样可以正常工作。

## 动态生成的内容
通过 ```v-html``` 创建的 ```DOM``` 内容不受 ```scoped``` 样式影响，但是你仍然可以通过深度作用选择器来为他们设置样式。

## 还有一些要留意
- **```Scoped``` 样式不能代替 ```class```。** 考虑到浏览器渲染各种 CSS 选择器的方式，当 ```p { color: red }``` 是 ```scoped``` 时 (即与特性选择器组合使用时) 会慢很多倍。如果你使用 ```class``` 或者 ```id``` 取而代之，比如 ```.example { color: red }```，性能影响就会消除。

- **在递归组件中小心使用后代选择器!** 对选择器``` .a .b ```中的``` CSS ```规则来说，如果匹配 ```.a``` 的元素包含一个递归子组件，则所有的子组件中的 ```.b``` 都将被这个规则匹配。

------------------------------

# CSS Modules
[CSS Modules](https://github.com/css-modules/css-modules) 是一个流行的，用于模块化和组合 ```CSS``` 的系统。```vue-loader``` 提供了与 ```CSS Modules``` 的一流集成，可以作为模拟 ```scoped CSS``` 的替代方案。

## 用法
首先，```CSS Modules``` 必须通过向 ```css-loader``` 传入 ```modules: true``` 来开启：
```js
// webpack.config.js
{
  module: {
    rules: [
      // ... 其它规则省略
      {
        test: /\.css$/,
        use: [
          'vue-style-loader',
          {
            loader: 'css-loader',
            options: {
              // 开启 CSS Modules
              modules: true,
              // 自定义生成的类名
              localIdentName: '[local]_[hash:base64:8]'
            }
          }
        ]
      }
    ]
  }
}
```
然后在你的 ```<style>``` 上添加 ```module``` 特性：
```html
<style module>
.red {
  color: red;
}
.bold {
  font-weight: bold;
}
</style>
```
这个 ```module``` 特性指引 ```Vue Loader``` 作为名为 ```$style``` 的计算属性，向组件注入 ```CSS Modules``` 局部对象。然后你就可以在模板中通过一个动态类绑定来使用它了：
```html
<template>
  <p :class="$style.red">
    This should be red
  </p>
</template>
```
因为这是一个计算属性，所以它也支持 ```:class``` 的对象/数组语法：
```html
<template>
  <div>
    <p :class="{ [$style.red]: isRed }">
      Am I red?
    </p>
    <p :class="[$style.red, $style.bold]">
      Red and bold
    </p>
  </div>
</template>
```
你也可以通过 ```JavaScript``` 访问到它：
```html
<script>
export default {
  created () {
    console.log(this.$style.red)
    // -> "red_1VyoJ-uZ"
    // 一个基于文件名和类名生成的标识符
  }
}
</script>
```
你可以查阅 [CSS Modules](https://github.com/css-modules/css-modules) 规范了解更多细节，诸如 [global exceptions](https://github.com/css-modules/css-modules#exceptions) 和 [composition](https://github.com/css-modules/css-modules#composition) 等。

## 可选用法
如果你只想在某些 ```Vue``` 组件中使用 ```CSS Modules```，你可以使用 ```oneOf``` 规则并在 ```resourceQuery``` 字符串中检查 ```module``` 字符串：
```js
// webpack.config.js -> module.rules
{
  test: /\.css$/,
  oneOf: [
    // 这里匹配 `<style module>`
    {
      resourceQuery: /module/,
      use: [
        'vue-style-loader',
        {
          loader: 'css-loader',
          options: {
            modules: true,
            localIdentName: '[local]_[hash:base64:5]'
          }
        }
      ]
    },
    // 这里匹配普通的 `<style>` 或 `<style scoped>`
    {
      use: [
        'vue-style-loader',
        'css-loader'
      ]
    }
  ]
}
```
## 和预处理器配合使用
```CSS Modules``` 可以与其它预处理器一起使用：
```js
// webpack.config.js -> module.rules
{
  test: /\.scss$/,
  use: [
    'vue-style-loader',
    {
      loader: 'css-loader',
      options: { modules: true }
    },
    'sass-loader'
  ]
}
```
## 自定义的注入名称
在 ```.vue``` 中你可以定义不止一个``` <style>```，为了避免被覆盖，你可以通过设置 ```module``` 属性来为它们定义注入后计算属性的名称。
```html
<style module="a">
  /* 注入标识符 a */
</style>

<style module="b">
  /* 注入标识符 b */
</style>
```

------------------------------------

# 热重载
