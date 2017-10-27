打开SQL Server 的管理工具，选中需要创建存储过程的数据库，找到“可编程性”，展开后可以看到“存储过程”。右键点击它，选择“新建存储过程”，右侧的编辑窗口打开了，里面装着微软自动生成的[SQL Server](http://hovertree.com/menu/sqlserver/)创建存储过程的语句。

将存储过程的名字，参数，操作语句写好后，点击语法分析，没有错误就直接“F5”运行就好了，存储过程创建完毕，以下是一个基本的存储过程的代码：（数据库生成的模板）

```
-- ================================================
-- Template generated from Template Explorer using:
-- Create Procedure (New Menu).SQL
--
-- Use the Specify Values for Template Parameters 
-- command (Ctrl-Shift-M) to fill in the parameter 
-- values below.
--
-- This block of comments will not be included in
-- the definition of the procedure.
-- ================================================
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author:		<Author,,Name>
-- Create date: <Create Date,,>
-- Description:	<Description,,>
-- =============================================
CREATE PROCEDURE <Procedure_Name, sysname, ProcedureName> 
	-- Add the parameters for the stored procedure here
	<@Param1, sysname, @p1> <Datatype_For_Param1, , int> = <Default_Value_For_Param1, , 0>, 
	<@Param2, sysname, @p2> <Datatype_For_Param2, , int> = <Default_Value_For_Param2, , 0>
AS
BEGIN
	-- SET NOCOUNT ON added to prevent extra result sets from
	-- interfering with SELECT statements.
	SET NOCOUNT ON;

    -- Insert statements for procedure here
	SELECT <@Param1, sysname, @p1>, <@Param2, sysname, @p2>
END
GO
```



