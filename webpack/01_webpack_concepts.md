# [webpack 概念](https://www.webpackjs.com/concepts/)

本质上，<span style="background: #f0150b; padding: .1rem; font-weight: 700;">```webpack``` 是一个现代 ```JavaScript``` 应用程序的静态模块打包器(```module bundler```)。</span>

当 ```webpack``` 处理应用程序时，它会递归地构建一个**依赖关系图(```dependency graph```)**，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 ```bundle```。

> 可以从[这里](#模块(modules))了解更多关于 ```JavaScript``` 模块和 ```webpack``` 模块的信息。

从 ```webpack v4.0.0``` 开始，可以不用引入一个配置文件。然而，```webpack``` 仍然还是[高度可配置](./02_webpack_config.md)的。在开始前你需要先理解四个核心概念：

- 入口(```entry```)
- 输出(```output```)
- ```loader```
- 插件(```plugins```)

本文档旨在给出这些概念的高度概述，同时提供具体概念的详尽相关用例。

## 入口(entry)
**入口起点(```entry point```)**指示 ```webpack``` 应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，```webpack``` 会找出有哪些模块和库是入口起点（直接和间接）依赖的。

每个依赖项随即被处理，最后输出到称之为 ```bundles``` 的文件中，我们将在下一章节详细讨论这个过程。

可以通过在 [webpack 配置](./02_webpack_config.md)中配置``` entry ```属性，来指定一个入口起点（或多个入口起点）。默认值为 ```./src```。

接下来我们看一个 ```entry``` 配置的最简单例子：

```webpack.config.js```
```
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```
> 根据应用程序的特定需求，可以以多种方式配置 ```entry``` 属性。从**入口起点**章节可以了解更多信息。


# 入口起点(entry points)
# 输出(output)
# 模式(mode)
# loader
# 插件(plugins)
# 配置(configuration)
# 模块(modules)
# 模块解析(module resolution)
# 依赖图(dependency graph)
# manifest
# 构建目标(targets)
# 模块热替换(hot module repla