
代办
1. [x] 数据库自动注入
2. [x] 配置数据库,配置注入
	1. [x] build之前获取注入配置
3. [ ] 了解事务的作用
	1. [x] 实现数据库存储事务
	2. [x] IAsyncActionFilter Action执行前或者之后执行自定义代码的工具
		```C#
			/// <summary>
			/// 方法级别的工作单元过滤器
			/// Action执行前或者之后执行自定义代码的工具
			/// </summary>
			public class UnitOfWorkFilter : IAsyncActionFilter
			{
				private static UnitOfWorkAttribute? GetUoWAttr(ActionDescriptor actionDesc)
				{
					var caDesc = actionDesc as ControllerActionDescriptor;
					if (caDesc == null)
					{
						return null;
					}
					//try to get UnitOfWorkAttribute from controller,
					//if there is no UnitOfWorkAttribute on controller, 
					//try to get UnitOfWorkAttribute from action
					var uowAttr = caDesc.ControllerTypeInfo
						.GetCustomAttribute<UnitOfWorkAttribute>();
					if (uowAttr != null)
					{
						return uowAttr;
					}
					else
					{
						return caDesc.MethodInfo
							.GetCustomAttribute<UnitOfWorkAttribute>();
					}
				}
				public async Task OnActionExecutionAsync(ActionExecutingContext context,
					ActionExecutionDelegate next)
				{
					var uowAttr = GetUoWAttr(context.ActionDescriptor);
					if (uowAttr == null)
					{
						await next();
						return;
					}
					using TransactionScope txScope = new(TransactionScopeAsyncFlowOption.Enabled);
					List<DbContext> dbCtxs = new List<DbContext>();
					foreach (var dbCtxType in uowAttr.DbContextTypes)
					{
						//用HttpContext的RequestServices
						//确保获取的是和请求相关的Scope实例
						var sp = context.HttpContext.RequestServices;
						DbContext dbCtx = (DbContext)sp.GetRequiredService(dbCtxType);
						dbCtxs.Add(dbCtx);
					}
					var result = await next();
					if (result.Exception == null)
					{
						foreach (var dbCtx in dbCtxs)
						{
							await dbCtx.SaveChangesAsync();
						}
						txScope.Complete();
					}
				}
			} 
			```
4. [ ] 了解事件在项目中的作用
	1. [x] 是否需要实现简单事件
5. [ ] 项目优化手段
	1. [ ] redis
	2. [x] memory
	3. [ ] 
6. [ ] 项目确定要实现的内容
	1. [ ] 文章封面
		1. [ ] 类似小红书, 封面图片+标题+用户名+点赞数
		2. [ ] 封面图片固定比例(高度不固定的话, 需要修改前端布局后续再说)
	2. [ ] 文章结构
		1. [ ] 内容顶部1-15张图片/视频
		2. [ ] 文章类别 视频/图文
		3. [ ] 下面文字构成内容
		4. [ ] 评论区