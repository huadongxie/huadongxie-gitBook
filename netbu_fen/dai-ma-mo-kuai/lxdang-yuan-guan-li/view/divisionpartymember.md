1、@{。。。。} 部分

2、@section Scripts{...} 部分

3、easyui-layout 控件

3.1  左边树形部分

```
<div data-options="region:'west',split:true,title:'行政区划',collapsible:true" style="width: 350px;">

        @Html.Partial("_DivisionTreePartial")

</div>
```

3.2 右边数据表部分

```
    <div data-options="region:'center', title:'党员列表'">

        @Html.Partial("_PartyMember")

    </div>
```



