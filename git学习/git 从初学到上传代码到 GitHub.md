## git 从初学到上传代码到 GitHub

**初始化仓库**：git init

**创建远端连接**：git remote add origin  地址

**拉取远端仓库文件**：git pull -- rebase origin master

**增加文件到缓冲区**：git add .        git add  名字

**提交文件到本地库**：git commit -m "注释“

**推送文件到远端**：git push origin master

**首次提交仓库代码会报错**：执行 git push --set-upstream origin master

**查看日志**：git log		

--pretty =oneline

--oneline

--grep 名字			按关键字查找历史文件 

--grep 名字 --author 名字  按关键字和作者名字查找历史文件

git reflog



**回到历史版本**：git reset 

--hard

--mixed(add+commit)

--soft(commit)

**撤回缓冲区的文件**：git rm

一种是 ***git rm --cached "文件路径"***，不删除物理文件，仅将该文件从缓存中删除；

一种是 **git rm --f  "文件路径"**，不仅将该文件从缓存中删除，还会将物理文件删除（不会回收到垃圾桶）。

## 熟悉常用的linux命令

**ctrl-/**   	//发送 SIGQUIT 信号给前台进程组中的所有进程，终止前台进程并生成 core 文件

**ctrl-s** 	//中断控制台输出

**ctrl-q**  	//恢复控制台输出

**ctrl+L**	//清屏

**ctrl+d**   // ( Terminate input, or exit shell ) 一个特殊的二进制值，表示 EOF，作用相当于在终端中输入exit后回车；

**ctrl+c**	// ( kill foreground process ) 发送 SIGINT 信号给前台进程组中的所有进程，强制终止程序的执行;

**ctrl-z**	 // ( suspend foreground process ) 发送 SIGTSTP 信号给前台进程组中的所有进程，常用于挂起一个进程，而并非结束进程，用户可以使用使用fg/bg操作恢复执行前台或后台的进程。

```shell
fg命令在前台恢复执行被挂起的进程，此时可以使用ctrl-z再次挂起该进程，

bg命令在后台恢复执行被挂起的进程，而此时将无法使用ctrl-z再次挂起该进程；

一个比较常用的功能：

正在使用vi编辑一个文件时，需要执行shell命令查询一些需要的信息，可以使用ctrl-z挂起vi，等执行完shell命令后再使用fg恢复vi继续编辑你的文件（当然，也可以在vi中使用！command方式执行shell命令，但是没有该方法方便）。
```



