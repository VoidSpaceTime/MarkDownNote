### 定义接口
```C#
 public interface IMemoryCacheHelper
 {
     /// <summary>
     /// 从缓存中获取数据，如果缓存中没有数据，则调用valueFactory获取数据。
     /// 可以用AOP+Attribute的方式来修饰到Service接口中实现缓存，更加优美，但是没有这种方式更灵活。
     /// 默认最长的缓存过期时间是expireSeconds秒，当然也可以在领域事件的Handler中调用Update更新缓存，或者调用Remove删除缓存。
     /// 因为IMemoryCache会把null当成合法的值，因此不会有缓存穿透的问题，但是还是建议用我这里封装的ICacheHelper，原因如下：
     /// 1）可以切换别的实现类，比如可以保存到MemCached、Redis等地方。这样可以隔离变化。
     /// 2）IMemoryCache的valueFactory用起来麻烦，还要单独声明一个ICacheEntry参数，大部分时间用不到这个参数。
     /// 3）这里把expireSeconds加上了一个随机偏差，这样可以避免短时间内同样的请求集中过期导致“缓存雪崩”的问题
     /// 4）这里加入了缓存数据的类型不能是IEnumerable、IQueryable等类型的限制
     /// </summary>
     /// <typeparam name="TResult">缓存的值的类型</typeparam>
     /// <param name="cacheKey">缓存的key</param>
     /// <param name="valueFactory">提供数据的委托</param>
     /// <param name="expireSeconds">缓存过期秒数的最大值，实际缓存时间是在[expireSeconds,expireSeconds*2)之间，这样可以一定程度上避免大批key集中过期导致的“缓存雪崩”的问题</param>
     /// <returns></returns>
     TResult? GetOrCreate<TResult>(string cacheKey, Func<ICacheEntry, TResult?> valueFactory, int expireSeconds = 60);

     Task<TResult?> GetOrCreateAsync<TResult>(string cacheKey, Func<ICacheEntry, Task<TResult?>> valueFactory, int expireSeconds = 60);

     /// <summary>
     /// 删除缓存的值
     /// </summary>
     /// <param name="cacheKey"></param>
     void Remove(string cacheKey);

```
### 接口实现
```C#
   /// <summary>
   /// 用ASP.NET的IMemoryCache实现的内存缓存
   /// </summary>
   public class MemoryCacheHelper : IMemoryCacheHelper
   {
       private readonly IMemoryCache memoryCache;
       public MemoryCacheHelper(IMemoryCache memoryCache)
       {
           this.memoryCache = memoryCache;
       }
		// 验证类型
       private static void ValidateValueType<TResult>()
       {
           // 获取泛型类型 TResult 的类型信息
           Type typeResult = typeof(TResult);

           // 如果 TResult 是泛型类型（例如 IEnumerable<string>），则获取其泛型定义（例如 IEnumerable<>）
           if (typeResult.IsGenericType)
           {
               typeResult = typeResult.GetGenericTypeDefinition();
           }

           // 检查 TResult 是否为以下不允许的类型：
           // - IEnumerable<>
           // - IEnumerable
           // - IAsyncEnumerable<TResult>
           // - IQueryable<TResult>
           // - IQueryable
           if (typeResult == typeof(IEnumerable<>) || typeResult == typeof(IEnumerable)
               || typeResult == typeof(IAsyncEnumerable<TResult>)
               || typeResult == typeof(IQueryable<TResult>) || typeResult == typeof(IQueryable))
           {
               // 如果是这些类型，抛出 InvalidOperationException 异常
               throw new InvalidOperationException($"TResult of {typeResult} is not allowed, please use List<T> or T[] instead.");
           }
       }
		// 内存中如果没有目标类型,初始化到内存中
       private static void InitCacheEntry(ICacheEntry entry, int baseExpireSeconds)
       {
           //过期时间.Random.Shared 是.NET6新增的
           double sec = Random.Shared.NextDouble(baseExpireSeconds, baseExpireSeconds * 2);
           TimeSpan expiration = TimeSpan.FromSeconds(sec);
           entry.AbsoluteExpirationRelativeToNow = expiration;
       }

       public TResult? GetOrCreate<TResult>(string cacheKey, Func<ICacheEntry, TResult?> valueFactory, int baseExpireSeconds = 60)
       {
           ValidateValueType<TResult>();
           //因为IMemoryCache保存的是一个CacheEntry，所以null值也认为是合法的，因此返回null不会有“缓存穿透”的问题
           //不调用系统内置的CacheExtensions.GetOrCreate，而是直接用GetOrCreate的代码，这样免得包装一次委托
           if (!memoryCache.TryGetValue(cacheKey, out TResult result))
           {
               using ICacheEntry entry = memoryCache.CreateEntry(cacheKey);
               InitCacheEntry(entry, baseExpireSeconds);
               result = valueFactory(entry)!;
               entry.Value = result;
           }
           return result;
       }

       public async Task<TResult?> GetOrCreateAsync<TResult>(string cacheKey, Func<ICacheEntry, Task<TResult?>> valueFactory, int baseExpireSeconds = 60)
       {
	       // 验证类型是否可用
           ValidateValueType<TResult>();
           // 尝试从内存中获取值,如果内存中没有
           if (!memoryCache.TryGetValue(cacheKey, out TResult result))
           {
	           // 
               using ICacheEntry entry = memoryCache.CreateEntry(cacheKey);
               InitCacheEntry(entry, baseExpireSeconds);
               result = (await valueFactory(entry))!;
               entry.Value = result;
           }
           return result;
       }

       public void Remove(string cacheKey)
       {
           memoryCache.Remove(cacheKey);
       }
   }
```
### 具体用法
```C#
		// 如果内存中无数据,获取数据
        Task<Category[]> FindData()
        {
            return repository.GetCategoriesAsync();
        }
        //用AOP来进行缓存控制看起来更优美（可以用国产的AspectCore或者Castle DynamicProxy），但是这样反而不灵活，因为缓存对于灵活性要求更高，所以用这种直接用ICacheHelper的不优美的方式更实用。
        var task = cacheHelper.GetOrCreateAsync($"CategoryController.FindAll",
            async (e) => CategoryVM.Create(await FindData()));
        return await task;
```