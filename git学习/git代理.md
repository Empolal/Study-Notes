# git走代理

## SSH 形式的仓库地址

**对于这种仓库，我们可以在 ~/.ssh/config 设置代理**

```bash
Host github.com
ProxyCommand connect -s 127.0.0.1:7890 %h %p   #-S为socks # -H为http
HostName %h
Port 22 		
User git
IdentityFile  ~/.ssh/id_rsa    #ssh链接所需要的密钥
IdentitiesOnly yes
```

```bash
# 开始 clone
# 如果觉得仓库太大，可以在 git clone 中加入参数 --depth=1，只拉取最近的一个 revision。

# 如果后面想看历史的版本，使用 git fetch 即可。
git fetch --unshallow
```

## HTTP 形式的仓库地址

```bash
# 端口号可以自己查看 ssr 的设置

git config --global http.proxy 'socks5://127.0.0.1:1086'  	# 127.0.0.1:1086对应代理的地址和端口
git config --global https.proxy 'socks5://127.0.0.1:1086'	

# 推荐，只代理 github，不影响国内 repo

git config --global http.https://github.com.proxy https://127.0.0.1:9870 # 127.0.0.1:1086对应代理的地址和端口
git config --global https.https://github.com.proxy https://127.0.0.1:9870

# 查看配置
git config -l --global


# 取消代理设置

git config --global --unset http.https://github.com.proxy	
git config --global --unset https.https://github.com.proxy

## 也可以修改后直接注释掉
git config --global -e

# V2rary 的端口设置
默认端口设置在 【设置】-【参数设置】-【core基础设置】
```

## push的问题
好像push的时候不走代理速度比较快，而且是HTTP连接形式的仓库，
==不知道SSH形式的仓库会不会更快==