# <span style="background: #f0150b; padding: .5rem; font-weight: 700;">详细教程</span>
---------------------------------------------
# 快速入门
> https://yarn.bootcss.com/docs/getting-started/

> ```Yarn```对你的代码来说是一个<span style="background: #f0150b; padding: .5rem; font-weight: 700;">包管理器</span>。

它可以让你使用并分享全世界开发者的（例如 JavaScript）代码。 Yarn 能够快速、安全、 并可靠地完成这些工作，所以你不用有任何担心。

通过Yarn你可以使用其他开发者针对不同问题的解决方案，使自己的开发过程更简单。 使用过程中遇到问题，你可以将其上报或者贡献解决方案。一旦问题被修复， Yarn会更新保持同步。

> 代码通过**包（```package```）** (或者称为**模块（```module```）**) 的方式来共享。 一个包里包含所有需要共享的代码，以及描述包信息的文件，称为 ```package.json``` 。

## 安装
> https://yarn.bootcss.com/docs/install/#windows-stable     

> **前提**: 安装```Node.js```

Linux(CentOS)
> ```sudo yum install yarn```       
> ```yarn --version```

Window
- [直接下载安装](https://classic.yarnpkg.com/latest.msi)
- [Chocolatey](https://chocolatey.org/) 安装
    > ```choco install yarn```
- [Scoop](https://scoop.sh/) 安装
    > ```scoop install yarn```

## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">使用方法</span>
> https://yarn.bootcss.com/docs/usage/

### 初始化一个新项目
```
yarn init
```
### 添加依赖包
```
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
```
### 将依赖项添加到不同依赖项类别中
> 分别添加到 ```devDependencies```、```peerDependencies```和 ```optionalDependencies``` 类别中：
```
yarn add [package] --dev
yarn add [package] --peer
yarn add [package] --optional
```
### 升级依赖包
```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```
### 移除依赖包
```
yarn remove [package]
```
### 安装项目的全部依赖
```
yarn
或者
yarn install
```



-----------------------------------------


# yarn工作流
将包管理器引入到项目中会引入一个围绕依赖关系的新工作流。 Yarn 尽最大努力不让你感知它的存在，并让工作流中的每一步 都易于理解。

<span style="background: #f0150b; padding: .5rem; font-weight: 700;">关于基本工作流程，您应该了解以下几点</span>：
1. 创建一个新项目
2. 添加/更新/删除依赖项
3. 安装/重新安装依赖项
4. 使用版本管理工具（例如 git）
5. 持续集成

## 创建一个新项目
无论您是否已有代码存储库/目录，还是正在启动一个全新的项目，每次添加```Yarn```的方式都相同。

在您要添加```Yarn```的目录（几乎应始终是项目的根目录）的终端/控制台中，运行以下命令：
> ```yarn init```

这将打开一个交互式表单，用于创建一个新的纱线项目，涉及以下问题：
```
name (your-project):
version (1.0.0):
description:
entry point (index.js):
git repository:
author:
license (MIT):
```
您可以为每个答案输入答案，也可以按Enter / Return键使用默认值或将其保留为空白。

### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">```package.json```</span>
现在，您应该拥有一个```package.json```类似于以下内容的：
```
{
  "name": "my-new-project",
  "version": "1.0.0",
  "description": "My New Project description.",
  "main": "index.js",
  "repository": {
    "url": "https://example.com/your-username/my-new-project",
    "type": "git"
  },
  "author": "Your Name <you@example.com>",
  "license": "MIT"
}
```
运行时```yarn init```，所有要做的就是创建此文件。在后台没有任何反应。您可以随意编辑该文件。

您```package.json```用于存储有关您的项目的信息。这包括项目的名称，维护者，源代码所在的位置，但最重要的是，需要为项目安装哪些依赖项。

## 管理依赖
当您要添加，升级或删除依赖项时，需要了解几个不同的命令。

> **每个命令将自动更新您的 ```package.json```和 ```yarn.lock```文件**。

### **添加依赖项**
如果要使用另一个软件包，则首先需要将其添加为依赖项。为此，您应该运行：
```
yarn add [package]
```
这将自动将添加```[package]```到您的依赖中 ```package.json```。它还会更新您的内容```yarn.lock```以反映更改。
```javascript
  {
    "name": "my-package",
    "dependencies": {
+     "package-1": "^1.0.0"
    }
  }
 ``` 
您还可以使用标志添加其他 类型的依赖项：
```javascript
yarn add --dev 添加到 devDependencies
yarn add --peer 添加到 peerDependencies
yarn add --optional 添加到 optionalDependencies
```
您可以通过指定依赖项版本或 标记来指定要安装的软件包版本。
```javascript
yarn add [package]@[version]
yarn add [package]@[tag]
```
的```[version]```或```[tag]```将是什么被添加到您的```package.json``` ，然后解决安装时依赖对。

例如：
```javascript
yarn add package-1@1.2.3
yarn add package-2@^1.0.0
yarn add package-3@beta
{
  "dependencies": {
    "package-1": "1.2.3",
    "package-2": "^1.0.0",
    "package-3": "beta"
  }
}
```
### **升级依赖**
```
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
```
这将升级您```package.json```和您的```yarn.lock```文件。
```javascript
  {
    "name": "my-package",
    "dependencies": {
-     "package-1": "^1.0.0"
+     "package-1": "^2.0.0"
    }
  }
```
### **删除依赖**
```
yarn remove [package]
```
这将更新您```package.json```和您的```yarn.lock```文件。


## 安装依赖
如果刚刚从版本控制中签出了软件包，则需要安装这些依赖项。

如果要为项目添加依赖项，则这些依赖项将在该过程中自动安装。

### **安装依赖项**
```yarn install```用于安装项目的所有依赖项。从项目```package.json```文件中检索依赖关系，并将其存储在```yarn.lock```文件中。

开发软件包时，安装依赖项通常是在执行以下操作：

您刚刚签出了需要这些依赖项才能起作用的项目的代码。
该项目的另一位开发人员添加了一个新的依赖项，您需要对其进行选择。
### **安装选件**
有许多安装依赖项的选项，包括：
- 安装所有依赖项：```yarn```或```yarn install```
- 安装软件包的一个版本和唯一一个版本： ```yarn install --flat```
- 强制重新下载所有软件包： ```yarn install --force```
- 仅安装生产依赖项： ```yarn install --production```
- 查看您可以传递给的标志的完整列表```yarn install```。

## 与版本管理工具协同工作
为了使人们成功开发或使用您的软件包，您需要确保将所有必需的文件都签入源代码控制系统。

### **所需文件**
必须将以下文件检入源代码管理中，以便任何人都可以管理您的程序包：

- ```package.json```：这具有您软件包的所有当前依赖关系。
- ```yarn.lock```：这将为您的软件包存储每个依赖项的确切版本。
- 提供软件包功能的实际源代码。

## 持续集成
> Continuous Integration: https://yarn.bootcss.com/docs/install-ci/

---------------------------------------------


# CLI命令
- [```yarn add```](https://yarn.bootcss.com/docs/cli/add)：安装软件包及其依赖的任何软件包。
- [```yarn audit  [--verbose] [--json] [--level] [--groups]```](https://yarn.bootcss.com/docs/cli/audit)：对已安装的软件包执行漏洞审核。
- [```yarn autoclean  [-I/--init] [-F/--force]```](https://yarn.bootcss.com/docs/cli/autoclean)：从程序包依赖项中清除并删除不必要的文件。
- [```yarn bin [<executable>]```](https://yarn.bootcss.com/docs/cli/bin)：显示```yarn bin```文件夹的位置。
- [```yarn cache```](https://yarn.bootcss.com/docs/cli/cache)：软件包存储在文件系统上用户目录中的全局缓存。
- [```yarn check [--integrity]|[--verify-tree]```](https://yarn.bootcss.com/docs/cli/check)：验证当前项目中的程序包依赖项版本是否```package.json```与```yarn```的锁定文件中的程序包依赖项版本匹配。
- [```yarn config```](https://yarn.bootcss.com/docs/cli/config)：管理```yarn```配置文件。
- [```yarn create <starter-kit-package> [<args>]```](https://yarn.bootcss.com/docs/cli/create)：从任何create-*入门工具包创建新项目。
- [```yarn dedupe```](https://yarn.bootcss.com/docs/cli/dedupe)：不需要重复数据删除命令。```yarn install```将已经重复数据删除。
- [```yarn generate-lock-entry```](https://yarn.bootcss.com/docs/cli/generate-lock-entry)：生成一个锁定文件条目。
- [```yarn global <add/bin/list/remove/upgrade> [--prefix]```](https://yarn.bootcss.com/docs/cli/global)：在操作系统上全局安装软件包。
- [```yarn help```](https://yarn.bootcss.com/docs/cli/help)：显示帮助信息。
- [```yarn import```](https://yarn.bootcss.com/docs/cli/import)：生成```yarn.lock```从npm的```package-lock.json```文件在相同的位置文件或npm已安装过的```node_modules```文件夹。
- [```yarn info <package> [<field>]```](https://yarn.bootcss.com/docs/cli/info)：显示有关包的信息。
- [```yarn init [--yes/-y]|[--private/-p]```](https://yarn.bootcss.com/docs/cli/init)：交互式创建或更新```package.json```文件。
- [```yarn install```](https://yarn.bootcss.com/docs/cli/install)：用于安装项目的所有依赖项。
- [```yarn licenses list|generate-disclaimer```](https://yarn.bootcss.com/docs/cli/licenses)：列出已安装软件包的许可证。
- [```yarn link [package...]```](https://yarn.bootcss.com/docs/cli/link)：开发过程中符号链接软件包文件夹。
- [```yarn list [--depth] [--pattern]```](https://yarn.bootcss.com/docs/cli/list)：列出已安装的软件包。
- [```yarn lockfile```](https://yarn.bootcss.com/docs/cli/lockfile)：不需要使用```lockfile```命令。```yarn install```将产生一个锁文件。
- [```yarn login```](https://yarn.bootcss.com/docs/cli/login)：存储您在 ```registry``` 上的用户名和 ```email``` 。
- [```yarn logout```](https://yarn.bootcss.com/docs/cli/logout)：清除你在 ```registry``` 上用户名和 ```email``` 。
- [```yarn outdated [package...]```](https://yarn.bootcss.com/docs/cli/outdated)：检查过时的软件包依赖项。
- [```yarn owner [list <package>]|[add/remove <user> <package>]```](https://yarn.bootcss.com/docs/cli/owner)：管理软件包所有者。
- [```yarn pack [--filename <filename>]```](https://yarn.bootcss.com/docs/cli/pack)：创建软件包依赖项的压缩gzip存档(并将文件名命名为```filename```)。
- [```yarn policies [set-version]```](https://yarn.bootcss.com/docs/cli/policies)：为您的项目定义整个项目的政策。
- [```yarn prune```](https://yarn.bootcss.com/docs/cli/prune)：不需要```prune```命令。```yarn install```将修剪无关的软件包。
- [```yarn publish```](https://yarn.bootcss.com/docs/cli/publish)：将程序包发布到```npm registry```。
- [```yarn remove <package...>```](https://yarn.bootcss.com/docs/cli/remove)：删除```package```直接依赖项中命名的程序包
- [```yarn run [[script] [<args>]]|[env]```](https://yarn.bootcss.com/docs/cli/run)：运行定义的程序包脚本。
- [```yarn self-update```](https://yarn.bootcss.com/docs/cli/self-update)：将```Yarn```更新到最新版本。
- [```yarn tag [add <package>@<version> <tag>]|[remove <package> <tag>]|[list [<package>]]```](https://yarn.bootcss.com/docs/cli/tag)：在包上添加，删除或列出标签。
- [```yarn team [create/destroy/add/remove/list <scope:team> [<user>]]```](https://yarn.bootcss.com/docs/cli/team)：维持团队成员资格。
- [```yarn test```](https://yarn.bootcss.com/docs/cli/test)：运行包定义的测试脚本。
- [```yarn unlink [package]```](https://yarn.bootcss.com/docs/cli/unlink)：取消链接先前为程序包创建的符号链接。
- [```yarn upgrade```](https://yarn.bootcss.com/docs/cli/upgrade)：根据指定范围将软件包升级到最新版本。
- [```yarn upgrade-interactive```](https://yarn.bootcss.com/docs/cli/upgrade-interactive)：这类似于```npm-check```交互式更新模式。它提供了一种更新过期软件包的简便方法。
- [```yarn version```](https://yarn.bootcss.com/docs/cli/version)：更新软件包版本。
- [```yarn versions```](https://yarn.bootcss.com/docs/cli/versions)：显示当前安装的 ```Yarn```、```Node.js``` 及他们的依赖项的版本信息。
- [```yarn why <query>```](https://yarn.bootcss.com/docs/cli/why)：显示有关为什么安装软件包的信息。
- [```yarn workspace <workspace_name> <command>```](https://yarn.bootcss.com/docs/cli/workspace)：将在选定的工作区中运行选定的```Yarn```命令。
- [```yarn workspaces [info [--json]]|[run <command>]```](https://yarn.bootcss.com/docs/cli/workspaces)：显示有关您的工作区的信息。


## CLI简介
```Yarn```提供了丰富的命令行命令集，可帮助您了解```Yarn```软件包的各个方面，包括安装，管理，发布等。

虽然此处按字母顺序提供了所有可用的命令，但一些更流行的命令是：
- ```yarn add```：添加要在当前软件包中使用的软件包。
- ```yarn init```：初始化程序包的开发。
- ```yarn install```：安装```package.json```文件中定义的所有依赖项。
- ```yarn publish```：将软件包发布到软件包管理器。
- ```yarn remove```：从当前软件包中删除未使用的软件包。
### **默认命令**
运行```yarn```不带命令将运行```yarn install```，通过提供任何标志。

### **用户定义的脚本**
运行```yarn <script> [<args>]```将运行用户定义的```script```。请参阅```yarn run```。

### **本地安装的CLI**
```yarn <command> [<args>]```如果与本地安装的CLI匹配，则运行将运行该命令。因此，您无需为简单的用例设置用户定义的脚本。

### **并发和 ```--mutex```**
当在同一服务器上以同一用户身份运行多个```yarn```实例时，可以通过在全局标志```--mutex```后接```file```或来确保在给定的时间仅运行一个实例（并避免冲突）```network```。

使用```fileYarn```时```.yarn-single-instance```，默认情况下将在当前工作目录中写入/读取互斥文件。您还可以指定备用或全局文件名。
```
--mutex file
--mutex file:/tmp/.yarn-mutex
```
使用```networkYarn```时```31997```，默认情况下会在端口上创建服务器。您还可以指定备用端口。
```
--mutex network
--mutex network:30330
```
### **详细输出 ```--verbose```**
运行```yarn <command> --verbose```将为执行打印详细信息（创建目录，复制文件，```HTTP```请求等）。

---------------------------------------------

# 从npm迁移到yarn
对于大多数用户而言，从```npm```迁移应该是一个相当简单的过程。纱线可以使用与```package.jsonnpm```相同的格式，并且可以从```npm```注册表中安装任何软件包。

如果您想在现有的```npm```项目上试用```Yarn```，只需尝试运行：
```
yarn
```
这将```node_modules```使用与```node.js```模块解析算法兼容的```Yarn```解析算法对文件夹进行 布局。

如果遇到错误，请检查是否存在问题，或将其报告给 Yarn问题跟踪器。

当您运行```yarn```或时```yarn add <package>```，```Yarn```将```yarn.lock```在程序包的根目录中生成一个文件。您无需阅读或理解此文件-只需将其检入源代码管理即可。当其他人开始使用Yarn而不是时```npm```，该```yarn.lock```文件将确保他们获得与您完全相同的依赖关系。

在大多数情况下，运行```yarn```或```yarn add```首次运行都可以。在某些情况下，```package.json```文件中的信息不够明确，无法消除依赖关系，并且```Yarn```选择依赖关系的确定性方式将遇到依赖关系冲突。这在较大的项目中尤其可能发生，这些项目有时```npm install```不起作用，并且开发人员经常```node_modules```从头开始删除和重建。如果发生这种情况，请先尝试使用```npm```来使依赖项的版本更明确，然后再转换为```Yarn```。

从```Yarn 1.7.0```开始，您可以使用将导入的```package-lock.json```状态导入```npm```到```Yarn```中```yarn import```。

项目中的其他开发人员可以继续使用```npm```，因此您无需让项目中的每个人都同时进行转换。使用的开发人员```yarn```都将获得彼此完全相同的配置，并且使用的开发人员```npm```可能会获得略有不同的配置，这是的预期行为```npm```。

以后，如果您决定不适合使用```Yarn```，则可以```npm```不做任何特殊更改就直接返回使用。```yarn.lock```如果项目中没有人再使用```Yarn```，则可以删除旧文件，但这不是必需的。

如果您现在正在使用```npm-shrinkwrap.json```文件，请注意，最终可能会导致一组不同的依赖关系。```Yarn```不支持```npmrinkwrap```文件，因为它们中没有足够的信息来增强```Yarn```的确定性算法。如果使用的是收缩包装文件，则将项目上的每个人都转换为同时使用```Yarn```可能会更容易。只需删除您现有的```npm-shrinkwrap.json```文件并检入新创建的```yarn.lock```文件。

## CLI命令比较
|npm (v5)|Yarn|
|-|-|
 | ```npm install```	 | ```yarn add``` | 
 | ```(N/A)```	         | ```yarn add --flat``` | 
 | ```(N/A)```	         | ```yarn add --har``` | 
 | ```npm install --no-package-lock```	 | ```yarn add --no-lockfile``` | 
 | ```(N/A)```	         | ```yarn add --pure-lockfile``` | 
 | ```npm install [package] --save```	     | ```yarn add [package]``` | 
 | ```npm install [package] --save-dev```	 | ```yarn add [package] --dev``` | 
 | ```(N/A)```	         | ```yarn add [package] --peer``` | 
 | ```npm install [package] --save-optional```	 | ```yarn add [package] --optional``` | 
 | ```npm install [package] --save-exact```	     | ```yarn add [package] --exact``` | 
 | ```(N/A)```	         | ```yarn add [package] --tilde``` | 
 | ```npm install [package] --global```	     | ```yarn global add [package]``` | 
 | ```npm update --global```             | ```yarn global upgrade```  |                    
 | ```npm rebuild```	 | ```yarn add --force``` | 
 | ```npm uninstall [package]```	     | ```yarn remove [package]``` | 
 | ```npm cache clean```	             | ```yarn cache clean [package]``` | 
 | ```rm -rf node_modules && npm install```  	 | ```yarn upgrade```  |                          
 | ```npm version major```                    	 | ```yarn version --major``` |                   
 | ```npm version minor```                    	 | ```yarn version --minor```   |                 
 | ```npm version patch ```                   	 | ```yarn version --patch```  |                  

---------------------------------------------

# 创建一个包
## 创建第一个包（Git）
```
git init <project>
cd <project>
yarn init
```
## ```package.json```
```javascript
{
  "name": <project-name>,
  "version": <version>,
  "description": <description>,
  "main": "index.js",
  "repository": {
    "url": <url>,
    "type": "git"
  },
  "author": "yoosonchan",
  "license": "MIT"
}
```
含义：
- **name**(名称)是包的标识符，如果要将其发布到全局注册表，则需要确保它是唯一的。
- **version**(版本)是软件包的semver兼容版本，您可以根据需要发布任意数量的软件包，但它们必须具有新版本。
- **description**(描述)是一个可选的但推荐的字段，其他Yarn用户使用它来搜索和了解您的项目。
- **main**用于定义由```Node.js```之类的程序使用的代码的入口点。如果未指定，则默认为```index.js```。
- **repository**(仓库)是另一个可选的但推荐的字段，可帮助您的软件包用户找到要回馈的源代码。
- **author**(作者)是软件包的创建者或维护者。它遵循格式``` "Your Name <you@example.com> (https://your-website.com)"```
- **license**(许可证)是软件包的已发布法律条款，以及软件包中代码的允许用法。

# 发布一个包
## 登录npm
```
yarn login
```
## 发布包
```
yarn publish
```
## 访问包
```
https://www.npmjs.com/package/<project>
```
### 安装并查看信息
```
yarn add <project>
yarn info <project>
```

---------------------------------------------

# 依赖&版本
程序包依赖关系对于程序包的成功至关重要。开发软件包的功能时，很有可能会使用其他软件包中定义的现有代码。这些包将成为您项目的依赖项。

您的```package.json```文件是所有依赖项声明的宿主，从开发到生产再到可选。您将为每个依赖项指定软件包名称和最低版本信息。

您的```yarn.lock```文件通过存储与软件包一起安装依赖项的版本来确保软件包在安装过程中是一致的。
## 依赖的类型
依赖关系可用于许多不同目的。在构建项目时需要一些依赖项，在运行程序时需要一些依赖项。因此有许多不同类型的依赖关系的，你可以有（例如 ```dependencies```，```devDependencies```和```peerDependencies```）。

您```package.json```将包含所有这些依赖项：
```
{
  "name": "my-project",
  "dependencies": {
    "package-a": "^1.0.0"
  },
  "devDependencies": {
    "package-b": "^1.2.1"
  },
  "peerDependencies": {
    "package-c": "^2.5.4"
  },
  "optionalDependencies": {
    "package-d": "^3.1.0"
  }
}
```
大多数人只有```dependencies```和```devDependencies```，但是每个都很重要。

### ```dependencies```
这些是您的常规依赖项，或者是运行代码时所需的依赖项（例如```React```或```ImmutableJS```）。

### ```devDependencies```
这些是您的开发依赖项。在开发工作流中某些时候需要的依赖关系，而在运行代码时（例如```Babel```或```Flow```）则不需要。

### ```peerDependencies```
对等依赖项是一种特殊类型的依赖项，只有在发布自己的程序包时才会出现。

具有对等依赖性意味着您的软件包需要的依赖性与安装软件包的人的依赖性完全相同。这对于```react```需要单个副本的软件包```react-dom```很有用，安装人员也要使用该副本。

### ```optionalDependencies```
可选依赖项就是：可选。如果他们无法安装，```Yarn```仍会说安装过程成功。

这对于不一定会在每台计算机上都起作用的依赖项很有用，并且如果没有安装依赖项（例如```Watchman```），则您有一个后备计划。

### ```bundledDependencies```
发布程序包时将捆绑的程序包名称数组。

捆绑的依赖项应位于项目内部。该功能基本上与普通依赖项相同。它们在运行时也会被打包```yarn pack```。

通常从```npm```注册表中安装常规依赖项。捆绑的依赖项在正常依赖项不足的情况下很有用：

当您想重新使用不是来自```npm```注册表或已修改的第三方库时。
当您想将自己的项目重新用作模块时。
当您想使用模块分发一些文件时。

## 依赖的版本
## 语义版本控制
```Yarn```中的软件包遵循语义版本控制，也称为“ ```semver```”。从注册表中安装新软件包时，它将```package.json```以```semver```版本范围添加到您的软件包中。

这些版本被分解成```major.minor.patch```, 如：```3.14.1```，```0.42.0```，```2.7.18```。版本的每个部分在不同的时间递增：
- ```major```: 对包的```API```有**重大修改**或者**不兼容的变更**时。
- ```minor```: 添加**新功能**的并保持**向后兼容** (```backwards-compatible```)时。
- ```patch```: **修复bug**并保持**向后兼容** (```backwards-compatible```)时。
  > **注意**： ```semver```格式有时还会有“标签”或“扩展名”，用于标记预发行版或```Beta```版（例如```2.0.0-beta.3```）

当开发人员谈论两个```semver```版本彼此“兼容”时，他们指的是**向后兼容(```backwards-compatible```)**的更改（```minor```和 ```patch```）。

## 版本范围
当您想指定一个依赖项时，您可以像以下```package.json```其中之一那样指定其名称和**版本范围**：
```json
{
  "dependencies": {
    "package-1": ">=2.0.0 <3.1.4",
    "package-2": "^0.4.2",
    "package-3": "~2.7.1"
  }
}
```
您会注意到，我们有许多字符与版本分开。这些```>=```，```<```，```^```和```~```，是**运营商**他们都用于指定**版本范围**的。

版本范围的目的是指定依赖项的哪些版本适用于您的代码。

### **比较器**(```Comparators```)
**每个版本范围都由比较器组成**。这些比较器只是一个*运算符*，加上一个*版本*。以下是一些基本运算符：
| 比较器 | 	描述 | 
|-|-|
| ```<2.0.0```	 | 任何小于 ```2.0.0``` | 
| ```<=3.1.4```	 | 小于或等于的任何版本 ```3.1.4``` | 
| ```>0.4.2```	 | 任何大于 ```0.4.2``` | 
| ```>=2.7.1```	 | 大于或等于的任何版本 ```2.7.1``` | 
| ```=4.6.6```	 | 等于的任何版本 ```4.6.6``` | 

> **注意**：如果未指定任何运算符，则```=```假定为版本范围。因此，```=``` 运算符实际上是可选的。

### **交集**(```Intersections```)
**比较器**(```Comparators```)可以由空格连接以创建**比较器集**(```comparator set```)。这创建了它包含的比较器的**交集**(```Intersections```)。例如，比较器集的```>=2.0.0 <3.1.4```意思是“大于或等于```2.0.0``` 和小于```3.1.4```”。

### **并集**(```Unions```)
一个完整的版本范围可以包含一个由```||```将多个比较器集组合在一起的**并集**(```Unions```)。如果联合的任何一方均得到满足，则整个版本范围得到满足。例如，版本范围的```<2.0.0 || >3.1.4``` 意思是“小于```2.0.0``` 或大于```3.1.4```”。

### **预发布标签**(```Pre-release tags```)
版本也可以具有**预发布标签**(```Pre-release tags```)（例如```3.1.4-beta.2```）。如果比较器包括带有预发布标签的版本，则它将仅与具有相同```major.minor.patch```版本的版本匹配。

例如，范围```>=3.1.4-beta.2```将匹配```3.1.4-beta.2```或 ```3.1.4-beta.12```，而不会匹配```3.1.5-beta.1```, 尽管技术上“大于等于”（```>=```）```>=3.1.4-beta.2```

预发行版本往往包含意外的重大更改，通常您不希望在指定版本之外匹配预发行版本，因此此行为很有用。

### **高级版本范围**
### 连字符范围(```Hyphen Ranges: -```)
连字符范围（例如```2.0.0 - 3.1.4```）指定了一个包含在内的集合。如果省略了部分版本（例如```0.4```或```2```），则将它们填充为零。

| 版本范围	 | 扩展版本范围 | 
|-|-|
| 2.0.0 - 3.1.4	 | >=2.0.0 <=3.1.4 | 
| 0.4 - 2	 | >=0.4.0 <=2.0.0 | 
### X范围(```X-Ranges: x```)
任何的```X```，```x```或者```*```可以用离开的部分或全部未指定的一个版本。

| 版本范围	 | 扩展版本范围 | 
|-|-|
| *	 | >=0.0.0 （任何版本） | 
| 2.x	 | >=2.0.0 <3.0.0 （匹配主要版本） | 
| 3.1.x	 | >=3.1.0 <3.2.0 （匹配主要版本和次要本） |

如果遗漏了一部分版本，则将其视为**x范围**。
| 版本范围	 | 扩展版本范围 | 
|-|-|
| ``（空字符串）	 | * 或者 >=0.0.0 | 
| 2	 | 2.x.x 或者 >=2.0.0 <3.0.0 | 
| 3.1	 | 3.1.x 或者 >=3.1.0 <3.2.0 | 
### 颚化符范围(```Tilde Ranges: ~```)
使用```~```指定的次要版本可以进行```patch```更改。使用```~```与指定的将只允许主版本```minor```的变化。

| 版本范围	 | 扩展版本范围 | 
|-|-|
| ~3.1.4	 | >=3.1.4 <3.2.0
| ~3.1	 | 3.1.x 或者 >=3.1.0 <3.2.0 | 
| ~3	 | 3.x 或者 >=3.0.0 <4.0.0 | 
> **注意**：在**颚化符范围**内指定预发布版本将仅与同一完整版本中的预发布版本匹配。例如，版本范围 ```~3.1.4-beta.2```将匹配，```3.1.4-beta.4```但不是```3.1.5-beta.2``` 因为```major.minor.patch```版本不同而匹配。

### 插入符范围(```Caret Ranges: ^```)
允许所做的更改不会修改版本中的第一个非零数字，如在```3.1.4```中的```3```或在```0.4.2```中的```4```。

| 版本范围	 | 扩展版本范围 | 
|-|-|
| ^3.1.4	 | >=3.1.4 <4.0.0 | 
| ^0.4.2	 | >=0.4.2 <0.5.0 | 
| ^0.0.2	 | >=0.0.2 <0.0.3 | 
> 注意：默认情况下，运行```yarn add [package-name]```时它将使用插入符号范围。

如果忽略了部分版本，则缺少的部分将用零填充。但是，它们仍将允许更改该值。

| 版本范围	 | 扩展版本范围 | 
|-|-|
| ^0.0.x	 | >=0.0.0 <0.1.0 | 
| ^0.0	 | >=0.0.0 <0.1.0 | 
| ^0.x	 | >=0.0.0 <1.0.0 | 
| ^0	 | >=0.0.0 <1.0.0 | 
### **更多资源**
有关此版本系统如何工作的完整规范，请参见[node-semver的README](https://github.com/npm/node-semver)。
可以使用[npm semver calculator](https://semver.npmjs.com/)在实际软件包上测试此版本系统 。

## 选择性依赖解决方案
```Yarn```支持选择性的版本解析，该解析使您可以通过文件中的```resolutions```字段在依赖项中定义自定义程序包版本或范围```package.json```。通常，这需要在```yarn.lock```文件中进行手动编辑。

有关完整规范，请参阅[选择性版本决议RFC](https://github.com/yarnpkg/rfcs/blob/master/implemented/0000-selective-versions-resolutions.md)。

### **你为什么想做这个？**
您可能依赖于不经常更新的软件包，而依赖于另一个获得重要升级的软件包。在这种情况下，如果直接依赖性指定的版本范围不包括新的子依赖性版本，则您将等待作者。

项目的子依赖项获得了重要的安全更新，您不想等待直接依赖项发布最低版本更新。

您所依赖的是一个未维护但可正常工作的软件包，并且其中一个依赖项已升级。您知道升级不会破坏事情，您也不想派发您所依赖的软件包，只是为了更新次要的依赖关系。

您的依赖项定义了较大的版本范围，而您的子依赖项仅得到了有问题的更新，因此您希望将其固定到较早的版本。

### **如何使用它？**
```resolutions```在```package.json```文件中添加一个字段并定义版本替代：
```package.json```
```
{
  "name": "project",
  "version": "1.0.0",
  "dependencies": {
    "left-pad": "1.0.0",
    "c": "file:../c-1",
    "d2": "file:../d2-1"
  },
  "resolutions": {
    "d2/left-pad": "1.1.1",
    "c/**/left-pad": "^1.1.2"
  }
}
```
然后运行```yarn install```。

### **提示与技巧**
- 如果您定义了无效的解决方案（例如，包名称无效），则会收到警告
- 如果您的分辨率版本或范围无效，您将收到警告。
- 如果您的分辨率版本或范围与原始版本范围不兼容，您将收到警告。
### **局限性和警告**
- 嵌套程序包可能无法正常工作。
- 某些边缘情况可能无法正常工作，因为这是一项相当新的功能。


---------------------------------------------

# 工作区
工作区(```workspaces```)是一种设置软件包体系结构的新方法，默认情况下从```Yarn 1.0```开始可用。它允许您以这样一种方式设置多个软件包，您只需运行```yarn install```一次即可一次安装所有软件包。

## 你为什么想做这个？
您的依赖关系可以链接在一起，这意味着您的工作空间可以相互依赖，同时始终使用最新的可用代码。这是比```yarn link```它更好的机制，因为它只影响您的工作区树，而不是整个系统。

您所有的项目依赖项将一起安装，从而为```Yarn```提供了更大的自由度来更好地对其进行优化。

```Yarn```将为每个项目使用一个锁文件，而不是不同的锁文件，这意味着更少的冲突和更轻松的查看。

## 如何使用它？
在package.json文件中添加以下内容。从现在开始，我们将这个目录称为“工作区根目录”：

package.json
```json
{
  "private": true,
  "workspaces": ["workspace-a", "workspace-b"]
}
```
请注意，这private: true是必填项！工作区并不是要发布的，因此我们添加了此安全措施，以确保没有任何东西可以意外地暴露它们。

创建此文件后，创建两个新的子文件夹，分别名为workspace-a和workspace-b。在每个package.json文件中，创建一个具有以下内容的文件：
```json
工作区-a / package.json：

{
  "name": "workspace-a",
  "version": "1.0.0",

  "dependencies": {
    "cross-env": "5.0.5"
  }
}
工作区-b / package.json：

{
  "name": "workspace-b",
  "version": "1.0.0",

  "dependencies": {
    "cross-env": "5.0.5",
    "workspace-a": "1.0.0"
  }
}
```
最后，在yarn install某个地方运行，最好在工作区根目录内运行。如果一切正常，那么您现在应该具有类似的文件层次结构：
```json
/package.json
/yarn.lock

/node_modules
/node_modules/cross-env
/node_modules/workspace-a -> /workspace-a

/workspace-a/package.json
/workspace-b/package.json
```
注意：请勿寻找/node_modules/workspace-b。除非其他软件包将其用作依赖项，否则它将不会在那里。

就是这样！需要workspace-a从位于文件workspace-b现在将使用当前位于项目内，而不是上的是什么NPM发布确切的代码，以及cross-env包装是否已正确重复数据删除，并在你的项目的根目录放置到被两个被使用workspace-a和workspace-b。

请注意通过符号链接/workspace-a别名的事实/node_modules/workspace-a。这是使您能够像正常包装一样要求包装的窍门！您还需要知道使用了该/workspace-a/package.json#name字段，而不是文件夹名称。这意味着，如果该/workspace-a/package.json name字段是"pkg-a"，别名将是以下几点： /node_modules/pkg-a -> /workspace-a你将能够导入代码/workspace-a与const pkgA = require("pkg-a");（或可能import pkgA from "pkg-a";）。

## 与Lerna相比有什么不同？
纱线的工作区是Lerna这样的工具可以（并且可以！）使用的低级原语。他们将永远不会尝试支持Lerna提供的高级功能，但是通过实现分辨率的核心逻辑并在Yarn本身内部链接步骤，我们希望能够实现新的用途并提高性能。

## 提示与技巧
- 该```workspaces```字段是一个数组，其中包含每个工作空间的路径。由于跟踪它们可能很繁琐，因此该字段也接受全局模式！例如，```Babel```通过一个```packages/*```指令引用了所有软件包。

- 工作区足够稳定，可以在大型应用程序中使用，并且不应从常规安装的工作方式进行任何更改，但是，如果您认为它们正在破坏某些内容，则可以通过在```Yarnrc```文件中添加以下行来禁用它们：
  ```
  workspaces-experimental false
  ```
- 如果仅对单个工作区进行更改，请使用–focus从注册表中快速安装同级依赖关系，而不是从头开始构建所有依赖关系。

## 局限性和警告
- 在您的工作空间和用户所得到的内容之间，程序包的布局将有所不同（工作空间相关性将被提升到更高的文件系统层次中）。由于起重过程尚未标准化，因此对此布局进行假设已经很危险，因此从理论上讲，这里没有新内容。如果遇到问题，请尝试使用该```nohoist```选项

- 在上面的示例中，如果```workspace-b```依赖的版本与```workspace-a```的```package.json```中引用的版本不同，则依赖项将从npm安装，而不是从本地文件系统链接。这是因为某些软件包实际上需要使用以前的版本才能构建新的软件包（```Babel```是其中之一）。

- 在工作空间中发布程序包时要小心。如果您正在准备下一个版本，并且决定使用一个新的依赖项，但是忘记在```package.json```文件中声明它，那么如果另一个软件包已经将该依赖项下载到工作区根目录，则您的测试可能仍会在本地通过。但是，对于将其从注册表中拉出的用户而言，它会被破坏，因为依赖项列表现在不完整，因此他们无法下载新的依赖项。当前，在这种情况下无法发出警告。

- 就文件夹层次结构而言，工作区必须是工作区根的后代。您不能也不能引用位于此文件系统层次结构之外的工作空间。

- 目前不支持嵌套工作区。



----------------------------------------------
# 配置: 其他文件
## ```envvars```环境变量
定义在```process.env```中的环境变量让你可以配置其他```yarn```功能。

### ```CHILD_CONCURRENCY```
```bash
process.env.CHILD_CONCURRENCY=#number#
```
控制并行运行以构建节点模块的子进程的数量。

将此数字设置为1将导致按顺序构建节点模块，这可以避免在使用```node-gyp```的```Windows```上发生链接器错误。

### ```npm_config```
为了与向下兼容```npm```，```Yarn```允许```npm```通过环境变量传递配置。例如，```--build-from-source```  ```npm``` CLI标志变为：```npm_config_build_from_source=true```。有关配置的更多信息```npm```，请参考```npm-config```页面。


## ```.yarnrc```文件
```.yarnrc```文件可让您配置其他```yarn```功能。该```config```命令还可用于设置这些选项。```yarn```将```.yarnrc```文件合并到文件树中。
### ```yarn-offline-mirror```
```
yarn-offline-mirror "./packages-cache"
```
维护软件包的脱机副本，以实现更可重复和可靠的构建。在此处查找更多信息。

值必须是相对文件路径，或```false```禁用镜像（默认）。
### ```yarn-offline-mirror-pruning```
```
yarn-offline-mirror-pruning true
```
控制脱机镜像的自动修剪。在此处查找更多信息。

值必须为布尔值，默认为```false```。
### ```yarn-path```
```
yarn-path "./bin/yarn"
```
指示```yarn```推迟到另一个```yarn```二进制文件中执行。如果要将Yarn捆绑到存储库中并让每个人都使用相同版本以保持一致性，则很有用。这是在```Yarn 1.0```中引入的，因此所有开发人员都必须安装```Yarn> = 1.0```。

值必须是相对文件路径，或者```false```要禁用（默认）。
### ```disable-self-update-check```
```
disable-self-update-check true
```
安装软件包时，如果您的```CLI```安装已过时，```Yarn```将提供升级说明。您可以在此处禁用此检查。

值必须为布尔值，默认为```false```。
### ```child-concurrency```
```
child-concurrency #number#
```
控制并行运行以构建节点模块的子进程的数量。

将此数字设置为1将导致按顺序构建节点模块，这可以避免在使用```node-gyp```的```Windows```上发生链接器错误。
### ```unsafe-disable-integrity-migration```
```
unsafe-disable-integrity-migration false
```
将此设置为```false```将会启用```yarn.lock```校验和迁移（启用```sha512```支持）。导致锁定文件格式更改。这是从```version```开始的默认设置```2.0```。

## ```yarn.lock```文件
为了在机器上获得一致的安装，```Yarn```需要比您在中配置的依赖项更多的信息```package.json```。```Yarn```需要准确存储每个依赖项安装了哪个版本。

为此，```Yarnyarn.lock```在项目的根目录中使用一个文件。这些“锁定文件”如下所示：
```bash
# THIS IS AN AUTOGENERATED FILE. DO NOT EDIT THIS FILE DIRECTLY.
# yarn lockfile v1
package-1@^1.0.0:
  version "1.0.3"
  resolved "https://registry.npmjs.org/package-1/-/package-1-1.0.3.tgz#a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0"
package-2@^2.0.0:
  version "2.0.1"
  resolved "https://registry.npmjs.org/package-2/-/package-2-2.0.1.tgz#a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0"
  dependencies:
    package-4 "^4.0.0"
package-3@^3.0.0:
  version "3.1.9"
  resolved "https://registry.npmjs.org/package-3/-/package-3-3.1.9.tgz#a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0"
  dependencies:
    package-4 "^4.5.0"
package-4@^4.0.0, package-4@^4.5.0:
  version "4.6.3"
  resolved "https://registry.npmjs.org/package-4/-/package-4-2.6.3.tgz#a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0"
```
这与其他软件包管理器（如```Bundler```或```Cargo```）中的锁文件相当。它与```npm```相似```npm-shrinkwrap.json```，但是它不是有损的，并且可以产生可重复的结果。

### **由Yarn管理**
您的```yarn.lock```文件是自动生成的，应完全由```Yarn```处理。使用```Yarn CLI```添加/升级​​/删除依赖项时，它将自动更新```yarn.lock```文件。不要直接编辑此文件，因为它很容易破坏某些内容。

### **仅当前套餐**
在安装过程中，```Yarn```将仅使用顶级```yarn.lock```文件，并且将忽略```yarn.lock```依赖项中存在的任何文件。顶级 ```yarn.lock```文件包括Yarn锁定整个依赖树中所有软件包的版本所需的一切。

### **检入源代码管理**
所有```yarn.lock```文件都应检查到源代码管理中（例如```git```或```mercurial```）。这允许```Yarn```在所有计算机上安装相同的完全相同的依赖关系树，无论是您同事的便携式计算机还是```CI```服务器。

框架和库作者还应该检查```yarn.lock```源代码控制。不必担心发布```yarn.lock```文件，因为它不会对库的用户产生任何影响。
> 参见https://yarnpkg.com/blog/2016/11/24/lockfiles-for-all/。