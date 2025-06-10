- 情况描述:
``` C#
public class UnitOfWorkFilter : IAsyncActionFilter
{
  public async Task OnActionExecutionAsync(ActionExecutingContext context,
      ActionExecutionDelegate next)
  {
	  // 执行前
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
      // 执行中
      var result = await next();
      // 执行后
      if (result.Exception == null)
      {
          foreach (var dbCtx in dbCtxs)
          {
              await dbCtx.SaveChangesAsync();
          }
          txScope.Complete();
      }
  }
```
- 问题点
	- SaveChangesAsync 是在执行后, 执行中无法确认是否Action是否执行成功
- 解决方法
	1. 使用手动事务
		1. 特性增加 全局跳过事务属性, 检测到后跳过自动事务一致性
		2. 事务范围控制在 Action中 处理完后返回response
		``` C#
		public class ArticlesController : ControllerBase
		{
		    private readonly IArticleService _articleService;
		    private readonly IUnitOfWork _unitOfWork;
		    
		    public ArticlesController(IArticleService articleService, IUnitOfWork unitOfWork)
		    {
		        _articleService = articleService;
		        _unitOfWork = unitOfWork;
		    }
		    
		    [HttpPost]
		    [UnitOfWorkAttribute(SkipGlobalFilter = true)] // 自定义特性，告诉全局过滤器跳过此Action
		    public async Task<IActionResult> Create(CreateArticleCommand command)
		    {
		        if (!ModelState.IsValid)
		        {
		            return BadRequest(ModelState);
		        }
		        
		        try
		        {
		            // 开始事务
		            using var transaction = await _unitOfWork.BeginTransactionAsync();
		            
		            try
		            {
		                // 创建文章
		                var articleId = await _articleService.CreateArticleAsync(
		                    command.Title,
		                    command.Content,
		                    command.AuthorId,
		                    command.CategoryIds);
		                
		                // 立即保存更改
		                await _unitOfWork.SaveChangesAsync();
		                
		                // 获取创建的文章详情
		                var article = await _articleService.GetArticleByIdAsync(articleId);
		                
		                // 提交事务
		                await transaction.CommitAsync();
		                
		                // 返回成功结果
		                return CreatedAtAction(
		                    nameof(GetById), 
		                    new { id = articleId }, 
		                    new { Success = true, Message = "文章创建成功", Data = article }
		                );
		            }
		            catch
		            {
		                // 回滚事务
		                await transaction.RollbackAsync();
		                throw;
		            }
		        }
		        catch (DomainException ex)
		        {
		            return BadRequest(new { Success = false, Message = ex.Message });
		        }
		        catch (Exception ex)
		        {
		            return StatusCode(500, new { Success = false, Message = "文章创建失败", Error = ex.Message });
		        }
		    }
		}
		``` 
	2. 通过其他方法给Action 标记/加入委托, 执行后获取 传入是否执行成功, 推送事件给用户通知
		1. **选择通知技术**：
		    - Web应用：WebSocket(SignalR) + 备选轮询机制
		    - 移动应用：推送通知
		    - 全平台：电子邮件作为备用通知渠道