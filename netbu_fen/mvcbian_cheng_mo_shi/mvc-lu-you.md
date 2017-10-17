### MVC 路由 {#mvc-0}

[http://www.tracefact.net/Asp-Net/AspNetMvc-Routing.aspx](http://www.tracefact.net/Asp-Net/AspNetMvc-Routing.aspx)

ASP.NET路由模块负责将即将到来的浏览器请求映射到特定的MVC控制器动作。

ASP.NET路由在两个地方设置

1，在应用程序Web配置文件（Web.config文件）中启用ASP.NET路由。在配置文件中有四个节点与路由有关：sytem.web.httpModules节，system.web.httpHandlers节，system.webserver.modules节，以及system.webserver.handlers节。特别要小心不要删除了这些节点，因为没有它们路由将不能工作。

2，也是更为重要的一点，在应用程序的Global.asax文件中创建了一个路由表。Global.asax文件是一个特殊的文件，它包含了作用于ASP.NET应用程序生命周期事件的事件处理程序。路由表在Application Start事件期间创建。

当一个MVC应用程序首次运行时，会调用Application\_Start\(\)方法。这个方法随后调用了RegisterRoutes\(\)方法。RegisterRoutes\(\)方法创建了路由表。

RouteConfig.cs 文件中 实现了 RegisterRoutes\(\)方法

`public static void RegisterRoutes(RouteCollection routes)`

`{`

`routes.IgnoreRoute("{resource}.axd/{*pathInfo}");`

`routes.MapRoute(`

`name: "Default",`

`url: "{controller}/{action}/{id}",`

`defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }`

`);`

默认的路由表包含了一个路由（名叫Default）。Default路由将URL的第一部分映射到控制器名，URL的第二部分映射到控制器动作，第三个部分映射到一个叫做id的参数。

假设你在浏览器的地址栏输入了下面的URL：

/Home/Index/3

默认的路由将这个URL映射为下面的参数：

Controller = Home

Action = Index

id = 3

当你请求URL /Home/Index/3时，将会执行下面的代码：

HomeController.Index\(3\)

Default路由包含了所有三个参数的默认值。如果你不提供控制器，那么控制器参数默认值为Home。如果你不提供动作，动作参数默认为值Index。最后，如果你不提供id，id参数默认为空字符串。

让我们看看几个例子，Default路由是如何将URL映射到控制器动作的。设想你在浏览器地址栏输入了下面的URL：

/Home

由于Default路由参数的默认值，输入这个URL将会调用代码清单2中的HomeController类的Index\(\)方法。

using System.Web.Mvc;namespace MvcApplication1.Controllers{    \[HandleError\]    public class HomeController : Controller    {        public ActionResult Index\(string id\)        {            return View\(\);        }    }}

在代码清单2中，HomeController类包含了一个叫做Index\(\)的方法，它接受一个叫做Id的参数。URL /Home将会导致调用Index\(\)方法，并使用空字符串作为Id参数的值。

Index\(\)方法也可以不接受任何的参数。URL /Home将会导致调用这个Index\(\)方法。URL /Home/Index/3也会调用这个方法（Id被忽略）。

Index\(int? id\) 也可以写成这样。Index\(\)方法拥有一个整数参数。因为这个参数是一个可空参数（可以拥有Null值），因此可以调用Index\(\)而不会引发错误

出于MVC框架调用控制器动作的方式，URL /Home也匹配代码清单3中HomeController类的Index\(\)方法。

