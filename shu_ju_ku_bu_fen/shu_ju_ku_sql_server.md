## 数据库sql Server {#sql-server}

### 生成测试数据

1、生成社会组织数据

declare @Id int

declare @leader varchar(20)

declare @name varchar(20)

set @Id = 1

while @Id &lt;10

begin

set @leader = &#039;负责人&#039;+ convert(varchar(20),@Id)

set @name = &#039;社会单位&#039;+ convert(varchar(20),@Id)

Insert into basedata.SocialUnitBase(SocialUnitId,SocialUnitName,RegisteredNumber,Status,VersionNumber,CreatedBy,CreatedOn)

values(100+ @Id,@name,@Id,0,1,&#039;系统管理员&#039;,&#039;2017-09-12 13:41:15.150&#039;)

Insert into basedata.SocialUnit(SocialUnitId,Leader) values(100+ @Id,@leader)

set @Id = @Id +1

end

1.1 数据库mysql