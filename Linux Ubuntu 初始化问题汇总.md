# 设置sudo/docker 权限
1. 简单版本
``` bash   
	  sudo usermod -aG sudo username 
```
1.  复杂版本：对sudoers进行修改
```text
	#User privilege specification 
	root ALL=(ALL:ALL) ALL
	#新增
	your_username**_ ALL=(ALL:ALL) ALL
```
# Docker 端口映射与 UFW 防火墙冲突的解决方案
## 背景
	Docker 默认会修改 iptables 规则，导致即使使用 UFW（Uncomplicated Firewall）配置了防火墙规则，Docker 容器映射的端口仍然会绕过 UFW 的控制而被公开访问。
## 推荐解决方案
[博客链接]("https://blog.csdn.net/qq_52726195/article/details/138470819")
```bash
# BEGIN UFW AND DOCKER
*filter
:ufw-user-forward - [0:0]              # 定义用户转发链
:ufw-docker-logging-deny - [0:0]       # 定义记录被拒绝连接的日志链
:DOCKER-USER - [0:0]                   # 定义Docker用户链（Docker自动创建的）
-A DOCKER-USER -j ufw-user-forward     # Docker流量先经过用户转发链处理
 
# 允许内部网络流量通过
-A DOCKER-USER -j RETURN -s 10.0.0.0/8
-A DOCKER-USER -j RETURN -s 172.16.0.0/12
-A DOCKER-USER -j RETURN -s 192.168.0.0/16
 
# 允许DNS响应流量
-A DOCKER-USER -p udp -m udp --sport 53 --dport 1024:65535 -j RETURN
 
# 阻止来自外部的TCP连接尝试访问内部容器网络
-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 192.168.0.0/16
-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 10.0.0.0/8
-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 172.16.0.0/12

# 阻止来自外部的UDP流量访问内部容器网络
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 192.168.0.0/16
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 10.0.0.0/8
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 172.16.0.0/12
 
# 处理完所有规则后返回
-A DOCKER-USER -j RETURN
 
# 记录被阻止的连接尝试（限制日志频率）
-A ufw-docker-logging-deny -m limit --limit 3/min --limit-burst 10 -j LOG --log-prefix "[UFW DOCKER BLOCK] "
-A ufw-docker-logging-deny -j DROP     # 丢弃不符合上述规则的数据包
 
COMMIT
# END UFW AND DOCKER
```
### 此配置的作用

	这段配置通过自定义 DOCKER-USER 链来控制 Docker 网络流量，实现了以下关键功能：
	
	1. **保护容器网络** ：阻止外部直接访问容器内部网络
	2. **允许内部通信** ：确保 Docker 容器之间可以正常通信
	3. **记录被阻止的访问** ：通过日志记录被拒绝的连接尝试
	4. **保留 DNS 功能** ：允许 DNS 响应流量，确保域名解析正常工作

# 服务器防火墙注意事项
 - 可以使用面板防火墙 
 - ![[./Assets/Linux Ubuntu 初始化问题汇总/Linux Ubuntu 初始化问题汇总-1741799766827.png|463x427]]
# 服务器DDNS插件
 - DDNS-GO 可以获取托管api Cloudflare , 创建 ssl身份验证, 
 - 也可以绑定三级域名到ip