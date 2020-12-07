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