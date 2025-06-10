# 网络问题
- [参考](https://blog.csdn.net/2301_79849395/article/details/142829852)
- ```
```
# 检查 Mihomo 代理是否正在运行
ps aux | grep mihomo

# 如果是以服务方式运行，检查服务状态
systemctl status mihomo

# 验证是否真的在端口 7890 上监听：
ss -tuln | grep 7897

# 配置docker代理
sudo vim /etc/docker/daemon.json


# 如果想让代理永久生效, 需要修改/etc/profile 文件
```
# 代理
- vim /etc/docker/daemon.json
```
{
  "proxies": {
    "http-proxy": "http://127.0.0.1:7890",
    "https-proxy": "http://127.0.0.1:7890"
  }
}
```
- 重启
```
sudo systemctl restart docker
```
- 验证是否生效
```
sudo docker info | grep -A 1 ' HTTP Proxy' 
```


## 容器通讯
### 容器与主机通讯
- 通过 172.17.0.1 进行通讯
### 容器与容器通讯
- 是否搭建网络 搭建网络后共用一个
- 未搭建的话通过
### 主机与容器通讯
- 通过容器网卡, 或者直接对映射端口
# 部署问题
## vs + docker desktop
## Linux + docker
1. vs打包项目为文件夹
2. 创建dockerfile 文件 ,可以使用vs生成 注释掉不必要部分
```dockerfile
# 此阶段用于在快速模式(默认为调试配置)下从 VS 运行时
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
#USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

ARG BUILD_CONFIGURATION=Release

COPY . .

# 时区
ENV TimeZone=Asia/Shanghai
# 使用软连接，并且将时区配置覆盖/etc/timezone
RUN ln -snf /usr/share/zoneinfo/$TimeZone /etc/localtime && echo $TimeZone > /etc/timezone
ENTRYPOINT ["dotnet", "PostWebApi.dll"]
```
3. 将 项目文件夹 dockerfile 文件发送至 Linux
``` bash
# 根据dockerfile 构建镜像
sudo docker build -t post.service.api:1.0.0 .
```
4. 使用run命令运行镜像 注意环境变量
```bash
sudo docker run --name post.service.api   -e "ConfigDB:ConnStr=Server=10.60.10.3;"   -p 5080:8080   -d post.service.api:1.0.0
```