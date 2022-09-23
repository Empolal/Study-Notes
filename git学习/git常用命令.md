``	

## 目录

[toc]

## 忽略某些文件

```bash
.gitignore
```

## 配置用户信息 config

```bash
# 显示当前的Git配置
git config --list

# 编辑Git配置文件
git config -e --global

# or
# 设置提交代码时的用户信息
git config --global user.name "[name]"
git config --global user.email "[email address]"

# 查看配置
git config --global --list
```

## 增加/删除文件 rm

```bash
# 添加指定文件到暂存区
git add [file1] [file2] 

# 添加指定目录到缓存区，包括子目录
git add [dir]

# 添加当前目录的所有文件到暂存区
git add .

# 删除工作目录和版本区的文件（两个地方文件一样），
git rm [file1] [file2]  # 默认执行git add

# 如果工作目录和版本区的文件不一样，Git会有报错，该方法可以暴力删除，工作、缓存区都被删了
git rm -f [file]	    # 默认执行git add

# 移除跟踪但不删除文件,以此来达到删除版本区的文件，进而删除远程文件
git rm --cached [file]	# 默认执行git add

# 停止追踪，并删除本地文件###########################################
git rm --r [file]

# 只删除工作区文件
rm [file]
```

## 重命名文件 mv 

```bash
git mv [旧名] [新名]
```

## 代码提交 commit

```bash
# 提交暂存区到仓库区
git commit -m [message]

# 提交暂存区的指定文件到仓库区
git commit [file1] [file2] ... -m [message]

# 跳过暂存区直接提交,前提是已经跟踪(tracked)的。
git commit -a -m [message]

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
git commit --amend -m [message]

# 重做上一次commit，把指定变化的文件一并提交(代码变了的情况)，防止弄乱commmit仓库历史
git commit --amend [file1] [file2] ...
```

## 查看/建立/删除分支 branch 

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 列出所有本地分支和远程分支
git branch -a

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 建立追踪关系，在现有分支与指定的远程分支之间##########################################################
git branch --set-upstream [branch] [remote-branch]
git branch ––track master origin/main
# 合并指定分支到当前分支
git merge [branch]

# 选择一个commit，合并进当前分支####################################################################
git cherry-pick [commit]

# 删除本地分支
git branch -d <分支名字>

# 在删除分支过程中如果删除的是没有merge的分支需要强制删除#############################################
git branch -D <分支名字>

# 删除远程分支
git push origin --delete <远程分支名字>

# or
git push origin :<远程分支名字>
# 相当于提交了一个空的分支

# 删除远程分支
git branch -dr [remote/branch]
```

## 查看信息 status,log,diff

```bash
# 显示有变更的文件
git status

# 显示当前分支的版本历史
git log

# 搜索提交历史，根据关键词
git  log  --grep [keyword]

# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD
```

## 远程同步 pull, push

```bash
# 下载远程仓库中的所有变动
git fetch [remote]

# 合并,可能会冲突，看《问题总结》
git merge [branch]

# 显示所有远程仓库
git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
git pull [remote] [remote-branch]:[local-branch]

# 上传本地指定分支到远程仓库
git push [remote] [local-branch]：[remote-branch]

# 强行推送当前分支到远程仓库，即使有冲突，慎用！！！会覆盖远程!!!!!
git push [remote] --force

# 推送所有分支到远程仓库
git push [remote] --all
```

## 撤销/恢复 checkout,reset,revert

```bash
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]
```

## 生成发布包 

```bash
# 生成最新发布包
git archivegit archive -o ./latest.zip HEAD

#导出指定提交记录
git archive -o ./git-1.4.0.tar [HEAD]
```

## 暂存 stash

```bash
# 存储命令，save 用来存储说明,以栈的方式存储文件
git stash save '说明'

# 查看stash中存储的文件
git stash list

# 弹出存储
git stash pop
```

## 合并历史  rebase
```bash
# 从当前commit合并到坐标位置的commit，坐标：帮助定位的，不参与合并
git rebase -i HEAD

# 放弃合并
git rebase --abort

# 大概原理
# git rebase 也只是选择哪几个参与合并，正真的合并靠的是P和S，通过P选择需
# 要留下的，S选择需要压缩的，注意的是
# 在P,S操作选择界面，最上面（最旧的）那一个，即使不选择S,也依然会被压缩。
# 再说明一下，假设我有ABCDE 5个从新到旧的commit，如果rebase到E,这个E是不 # 会参与合并的，此时这个E想到与坐标，
# 那么参与合并的ABCD,D是一定会被合并的，即使不能改为S
# (有个疑问，那是不是说，即使我什么都不改，也依然会有一个被压缩)
# 并不会，
```
