代码位置：

Tx.Party.MvcUI\Areas\basedata\Views\AdministrativeDivision\AdministrativeDivision.cshtml

Tx.Party.MvcUI\Areas\basedata\Views\AdministrativeDivision\AdministrativeDivisionEdit.cshtml

```
@{
    ViewBag.Title = "行政区划";
    Layout = "~/Views/Shared/_LayoutIndex.cshtml";
}
```

指定使用默版文件的位置。

```
@section Scripts{

    <script type="text/javascript">

        //键盘事件
        function keydown() {
            if (event.keyCode == 13) {
                query_region();
            }
        }

        function query_division() {
            $('#treeGrid1').treegrid('load');
        }

        function append_ad() {
            var row = $('#treeGrid1').treegrid('getSelected');
            if (row) {
                top._currentDialog = new Object();
                top._currentDialog.editType = 'add';
                top._currentDialog.saveDataUrl = '@Url.Content("~/basedata/AdministrativeDivision/CreateAdministrativeDivision")';
                top._currentDialog.parentNumber = row.DivisionNumber;
                top._currentDialog.syncRow = onAfterAppend;

                showWindow('editDialog1', "新增行政区划档案", '@Url.Content("~/basedata/AdministrativeDivision/EditAdministrativeDivision")', 480, 300);
            }
            else {
                $.messager.alert('提示信息', '请选择要增加子节点的行政区划档案记录', 'info');
            }
        }

        function onAfterAppend(node) {
            $('#treeGrid1').treegrid('append', {
                parent: node.ParentNumber,
                data: [node]
            });
        }

        //加载前事件
        function treeGrid1_onBeforeLoad(row, param) {
            if ($('#treeGrid1').treegrid('options').url == undefined) {
                $('#treeGrid1').treegrid('options').url = '@Url.Content("~/basedata/AdministrativeDivision/ListSubDivision")';
            }
        }

        //加载成功事件
        function treeGrid1_onLoadSuccess(data) {
        };

        //加载失败事件
        function treeGrid1_onLoadError(data) {
            $.messager.alert('错误信息', '对不起，获取数据时发生错误！请稍后再试', 'error');
        };

        function treeGrid1_onSelect(row) {
            if (row) {
                var level = $('#treeGrid1').treegrid("getLevel", row.DivisionNumber);
                level > 1 ? $('#btnAdd').linkbutton('disable') : $('#btnAdd').linkbutton('enable');
            } else {
                $('#btnAdd').linkbutton('disable');
            }           
        }

    </script>

}
```

@section Scripts{  
}

MVC视图中，Javascripts代码被放于下面的Razor代码中（@section Scripts{}）。

好处：在视图进行JavaScript编程时，是一个很好的实践，在共享视图（\_Layout.cshtml），存在节点（@RenderSection\("scripts", required: false\)），在视图执行时，Razor引擎会将Javascripts代码**抽调**出来，然后在执行的时候，再将这些代码放置在这个地方。

本节的 代码会抽出来放到Tx.Party\Tx.Party.MvcUI\Views\Shared\\_LayoutIndex.cshtml 中的以下代码位置，在最终生成的浏览器页面中，就会很规整。

`@RenderSection("Styles", required: false)`

`@RenderSection("Scripts", required: false)`

布局 Tx.Party\Tx.Party.MvcUI\Areas\basedata\Views\PartyMember\DivisionPartyMember.cshtml

```
<div class="easyui-layout" data-options="fit:true">

    <div data-options="region:'west',split:true,title:'行政区划',collapsible:false" style="width: 350px;">

        @Html.Partial("_DivisionTreePartial")

    </div>

    <div data-options="region:'center', title:'党员列表'">

        @Html.Partial("_PartyMember")

    </div>

</div>
```

### table标签（对象）

在 HTML 文档中 &lt;table&gt; 标签每出现一次，一个 Table 对象就会被创建。

