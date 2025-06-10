# 打包应用
```C#
using Microsoft.AspNetCore.Diagnostics.HealthChecks; // 添加此命名空间  
using Microsoft.Extensions.DependencyInjection; // 添加此命名空间  

// 添加健康检查服务  
builder.Services.AddHealthChecks();

// 配置健康检查中间件  
//app.MapHealthChecks("/health");
app.UseStaticFiles();
app.UseHealthChecks("/health");

//app.UseHttpsRedirection(); // 发布时 注释掉HTTPS重定向中间件

```
## 使用IIS部署应用
1. 需要在启用或关闭windows 功能中打开iis(Internet information service)
2. 新建网站, 物理路径建议在. C:\inetpub\\** 下, 避免出现权限问题
3. 将发布文件复制到 inetpub\\** 路径下
4. 安装 Windows Hosting Bundle, 安装后重新启动
5. 安装 IIS rewrite
6. 访问网页应该是404, 访问路径/health 查看是否正确启动
## Linux + Nginx
1. 安装dotnet sdk
2. 复制发布内容
3. 配置nginx
4. 配置守卫运行
5. 运行