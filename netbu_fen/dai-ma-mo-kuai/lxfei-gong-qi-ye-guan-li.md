### CorporationEdit.cshtml 

    &lt;a href="javascript:void\(0\)" class="easyui-linkbutton" iconcls="icon-save" onclick="save\(\)"&gt;保存&lt;/a&gt;

保存按钮调用 js save\(\)方法

```
 function save() {
            $('#form1').form('submit', {
                url: top._currentDialog.saveDataUrl,

                onSubmit: function (param) {
                    param.HasPartyOrganization = $('#switchButton1').switchbutton('options').checked;
                    
                    return $('#form1').form('validate');
                },
                success: function (result) {
                    var result = eval('(' + result + ')');

                    if (result.success) {
                        if (top._currentDialog.syncRow) {
                            top._currentDialog.syncRow(result.rows);
                        }
                        exit();
                    } else {
                        $.messager.alert('提示信息', result.message, 'error');
                    }
                }
            });
        }
```

$（‘\#form1’）.form\('submit',....\) 方法

