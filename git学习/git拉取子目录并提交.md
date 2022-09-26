git init
# 设置 sparse功能
git config core.sparsecheckout true
# 设置要拉取的目录
echo [要拉取的子目录名]/* >> .git/info/sparse-checkout

git remote add origin [仓库名]

git pull origin main