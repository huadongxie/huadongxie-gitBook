### CorporationEdit.cshtml

```
<a href="javascript:void(0)" class="easyui-linkbutton" iconcls="icon-save" onclick="save()">保存</a>
```

保存按钮调用save\(）方法

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

# submit\(\) 方法

当提交表单时，会发生 submit 事件。

该事件只适用于表单元素。

submit\(\) 方法触发 submit 事件，或规定当发生 submit 事件时运行的函数。

## 将函数绑定到 submit 事件

```
$(selector).submit(function)


```



