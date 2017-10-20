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



# Controller 类

提供用于响应对 ASP.NET MVC 网站所进行的 HTTP 请求的方法。



this.Ajax\(result\)  Ajax方法是  项目DLL（Tx.Web.MVC）中封装的一个方法

```
public static class AjaxController
{
    // Methods
    public static AjaxResult Ajax(this Controller controller);
    public static AjaxResult Ajax(this Controller controller, object data);
    public static AjaxResult Ajax(this Controller controller, int total, object data);
    public static AjaxResult Ajax(this Controller controller, int total, object data, object footer);
    public static AjaxErrorResult AjaxError(this Controller controller, ControllerContext context, string message = "对不起，处理你的请求时发生错误!");
    public static AjaxErrorResult AjaxError(this Controller controller, ControllerContext context, int clientCode, string message = "对不起，处理你的请求时发生错误!");
    public static AjaxExceptionResult AjaxException(this Controller controller, ControllerContext context, Exception ex);
    public static AjaxResult AjaxValidate(this Controller controller, ControllerContext context);
}
```



