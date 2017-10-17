## 例子分析

SystemUser

View端：Tx.Party.MvcUI\Areas\Admin\Views\SystemUser\SystemUser.cshtml

`@{`

`Layout = "~/Views/Shared/_LayoutIndex.cshtml";`

`ViewBag.Title = "公共码表";`

`}`

ViewBag ：**使用ViewBag\(视图包\)传递数据**

**ViewBag 允许在一个动态的对象上定义任意属性,并在视图中访问它.这个动态的对象可以通过Controller.ViewBag属性访问它.**

ViewBag.Title 就是 显示网页的title  ，可以在layout里面 定义一个 @ViewBag.Title - XXX网站

@ViewBag.Title这部分 可以根据继承的页面 动态的来设置

D:\TXLC-Test\源代码\Tx.Party\Tx.Party.MvcUI\Views\Shared\_LayoutIndex.cshtml

中的 ：

head&gt;

&lt;meta charset="utf-8"&gt;

&lt;meta http-equiv="X-UA-Compatible" content="IE=10; IE=9; IE=8; IE=EDGE"&gt;

&lt;title&gt;@ViewBag.Title&lt;/title&gt;

&lt;link rel="stylesheet" type="text/css" href="@Url.Content\("~/Content/jquery-easyui/themes/default/easyui.css"\)"&gt;

注意ViewBag 是动态类型 属性的名字可以任意取.

@section Scripts{

&lt;script type="text/javascript"&gt;

Asp.net MVC中提供了RenderSection方法，这样就能够在Layout中定义一些区块，这些区块留给使用Layout的view来实现

比如我们定义的Layout如下， 定义了一个”Script”的section， 把这个section留给各个view去填充。

[http://www.cnblogs.com/JustRun1983/p/3231563.html](http://www.cnblogs.com/JustRun1983/p/3231563.html)

### //查询事件 {#-0}

function query\_data\(\) {

$\('\#dataGrid1'\).datagrid\('load'\);

}

$\(\) 方法是在DOM中使用过于频繁的 document.getElementById\(\) 方法的一个便利的简写，就像这个DOM方法一样，这个方法返回参数传入的id的那个元素。

getElementById\(\) 方法可返回对拥有指定 ID 的第一个对象的引用。

[http://www.w3school.com.cn/jsref/met\_doc\_getelementbyid.asp](http://www.w3school.com.cn/jsref/met_doc_getelementbyid.asp)

dataGrid1 是在 中定义的 table 的ID.

easyui datagrid属性和方法

方法（Methods）:

| load | param | 载入并显示第一页的记录，如果传递了'param'参数，它将会覆盖查询参数属性的值。通过传递一些参数，通常做一个查询，这个方法可以被称为从服务器加载新数据。 |
| --- | --- | --- |
| reload | param | 重载记录，跟'load'方法一样但是重载的是当前页的记录而非第一页。 |

Table de data-option中定义了 dataGrid1\_onBeforeLoad

执行//加载前事件

function dataGrid1\_onBeforeLoad\(param\) {

if \($\('\#dataGrid1'\).datagrid\('options'\).url == undefined\) {

$\('\#dataGrid1'\).datagrid\('options'\).url = '@Url.Content\("~/Admin/SystemUser/ListSystemUsers"\)';

}

@Url.Content ：将虚拟地址转化为实际地址。

ListSystemUsers 在 D:\TXLC-Test\源代码\Tx.Party\Tx.Party.MvcUI\Areas\Admin\Controllers\SystemUserController.cs

中有定义：

