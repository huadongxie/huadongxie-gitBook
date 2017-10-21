#### 判断用户权限

[http://localhost:37772/Admin/SystemUser/ListSubDivision](http://localhost:37772/Admin/SystemUser/ListSubDivision)

ListSubDivision\(Int64? id\) 传入了参数。如果是admin类账户 传入的是null

```
                if (id.HasValue && HasDivisionPrivilege(id.Value) == false)
                    throw new ApplicationException("对不起，您要操作的行政区划不在您的操作权限范围内！");
```

这条语句 HasDivisionPrivilege 就不会执行。

同样当选择 树形菜单 treeGrid 进行数据 筛选的时候，也是 通过 HasDivisionPrivilege来判断权限。

exp: 以admin身份选中  广元市的时候，传入id 为 510801000000

![](/assets/TreeGridSelcet1.png)

```
        protected bool HasDivisionPrivilege(Int64 divisionNumber)
        {
            QueryParameter param = new QueryParameter() { TableName = string.Format("[basedata].[f_GetRecursiveDivision]({0})", CurrentUser.DivisionNumber) };
            param.AddWhereExpr(SimpleExpression.Equal("DivisionNumber", DbType.Int64, divisionNumber));

            return this._dataService.Exists(param);
        }
```

CommandText = "SELECT  \*  FROM \[basedata\].\[f\_GetRecursiveDivision\]\(510000000000\) "

其中 510000000000 是当前 用户的权限掩码。通过 f\_GetRecursiveDivision（数据库的表值函数）返回admin的数据的行政区划内码

```
 string tableName = (id.HasValue) ? string.Format("[basedata].[f_GetSubAdministrativeDivision]({0})", id.Value) : string.Format("[basedata].[f_GetAdministrativeDivision]({0})", CurrentUser.DivisionNumber);

                QueryParameter param = new QueryParameter()
                {
                    TableName = tableName
                };

                DataSet dataSet = this._dataService.GetData(param);
```

然后继续执行，如果id.HasValue有值（510801000000 广元的数据掩码），就调用f\_GetSubAdministrativeDivision（（数据库的表值函数））返回 广元 的行政区内码，以便在只调出广元的相关数据。

exp:http://localhost:37772/Admin/SystemUser/ListSubDivision?id=510801000000

```
[{"DivisionName":"旺苍县","DivisionNumber":510821000000,"DivisionCategoryText":null,"Opened":true,"state":"closed","Description":null}]
```



右边DataGrid控件 

在

```
        function dataGrid1_onBeforeLoad(param) {
            if (_divisionNumber) {
                param.divisionNumber = _divisionNumber;
                param.searchText = $('#tbSearchText').textbox('getValue');

                if ($('#dataGrid1').datagrid('options').url == undefined) {
                    $('#dataGrid1').datagrid('options').url = '@Url.Content("~/basedata/PartyOrganization/ListDivisionPartyOrganization")';
                }
            }
        }
```

/basedata/PartyOrganization/ListDivisionPartyOrganization

```
public ActionResult ListDivisionPartyOrganization(PartyOrganizationParameter parameter)
        {
            try
            {
                if (parameter.divisionNumber.HasValue == false)
                    throw new ApplicationException("对不起，你还没有选择行政区！");

                if (HasDivisionPrivilege(parameter.divisionNumber.Value) == false)
                    throw new ApplicationException("对不起，你没有区划代码为【{0}】的行政区操作权限！");

                Tuple<int, IList<PartyOrganization>> result = this._partyOrganizationService.ListDivisionPartyOrganization(parameter, CurrentUser);

                return this.Ajax(result.Item1, result.Item2);
            }
            catch (Exception ex)
            {
                logger.Error("ERROR", ex);
                return this.AjaxException(this.ControllerContext, ex);
            }
        }
```



将PartyOrganizationParameter parameter 作为参数传递进来



