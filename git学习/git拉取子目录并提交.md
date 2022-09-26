git init
# 设置 sparse功能
git config core.sparsecheckout true
# 设置要拉取的目录
echo [要拉取的子目录名]/* >> .git/info/sparse-checkout

git remote add origin [仓库名]

git pull origin main

# 查看当前 跟踪的子目录
git sparse-checkout disable

# 关闭sparse命令
git config core.sparsecheckout true
# 并进入 .git/info/sparse-checkout文件修改，把里面都改成*
