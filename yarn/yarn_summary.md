## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">总结</span>
-----
> [软件包管理](https://www.yarnpkg.com.cn/)

> [yarn文档](https://yarn.bootcss.com/docs/)

> [yarn CLI](https://yarn.bootcss.com/docs/cli/)

> [版本管理：node-semver](https://github.com/npm/node-semver)   
> [版本管理计算器：npm semver calculator](https://semver.npmjs.com/)
---------------------------------------------

### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">文件</span>
> [```package.json说明文档```](https://yarn.bootcss.com/docs/package-json/)     
> [其他文件说明](./yarn.md/#其他文件)

```package.json```
```json
{
    /* 必要字段 */
    "name": <project-name: string>,
    "version": <version: string>,
    /* 信息字段 */
    "description": <description: string>,
    "keywords": <keywords: array of string>,
    "license": <license: string>,
    /* 链接字段 */
    "homepage": <homepage: url>,
    "bugs": <bugs: url>,
    "repository": {
        type: "git",
        url: <url: url>
    },
    /* 维护者字段 */
    "author": {
        "name": <name: string>,
        "email": <email: email>,
        "url": <url: url>"
    },
    /* 贡献者字段 */
    "contributors": [
        {
            "name": <name: string>,
            "email": <email: email>,
            "url": <url: url>"
        }
    ],
    /* 文件字段 */
    // 包含文件
    "files": [
        <file: string>, 
        <directory/: string>,
        "glob/*.{js,json}"
    ],
    // 项目入口文件
    "main": <file: string>,
    // 可执行文件
    "bin": {
        <filename: string>: <href: string>
    },
    // 手册文件
    "man": [<file:string>],
    // 指定确切的位置放置文件
    "directories": {
        "lib": "path/to/lib/",
        "bin": "path/to/bin/",
        "man": "path/to/man/",
        "doc": "path/to/doc/",
        "example": "path/to/example/"
    },
    /* 任务字段 */
    "scripts": {
        <commandname: string>: <command: string>
    },
    "config": {
        "port": "8080"
    },
    /* 依赖字段 */
    "dependencies": {
        <package>: <version|tag: string>,
        <package>: <[^, >, <, >=, <=]version: string>
    },
    "devDependencies": {
        <package>: <version|tag: string>,
        <package>: <[^, >, <, >=, <=]version: string>
    },
    "peerDependencies": {
        <package>: <version|tag: string>,
        <package>: <[^, >, <, >=, <=]version: string>
    },
    "optionalDependencies": {
        <package>: <version|tag: string>,
        <package>: <[^, >, <, >=, <=]version: string>
    },
    "bundledDependencies": {
        <package>: <version|tag: string>,
        <package>: <[^, >, <, >=, <=]version: string>
    },
    "flat": <true|false>,
    // 覆盖特定嵌套依赖项的版本
    "resolutions": {
        <package>: <version|tag>
    },
    /* 系统字段 */
    "engines": {
        "node": <[^, >, <, >=, <=]version: string>,
        "zlib": <[^, >, <, >=, <=]version: string>,
        "yarn": <[^, >, <, >=, <=]version: string>"
    },
    "os": ["darwin", "linux", "!win32"],
    "cpu": ["x64", "ia32", "!arm", "!mips"],
    /* 发布字段 */
    "private": <true|false>,
    "publishConfig": {
        ...
    }
}
```
### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">依赖类型</span>
| 依赖类型 | 说明 |
|-|-|
| dependencies | 常规依赖：运行时 |
| devDependencies | 开发依赖：开发工作流中 |
| peerDependencies | 对等依赖：发布自己程序包时 |
| optionalDependencies | 可选依赖：后备 |
| bundledDependencies | 捆绑依赖：发布程序时捆绑的依赖 |
|||
### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">版本</span>
Semantic Versioning
> ```major.minor.patch```     
> 主要.次要.修补

| ranges | 说明 |
|-|-|
| ```<, <=, >, >=, =``` | comparators：对比器 |
| ```空格``` | comparators set：交集(intersection)，并集(union) |
| ```tag``` | 预发布标签(Pre-release tags)：```3.1.4-beta.2``` |
| ```-``` | 连续闭区间 |
| ```x``` | x所在级的前一级的一个版本左闭右开区间：```3.1```等于```3.1.x```等于```>=3.1.0 <3.2.0``` |
| ```~``` | ```minor```的一个版本左闭右开区间：```3.1```等于```3.1.x```，```~3```等于```3.x``` |
| ```^``` | 第一个非零版本号的左闭右开区间：```0.4.2```等于```>=0.4.2 <0.5.0``` |
| ```*或空字串``` | 所有版本 |
|||

### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">命令</span>
> [详细清单](./yarn.md/#CLI命令)


### **初始化**
```
yarn init
```

### **添加依赖项**
```
yarn add [package]
yarn add --dev [package]@[]
yarn add --peer [package]@[version]
yarn add --optional [package]@[tag]
```
### **升级依赖项**
```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```
### **删除依赖项**
```
yarn remove [package]
```
### **安装依赖**
```bash
yarn或yarn install          # 安装所有依赖项
yarn install --flat         # 安装软件包的一个版本和唯一一个版本
yarn install --force        # 强制重新下载所有软件包
yarn install --production   # 仅安装生产依赖项 
```
### **发布软件包**
```bash
yarn publish    # 将软件包发布到软件包管理器。
```