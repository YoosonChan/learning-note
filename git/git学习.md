## 安装git

Linux
> ```$ git // 查看是否安装，若没安装会提示安装方法```
> ```$ sudo apt-get install git```

Mac
> 1. homwbrew：http://brew.sh/
> 2. Xcode

Windows
> 官网下载，直接安装：https://git-scm.com/downloads

## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">设置</span>
```
$ git config --global user.name "your name"
$ git config --global user.email "email@example.com"
```


------------------------------------------------------------------------------------


# <span style="background: black; padding: .5rem; font-weight: 100;">创建版本库</span>
## 创建目录
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">初始化</span>
```
$ git init
$ ls -ah // 目录默认隐藏，是用此命令查看
```

## <span style="background: black; padding: .5rem; font-weight: 100;">添加文件</span>
> 文件名： readme.md
### <span style="background: #f0150b; padding: .5rem; font-weight: 100;">文件**添加**到仓库</span>
> ```git add <file>```
```
$ git add readme.md
```
### <span style="background: #f0150b; padding: .5rem; font-weight: 100;">文件**提交**到仓库</span>
> ```git commit -m <message>```
```
$ git commit -m "提交说明内容"
```

## <span style="background: black; padding: .5rem; font-weight: 100;">修改文件</span>
### <span style="background: #f0150b; padding: .5rem; font-weight: 100;">查看当前仓库**状态**</span>
> ```git status```

### <span style="background: #f0150b; padding: .5rem; font-weight: 100;">查看当前仓库文件具体**修改内容**</span>
> ```git diff```
### 提交文件
```
$ git add <file>
$ git status
$ git commit -m <message>
$ git status
```
当前没有需要提交的修改，则工作目录是干净（working tree clean）的


-------------------------------------------------------------------------------------------


# <span style="background: black; padding: .5rem; font-weight: 100;">版本回退</span>
在Git中，每当你觉得文件修改到一定程度的时候，就可以“<span style="background: red">保存一个快照</span>”，这个快照在Git中被称为commit。一旦你把文件改乱了，或者误删了文件，还可以<span style="background: red">从最近的一个commit恢复</span>，然后继续工作。
### <span style="background: #f0150b; padding: .5rem; font-weight: 100;">查看文件修改**历史记录**</span>
> ```git log```     
> ```git log --pretty=online```（简化输出信息命令行）
> 
<span style="background: red">```commit id```</span>是一个SHA1计算出来的十六进制表示的大数字

### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">回退版本</span>
> ```git reset --hard HEAD^```

#### <span style="background: black; padding: .5rem; font-weight: 100;">获取版本号</span>
首先，Git必须知道当前版本是哪个版本，在Git中，用<span style="background: red">**HEAD**</span>表示<span style="background: red">当前版本</span>，<span style="background: red">上一个版本</span>就是<span style="background: red">HEAD **^**</span>，*上上一个版本就是HEAD^^*，当然<span style="background: red">往上**100**个版本</span>写100个^比较容易数不过来，所以写成<span style="background: red">HEAD~100</span>。

> **注：代码回退回退到过去版本之后，过去结点往后的版本通过```git log```就查找不到历史记录了，若要回退到未来版本只有在未关闭命令行的情况下```git reset --hard <commit id>```.```commit id```不需要输全，输入前几位，git会自动为你查找.** 
### <span style="background: #f0150b; padding: .5rem; font-weight: 700;">回退过去未来版本</span>
> ```git reflog```      

若已经关闭电脑，无法回退的情况下，还可以使用命令<span style="background: red">```git reflog```</span>,查看每一次记录，找到需要回退的```commit id```。

> **Git的版本回退速度非常快，因为Git在内部有个指向当前版本的<span style="background: red">HEAD指针</span>，当你回退版本的时候，Git仅仅是把HEAD从指向指定的版本处**
```
┌────┐
│HEAD│
└────┘
   │
   └──> ○ version 3
        │
        ○ version 2
        │
        ○ version 1
```


------------------------------------------------------------------------------------------------


# <span style="background: black; padding: .5rem; font-weight: 100;">工作区与暂存区</span>
- <span style="background: red; padding: .25rem;">工作区（Working Directory）</span>
    - .git目录（隐藏目录）--> git版本库
- <span style="background: red; padding: .25rem;">版本库（Repository）</span>
    - stage(或index) --> <span style="background: red; padding: .25rem;">暂存区</span>
    - master --> git自动创建的第一个<span style="background: red; padding: .25rem;">分支</span>

```
┌───工作区───┐   ┌───版本库───────────────────────┐
|           |   |           HEAD─┒               |
|   目录─────(add)───>┌─stage─┐  └──>┌──master──┐ |
|           |   |    |        |     |           ||
|           |   |    |  目录──(commit)──> 目录   ||
|           |   |    |        |     |           ||
|           |   |    └────────┘     └───────────┘|
└───────────┘   └────────────────────────────────┘
```


------------------------------------------------------------------------------------------------


