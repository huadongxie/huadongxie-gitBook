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

SQL-92 设置语句 

当 SET ANSI\_NULLS 为 ON 时，即使 column\_name 中包含空值，使用 WHERE column\_name = NULL 的 SELECT 语句仍返回零行。                       即使column\_name 中包含非空值，使用 WHERE column\_name &lt;&gt; NULL 的 SELECT 语句仍会返回零行。  
当 SET ANSI\_NULLS 为 OFF 时，等于 \(=\) 和不等于 \(&lt;&gt;\) 比较运算符不遵从 SQL-92 标准。使用 WHERE

column\_name = NULL 的 SELECT 语句返回 column\_name 中包含空值的行。使用 WHERE column\_name &lt;&gt; NULL

的 SELECT 语句返回列中包含非空值的行。此外，使用 WHERE column\_name &lt;&gt; XYZ\_value 的 SELECT 语句返

回所有不为 XYZ\_value 也不为 NULL 的行。

