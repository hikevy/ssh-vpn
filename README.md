## 预备
7897 本地clash端口
1080 远程端口

这个过程需要保证两个服务器都开着

## 设置
本地
```bash
autossh -M 0 \
  -N \
  -o ServerAliveInterval=30 \
  -o ServerAliveCountMax=3 \
  -R 1080:127.0.0.1:7897 \
  ubuntu@36.103.199.20
```

远程
```bash
echo 'export http_proxy=http://127.0.0.1:1080' >> ~/.bashrc
echo 'export https_proxy=http://127.0.0.1:1080' >> ~/.bashrc
echo 'export ALL_PROXY=socks5h://127.0.0.1:1080' >> ~/.bashrc
source ~/.bashrc
```

## 测试
在两边测试
```
curl --proxy http://127.0.0.1:7897 https://api.ipify.org

curl --proxy http://127.0.0.1:1080 https://api.ipify.org
```
查看结果是否一致





