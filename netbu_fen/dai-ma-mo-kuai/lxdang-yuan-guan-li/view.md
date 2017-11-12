\_partymember.cshtml

1. JS部分

         1.1    //键盘事件 function keydown\(\)

```
   function keydown() {
        if (event.keyCode == 13) {
            query_member();
        }
    }   
```

         1.2 query\_member

```
    function query_member() {
        $('#dataGrid1').datagrid('load');
    }
```

         1.3新增党员档案记录 add\_member

```
   function add_member() {
        top.currentDialog = new Object();
        top.currentDialog.editType = 'add';
        top.currentDialog.saveDataUrl = '@Url.Content("~/basedata/PartyMember/CreatePartyMember")';
        top.currentDialog.syncRow = appendRow;

        showWindow('editDialog1', "新增党员档案", '@Url.Content("~/basedata/PartyMember/EditPartyMember")', 640, 480);
    }
```

        1.4增加行appendRow

        1.5更新行事件updateRow

         1.6         

1. table部分
2. toolbar1部分



