Tx.Party.Services\Admin\SystemUserService.cs

```
public int DistributeSocialUnitAccounts(long divisionNumber, int socialUnitType, long accountCount, long createdBy)
```

1、使用事务 TransactionScope

定义变量 firstSocialUnitNumber    ：根据参数判断是非公还是社会组织的号码，分别从GetNextCorporationNumber和GetNextSocialOrganizationNumber中返回

2、调用方法

\Tx.Party.DataAccess\BaseDAO.cs

```

```



