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

