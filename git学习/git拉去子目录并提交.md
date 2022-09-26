git init
# 设置 sparse功能
git config core.sparsecheckout true
# 设置要拉去的目录
echo [要删除的目录名]/* >> .git/info/sparse-checkout

git remote add origin git@github.com:Empolal/Study-Notes.git

git pull origin main