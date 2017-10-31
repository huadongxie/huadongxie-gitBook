Tx.Party.Services\Admin\SystemUserService.cs

```
public int DistributeSocialUnitAccounts(long divisionNumber, int socialUnitType, long accountCount, long createdBy)
```

1、使用事务 TransactionScope

定义变量 firstSocialUnitNumber    ：根据参数判断是非公还是社会组织的号码，分别从GetNextCorporationNumber和GetNextSocialOrganizationNumber中返回

2、调用方法

\Tx.Party.DataAccess\BaseDAO.cs

```
        public long GetNextCorporationNumber(long divisionNumber, long stepValue = 1)
```

获取指定行政区划编码的下一个有效非公企业编码

1、调用存储过程  p\_GetNextCorporationNumber ，加入参数 DivisionNumber（区划编码），StepValue（步长），NextNumber（下一个编码）

exp:用户admin登录操作 admin编号位 51000000000000001，admin区划编号位 510000000000

