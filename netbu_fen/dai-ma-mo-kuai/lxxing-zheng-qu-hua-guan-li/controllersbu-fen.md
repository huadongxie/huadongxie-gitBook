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

**return this.Ajax\(result\)**  Ajax方法是  项目DLL（Tx.Web.MVC）中封装的一个方法

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

传入参数   PartyOrganization result 是一个     /// 党组织档案数据实体类  
 形式参数是 object data

```
    public partial class PartyOrganization
    {
        /// <summary>
        /// 行政区划名称
        /// </summary>
        public string DivisionName { get; set; }

        /// <summary>
        /// 党组织类别名称
        /// </summary>
        public string PartyCategoryText { get; set; }

        /// <summary>
        /// 党组织所在单位情况
        /// </summary>
        public string PartyOrganSocialUnitText { get; set; }

        /// <summary>
        /// 社会单位
        /// </summary>
        public string PartyOrganizationSocialUnitText { get; set; }
    }
```

返回值为 **public static AjaxResult ：ActionResult 其中 ActionResult 是 System.Web.Mvc 命名空间 中定义的**

[https://msdn.microsoft.com/zh-cn/library/system.web.mvc.actionresult\(v=vs.118\).aspx](https://msdn.microsoft.com/zh-cn/library/system.web.mvc.actionresult%28v=vs.118%29.aspx)

# ActionResult 类

封装一个操作方法的结果并用于代表该操作方法执行框架级操作。

## public abstract class AjaxResult : ActionResult

```

```

实现方法为：

```
  public static AjaxResult Ajax(this Controller controller, object data)
{
    return new AjaxDataResult(data);
}
```

```
public AjaxDataResult(object data)
{
    AjaxResponseModel model1 = new AjaxResponseModel {
        total = 0,
        rows = data
    };
    base.Data = model1;
}

AjaxDataResult 的实现：
```

base.data  定义为： public AjaxResponseModel{get;set}

```
public AjaxResponseModel()
{
    this.scripts = string.Empty;
    this._clientCode = 0;
    this._internalHttpCode = 200;
    this._httpStatusCode = 200;
    this._message = "OK";
    this._total = 0;
    this._errors = new List<ValidateError>();
}
```

```
public class AjaxResponseModel
{
    // Fields
    private int _clientCode;
    private IList<ValidateError> _errors;
    private int _httpStatusCode;
    private int _internalHttpCode;
    private string _message;
    private int _total;
    [CompilerGenerated, DebuggerBrowsable(DebuggerBrowsableState.Never)]
    private object <footer>k__BackingField;
    [CompilerGenerated, DebuggerBrowsable(DebuggerBrowsableState.Never)]
    private object <rows>k__BackingField;
    private string scripts;

    // Methods
    public AjaxResponseModel();
    public void AddError(string filedName, string message);

    // Properties
    public int clientCode { get; set; }
    public IList<ValidateError> errors { get; }
    public object footer { get; set; }
    public int httpStatusCode { get; set; }
    public int internalHttpCode { get; set; }
    public string message { get; set; }
    public object rows { get; set; }
    public string Scripts { get; set; }
    public bool success { get; }
    public int total { get; set; }
}
```



