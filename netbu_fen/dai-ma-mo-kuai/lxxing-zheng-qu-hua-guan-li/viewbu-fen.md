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

##### table标签（对象）

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

## id定义和用法\(全局属性\)

id 属性规定 HTML 元素的唯一的 id。

id 在 HTML 文档中必须是唯一的。

id 属性可用作链接锚（link anchor），通过 JavaScript（HTML DOM）或通过 CSS 为带有指定 id 的元素改变或添加样式。

[http://www.w3school.com.cn/tags/att\_standard\_id.asp](http://www.w3school.com.cn/tags/att_standard_id.asp)

## class定义和用法\(全局属性\)

class 属性规定元素的类名（classname）。

class 属性大多数时候用于指向样式表中的类（class）。不过，也可以利用它通过 JavaScript 来改变带有指定 class 的 HTML 元素。

[http://www.w3school.com.cn/tags/att\_standard\_class.asp](http://www.w3school.com.cn/tags/att_standard_class.asp)

## border\(table属性\)定义和用法

border 属性规定规定围绕表格的边框的宽度。

border 属性会为每个单元格应用边框，并用边框围绕表格。如果 border 属性的值发生改变，那么只有表格周围边框的尺寸会发生变化。表格内部的边框则是 1 像素宽。

提示：设置 border="0"，可以显示没有边框的表格。

从实用角度出发，最好不要规定边框，而是使用 CSS 来添加[边框样式和颜色](http://www.w3school.com.cn/css/css_border.asp)。

## style\(全局属性\)定义和用法

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

# HTML data-\* 属性定义和用法

data-\* 属性用于存储页面或应用程序的私有自定义数据。

data-\* 属性赋予我们在所有 HTML 元素上嵌入自定义 data 属性的能力。

存储的（自定义）数据能够被页面的 JavaScript 中利用，以创建更好的用户体验（不进行 Ajax 调用或服务器端数据库查询）。

data-\* 属性包括两部分：

* 属性名不应该包含任何大写字母，并且在前缀 "data-" 之后必须有至少一个字符
* 属性值可以是任意字符串

注释：用户代理会完全忽略前缀为 "data-" 的自定义属性。

# esayui data-option 属性

data-options是jQuery Easyui 的一个特殊属性。通过这个属性，可以对easyui组件的实例化可以完全写入到html中，例如：

`<div class="easyui-dialog" style="width:400px;height:200px"`

`data-options="title:'My Dialog',collapsible:true,iconCls:'icon-ok',onOpen:function(){}">`

`dialog content.`

`</div>`

属性，事件，都可以直接写在data-options里面，这样就方便多了。

**  easyui 里面的组件属性，同样可以写在标签里面**。

```
<pre name="code" class="html"> <div class="easyui-accordion" style="width: 220px; height: 356px; margin-left: 150px;       margin-top: 0px; float: left">
        <div title="配置管理" data-options="iconCls:'icon-ok'" style="overflow: auto;        padding: 10px;">
            <ul class="easyui-tree">
                <li>
                    <span>流程配置</span>
                </li>

                <li>
                    <span>公约配置</span>
                </li>


                <li>
                    <span>学生信息分类配置</span>
                </li>

                <li>
                    <span>说明配置</span>
                </li>

            </ul>
        </div>
```

总结：**data-option就是一个可以在标签等容器中显示图标的方法。如：**

![](http://img.blog.csdn.net/20141227215737187?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMDM3NTY2Mw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

treegrid\(树形表格\)

### TreeGrid\(树形表格\)

树形表格用于显示分层数据表格。它是基于数据表格、组合树控件和可编辑表格。树形表格允许用户创建可定制的、异步展开行和显示在多列上的分层数据。

#### toolbar\(来自DataGrid\)

array,selector

顶部工具栏的DataGrid面板。可能的值：  
1\) 一个数组，每个工具属性都和linkbutton一样。  
2\) 选择器指定的工具栏。

在&lt;div&gt;标签上定义工具栏：

```
$('#dg').datagrid({
    toolbar: '#tb'
});
<div id="tb">
<a href="#" class="easyui-linkbutton" data-options="iconCls:'icon-edit',plain:true"/a>
<a href="#" class="easyui-linkbutton" data-options="iconCls:'icon-help',plain:true"/a>
</div>
```

datagrid\(数据表格\)

通过数组定义工具栏：

```
$('#dg').datagrid({
    toolbar: [{
        iconCls: 'icon-edit',
        handler: function(){alert('编辑按钮')}
    },'-',{
        iconCls: 'icon-help',
        handler: function(){alert('帮助按钮')}
    }]
});
```

#### fitcolumns\(来自DataGrid\)

boolean

datagrid\(数据表格\)

真正的自动展开/收缩列的大小，以适应网格的宽度，防止水平滚动。

#### fit\(来自DataGrid-&gt;Panel\)

boolean

panel\(面板\)

当设置为true的时候面板大小将自适应父容器。下面的例子显示了一个面板，可以自动在父容器的最大范围内调整大小。

```
<div style="width:200px;height:100px;padding:5px">
    <div class="easyui-panel" style="width:200px;height:100px"
            data-options="fit:true,border:false">
        Embedded Panel
    </div>
</div>
```

#### rownumbers\(来自DataGrid\)

boolean

如果为true，则显示一个行号列。

treegrid\(树形表格\)

#### idField\(来自TreeGrid\)

string

定义关键字段来标识树节点。**（必须的）**

#### treeField\(来自TreeGrid\)

string

定义树节点字段。**（必须的）**

#### onBeforeLoad\(来自TreeGrid\)

row、param

在请求数据加载之前触发，返回false可以取消加载动作。



