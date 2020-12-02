## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">概念详解</span>
> [教程来源: 廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

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


-------------------------------------------------


# 管理修改
Git跟踪并管理的是**修改**，而非*文件*。

> 比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

(**修改** -> ```git add```) * ```n``` -> ```git commit```

每次修改，如果不用```git add```到**暂存区**，那就不会加入到```commit```中

# 撤销修改
- 命令```git checkout -- readme.txt```意思就是，把```readme.txt```文件在工作区的修改全部撤销，这里有两种情况：

    - 一种是```readme.txt```自修改后还**没有被放到** *暂存区*，现在，撤销修改就回到和版本库一模一样的状态；

    - 一种是```readme.txt``` **已经添加到** *暂存区*后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    总之，就是让这个文件回到最近一次git commit或git add时的状态。


在```commit```之前，你发现了这个问题。用```git status```查看一下，修改只是添加到了**暂存区**，还没有提交。
- 用命令```git reset HEAD <file>```可以把**暂存区**的修改撤销掉（unstage），重新放回**工作区**.

- git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。

## 小结
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

# 删除文件
一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用```rm命令```删了：```rm test.txt```

这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，```git status```命令会立刻告诉你哪些文件被删除了.

现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令```git rm```删掉，并且```git commit```.
> ```git rm test.txt```     
> ```git commit -m "remove test.txt"```

另一种情况是**删错**了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本.
> ```git checkout -- test.txt```

---------------------------------------------
# 添加远程仓库
1. 创建仓库
2. ```git remote add origin <url>```
    > 添加后，远程库的名字就是```origin```，这是Git默认的叫法，也可以改成别的，但是```origin```这个名字一看就知道是远程库。
3. ```git push -u origin master```
    > 推送本地库的所有内容到远程库      
    > 把本地库的内容推送到远程，用```git push```命令，实际上是把当前分支```master```推送到远程。        
    > 由于远程库是空的，我们**第一次推送** ```master```分支时，加上了```-u``` **参数**，Git不但会把本地的```master```分支内容推送的远程新到```master```分支，还会把本地的```master```分支和远程的```master```分支关联起来，在以后的推送或者拉取时就可以简化命令。
4. 之后推送```git push origin master```

## SSH警告
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：
```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```
这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。

# 从远程克隆
```git clone <url>```

GitHub给出的地址不止一个，还可以用```https://github.com/michaelliao/gitskills.git```这样的地址。实际上，**Git支持多种协议**，**默认**的```git://```使用```ssh```，但也可以使用```https```等其他协议。

使用```https```除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放```http```端口的公司内部就无法使用```ssh```协议而只能用```https```。


----------------------------------

# 创建与合并分支
Git鼓励大量使用分支：

查看分支：```git branch```

创建分支：```git branch <name>```

切换分支：```git checkout <name>```或者```git switch <name>```

创建+切换分支：```git checkout -b <name>```或者```git switch -c <name>```

合并某分支到当前分支：```git merge <name>```

删除分支：```git branch -d <name>```

# 解决冲突
Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，必须手动解决冲突后再提交。

查看冲突文件内容：
Git用```<<<<<<<```，```=======```，```>>>>>>>```标记出不同分支的内容,修改之后再提交。

用```git log --graph```命令可以看到分支合并图


# 分支管理策略
通常，合并分支时，如果可能，Git会用```Fast forward```模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用```Fast forward```模式，Git就会在```merge```时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

## ```--no-ff```方式的```git merge```
合并dev分支，请注意```--no-ff```参数，表示```禁用Fast forward```：
```
git merge --no-ff -m "merge with no-ff" dev
```
因为本次合并要创建一个**新的** ```commit```，所以加上```-m参数```，把```commit描述```写进去。

不使用Fast forward模式，merge后：
![不使用Fast forward模式，merge后](https://www.liaoxuefeng.com/files/attachments/919023225142304/0)

## <span style="background: red; padding: .5rem; font-weight: 100;">分支策略</span>
在实际开发中，我们应该按照几个基本原则进行分支管理：

- 首先，```master```分支应该是非常稳定的，也就是**仅用来发布新版本**，*平时不能在上面干活*；

- 那在哪干活呢？**干活都在```dev分支```上**，也就是说，```dev分支```是**不稳定**的，*到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本*；

- 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![团队合作的分支](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

## 小结
Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上```--no-ff参数```就可以用**普通模式合并**，合并后的历史有分支，能看出来曾经做过合并，而```fast forward合并```就看不出来曾经做过合并。


# <span style="background: red; padding: .5rem; font-weight: 100;">Bug分支</span>
软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，所以，**每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除**。

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，*但是，当前正在dev上进行的工作还没有提交*。

并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

幸好，**Git还提供了一个```stash```功能**，**可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作**

分支bug修改完成后，使用```git stash list```命令查看工作现场列表。

但是恢复，有两个办法：

- 一是用```git stash apply``` **恢复**，但是恢复后，```stash```内容并不删除，你需要用```git stash drop```来**删除**；
- 另一种方式是用```git stash pop```，**恢复的同时把stash内容也删了**.

你可以多次stash，恢复的时候，先用```git stash list```查看，然后恢复指定的```stash```，用命令：
```
$ git stash apply stash@{0}
```
## <span style="background: red; padding: .5rem; font-weight: 100;">```cherry-pick```</span>

在```master```分支上修复了bug后，我们要想一想，```dev```分支是早期从```master```分支分出来的，所以，这个bug其实在当前```dev```分支上也存在。

那怎么在```dev```分支上修复同样的bug？重复操作一次，提交不就行了？

有木有更简单的方法？

同样的bug，要在```dev```上修复，我们只需要把```4c805e2 fix bug 101```这个提交所做的修改“复制”到```dev```分支。注意：我们只想复制```4c805e2 fix bug 101```这个提交所做的修改，并不是把整个```master```分支```merge```过来。

为了方便操作，Git专门提供了一个```cherry-pick```命令，让我们能复制一个特定的提交到当前分支.

```bash
$ git branch
* dev
  master
$ git cherry-pick 4c805e2
[master 1d4b803] fix bug 101
 1 file changed, 1 insertion(+), 1 deletion(-)
```
Git自动给```dev```分支做了一次提交，注意这次提交的```commit```是```1d4b803```，它并不同于```master```的```4c805e2```，因为这两个```commit```只是改动相同，但确实是两个不同的```commit```。用```git cherry-pick```，我们就不需要在dev分支上手动再把修bug的过程重复一遍。

有些聪明的童鞋会想了，既然可以在```master```分支上修复bug后，在```dev```分支上可以“重放”这个修复过程，那么直接在```dev```分支上修复bug，然后在```master```分支上“重放”行不行？当然可以，不过你仍然需要```git stash```命令保存现场，才能从```dev```分支切换到```master```分支。

## 小结
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场```git stash```一下，然后去修复bug，修复后，再```git stash pop```，回到工作现场；

在```master```分支上修复的bug，想要合并到当前```dev```分支，可以用```git cherry-pick <commit>```命令，把bug提交的修改“复制”到当前分支，避免重复劳动。




# <span style="background: red; padding: .5rem; font-weight: 100;">Feature分支</span>
软件开发中，总有无穷无尽的新的功能要不断添加进来。

**添加一个新功能时**，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个```feature分支```，在上面开发，完成后，合并，最后，删除该```feature分支```。

现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。
```
$ git switch -c feature-vulcan
```
开发完成后：
```
$ git add vulcan.py
$ git status
$ git commit -m "add feature vulcan"
```
切回```dev```：
```
$ git switch dev
```
一切顺利的话，```feature```分支和```bug```分支是类似的，合并，然后删除。

但是！

就在此时，接到上级命令，因经费不足，新功能必须取消！

虽然白干了，但是这个包含机密资料的分支还是必须就地销毁：
```
$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
```
销毁失败。Git友情提醒，```feature-vulcan```分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用大写的```-D```参数。

现在我们强行删除：
```
$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 287773e).
```
终于删除成功！

## 小结
开发一个新```feature```，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过```git branch -D <name>```强行删除。


# <span style="background: red; padding: .5rem; font-weight: 100;">多人协作</span>

当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

要查看远程库的信息，用git remote, 或者，用git remote -v显示更详细的信息, 上面显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。

## 推送分支
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

```$ git push origin master```

如果要推送其他分支，比如```dev```，就改成：

```$ git push origin dev```

<span style="background: red; padding: .5rem; font-weight: 100;">但是，并不是一定要把本地分支往远程推送，</span>: 

| 分支 | 说明 |
|-|-|
| ```master```分支 | 主分支，因此要时刻与远程同步； | 
| ```dev```分支 | 开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步； | 
| ```bug```分支 | 只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug； | 
| ```feature```分支 | 是否推到远程，取决于你是否和你的小伙伴合作在上面开发。 | 

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

## 抓取分支
多人协作时，大家都会往```master```和```dev```分支上推送各自的修改。

现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把```SSH Key```添加到```GitHub```）或者同一台电脑的另一个目录下克隆：
```
$ git clone git@github.com:michaelliao/learngit.git
```
当你的小伙伴从远程库```clone```时，默认情况下，你的小伙伴只能看到本地的```master```分支。不信可以用```git branch```命令看看：
```
$ git branch
* master
```
现在，你的小伙伴要在```dev```分支上开发，就必须创建远程```origin```的```dev```分支到本地，于是他用这个命令创建本地```dev```分支：
```
$ git checkout -b dev origin/dev
```
现在，他就可以在```dev```上继续修改，然后，时不时地把```dev```分支```push```到远程：
```
$ git add env.txt
$ git commit -m "add env"
$ git push origin dev
```
你的小伙伴已经向```origin/dev```分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送.

但是，推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用```git pull```把最新的提交从```origin/dev```抓下来，然后，在本地合并，解决冲突，再推送.

但是，```git pull```也失败了，原因是没有指定本地```dev```分支与远程```origin/dev```分支的链接，根据提示，设置```dev```和```origin/dev```的链接：
```
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```
再pull,成功后，合并解决冲突，提交，推送。

## <span style="background: red; padding: .5rem; font-weight: 100;">多人协作的工作模式通常是这样</span>：

- 首先，可以试图用```git push origin <branch-name>```推送自己的修改；

- 如果推送失败，则因为远程分支比你的本地更新，需要先用```git pull```试图合并；

- 如果合并有冲突，则解决冲突，并在本地提交；

- 没有冲突或者解决掉冲突后，再用```git push origin <branch-name>```推送就能成功！

- 如果```git pull```提示```no tracking information```，则说明本地分支和远程分支的链接关系没有创建，用命令```git branch --set-upstream-to <branch-name> origin/<branch-name>```。

## 小结
- 查看远程库信息，使用```git remote -v```；

- 本地新建的分支如果不推送到远程，对其他人就是不可见的；

- 从本地推送分支，使用```git push origin branch-name```，如果推送失败，先用```git pull```抓取远程的新提交；

- 在本地创建和远程分支对应的分支，使用```git checkout -b branch-name origin/branch-name```，本地和远程分支的名称最好一致；

- 建立本地分支和远程分支的关联，使用```git branch --set-upstream branch-name origin/branch-name```；

- 从远程抓取分支，使用```git pull```，如果有冲突，要先处理冲突。


# Rebase
多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后```push```的童鞋不得不先```pull```，在本地合并，然后才能```push```成功。

每次合并再```push```后，分支变成了这样：
```
$ git log --graph --pretty=oneline --abbrev-commit
* d1be385 (HEAD -> master, origin/master) init hello
*   e5e69f1 Merge branch 'dev'
|\  
| *   57c53ab (origin/dev, dev) fix env conflict
| |\  
| | * 7a5e5dd add env
| * | 7bd91f1 add new env
| |/  
* |   12a631b merged bug fix 101
|\ \  
| * | 4c805e2 fix bug 101
|/ /  
* |   e1e9c68 merge with no-ff
|\ \  
| |/  
| * f52c633 add merge
|/  
*   cf810e4 conflict fixed
```
总之看上去很乱，有强迫症的童鞋会问：为什么Git的提交历史不能是一条干净的直线？

其实是可以做到的！

Git有一种称为```rebase```的操作，有人把它翻译成"**变基**"。

在和远程分支同步后，我们对```hello.py```这个文件做了两次提交。用```git log```命令看看：
```
$ git log --graph --pretty=oneline --abbrev-commit
* 582d922 (HEAD -> master) add author
* 8875536 add comment
* d1be385 (origin/master) init hello
*   e5e69f1 Merge branch 'dev'
|\  
| *   57c53ab (origin/dev, dev) fix env conflict
| |\  
| | * 7a5e5dd add env
| * | 7bd91f1 add new env
...
```
注意到Git用```(HEAD -> master)```和```(origin/master)```标识出当前分支的```HEAD```和远程```origin```的位置分别是```582d922 add author```和```d1be385 init hello```，本地分支比远程分支快两个提交。

现在我们尝试推送本地分支：
```
$ git push origin master
To github.com:michaelliao/learngit.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
很不幸，失败了，这说明有人先于我们推送了远程分支。按照经验，先```pull```一下：
```
$ git pull
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (1/1), done.
remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:michaelliao/learngit
   d1be385..f005ed4  master     -> origin/master
 * [new tag]         v1.0       -> v1.0
Auto-merging hello.py
Merge made by the 'recursive' strategy.
 hello.py | 1 +
 1 file changed, 1 insertion(+)
 ```
再用```git status```看看状态：
```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
加上刚才合并的提交，现在我们本地分支比远程分支超前3个提交。

用```git log```看看：
```
$ git log --graph --pretty=oneline --abbrev-commit
*   e0ea545 (HEAD -> master) Merge branch 'master' of github.com:michaelliao/learngit
|\  
| * f005ed4 (origin/master) set exit=1
* | 582d922 add author
* | 8875536 add comment
|/  
* d1be385 init hello
...
```
对强迫症童鞋来说，现在事情有点不对头，提交历史分叉了。如果现在把本地分支```push```到远程，有没有问题？

有！

什么问题？

不好看！

有没有解决方法？

有！

这个时候，```rebase```就派上了用场。我们输入命令```git rebase```试试：
```
$ git rebase
First, rewinding head to replay your work on top of it...
Applying: add comment
Using index info to reconstruct a base tree...
M	hello.py
Falling back to patching base and 3-way merge...
Auto-merging hello.py
Applying: add author
Using index info to reconstruct a base tree...
M	hello.py
Falling back to patching base and 3-way merge...
Auto-merging hello.py
```
输出了一大堆操作，到底是啥效果？再用```git log```看看：
```
$ git log --graph --pretty=oneline --abbrev-commit
* 7e61ed4 (HEAD -> master) add author
* 3611cfe add comment
* f005ed4 (origin/master) set exit=1
* d1be385 init hello
...
```
原本分叉的提交现在变成一条直线了！这种神奇的操作是怎么实现的？其实原理非常简单。我们注意观察，发现Git把我们本地的提交“挪动”了位置，放到了```f005ed4 (origin/master) set exit=1```之后，这样，整个提交历史就成了一条直线。```rebase```操作前后，最终的提交内容是一致的，但是，我们本地的```commit```修改内容已经变化了，它们的修改不再基于```d1be385 init hello```，而是基于```f005ed4 (origin/master) set exit=1```，但最后的提交```7e61ed4```内容是一致的。

**这就是```rebase```操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。**

最后，通过```push```操作把本地分支推送到远程：
```
Mac:~/learngit michael$ git push origin master
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 576 bytes | 576.00 KiB/s, done.
Total 6 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To github.com:michaelliao/learngit.git
   f005ed4..7e61ed4  master -> master
```
再用```git log```看看效果：
```
$ git log --graph --pretty=oneline --abbrev-commit
* 7e61ed4 (HEAD -> master, origin/master) add author
* 3611cfe add comment
* f005ed4 set exit=1
* d1be385 init hello
...
```
远程分支的提交历史也是一条直线。

## 小结
```rebase```操作可以把本地未push的分叉提交历史整理成直线；

```rebase```的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

-------------------------------------------

# 标签管理
发布一个版本时，我们通常先在版本库中打一个标签（```tag```），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（**跟分支很像对不对？但是分支可以移动，标签不能移动**），所以，创建和删除标签都是瞬间完成的。

Git有commit，为什么还要引入tag？

“请把上周一的那个版本打包发布，commit号是6a5819e...”

“一串乱七八糟的数字不好找！”

如果换一个办法：

“请把上周一的那个版本打包发布，版本号是v1.2”

“好的，按照tag v1.2查找commit就行！”

所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

# 创建标签
默认标签是打在**最新提交的commit上**的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的```commit id```，然后打上就可以了。

注意，标签不是按时间顺序列出，而是按字母排序的。可以用```git show <tagname>```查看标签信息

还可以创建带有说明的标签，用```-a```指定标签名，```-m```指定说明文字：
```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

> **注意**：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

## 小结
- 命令```git tag <tagname>```用于新建一个标签，默认为```HEAD```，也可以指定一个```commit id```；

- 命令```git tag -a <tagname> -m "blablabla..."```可以指定标签信息；

- 命令```git tag```可以查看所有标签。

# 操作标签

如果标签打错了，也可以删除。

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令```git push origin <tagname>```

或者，一次性推送全部尚未推送到远程的本地标签：
```
$ git push origin --tags
```

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
```
$ git tag -d v0.9
Deleted tag 'v0.9' (was f52c633)
```
然后，从远程删除。删除命令也是```push```，但是格式如下：
```
$ git push origin :refs/tags/v0.9
To github.com:michaelliao/learngit.git
 - [deleted]         v0.9
```
要看看是否真的从远程库删除了标签，可以登陆GitHub查看。

## 小结
- 命令```git push origin <tagname>```可以推送一个本地标签；

- 命令```git push origin --tags```可以推送全部未推送过的本地标签；

- 命令```git tag -d <tagname>```可以删除一个本地标签；

- 命令```git push origin :refs/tags/<tagname>```可以删除一个远程标签。


--------------------------------------------


# <span style="background: red; padding: .5rem; font-weight: 100;">自定义Git</span>

## <span style="background: red; padding: .5rem; font-weight: 100;">忽略特殊文件</span>
有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，每次```git status```都会显示```Untracked files ...```，有强迫症的童鞋心里肯定不爽。

好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的```.gitignore```文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写```.gitignore```文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore

<span style="background: red; padding: .5rem; font-weight: 100;">忽略文件的原则是</span>：

- 忽略操作系统自动生成的文件，比如缩略图等；
- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
- 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

**注意的是把.gitignore也要提交到Git！**当然检验```.gitignore```的标准是```git status```命令是不是说```working directory clean```。

使用Windows的童鞋注意了，如果你在资源管理器里新建一个```.gitignore```文件，它会非常弱智地提示你必须输入文件名，但是在文本编辑器里“保存”或者“另存为”就可以把文件保存为```.gitignore```了。

有些时候，你想添加一个文件到Git，但发现添加不了，原因是这个文件被```.gitignore```忽略了：
```
$ git add App.class
```
如果你确实想添加该文件，可以用```-f```强制添加到Git：
```
$ git add -f App.class
```
或者你发现，可能是```.gitignore```写得有问题，需要找出来到底哪个规则写错了，可以用```git check-ignore```命令检查：
```
$ git check-ignore -v App.class
.gitignore:3:*.class	App.class
```

Git会告诉我们，```.gitignore```的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。

还有些时候，当我们编写了规则排除了部分文件时：
```
# 排除所有.开头的隐藏文件:
.*
# 排除所有.class文件:
*.class
```
但是我们发现```.*```这个规则把```.gitignore```也排除了，并且```App.class```需要被添加到版本库，但是被```*.class```规则排除了。

虽然可以用```git add -f```强制添加进去，但有强迫症的童鞋还是希望不要破坏```.gitignore```规则，这个时候，可以添加两条例外规则：
```
# 排除所有.开头的隐藏文件:
.*
# 排除所有.class文件:
*.class

# 不排除.gitignore和App.class:
!.gitignore
!App.class
```
把指定文件排除在```.gitignore```规则外的写法就是!+文件名，所以，只需把例外文件添加进去即可。

### 小结
忽略某些文件时，需要编写```.gitignore```；

```.gitignore```文件本身要放到版本库里，并且可以对```.gitignore```做版本管理！


## <span style="background: red; padding: .5rem; font-weight: 100;">配置别名</span>

有没有经常敲错命令？比如```git status```？```status```这个单词真心不好记。

如果敲```git st```就表示```git status```那就简单多了，当然这种偷懒的办法我们是极力赞成的。

我们只需要敲一行命令，告诉Git，以后```st```就表示```status```：

```$ git config --global alias.st status```
好了，现在敲```git st```看看效果。

当然还有别的命令可以简写，很多人都用co表示```checkout```，```ci```表示```commit```，```br```表示```branch```：
```
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
```
以后提交就可以简写成：

```$ git ci -m "bala bala bala..."```
```--global```参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

在撤销修改一节中，我们知道，命令```git reset HEAD file```可以把暂存区的修改撤销掉（```unstage```），重新放回工作区。既然是一个```unstage```操作，就可以配置一个```unstage```别名：

```$ git config --global alias.unstage 'reset HEAD'```
当你敲入命令：

```$ git unstage test.py```
实际上Git执行的是：

```$ git reset HEAD test.py```
配置一个git last，让其显示最后一次提交信息：

```$ git config --global alias.last 'log -1'```
这样，用git last就能显示最近一次的提交：
```
$ git last
commit adca45d317e6d8a4b23f9811c3d7b7f0f180bfe2
Merge: bd6ae48 291bea8
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 22:49:22 2013 +0800

    merge & fix hello.py
```
甚至还有人丧心病狂地把```lg```配置成了：
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
来看看```git lg```的效果：

![git lg的效果](https://www.liaoxuefeng.com/files/attachments/919059728302912/0)

### 配置文件
配置Git的时候，加上```--global```是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在```.git/config```文件中：
```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```
别名就在```[alias]```后面，要删除别名，直接把对应的行删掉即可。

而当前用户的Git配置文件放在用户主目录下的一个隐藏文件```.gitconfig```中：
```
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```
配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。


## [<span style="background: red; padding: .5rem; font-weight: 100; color: #fff">搭建Git服务器</span>](https://www.liaoxuefeng.com/wiki/896043488029600/899998870925664)


--------------------------------------
# GUI工具
> SourceTree

--------------------------------------
# 其他
```
git describe 的​​语法是：

git describe <ref>

<ref> 可以是任何能被 Git 识别成提交记录的引用，如果你没有指定的话，Git 会以你目前所检出的位置（HEAD）。

它输出的结果是这样的：

<tag>_<numCommits>_g<hash>

tag 表示的是离 ref 最近的标签， numCommits 是表示这个 ref 与 tag 相差有多少个提交记录， hash 表示的是你所给定的 ref 所表示的提交记录哈希值的前几位。

当 ref 提交记录上有某个标签时，则只输出标签名称
```