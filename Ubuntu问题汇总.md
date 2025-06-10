# 命令
```bash

```
# 网络问题 
```
# 查看内网 IP
ip addr show | grep "inet " | grep -v 127.0.0.1
# 或者
hostname -I

# 临时设置代理
export http_proxy=“http://proxy-XXXXX”
export https_proxy=“https://proxy-XXXXX:”

# 查看代理
env | grep -i proxy

# 临时取消代理
unset http_proxy
unset https_proxy

```