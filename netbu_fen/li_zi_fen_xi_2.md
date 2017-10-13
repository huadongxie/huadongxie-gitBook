## 例子分析2 {#2}

Role

### view {#view}

D:\TXLC-Test\源代码\Tx.Party\Tx.Party.MvcUI\Areas\Admin\Views\Role\Role.cshtml

function dataGrid1_onBeforeLoad(param) {

param.searchText = $(&#039;#tbSearchText&#039;).textbox(&#039;getValue&#039;);

if ($(&#039;#dataGrid1&#039;).datagrid(&#039;options&#039;).url == undefined) {

$(&#039;#dataGrid1&#039;).datagrid(&#039;options&#039;).url = &#039;@Url.Content(&quot;~/Admin/Role/ListRole&quot;)&#039;;

}

}

&#039;@Url.Content(&quot;~/Admin/Role/ListRole&quot;)&#039;:指定了action

### Controller {#controller}

D:\TXLC-Test\源代码\Tx.Party\Tx.Party.MvcUI\Areas\Admin\Controllers\RoleController.cs

获取数据

返回数据

指向了IxxxService中的服务，用来获取数据。

### Models {#models}

D:\TXLC-Test\源代码\Tx.Party\Tx.Party.DataAccess\Admin\**RoleDAO.Designer.cs**

返回一个list

D:\TXLC-Test\源代码\Tx.Party\Tx.Party.Common\Models\Admin\**Role.Designer.cs**

中定义了各种字段，与数据库表的字段对于。