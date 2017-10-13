### Asp.Net MVC 控制器 {#asp-net-mvc}

MVC控制器负责响应对ASP.NET MVC网站发起的请求。每一个浏览器请求都映射到了一个专门的控制器。举个例子，设想一下你在浏览器地址栏输入了下面的URL：

[http://localhost/product/index/3](http://localhost/product/index/3)

在这种情况下，将会调用一个名为ProductController的控制器。ProductController负责生成对浏览器请求的响应。举个例子，控制器可能会返回一个特定的视图，或者是将用户重定向到另一个控制器。

你可以通过在ASP.NET MVC应用程序的Controllers文件夹下添加一个新的控制器来创建一个新控制器。右键点击控制器的文件夹，并且选择菜单项“Add（添加）”，“New（新建项）”，并选择“MVC Controller Class（MVC控制器类）”（见图1）。控制器的名字必须含有Controller后缀。举个例子，控制器名称ProductController没什么问题，但是控制器Product就不起作用。

控制器不过是一个类（Visual Basic.Net 或者是C\#类）。一个控制器是一个继承自System.Web.Mvc.Controller基类的类。因为控制器继承自这个基类，所以控制器轻松地继承了一些有用的方法（我们不久将会讨论这些方法）。

**理解控制器动作**

控制器暴露出控制器动作。动作是控制器的一个方法，当你在浏览器地址栏输入某一特定的URL时，将会调用这个方法。举个例子，假设你对下面这个URL发出请求：

[http://localhost/Product/Index/3](http://localhost/Product/Index/3)

在本例中，Index\(\)方法在ProductController类上被调用。Index\(\)方法是控制器动作的一个例子。

一个控制器动作必须是控制器类的一个公共方法。C\#方法，默认时，是私有方法。意识到你添加到控制器类中的任何公共方法都会自动被暴露为控制器动作（你必须非常小心，因为控制器动作可以被全球的任何人调用，仅仅简单地通过在浏览器地址栏输入正确的URL）。

控制器动作还要满足一些额外的需求。作为控制器动作来使用的方法不能够重载。另外，控制器动作不能为静态方法。除了这些以外，你可以将任何方法作为控制器动作来使用。

** 理解控制器结果**

控制器动作返回一种叫做**动作结果**（Action Result）的东西。动作结果是控制器动作返回给浏览器请求的东西。

ASP.NET MVC框架支持六种标准类型的动作结果：

1. ViewResult – 代表HTML及标记。
2. EmptyResult – 代表无结果。
3. RedirectResult – 代表重定向到一个新的URL。
4. RedirectToRouteResult – 代表重定向到一个新的控制器动作。
5. JsonResult – 代表一个JSON（Javascript Object Notation）结果，它可以用于AJAX应用程序。
6. ContentResult – 代表着文本结果。

所有这些动作结果都继承自ActionResult基类。

在大多数情况下，控制器动作 ViewResult

using System;using System.Collections.Generic;using System.Linq;using System.Web;using System.Web.Mvc;namespace MvcApp.Controllers{     public class BookController : Controller     {          public ActionResult Index\(\)          {               return View\(\);          }     }}

当一个动作返回一个ViewResult，将会向浏览器返回HTML。代码清单2中的Index\(\)方法向浏览器返回了一个名为Index.aspx的视图。（或Index.cshtml）

注意到代码清单2中的Index\(\)动作并没有放回一个ViewResult\(\)。而是调用了Controller基类的View\(\)方法。通常情况下，你并不直接返回一个动作结果。而是调用Controller基类的下列方法之一：

1. View – 返回一个ViewResult结果。
2. Redirect – 返回一个RedirectResult 动作结果。
3. RedirectToAction – 返回一个RedirectToAction动作结果。
4. RedirectToRoute – 返回一个RedirectToRoute动作结果。
5. Json – 返回一个JsonResult动作结果。
6. Content – 返回一个ContentResult动作结果。

因此，如果你想向浏览器返回一个视图，你可以调用View\(\)方法。如果你想要降用户从一个控制器动作重定向到另一个，你可以调用RedirectToAction\(\)方法。举个例子，代码清单3中的Details\(\)动作要么显示一个视图，要么将用户重定向到Index\(\)动作，取决于Id参数是否含有值。

using System;using System.Collections.Generic;using System.Linq;using System.Web;using System.Web.Mvc;namespace MvcApp.Controllers{     public class CustomerController : Controller     {          public ActionResult Details\(int? Id\)          {               if \(Id == null\)                    return RedirectToAction\("Index"\);               return View\(\);          }          public ActionResult Index\(\)          {               return View\(\);          }     }}

ContentResult动作结果很特别。你可以使用ContentResult动作结果来将动作结果作为纯文本返回。举个例子，代码清单4中的Index\(\)方法将消息作为了纯文本返回，而不是HTML。

如果一个控制器动作返回了一个结果，而这个结果并非一个动作结果 – 例如，一个日期或者整数 – 那么结果将自动被包装在ContentResult中。举个例子，当调用代码清单5中的WorkController的Index\(\)动作时，日期将自动作为一个ContentResult返回。

