## Lx项目中数据关联页面 {#lx}

在DivisionPartyOrganization.cshtml 中 点击”修改”按钮的时候

**&lt;**td**&gt;&lt;**a id**=**"btnEdit" href**=**"javascript:void\(0\)" class**=**"easyui-linkbutton" iconcls**=**"icon-edit" plain**=**"true" disabled**=**"true" onclick**=**"edit\_organ\(\)"**&gt;**修改**&lt;/**a**&gt;&lt;/**td**&gt;**

**会调用edit\_organ\(\)**

**var row = $\('\#dataGrid1'\).treegrid\('getSelected'\);**

**执行完成后 row 对象得到数据：**

row:

CollectedBy:null

CollectedOn:null

CommitteeSealed:null

CommitteeSealedOn:null

Contact:"这是测试"

CreatedBy:51000000000000000

CreatedOn:"2017-09-29 15:53:16"

Description:"这是测试"

DivisionName:"四川省"

DivisionNumber:510000000000

ModifiedBy:51000000000000000

ModifiedOn:"2017-10-06 10:22:21"

Name:"这是测试"

PartyCategoryId:4

PartyCategoryText:"党总支部"

PartyOrganSocialUnit:2

PartyOrganSocialUnitText:"法人单位"

PartyOrganizationId:20

PartyOrganizationSocialUnitText:null

Secretary:"这是测试"

SecretarySigned:false

SecretarySignedOn:null

Status:0

Telephone:"139888888888"

VersionNumber:3

**proto**:Object

转到EditPartyOrganization.cshtml

$\(function \(\) {….}

javaScript 代码，自动执行。

**if** **\(**top**.**\_currentDialog**.**editType **==** 'edit'**\)** **{**

$**\(**'\#form1'**\).**form**\(**'load'**,** '@Url.Content\("~/basedata/PartyOrganization/LoadPartyOrganization"\)'**\);**

**};**

function dataGrid1\_onBeforeLoad**\(**param**\)** **{**

**if** **\(**\_divisionNumber**\)** **{**

param**.**divisionNumber **=** \_divisionNumber**;**

param**.**searchText **=** $**\(**'\#tbSearchText'**\).**textbox**\(**'getValue'**\);**

**if** **\(**$**\(**'\#dataGrid1'**\).**datagrid**\(**'options'**\).**url **==** undefined**\)** **{**

$**\(**'\#dataGrid1'**\).**datagrid**\(**'options'**\).**url **=** '/basedata/PartyOrganization/ListDivisionPartyOrganization'**;**

**}**

**}**

**}**

### **easyui datagrid 的数据加载** {#easyui-datagrid}

easyui datagrid加载数据只有两种方式：一种是ajax加载目标url返回的json数据；另一种是加载js对象，也就是使用loadDate方法。

#### Url加载数据 {#url}

调用方式

可以将url写在DOM里面或者声明datagrid对象的url属性。

&lt;table id="tt" style="width:700px;height:auto" title="DataGrid" idField="itemid" url="datagrid\_data2.json"&gt;

或

$\('\#test'\).datagrid\({

url:'datagrid\_data2.json'

}\);

相关方法

