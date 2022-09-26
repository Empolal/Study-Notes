- [初始化](#首先初始化)
- [设置 sparse功能](#设置sparse功能)
- [设置要拉取的目录](#设置要拉取的目录)
- [修改目录](#修改目录)
- [查看当前跟踪目录](#查看当前跟踪的子目录)
- [关闭](#关闭sparse命令)
# 首先初始化
```
git init
```
# 设置 sparse功能
```
git config core.sparsecheckout true
```
# 设置要拉取的目录
```
echo [要拉取的子目录名]/* >> .git/info/sparse-checkout

git remote add origin [仓库名]

git pull origin main
```
# 修改目录
***如果以后修改了.git/info/sparse-checkout,增加或删除部分目录,可以执行如下命令重新Checkout***
```
git checkout master
```
# 查看当前跟踪的子目录
```
cat .git/info/sparse-checkout
```
==这个sparse-checkout 是你自己创建的，所以下次git init就没了==

# 关闭sparse命令
```
git config core.sparsecheckout false
```
***并进入 .git/info/sparse-checkout文件修改，把里面都改成***
