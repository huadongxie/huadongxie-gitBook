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

ActionResult 是命名空间 namespace System.Web.Mvc 中定义的 类。

封装一个操作方法的结果并用于代表该操作方法执行框架级操作。

# System.Web.Mvc 命名空间

System.Web.Mvc命名空间包含一些类和接口，它们支持用于创建 Web 应用程序的 ASP.NET 模型视图控制器 \(MVC\) 框架。该命名空间包含表示控制器、控制器工厂、操作结果、视图、分部视图以及模型联编程序等的类。

