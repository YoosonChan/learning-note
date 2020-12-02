## [Git练习网站```learning git branching```](https://learngitbranching.js.org/?locale=zh_CN)
> ```部分命令：andbox  |  levels  |  undo  |  reset```

> [廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

----------------------------------------------
# 总结
---------------------------------
## <span style="background: #f0150b; padding: .5rem; font-weight: 700;">概念框架</span>
```
[工作区:workspace]-(add)-[->[暂存区:stage]-(commit)->[分支:master]<-(指针pointer:HEAD)]:版本库<-(pull|push)->[远程仓库:origin]
```
> 默认开发分支：```master```        
> 默认远程版本库：```origin```      
> 默认开发分支：```HEAD```      
多个组合：      
>> ```^n```: 多个父级        
>> ```^*```: 多少代      
>> ```~n```: 多少代      
----------------------------------


# <span style="background: #f0150b; padding: .5rem; font-weight: 700;">代码清单</span>
## 创建版本库
```bash
git clone <url>     # 克隆
git init            # 初始化本地版本库
```
## 修改提交
```bash
git status              # 状态
git diff                # 变更内容
git diff HEAD -- <file> # 查看指定文件变更内容
git add .               # 跟踪（添加）所有文件
git add <file>          # 跟踪（添加）指定文件
git add -f <file>       # 强制添加指定文件
git mv <old> <new>      # 文件改名
git rm <file>           # 删除文件
git rm --cached <file>  # 停止跟踪文件但不删除
git commit -m <msg>     # 提交所有文件
git commit --amend      # 修改最后一次提交
```

## 查看提交历史
```bash
git log                 # 查看提交历史
git log -1              # 最后一次提交信息
git log --pretty=online # 查看简化提交历史
git log -p <file>       # 查看指定文件提交历史
git log --graph         # 查看分支合并图
git log --graph --pretty=oneline --abbrev-commit
                        # 查看简化分支合并图
git blame <file>        # 列表形式查看指定文件历史
git reflog              # 查看命令历史（便于找回撤销失误的提交记录的commit id）
```
> 以下```<pointer> = <commitid | HEAD^* | HEAD~n | branch | tag>```(以上在原理上均为指针)

## 撤销
```bash
git reset [--hard] <pointer>    # 撤销未提交
git revert <pointer>            # 撤销指定提交
git checkout HEAD <file>        # 撤销指定的未提交文件的修改内容
```

## 分支与标签
```bash
git branch                  # 显示所有本地分支

# 切换新分支/标签
git checkout <pointer>
git switch <pointer>

# 新建分支/标签
git branch <new branch>     # HEAD保持当前 
    # HEAD移动至新分支
    git checkout -b <new branch>    
    git switch -c <new branch>

git branch -d <branch>      # 删除分支
git branch -D <branch>      # 强制删除分支 

# 移动分支
git branch -f <pointer> <pointer>

git branch --set-upstream-to=<remote>/<branch> <branch>
                        # 将本地分支与远程分支链接(例：origin/dev dev)

git tag                 # 本地标签列表
git show <tagname>      # 查看标签信息
git tag <tagname>       # 基于最新提交创建标签
git tag <tagname> <commit>
                        # 指定提交创建标签
git tag -a <tagname> -m <msg>
                        # 创建带有说明的标签，用-a指定标签名，-m指定说明文字
git tag -d <tagname>    # 删除标签
```

## 合并与衍合
```bash
git merge <pointer: obj>    # 目标合并到当前（Fast forward模式，无合并历史记录）
git rebase <pointer: obj>   # 当前衍合到目标（之后还需互换合并）
git rebase <cur> <obj>      # 目标衍合到当前
git rebase -i <pointer>     # 交互式对话框合并
git merge --no-ff -m <msg> <branch>
                            # 目标合并到当前(普通模式，有合并历史记录)
```

## 远程操作
> ```<remote>```默认情况为```origin```
```bash
git remote -v                   # 查看远程版本库信息
git remote show <remote>        # 查看指定远程版本库信息
git remote add <remote> <url>   # 添加远程版本库
git fetch <remote>              # 从远程库获取代码
git pull <remote> <branch>      # 下载代码及快速合并(merge合并)
git pull --rebase               # 下载代码及快速合并（rebase合并）
git push -u <remote> <branch>   # 第一次上传代码
git push <remote> <branch|tag>  # 上传代码/标签及快速合并
git push <remote> :<branch/tag-name>
                                # 删除远程分支或标签
git push --tags                 # 上传所有标签
```

## Bug分支
```bash
git stash                   # 暂存工作现场 
git stash list              # 查看暂存工作现场
git stash apply             # 恢复暂存工作现场
git stash drop              # 删除暂存工作现场
git stash pop               # 恢复并删除暂存工作现场
git cherry-pick <pointer>[] # 复制特定提交到当前分支
```

## ```.gitignore```
> [.gitignore清单](https://github.com/github/gitignore)
```bash
git check-ignore            # 检查.gitignore
git check-ignore -v <file>  # 检查指定文件的.gitignore

# 部分规则
    # 排除所有.开头的隐藏文件:
    .*
    # 排除所有.class文件:
    *.class

    # 不排除.gitignore和App.class:
    !.gitignore
    !App.class
```

----------------------------------------------