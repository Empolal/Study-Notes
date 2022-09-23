[TOC]

## git分支管理工具SourceTree

## Git生成公钥及查看公钥

**本地仓库读/写远程仓库，其过程类比于人（本地仓库）那钥匙（公钥）开门（远程仓库），所以要让本地拥有权限访问origin，须在远程仓库创建本地账户生成的密钥。**

#### 1、配置本地用户名及邮箱

```bash
# 配置用户名
git config --global user.name "用户名"
# 配置邮箱
git config --global user.email "邮箱地址"
```

  以上命令执行结束后，可用 git config --global --list 命令查看配置是否成功

```bash
# 单个查看用户名
git config user.name
# 单个查看email
git config user.email
```



#### 2、git生成公钥

 1）在git bash窗口输入下面指令即可生成带注释的公钥

```bash
ssh-keygen -t rsa -C '邮箱地址'
```

 2）设置存放公钥的位置，默认的话直接回车键确认

 3）输入密码和确认密码，不设置密码直接按回车键

#### 3、git查看ssh公钥的方法

 1）通过git bash命令窗口

  ①直接输入cat ~/.ssh/id_rsa.pub即可查看

  ②逐步进入目录打开文件

   a.进入.ssh目录：cd ~/.ssh

   b.找到id_rsa.pub文件：ls 或者 ls ~/.ssh 直接进入并查看下级目录

   c.查看公钥：cat id_rsa.pub 或者vim id_rsa.pub

 2）直接打开用户目录下的.ssh文件夹，打开里面的id_rsa.pub文件即可查看

## Github 创建仓库访问deploy key

进入github仓库点击Setting

