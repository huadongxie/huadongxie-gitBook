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

Tx.Party.MvcUI\Areas\basedata\Views\AdministrativeDivision\AdministrativeDivision.cshtml

中使用了easyUI 的TreeGrid树形表格

### TreeGrid\(树形表格\)

树形表格用于显示分层数据表格。它是基于数据表格、组合树控件和可编辑表格。树形表格允许用户创建可定制的、异步展开行和显示在多列上的分层数据。

####  data-option 属性

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



### 

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

#### onLoadError\(来自TreeGrid\)

数据加载失败的时候触发，参数和jQuery的$.ajax\(\)函数的'error'回调函数一样。

#### onSelect（来自TreeGrid）

在用户选择的时候触发，返回false则取消该动作。**（该事件自1.4版开始可用）**

#### singleselect\(来自datagrid\)

boolean

如果为true，则只允许选择一行。

