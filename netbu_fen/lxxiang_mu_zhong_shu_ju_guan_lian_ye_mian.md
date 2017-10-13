## Lx项目中数据关联页面 {#lx}

在DivisionPartyOrganization.cshtml 中 点击”修改”按钮的时候

**&lt;**td**&gt;&lt;**a id**=**&quot;btnEdit&quot; href**=**&quot;javascript:void(0)&quot; class**=**&quot;easyui-linkbutton&quot; iconcls**=**&quot;icon-edit&quot; plain**=**&quot;true&quot; disabled**=**&quot;true&quot; onclick**=**&quot;edit_organ()&quot;**&gt;**修改**&lt;/**a**&gt;&lt;/**td**&gt;**

**会调用edit_organ()**

**var row = $(&#039;#dataGrid1&#039;).treegrid(&#039;getSelected&#039;);**

**执行完成后 row 对象得到数据：**

1.  row:
    1.  CollectedBy:null
    2.  CollectedOn:null
    3.  CommitteeSealed:null
    4.  CommitteeSealedOn:null
    5.  Contact:&quot;这是测试&quot;
    6.  CreatedBy:51000000000000000
    7.  CreatedOn:&quot;2017-09-29 15:53:16&quot;
    8.  Description:&quot;这是测试&quot;
    9.  DivisionName:&quot;四川省&quot;
    10.  DivisionNumber:510000000000
    11.  ModifiedBy:51000000000000000
    12.  ModifiedOn:&quot;2017-10-06 10:22:21&quot;
    13.  Name:&quot;这是测试&quot;
    14.  PartyCategoryId:4
    15.  PartyCategoryText:&quot;党总支部&quot;
    16.  PartyOrganSocialUnit:2
    17.  PartyOrganSocialUnitText:&quot;法人单位&quot;
    18.  PartyOrganizationId:20
    19.  PartyOrganizationSocialUnitText:null
    20.  Secretary:&quot;这是测试&quot;
    21.  SecretarySigned:false
    22.  SecretarySignedOn:null
    23.  Status:0
    24.  Telephone:&quot;139888888888&quot;
    25.  VersionNumber:3
    26.  __proto__:Object

转到EditPartyOrganization.cshtml

$(function () {….}

javaScript 代码，自动执行。

**if** **(**top**.**_currentDialog**.**editType **==** &#039;edit&#039;**)** **{**

$**(**&#039;#form1&#039;**).**form**(**&#039;load&#039;**,** &#039;@Url.Content(&quot;~/basedata/PartyOrganization/LoadPartyOrganization&quot;)&#039;**);**

**};**

function dataGrid1_onBeforeLoad**(**param**)** **{**

**if** **(**_divisionNumber**)** **{**

param**.**divisionNumber **=** _divisionNumber**;**

param**.**searchText **=** $**(**&#039;#tbSearchText&#039;**).**textbox**(**&#039;getValue&#039;**);**

**if** **(**$**(**&#039;#dataGrid1&#039;**).**datagrid**(**&#039;options&#039;**).**url **==** undefined**)** **{**

$**(**&#039;#dataGrid1&#039;**).**datagrid**(**&#039;options&#039;**).**url **=** &#039;/basedata/PartyOrganization/ListDivisionPartyOrganization&#039;**;**

**}**

**}**

**}**

### **easyui datagrid 的数据加载** {#easyui-datagrid}

easyui datagrid加载数据只有两种方式：一种是ajax加载目标url返回的json数据；另一种是加载js对象，也就是使用loadDate方法。

#### Url加载数据 {#url}

调用方式

可以将url写在DOM里面或者声明datagrid对象的url属性。

&lt;table id=&quot;tt&quot; style=&quot;width:700px;height:auto&quot; title=&quot;DataGrid&quot; idField=&quot;itemid&quot; url=&quot;datagrid_data2.json&quot;&gt;

或

$(&#039;#test&#039;).datagrid({

url:&#039;datagrid_data2.json&#039;

});

相关方法