![Setting](https://gitee.com/empolal/blog-image/raw/master/img/image-20201128231542665.png)

选择Deploy Keys-->add deploy key--->Allow write access(本机写入的权限，要注意勾上)

![Deploy Keys](https://gitee.com/empolal/blog-image/raw/master/img/image-20201128231710440.png)

## SSH keys和Deploy key区别

### 1.SSH keys和Deploy key区别

github账户的SSH keys，相当于这个账号的最高级key，只要是这个账号有的权限（任何项目），都能进行操作。
仓库的Deploy keys，顾名思义就是这个仓库的专有key，用这个key，只能操作这个项目，其他项目都没有权限。
说白了就相当于你有一所大别墅，SSH key能开别墅中的任何一个房间。而Deploy key只能开进别墅中的一个单间。

### 2.http和SSh的仓库链接

```bash
# gitee.com
ssh -T git@gitee.com
# github.com
ssh -T git@gitee.com
```

查看公钥链接是否正确

## 远程仓库与本地仓库的关联

有了访问权限后,就需要将远程仓库与本地仓库关联起来,才能进行一系列的拉取和推送工作

#### 1.查看本地仓库

```bash
git remote -v
```

![](https://gitee.com/empolal/blog-image/raw/master/img/git_remote_v.png)

此时出现两个origin，表示具有拉取（fetch）和推送(push)的权限，如果只有一个说明创建deploy密钥时没有赋予写权限，即没有push说明我们本地仓库不具备推送到远程仓库的权限。

#### 2.添加与远程仓库的关联

若什么都没有，则表示你没有提添加与远程的关联

```bash
# 添加与远程仓库的关联
git remote add <主机名> git@gitee.com:Mr_Hz/MyGit.git
# 强制关联
git pull origin master --allow-unrelated-histories
# git相关命令
# 修改主机名
git remote rename <原主机名> <新主机名>
# 删除本地仓与远程仓的关联
git remote rm <主机名>
# 更换关联的远程仓库
git remote set-url <主机名> <新仓库地址>
```

## 本地分支关联远程分支

~~~bash
# 此命令使用前提是，要先提交本地分支到远程分支
git branch –set-upstream <本地新建分支名> <origin/远程分支名>
~~~



## Git远程操作pull和push使用总结

#### 1.git pull，这个命令是用来获取远程分支的更新并与本地要更新的分支合并。

命令形式:

```bash
git pull <远程主机名> <远程分支名>:<本地分支名>
```

在合并origin 与local不相关的分支时会出现    <!--fatal: refusing to merge unrelated histories-->
可已采用以下方式强制合并分支

```bash
git pull origin master --allow-unrelated-histories
```

(1)

```bash
# 取得远程的debug分支的更新，与本地的master分支合并。
git pull origin <远程分支名>:<本地分支名>
# 如果去掉后面的本地分支名表示更新并与当前分支合并
git pull origin <远程分支名>
```

（2）

```bash
git pull origin
```

表示取得与当前分支关联的远程分支的更新并合并。如果没有建立追踪关系，就会有如下提示，(待加入)

这个时候执行

```bash
git branch ––track master origin/main
```

即表示本地master分支与远程main分支建立追踪关系。例外如果当前分支只有一个关联分支，那么可以执行git pull操作。

#### 2.git push，这个命令是用来将本地分支的更新推送到远程分支。

```bash
git push <远程主机名> <本地分支名>:<远程分支名>
```



#######################################################################

~~~bash
# 表示将本地分支master的更新推送到远程分支main上
git push origin master:main
# 省略了远程分支名，表示将本地分支master的更新推送到与之关联的同名分支，如果分支不存在就会在远程新建一个master分支。
git push origin master
# 省略了本地分支名，表示将远程分支main删除
git push origin :main
# 等同于命令
git push origin –delete main

# 慎用 --force,会覆盖远程分支，
git push origin [本地分支]:[远程分支] --force
~~~



（1）git push origin master:main， 表示将本地分支master的更新推送到远程分支main上。
（2）git push origin master， 省略了远程分支名，表示将本地分支master的更新推送到与之关联的**同名**分支，如果分支不存在就会在远程新建一个master分支。
（3）git push origin :main， 省略了本地分支名，表示将远程分支main删除，等同于命令（git push origin –delete main).



## git命令提交本地代码到远程仓库

**一、先拉取代码将本更新，**

~~~bash
git clone 仓库地址
~~~

**二、将本地更新代码提交到远程仓库中去**

~~~bash
# 切换到项目
cd <文件夹名字>
# 添加修改到缓冲区
git add .(注意add与点之间有空格)
# 提交修改到仓库
git commit -m "提交信息"
# 提交修改到远程仓库
git push -u origin master
~~~

~~~bash
git diff 分支名字
~~~

## git revert 与git reset 的区别

```bash
git revert commit_id`之后并不会回滚到该id的内容，而是将该id的内容给逆向操作一遍，比如说，a操作添加了“haha”，commit了a，b操作添加了“xixi”，commit b。现在想回滚到只添加了“haha”，需要的是删除“xixi”，也就是逆向操作b，所以应该` git revert b的commit_id`。回退也会作为一次提交` git revert ` 应该翻译成“反转、逆转”比较好理解，而不是回退。`
```

```bash
# 更为重要的是revert是revert 是回滚某个 commit ，不是回滚“到”某个
# 要回滚的commit,相当于没有被执行
# 所以哪一个commit有错误就回退到那个commit
# 与reset不同，要回到错之前的一个commit
```



而相对于 git reset：

```bash
git reset `的原理是，让最新提交的指针回到以前某个时点，该时点之后的提交都从历史中消失。`
# 由于reset会删除之后的commit,导致与远端历史版本不同，会push不上去
# 如果确定之后的版本不要，则git push -f
```



```bash
# 只是移动版本库中的HEAD,并没有改变缓存区和工作目录中的文件
git reset --soft [HEAD~]    

# 与 git commit --amend 区别
# git commit --amend 只能重置最近的一次提交，而reset --soft 可以在多次提交中重置

# 更新索引(缓存区),改变了版本库的HEAD和缓存区
git reset --mixed [HEAD~]

# 三个同时改了,回到之前的HEAD,之后的提交记录不在，可以从reflog 中恢复
git reset --hard [HEAD]
```

![reset](https://gitee.com/empolal/blog-image/raw/master/git/reset.png)

```bash
# 反做commit-id对应的内容，如果不使用-n，在revert后会弹出编辑器用于编辑提交信息
git revert -n commit-id
# 如果遇到合并冲突，可以选择退出本次合并
git merge --abort
# 也可以,合并冲突后退出
git revert --abort
# 合并后退出，但是保留变化
git revert --quit
# 合并后解决冲突，继续操作
git add .
git commit -m '提交的信息'
# 反做多个commit-id
git revert commit-idA..commit-idB
```

## 首次push报错

```bash
git push --set-upstream origin master
```

## 合并冲突

```bash
# 查看哪个文件发生冲突
git ls-files -s
# 查看文件对应的版本的内容
git show :n:filename
# code filename 命令打开文件，手动修改冲突
# 在 git commit 后就可以解决合并冲突
```

## 首次上传

新建仓库不要用任何文件初始化，等git push完后就行，否则就会变成两个不同版本的仓库合并。需要先pull(fetch+merge)再push。

## pull下来的远程分支

```bash
# origin/main 是从远程拉去的对应分支，对它不具有操作意义
# 可以新建一个test分支，指向这个分支
```

## clone项目最近的提交（项目太大）

```bash
git clone --depth=1 [仓库地址]
```

## git relfog 与git log

- reflog 不是仓库的一部分，他**单独存储**，与log不是一个存储

- reflog 只记录**每次本地**的操作，push,clone,pull这些**不包含**reflog，但包含log

## 列出master分支下跟踪的文件

```bash
git ls-tree -r master --name-only
```

