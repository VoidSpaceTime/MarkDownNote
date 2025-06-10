## 常用命令
``` bash
nginx -t # 检查配置是否正确
nginx -s reload # 重载配置
```
# 反向代理配置文件
- **客户端真实信息透传**
	- **问题**：后端服务无法直接获取客户端 IP 或协议。
	- 方案: 
	```nginx
	proxy_set_header X-Real-IP $remote_addr; # 透传客户端IP 
	proxy_set_header X-Forwarded-Proto $scheme; # 标识HTTP/HTTPS
	```
- **WebSocket 协议支持**  
	- **问题**：WebSocket 需升级协议头。  
    - **方案**：    
    ```nginx
    proxy_set_header Upgrade $http_upgrade;  
    proxy_set_header Connection "upgrade";  # 触发协议升级
    ```
- **跨域请求处理（CORS）**  
	- **问题**：跨域请求需验证来源。  
	- **方案**：    
    ```nginx
    proxy_set_header Origin $http_origin;  # 传递来源域名
    add_header Access-Control-Allow-Origin $http_origin;  # 动态设置响应头
    ```
    - **自定义业务逻辑标识**  
    - **场景**：区分 API 版本或环境。
    ```nginx
    location /api/v1 {  
        proxy_set_header X-API-Version "v1";  
    }  
    location /api/v2 {  
        proxy_set_header X-API-Version "v2";  # 标识API版本
    }
    ```
- **动态请求头控制**  
    • **条件化传递**：结合 `map` 指令根据请求特征动态设置 Header 值。  
    • **敏感信息过滤**：置空特定 Header 减少信息泄露风险：
    ```nginx
    proxy_set_header User-Agent "";  # 移除设备信息
    ```
- **多级代理与负载均衡**  
    在多级代理架构中，需确保 `X-Forwarded-For` 正确追加而非覆盖：
    ```nginx
    proxy_set_header X-Forwarded-For "$http_x_forwarded_for, $remote_addr";  # 手动拼接IP链
    ```
-  **协议一致性处理**  
    当客户端通过 HTTPS 访问而代理使用 HTTP 时，需显式声明协议：
    ```nginx
    proxy_set_header X-Forwarded-Proto "https";  # 强制标识HTTPS
    ```
# 注意问题
1. proxy_pass http://127.0.0.1:8001 这个默认会追加/ 端口后面不需要增加/
``` conf
# client: info -> nginx -> node /info
location /api/user/{
	proxy_pass http://127.0.0.1:8001/
}

# client: info -> nginx -> node //info
location /api/user{
	proxy_pass http://127.0.0.1:8001/
}
# client: info -> nginx -> node /info
location /api/user{
	proxy_pass http://127.0.0.1:8001
}
```