在View中一般以url属性指定Controllers的方法以获取数据。

```
                    $('#dataGrid1').datagrid('options').url = '@Url.Content("~/basedata/PartyOrganization/ListPartyOrganizationSocialUnit")';
```

ListPartyOrganizationSocialUnit 方法 会返回 json 格式的数据。

```
 public ActionResult ListPartyOrganizationSocialUnit(int partyOrganizationId)
        {
            try
            {
                QueryParameter param = new QueryParameter() { TableName = "basedata.V_SocialUnitPartyOrganization" };
                param.AddWhereExpr(SimpleExpression.Equal("PartyOrganizationId", DbType.Int32, partyOrganizationId));
                var result = this._partyOrganizationService.GetObjects<SocialUnitPartyOrganization>(param);

                return this.Ajax(result);
            }
            catch (Exception ex)
            {
                logger.Error("ERROR", ex);
                return this.AjaxException(this.ControllerContext, ex);
            }
        }
```

ActionResult 是命名空间 namespace System.Web.Mvc 中定义的 类





