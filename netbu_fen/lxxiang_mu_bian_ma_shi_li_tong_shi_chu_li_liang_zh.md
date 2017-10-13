## lx项目编码实例 -同时处理两张表的数据。 {#lx}

父表：SocialUnitBase

子表：SocialUnit

D:\TXLC\源代码\Tx.Party\Tx.Party.Services\basedata\SocialUnitService.cs

//创建社会单位档案记录

public int CreateSocialUnit(SocialUnit socialUnit)

{

socialUnit.SocialUnitId = this._socialUnitDAO.GetNextValue(&quot;basedata.SocialUnitBase&quot;, &quot;SocialUnitId&quot;, 1, 1);

int affectedRecords = 0;

//新建一个事务，插入父表和子表

using (TransactionScope scope = new TransactionScope())

{

affectedRecords += this._socialUnitBaseDAO.Insert(socialUnit);

affectedRecords += this._socialUnitDAO.Insert(socialUnit);

scope.Complete();

}

return affectedRecords;

}