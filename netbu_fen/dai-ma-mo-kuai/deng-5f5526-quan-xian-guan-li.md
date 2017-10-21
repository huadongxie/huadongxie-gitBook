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

其中 510000000000 是当前 用户的权限掩码。
