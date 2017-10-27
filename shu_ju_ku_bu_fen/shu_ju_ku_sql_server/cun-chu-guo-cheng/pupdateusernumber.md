-- =============================================

-- 开发人员:

-- 开发日期: 2017-10

-- 功    能: 修改创建用户

-- &lt;参数定义&gt;

-- &lt;param name="UserNumber"&gt;原来的用户编码&lt;/param&gt;

-- &lt;param name="NewUserNumber"&gt;新的用户编码&lt;/param&gt;

-- &lt;/参数定义&gt;

-- 测    试: \[dbo\].\[p\_UpdateUserNumber\] @UserNumber = 510200000000, @NewUserNumber = 510300000000

-- =============================================

```
USE [tx_NewParty_Pro]
GO
/****** Object:  StoredProcedure [dbo].[p_UpdateUserNumber]    Script Date: 2017/10/27 11:41:07 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
```



##### GO

官方说法是：GO只是SQL Server管理器（SSMS）中用来提交T-SQL语句的一个标志

我的理解是：GO相当于一个.sql文件的结束标记

```
declare @a int
set @a=1
select @a
```

成功执行

```
declare @a int
go
set @a=1
select @a
```

失败：消息 137，级别 15，状态 1，第 1 行

必须声明标量变量 "@a"。

总结：我们都知道如果一个变量@a是声明在a.sql文件中的，那么在b.sql中是不能为@a赋值的，因为这根本就是两个脚本文件。而**GO语句正是起到了分割.sql文件的作用。**

```
select * from [Admin].[Module]
select * from [Admin].[Role]
go 2
```

执行了两次 会返回4个记录。

```
select * from [Admin].[Module]
go
select * from [Admin].[Role]
go 2
```

go 分开了 两条语句，第一条执行了一次，第二条执行了两次。共返回3个记录集

