Admin\Controllers\SystemUserController.cs

```
public ActionResult DistributeSocialUnitAccounts(int socialUnitType, int count)
{
 try
            {
                if ((socialUnitType == (int)SocialUnitType.Corporation || socialUnitType == (int)SocialUnitType.SocialOrganization) == false)
                    throw new ApplicationException("对不起，要分配的账号类型必须是非公企业或社会组织管理员账号！");

                if (count < 1)
                    throw new ApplicationException("对不起，要分配的账号数量必须大于零！");

                this._systemUserService.DistributeSocialUnitAccounts(CurrentUser.DivisionNumber, socialUnitType, count, CurrentUserNumber);

                return this.Ajax();
            }
            catch (Exception ex)
            {
                logger.Error("ERROR", ex);
                return this.AjaxException(this.ControllerContext, ex);
            }            
}
```

1、判断是不是分配非公账号（与社会组织区分开）

2、判断要分配的账号是不是大于0

3、调用

\Tx.Party.Services\Admin\ISystemUserService.cs 的 DistributeSocialUnitAccounts



