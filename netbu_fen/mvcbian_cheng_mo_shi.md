## MVC编程模式 {#mvc}

本此项目使用MVC编程模式

MVC 是三种 ASP.NET 编程模式中的一种。其它两种为Web Pages（Web 页面）、Web Forms（Web 窗体）。

MVC 是一种使用 MVC（Model View Controller 模型-视图-控制器）设计创建 Web 应用程序的模式：

Model（模型）表示应用程序核心（比如数据库记录列表）。

View（视图）显示数据（数据库记录）。

Controller（控制器）处理输入（写入数据库记录）。

MVC 模式同时提供了对 HTML、CSS 和 JavaScript 的完全控制。

[http://www.cnblogs.com/DotCpp/p/3269043.html](http://www.cnblogs.com/DotCpp/p/3269043.html)

ASP.NET MVC由以下两个核心组成部分构成：

一个名为UrlRoutingModule的自定义HttpModule，用来解析Controller与Action名称；

[https://msdn.microsoft.com/zh-cn/library/system.web.routing.urlroutingmodule.aspx](https://msdn.microsoft.com/zh-cn/library/system.web.routing.urlroutingmodule.aspx)

[http://referencesource.microsoft.com/\#System.Web/Routing/UrlRoutingModule.cs,9b4115ad16e4f4a1](http://referencesource.microsoft.com/#System.Web/Routing/UrlRoutingModule.cs,9b4115ad16e4f4a1)

一个名为MvcHandler的自定义HttpHandler，用来实现对Controller的激活和Action的执行；

![ASP.NET MVC源代码探究之\(一\)分析UrlRoutingModule类 - 昨日档案 - 昨日档案](../assets/aspnet_mvcyuan_dai_ma_tan_jiu_4e4b28_4e0029_fen_xi_urlroutingmod.jpeg)

整个ASP.NET MVC系统的路由信息全部存放在RoteTable这个类的静态变量Routes（为一个RouteDictionary类型）中，网站开始运行时，在Application\_Start中对路由进行注册：RouteTable.Routes.Add\("default", new Route{Url="{controller}/{action}"}\);

当一个URL请求到来时，被UrlRoutingModule拦截，拦截后执行流程如下：

封装当前http上下文，变为HttpContextWrapper对象。

根据当前的http上下文，从Routes中得到与当前请求URL相符合的RouteData对象。该对象存储有RouteHandler信息。

把RouteData与http上下文请求封装成一个RequestContext对象。

根据RequestContext对象，从RouteData的RouteHandler中获取IHttpHandler。

执行IHttpHandler，进行请求的真正处理。

![http://www.cnblogs.com/DotCpp/](../assets/httpwwwcnblogscomdotcpp.jpeg)

UrlRoutingModule的代码如下：

HttpContextWrapper httpContext = new HttpContextWrapper\(HttpContext.Current\);

RouteData routeData = RouteTable.Routes.GetRouteData\(httpContext\);

RequestContext requestContext = new RequestContext{ data = routeData, context= httpContext};

IHttpHandler handler = routeData.RouteHandler.GetHttpHandler\(requestContext\);

httpContext.RemapHandler\(handler\);

经过上面最后一步，执行HttpHandle后，程序正式进入Controller激活里面，相关类关系如下图所示：

![http://www.cnblogs.com/DotCpp/](../assets/httpwwwcnblogscomdotcpp.jpeg)

同URL路由一样，MVC初始化时，也需要注册控制器的一些信息，这里是要让框架知道默认的控制器工厂是什么，所以在Application\_Start中：

ControllerBuilder.Current.SetControllerFactory\(new DefaultControllerFactory\(\)\);

程序通过上面的URL路由转换后，进入HttpHandle中，经过以下步骤实现对Controller的激活：

从Requestcontext封装的RouteData中得到Controller名字。

通过ControllerBuilder得到当前默认的Controller工厂。

根据Controller的名字，创建控制器对象（在ControllerFactory初始化的时候，会扫描整个程序集中所有实现IController接口的控制器类型，所以当调用CreateController时，实际上是直接获取）。

最后执行控制器。执行的实质其实就是执行ActionInvoker.InvokeAction，即根据请求上下文执行相应的Action。

![http://www.cnblogs.com/DotCpp/](../assets/httpwwwcnblogscomdotcpp.jpeg)

在自定义的MvcHandler中，代码如下：

string controllerName =this.Requestcontext.RouteData.Controller;

IControllerFactory factory = ControllerBuilder.Current.GetControllerFactory\(\);//通过controllerName得到Control\(如HomeController\)

IController controller = controllerFactory.CreateController\(this.RequestContext,controllerName\);

controller.Execute\(this.RequestContext\);

一个典型的IActionInvoker接口实现ControllerActionInvoker的InvokeAction方法如下：

![复制代码](../assets/fu_zhi_dai_ma.gif)

public void InvokeAction\(ControllerContext controllerContext,

string actionName\)

{

//找到Action方法

MethodInfo method = controllerContext.Controller.GetType\(\).GetMethods\(\)

.First\(m=&gt;string.Compare\(actionName,m.Name,true\)==0\);

//获取Action参数，并进行Model绑定

List&lt;object&gt; parameters = new List&lt;object&gt;\(\);

foreach\(ParameterInfo parameter in method.GetParameters\(\)\)

{

parameters.Add\(this.ModelBinder.BindModel\(controllerContext,

parameter.Name, parameter.ParameterType\)\);

}

//执行Action，并得到ActionResult

ActionResult actionResult = method.Invoke\(controllerContext.Controller,

parameters.ToArray\(\)\) as ActionResult;

//最终ActionResult用HttpResponse将数据传回客户进行显示

actionResult.ExecuteResult\(controllerContext\);

}

![复制代码](../assets/fu_zhi_dai_ma.gif)

最终形成一个Http Response传回到客户端！！

也可以创建自定义路由（参考网上资料）

###  {#mvc-0}

###  {#asp-net-mvc}

### Asp.Net MVC 视图 {#asp-net-mvc-0}

**理解视图**

ASP.NET MVC与ASP.NET或者动态服务器页（ASP）不同，它并没有任何直接对应于一个页面的东西。在ASP.NET MVC应用程序中，磁盘上并没有一个页面来对应你在浏览器地址栏中输入的URL路径。在ASP.NET MVC应用程序中，最接近页面的东西是称为视图（View）的东西。

在ASP.NET MVC应用程序中，即将到达的浏览器请求被映射到了控制器动作。一个控制器动作可能会返回一个视图。然而，一个控制器动作可能执行某种类型的操作，例如将你重定向到另一个控制器动作。

代码清单1含有一个简单的控制器，叫做HomeController。HomeController暴露出了两个控制器动作，叫做Index\(\)和Details\(\)。

你可以通过在浏览器的地址栏输入下面的URL，调用第一个动作，Index\(\)动作：

/Home/Index

你可以通过在浏览器中输入这个地址，来调用第二个动作，Details\(\)动作：

/Home/Details

Index\(\)动作返回一个视图。你所创建的大多数动作都将返回一个视图，然而，动作可以返回任何类型的动作结果。例如，Details\(\)动作返回了一个RedirectToActionResult，它可以将即将到达的请求重定向到Index\(\)动作。

Index\(\)动作包含了下面一行代码：

return View\(\);

这行的代码返回了一个视图，该视图在服务器上的路径必须和下面的路径一样：

\Views\Home\Index.aspx

视图的路径由控制器和控制器动作的名称推断得出。

如果你愿意，可以显式地指明视图。下面一行代码返回了一个视图，名为“Fred”：

return View\("Fred"\);

当执行这行代码时，将会从下面的路径返回一个视图：

\Views\Home\Fred.aspx

**创建一个视图**

你可以在解决方案浏览器中的文件夹上点击右键，并且选择菜单项“Add（添加）”、“New Item（新建项）”（如图1）。选择“MVC View Page”模板将标准视图添加到你的项目中。

应该意识到你不能像ASP.NET或者ASP应用程序中那样，随意向项目中添加视图。你必须将视图添加到文件夹中，并且该文件夹的名称与控制器的名称相同（不含Controller后缀）。举个例子，如果你想创建一个新的、叫做Index的视图，该视图可以由名为ProductController的控制器返回，那么你必须添加这个视图到项目的如下文件夹中：

\Views\Product\Index.aspx

含有视图的文件夹的名称必须与返回该视图的控制器的名称相对应。