```
<table id="treeGrid1" class="easyui-treegrid" border="false" style="width: auto; height: 100px"
       data-options="toolbar:'#toolbar1',fitcolumns:false,fit:true,rownumbers:true, idField:'DivisionNumber', treeField:'DivisionName',onBeforeLoad:treeGrid1_onBeforeLoad, onLoadError: treeGrid1_onLoadError, onSelect:treeGrid1_onSelect"
       singleselect="true" >
    <thead>
        <tr>
            <th field="DivisionName" halign="center" align="left" width="300px">区划名称</th>
            <th field="DivisionNumber" halign="center" align="left" width="100px">区划代码</th>
            <th field="DivisionCategoryText" halign="center" align="left" width="100px">类型</th>
            <th field="ParentNumber" hidden="hidden"></th>
            <th field="Opened" halign="center" align="center" width="50px" formatter="formatBool">启用</th>
            <th field="Description" halign="center" align="left" width="200px">备注</th>
        </tr>
    </thead>
</table>
```

Html table 标签介绍 ： [http://www.w3school.com.cn/tags/tag\_table.asp](http://www.w3school.com.cn/tags/tag_table.asp)

id="treeGrid1"   HTML 全局属性  用于规定元素的唯一 id。

#### id定义和用法\(全局属性\)

id 属性规定 HTML 元素的唯一的 id。

id 在 HTML 文档中必须是唯一的。

id 属性可用作链接锚（link anchor），通过 JavaScript（HTML DOM）或通过 CSS 为带有指定 id 的元素改变或添加样式。

[http://www.w3school.com.cn/tags/att\_standard\_id.asp](http://www.w3school.com.cn/tags/att_standard_id.asp)

#### class定义和用法\(全局属性\)

class 属性规定元素的类名（classname）。

class 属性大多数时候用于指向样式表中的类（class）。不过，也可以利用它通过 JavaScript 来改变带有指定 class 的 HTML 元素。

[http://www.w3school.com.cn/tags/att\_standard\_class.asp](http://www.w3school.com.cn/tags/att_standard_class.asp)

#### border\(table属性\)定义和用法

border 属性规定规定围绕表格的边框的宽度。

border 属性会为每个单元格应用边框，并用边框围绕表格。如果 border 属性的值发生改变，那么只有表格周围边框的尺寸会发生变化。表格内部的边框则是 1 像素宽。

提示：设置 border="0"，可以显示没有边框的表格。

从实用角度出发，最好不要规定边框，而是使用 CSS 来添加[边框样式和颜色](http://www.w3school.com.cn/css/css_border.asp)。

#### style\(全局属性\)定义和用法

style 属性规定元素的行内样式（inline style）

style 属性将覆盖任何全局的样式设定，例如在 &lt;style&gt; 标签或在外部样式表中规定的样式。

## 语法

```
<
element 
style="
value
"
>
```

### 属性值

| 值 | 描述 |
| :--- | :--- |
| style\_definition | 一个或多个由分号分隔的 CSS 属性和值。 |

#### HTML data-\* 属性定义和用法

data-\* 属性用于存储页面或应用程序的私有自定义数据。

data-\* 属性赋予我们在所有 HTML 元素上嵌入自定义 data 属性的能力。

存储的（自定义）数据能够被页面的 JavaScript 中利用，以创建更好的用户体验（不进行 Ajax 调用或服务器端数据库查询）。

data-\* 属性包括两部分：

* 属性名不应该包含任何大写字母，并且在前缀 "data-" 之后必须有至少一个字符
* 属性值可以是任意字符串

注释：用户代理会完全忽略前缀为 "data-" 的自定义属性。

#### [esayui tree-grid](/netbu_fen/dai-ma-mo-kuai/lxxing-zheng-qu-hua-guan-li/viewbu-fen/treegrideasyui.md)

#### &lt;thead&gt;定义和用法

&lt;thead&gt; 标签定义表格的表头。该标签用于组合 HTML 表格的表头内容。

thead 元素应该与[tbody](http://www.w3school.com.cn/tags/tag_tbody.asp)和[tfoot](http://www.w3school.com.cn/tags/tag_tfoot.asp)元素结合起来使用。

tbody 元素用于对 HTML 表格中的主体内容进行分组，而 tfoot 元素用于对 HTML 表格中的表注（页脚）内容进行分组。

注释：如果您使用 thead、tfoot 以及 tbody 元素，您就必须使用全部的元素。它们的出现次序是：thead、tfoot、tbody，这样浏览器就可以在收到所有数据前呈现页脚了。您必须在 table 元素内部使用这些标签。

提示：在默认情况下这些元素不会影响到表格的布局。不过，您可以使用 CSS 使这些元素改变表格的外观。

##### 提示和注释：

注释：&lt;thead&gt; 内部必须拥有 &lt;tr&gt; 标签！

注释：&lt;thead&gt;、&lt;tbody&gt; 以及 &lt;tfoot&gt; 很少被使用，这是因为糟糕的浏览器支持。我们期望在 XHTML 的未来版本中这种情况会发生变化。假如您使用 Internet Explorer 5.0 或更新的浏览器，可以在我们的 XML 教程中查看一个[例子](http://www.w3school.com.cn/tiy/t.asp?f=xmle_cd_catalog_island_thead)。

#### &lt;th&gt;定义和用法

定义表格内的表头单元格。

HTML 表单中有两种类型的单元格：

* 表头单元格 - 包含表头信息（由 th 元素创建）
* 标准单元格 - 包含数据（由 td 元素创建）

th 元素内部的文本通常会呈现为居中的粗体文本，而 td 元素内的文本通常是左对齐的普通文本。

#### &lt;tr&gt;&lt;定义和用法

&lt;tr&gt; 标签定义 HTML 表格中的行。

tr 元素包含一个或多个[th](http://www.w3school.com.cn/tags/tag_th.asp)或[td](http://www.w3school.com.cn/tags/tag_td.asp)元素。

#### &lt;field&gt;属性\(来自easyui-dataGrid\)

string

列字段名称

该列对应的字段名称

#### &lt;halign&gt;\(来自easyui-dataGrid\)

string

指明如何对齐列标题。可以使用的值有：'left','right','center'。如果没有指定，则按照align属性进行对齐。  
**（该属性自1.3.2版开始可用）**

#### &lt;aling&gt;\(来自easyui-dataGrid\)

string

指明如何对齐列数据。可以使用的值有：'left','right','center'。

#### &lt;width&gt;\(来自easyui-dataGrid\)

number

列的宽度。如果没有定义，宽度将自动扩充以适应其内容。

## 数据传递

#### 1.属性中指定

datagrid1 中

```
<table id="treeGrid1" class="easyui-treegrid" border="false" style="width: auto; height: 100px"
       data-options=" url:'@Url.Content("~/basedata/AdministrativeDivision/ListSubDivision")', toolbar:'#toolbar1',fitcolumns:false,fit:true,rownumbers:true, idField:'DivisionNumber', treeField:'DivisionName', onLoadError: treeGrid1_onLoadError, onSelect:treeGrid1_onSelect"
       singleselect="true" >
```

url:'@Url.Content\("~/basedata/AdministrativeDivision/ListSubDivision"\)'

url 指定数据来源  listSubDivision方法 返回数据为 \[{"DivisionName":"四川省","DivisionNumber":510000000000,"DivisionCategoryText":null,"Opened":true,"state":"closed","Description":null}\]。

&lt;th&gt;中的 field 属性 按 字段名 取出数据

![](/assets/Division.png)

#### 2.使用js代码处理

onBeforeLoad:treeGrid1\_onBeforeLoad

```
<table id="treeGrid1" class="easyui-treegrid" border="false" style="width: auto; height: 100px"
       data-options="toolbar:'#toolbar1',fitcolumns:false,fit:true,rownumbers:true, idField:'DivisionNumber', treeField:'DivisionName',onBeforeLoad:treeGrid1_onBeforeLoad, onLoadError: treeGrid1_onLoadError, onSelect:treeGrid1_onSelect"
       singleselect="true" >
```

在onBeforeLoad事件中调用js方法。

```
        //加载前事件
        function treeGrid1_onBeforeLoad(row, param) {
            if ($('#treeGrid1').treegrid('options').url == undefined) {
                $('#treeGrid1').treegrid('options').url = '@Url.Content("~/basedata/AdministrativeDivision/ListSubDivision")';
            }
        }
```

通过$\('\#treeGrid1'\)得到树表格对象，通过treeGrid\('option'\) 访问并设定url的值。

url 调用的是 ListSubDivision\(Int64?id\) 方法

第一次调用时传入参数id = null

tableName=\[basedata\].\[f\_GetAdministrativeDivision\]\(510000000000\)

"SELECT  \*  FROM \[basedata\].\[f\_GetAdministrativeDivision\]\(510000000000\) "

```
SELECT  *  FROM [basedata].[f_GetAdministrativeDivision](510000000000) 
```

这条sql语句 是调用 SQLSERVER的 表值函数 f\_GetAdministrativeDivision

```
USE [tx_NewParty]
GO
/****** Object:  UserDefinedFunction [basedata].[f_GetAdministrativeDivision]    Script Date: 2017/10/18 14:23:13 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

-- =============================================
-- 开发人员: 
-- 开发日期：2017-09
-- 功    能: 获取指定行政区划

-- <参数定义>
-- <param name="DivisionNumber"行政区划代码</param>
-- </参数定义>

-- 测    试: SELECT * FROM [basedata].[f_GetAdministrativeDivision] (510000000000)
-- =============================================
ALTER FUNCTION [basedata].[f_GetAdministrativeDivision] 
(  
    @DivisionNumber bigint = NULL
)
RETURNS @result TABLE
	(DivisionNumber bigint NOT NULL,
	 DivisionName nvarchar(50) NOT NULL,
	 ParentNumber bigint NULL,
	 DivisionCategoryText nvarchar(50) NULL,
	 Opened bit NOT NULL,
	 ChildrenCount int,
	 Description nvarchar(200) NULL)
AS
BEGIN
 	INSERT INTO @result(DivisionNumber, DivisionName, ParentNumber, DivisionCategoryText, Opened, Description)
		 SELECT DivisionNumber, DivisionName, ParentNumber, DivisionCategoryText, Opened, Description
           FROM basedata.V_AdministrativeDivision
          WHERE DivisionNumber = @DivisionNumber;

    UPDATE @result
	   SET ChildrenCount = t1._count
      FROM @result r INNER JOIN (SELECT r1.DivisionNumber, _count = COUNT(1)
	                               FROM @result r1 INNER JOIN basedata.AdministrativeDivision ad 
								        ON (r1.DivisionNumber = ad.ParentNumber)
                               GROUP BY r1.DivisionNumber) t1
		   ON (r.DivisionNumber = t1.DivisionNumber);
       
	RETURN 
END
```

在点击树根节点是

传入参数

ID=510000000000

调用另一个 函数f\_GetSubAdministrativeDivision

result 反回的根节点下的其他数据

```
[{"DivisionName":"天府园区","DivisionNumber":510000000001,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":null},{"DivisionName":"华阳","DivisionNumber":510000000033,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":"这是一个测试"},{"DivisionName":"天府新区高新南区","DivisionNumber":510000000044,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":"这是一个测试"},{"DivisionName":"四川直属园区1","DivisionNumber":510000000051,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":null},{"DivisionName":"ParentNumber","DivisionNumber":510000000099,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":null},{"DivisionName":"天府新区","DivisionNumber":510000000111,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":"这是一个测试"},{"DivisionName":"test 测试","DivisionNumber":510000000321,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":null},{"DivisionName":"青羊区天府广场","DivisionNumber":510000000331,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":"123"},{"DivisionName":"TEST 这事一个测试","DivisionNumber":510000000456,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":null},{"DivisionName":"test 下拉框","DivisionNumber":510000000666,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":null},{"DivisionName":"ABC","DivisionNumber":510000000789,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":null},{"DivisionName":"fuchen","DivisionNumber":510000000999,"DivisionCategoryText":"工业园区","Opened":true,"state":"open","Description":"cehsi"},{"DivisionName":"成都市","DivisionNumber":510101000000,"DivisionCategoryText":null,"Opened":true,"state":"closed","Description":null},{"DivisionName":"广元市","DivisionNumber":510801000000,"DivisionCategoryText":null,"Opened":true,"state":"closed","Description":null},{"DivisionName":"new_test","DivisionNumber":511000000001,"DivisionCategoryText":"工业园区","Opened":false,"state":"open","Description":"12"},{"DivisionName":"第二综合党委","DivisionNumber":515000000000,"DivisionCategoryText":null,"Opened":true,"state":"open","Description":null}]
```

#### 点击事件处理

在onSelect 中调用js方法treeGrid1\_onSelect

```
        function treeGrid1_onSelect(row) {
            if (row) {
                var level = $('#treeGrid1').treegrid("getLevel", row.DivisionNumber);
                level > 1 ? $('#btnAdd').linkbutton('disable') : $('#btnAdd').linkbutton('enable');
            } else {
                $('#btnAdd').linkbutton('disable');
            }           
        }
```

row 是easyui中onSelect 的参数，

#### &lt;getLevel 方法&gt;\(来自easyui-treegrid\)

参数id

获取指定节点等级。

