Tx.Party.Services\Admin\SystemUserService.cs

```
public int DistributeSocialUnitAccounts(long divisionNumber, int socialUnitType, long accountCount, long createdBy)
```

、使用事务 TransactionScope

定义变量 firstSocialUnitNumber    ：根据参数判断是非公还是社会组织的号码，分别从GetNextCorporationNumber和GetNextSocialOrganizationNumber中返回

2、调用方法

\Tx.Party.DataAccess\BaseDAO.cs GetNextCorporationNumber

```
        public long GetNextCorporationNumber(long divisionNumber, long stepValue = 1)
```

获取指定行政区划编码的下一个有效非公企业编码

1、调用存储过程  p\_GetNextCorporationNumber ，加入参数 DivisionNumber（区划编码），StepValue（步长），NextNumber（下一个编码）

exp:用户admin登录操作 admin编号位 51000000000000001，admin区划编号位 510000000000

返回值计算出来 为  510000000000021。

3、根据出传入的accountCount 数量 进行循环。

```
3.1  新建一个 SystemUser 对象 ，并对属性赋值。UserNumber = \(firstSocialUnitNumber + index\) \* 100 + 1

                                                                                 UserNumber = 51000000000002101

                    PrivilegeMask1 = \(firstSocialUnitNumber + index\) \* 100,
```

PrivilegeMask1 = 51000000000002100

```
              PrivilegeMask2 = \(firstSocialUnitNumber + index\) \* 100 + 99,
```

PrivilegeMask2 = 51000000000002199

3.2调用\Tx.Party.DataAccess\Admin\SystemUserDAO.cs中的CreateDefaultUser

```
     3.2.1根据传入的参数 SystemUser\(一个对象）
```

```
string sql = @"MERGE [Admin].[SystemUser] AS t
                           USING (SELECT DivisionNumber = @DivisionNumber, SocialUnitType = @SocialUnitType, UserNumber = @UserNumber, UserName = @UserName, LoginName = @LoginName, Password = @Password, PrivilegeMask1 = @PrivilegeMask1, PrivilegeMask2 = @PrivilegeMask2,CreatedBy = @CreatedBy, ModifiedBy = @ModifiedBy) AS s
                                ON(s.UserNumber = t.UserNumber)
                           WHEN MATCHED THEN
                                UPDATE SET ModifiedBy = s.ModifiedBy
                           WHEN NOT MATCHED THEN
                                INSERT(DivisionNumber, SocialUnitType, UserNumber, UserName, LoginName, Password, PrivilegeMask1, PrivilegeMask2, Opened, CreatedBy, CreatedOn) 
                                VALUES(s.DivisionNumber, s.SocialUnitType, s.UserNumber, s.UserName, s.LoginName, s.Password, s.PrivilegeMask1, s.PrivilegeMask2, 1, s.CreatedBy, GETDATE());";
```

```
DatabaseProviderFactory factory = new DatabaseProviderFactory();
            Database db = factory.CreateDefault();
            DbCommand command = db.GetSqlStringCommand(sql);
```

           return db.ExecuteNonQuery\(command\);

执行SQL语句，提交数据执行。





