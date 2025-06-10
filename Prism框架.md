# 安装
- Nuget 安装Prism.DryIoc包
- 简单使用
	- App 继承PrismApplication 实现基类即可
- 模板使用
	- 扩展安装Prism扩展创建项目的时候使用固定空模板
# 区域
- 作用: 指定一个区域, 用来切换控件(类似 div 前端通过router 切换视图)
# 模块化
## 项目中引用
- 模块中创建 类似main文件, 继承IModule接口
- 在 RegisterTypes 函数中RegisterForNavigation< View>(); 注入模块
- 在项目中 ConfigureModuleCatalog 中 AddModule< ModelFIle> ();
## 位置加载
```C#
protected override ImoduleCatalog CreateModuleCatalog()
{
	retrun new DirectoryModuleCatalog() {ModulePath=@".\Moudles"} // 引用主程序下moudles文件夹内的moudle  , 可以热加载 具体方式官方文档有示例
}
```
# 导航
```C#
// 继承 INavigationAware 实现三个接口
IsNavigaionTarget // 是否重用原来的实例
OnNavigatedFrom // 用来拦截导航请求 否为拦截切换
OnNavigatedTo// 接受传参
```
# 坑
1. 前端中  使用Prism:ViewModelLocator.AutoWireViewModel = "True" 可以自动搜索 同名+Model 实现自动绑定
	1. 注意这里有坑 ,ViewModel文件一定要放到ViewModels里面
	2. 注意ViewModel 名字 要与View 对应得上