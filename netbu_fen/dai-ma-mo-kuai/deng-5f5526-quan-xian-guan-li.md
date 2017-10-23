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

exp:[http://localhost:37772/Admin/SystemUser/ListSubDivision?id=510801000000](http://localhost:37772/Admin/SystemUser/ListSubDivision?id=510801000000)

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

1、判断选择的行政区

2、判读是否有此行政区的数据权限。

3、查询数据库，得到数据 ,转化成josn格式，返回View

测试地址

```
http://localhost:37772/basedata/PartyOrganization/ListDivisionPartyOrganization?page=1&rows=10&divisionNumber=510801000000
```

exp:返回数据

```
{
  "Scripts": "",
  "success": true,
  "clientCode": 0,
  "internalHttpCode": 200,
  "httpStatusCode": 200,
  "message": "OK",
  "total": 2,
  "errors": [],
  "rows": [
    {
      "DivisionName": "东河镇",
      "PartyCategoryText": "党总支部",
      "PartyOrganSocialUnitText": "法人单位",
      "PartyOrganizationSocialUnitText": null,
      "PartyOrganizationId": 20,
      "PartyCategoryId": 4,
      "DivisionNumber": 510821100000,
      "Name": "雅化集团旺苍化工有限公司总支委员会",
      "Secretary": "李文乾",
      "Contact": "雷伟",
      "Telephone": "13547164768",
      "PartyOrganSocialUnit": 2,
      "CollectedBy": null,
      "CollectedOn": null,
      "SecretarySigned": false,
      "SecretarySignedOn": null,
      "CommitteeSealed": null,
      "CommitteeSealedOn": null,
      "Status": 0,
      "VersionNumber": 8,
      "CreatedBy": 51082110000000201,
      "CreatedOn": "2017-09-28 14:30:23",
      "ModifiedBy": 51000000000000001,
      "ModifiedOn": "2017-10-21 14:18:42",
      "Description": "asdf"
    },
    {
      "DivisionName": "嘉川镇",
      "PartyCategoryText": "党委",
      "PartyOrganSocialUnitText": "法人单位",
      "PartyOrganizationSocialUnitText": null,
      "PartyOrganizationId": 21,
      "PartyCategoryId": 3,
      "DivisionNumber": 510821101000,
      "Name": "旺苍县第六建筑工程公司党支部",
      "Secretary": "张明玉",
      "Contact": "张明玉",
      "Telephone": "13518323720",
      "PartyOrganSocialUnit": 2,
      "CollectedBy": null,
      "CollectedOn": null,
      "SecretarySigned": false,
      "SecretarySignedOn": null,
      "CommitteeSealed": null,
      "CommitteeSealedOn": null,
      "Status": 0,
      "VersionNumber": 6,
      "CreatedBy": 51082110100000601,
      "CreatedOn": "2017-09-28 21:05:22",
      "ModifiedBy": 51000000000000001,
      "ModifiedOn": "2017-10-21 14:27:50",
      "Description": null
    }
  ],
  "footer": null
}
```

元组是一种数据结构，具有特定数量和元素序列。元组的一个示例是用于存储人员的姓名等标识符的第一个元素，第二个元素和人员收入中该年度第三个元素中的每一年中的数据结构具有三个元素 （称为 3 元组或三元组）。.NET Framework 直接支持具有 1 到 7 元素的元组。此外，您可以创建由嵌套中的元组对象的元组的八个或多个元素[Rest](https://msdn.microsoft.com/zh-cn/library/dd386918%28v=vs.110%29.aspx)属性[Tuple&lt;T1, T2, T3, T4, T5, T6, T7, TRest&gt;](https://msdn.microsoft.com/zh-cn/library/dd383325%28v=vs.110%29.aspx)对象。

元组常用四种方法︰

* 来表示一组数据。例如，一个元组可以表示的数据库记录，并且其组件可以表示每个字段的记录。

* 若要提供轻松访问和数据集的操作。

* 若要从方法返回多个值，而无需使用**out**参数 （在 C\# 中\) 或**ByRef**参数 （在 Visual Basic 中\)。

* 若要将多个值传递给通过单个参数的方法。例如，[Thread.Start\(Object\)](https://msdn.microsoft.com/zh-cn/library/6x4c42hc%28v=vs.110%29.aspx)方法只有一个参数，允许你提供一个线程在启动时执行的方法的值。如果你提供[Tuple&lt;T1, T2, T3&gt;](https://msdn.microsoft.com/zh-cn/library/dd387150%28v=vs.110%29.aspx)对象作为方法自变量，则可以提供有三个项的数据的线程的启动例程。

```
Tuple<int, IList<PartyOrganization>> result = this._partyOrganizationService.ListDivisionPartyOrganization(parameter, CurrentUser);
```

ListDivisionPartyOrganization\(parameter, CurrentUser\);

在PartyOrganizationservice.cs中实现。

```
 SqlMultiTablePageParameter param = new SqlMultiTablePageParameter(parameter.page, parameter.rows, OrderExpression.Asc("po.PartyOrganizationId"));
```

SqlMultiTablePageParameter 定义在TX.Query 中 Tx.Core.dll

```
namespace Tx.Query
{
    public class SqlMultiTablePageParameter : MultiTableParameter
    {
        public SqlMultiTablePageParameter(int pageIndex, int pageSize);
        public SqlMultiTablePageParameter(int pageIndex, int pageSize, OrderExpression orderExpression);

        public int PageIndex { get; set; }
        public int PageSize { get; set; }
        public int StartRow { get; }
        public override string CommandText { get; }
    }
}
```

其中 SqlMultiTablePageParameter构造函数实现如下\(Tx.Core.dll\)

```
public SqlMultiTablePageParameter(int pageIndex, int pageSize, OrderExpression orderExpression) : this(pageIndex, pageSize)
{
    if (orderExpression > null)
    {
        base.OrderExpressions.Add(orderExpression);
    }
}

 

```



MultiTableParameter  定义在Tx.Query中

```
 public abstract class MultiTableParameter : AbstractParameter
    {
        protected MultiTableParameter();

        public IList<IExpression> FromExpressions { get; }
        public override string FromCommandText { get; }

        public MultiTableParameter AddFromExpr(FromExpression exp);
        public MultiTableParameter AddFromExpr(LogicExpression exp);
        public MultiTableParameter AddFromExpr(SimpleExpression exp);
        public MultiTableParameter AddFromExpr(CompareExpression exp);
        public MultiTableParameter AddFromExpr(SegmentExpression exp);
    }
```

AbstractParameter 定义在 Tx.Query中

```
  public abstract class AbstractParameter
    {
        protected AbstractParameter();

        public string OrderByCommandText { get; }
        public IList<IExpression> OrderExpressions { get; }
        public string WhereCommandText { get; }
        public IList<IExpression> HavingExpressions { get; }
        public IList<IExpression> GroupExpressions { get; }
        public IList<IExpression> WhereExpressions { get; }
        public string SelectCommandText { get; }
        public IList<IExpression> SelectExpressions { get; }
        public virtual string FromCommandText { get; }
        public virtual string CommandText { get; }

        public AbstractParameter AddGroupExpr(GroupExpression exp);
        public AbstractParameter AddHavingExpr(SimpleExpression exp);
        public AbstractParameter AddHavingExpr(LogicExpression exp);
        public AbstractParameter AddOrderExpr(OrderExpression exp);
        public AbstractParameter AddSelectExpr(SelectExpression exp);
        public AbstractParameter AddSelectExprs(params SelectExpression[] exps);
        public AbstractParameter AddWhereExpr(SegmentExpression exp);
        public AbstractParameter AddWhereExpr(SimpleExpression exp);
        public AbstractParameter AddWhereExpr(LogicExpression exp);
        public void AssignAdvancedQueryParam(IList<FieldParam> paramList);
    }
```



