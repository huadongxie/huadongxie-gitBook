## lx项目用户登录及权限。 {#lx}

在web.config文件中配置了认证模式：forms

Forms： 基于窗体的身份验证，使用HTTP客户端重定向功能。使用Forms验证，可以根据用户在基于Web的窗体上输入的凭证，为他们提供访问站点或资源的权限。终端用户尝试访问Web站点时，使用匿名身份进入站点，这是默认的身份验证模式。如果他是未通过验证上的请求即匿名的，就会被Asp.net重定向功能重定向到特定的登录页面上（如果下文的的loginUrl）。终端用户输入相应的登录信息，通过了身份验证过程后，就给他提供一个HTTP cookie，以便在后续的请求中使用。这是日前大多数web应用程序使用的方式，推荐使用此方式。

&lt;authentication mode=&quot;Forms&quot;&gt;

&lt;forms name=&quot;.TXPARTY&quot; loginUrl=&quot;~/Account/Login&quot; timeout=&quot;2880&quot; /&gt;

&lt;/authentication&gt;

&lt;!--通过forms段，可以修改Forms验证系统的行为。其中Name: 指定终端用户完成身份验证后发送给他们的的Http cookie的名称。默认情况下，这个cookie的名称是.ASPXAUTH。LoginUrl：如果如果没找到有效的验证cookie、未通过验证或超时后重定向的页面URL，一般为登录页面，让用户重新登录，默认设置为login.aspx。Protection：指定 cookie数据的保护方式，该cookie在终端用户通过身份验证后存储在他的机器上。可设置为：All表示加密数据，并进行有效性验证两种方式，应该总使用这种方式。None表示不保护Cookie，Encryption表示对Cookie内容进行加密，validation表示对Cookie内容进行有效性验证，TimeOut: 指定Cookie的失效时间，超时后要重新登录。其中&lt;forms&gt;元素必须嵌套在&lt;authentication&gt;元素中。--&gt;

### Controllers {#controllers}

通过web.config的文件配置 将认证指向了 ~/Account/Login

D:\TXLC\源代码\Tx.Party\Tx.Party.MvcUI\Controllers\AccountController.cs

中的实现方法

ActionResult是在程序集System.Web.Mvc.dll System.Web.Mvc ActionResult.cs

中定义的类。

public ActionResult Login(string returnUrl)

{

ViewBag.ReturnUrl = returnUrl;

Console.WriteLine(&quot;123&quot;);

return View();

}

ViewBag 是在程序集中 ControllerBase 类中定义的一个动态 属性 用于获取动态视图数据字典。控制器可以使用ViewBag对象来将数据或对象传递到视图模板中

[Dynamic]

public dynamic ViewBag { get; }

View() 是在Controller 类中定义的方法 return View();意思就是返回要浏览的视图（也就是我们的页面文件）他的名字是与[控制器](https://www.baidu.com/s?wd=%E6%8E%A7%E5%88%B6%E5%99%A8&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1dBm164nAF9nAnYrj7huW9h0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnH63nWDYrHTYnWf3PW6vrjRsr0)名字一样的view

### View {#view}

通过web.config的文件配置 将认证指向了 ~/Account/Login 控制器通过 return Veiw()

调用了 Login.cshtml,在浏览器中显示。

Cshtml 中

定义了

&lt;button class=&quot;login-button&quot; id=&quot;loginBtn&quot; type=&quot;button&quot; onclick=&quot;login()&quot;&gt;登&amp;ensp;&amp;ensp;&amp;ensp;录&lt;/button&gt;

在点击登录按钮是 调用 login()方法。

function login() {

。。。

$(&#039;#loginBtn&#039;).html(&#039;正&amp;ensp;在&amp;ensp;登&amp;ensp;录&amp;ensp;...&#039;);

//

$ 是 jquery的一种简洁语法 相当于获取 Id为loginBtn的元素，改变其显示文字。

Html也是jquery定义的：html( htmlString )

Description: Set the HTML contents of each element in the set of matched elements.

htmlString

Type: htmlString

A string of HTML to set as the content of each matched element.

When .html() is used to set an element&#039;s content, any content that was in that element is completely replaced by the new content. Additionally, jQuery removes other constructs such as data and event handlers from child elements before replacing those elements with the new content.

_https://api.jquery.com/html/#html2_

$(&#039;#login&#039;).login(function (result) {

if (result.success) {

$(&#039;#loginBtn&#039;).html(&#039;登录成功，正在跳转...&#039;);

window.location.href = &#039;@Url.Content(&quot;~/Account/Index&quot;)&#039;;

//console.log(&#039;success!&#039;);

} else {

$(&#039;#loginBtn&#039;).html(&#039;登&amp;ensp;&amp;ensp;&amp;ensp;录&#039;);

$.loginMessage(result.message, &#039;error&#039;);

}

isPost = false;

});

$(&#039;#login&#039;).login(….)：获取id为 login的元素，本次是”form”元素。执行login 方法,(相当于定义了个新的login方法？然后执行？)

function (result) {。。。}定义了个匿名方法，然后执行？

&lt;form id=&quot;login&quot; action=&quot;@Url.Content(&quot;~/Account/Login&quot;)&quot; autocomplete=&quot;off&quot;&gt;。

function (result) 这个方法是在login.js中实现的。