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

##### 

```
ALTER PROCEDURE [dbo].[p_UpdateUserNumber] 
    @UserNumber bigint,
    @NewUserNumber bigint
AS
BEGIN

    SET XACT_ABORT ON;

    IF NOT EXISTS(SELECT 1 FROM [Admin].[SystemUser] WHERE UserNumber = @UserNumber) RETURN 1;
    IF NOT EXISTS(SELECT 1 FROM [Admin].[SystemUser] WHERE UserNumber = @NewUserNumber) RETURN 2;

    BEGIN TRANSACTION;

   DECLARE @DivisionNumber bigint, @NewDivisionNumber bigint;

   SELECT @DivisionNumber = DivisionNumber FROM [Admin].[SystemUser] WHERE UserNumber = @UserNumber;
   SELECT @NewDivisionNumber = DivisionNumber FROM [Admin].[SystemUser] WHERE UserNumber = @NewUserNumber;

        -- 更新社会单位档案区划代码
     UPDATE [basedata].[SocialUnitBase] 
       SET DivisionNumber = @NewDivisionNumber, CreatedBy = @NewUserNumber, ModifiedBy = @NewUserNumber
     WHERE CreatedBy = @UserNumber;

     -- 更新党组织档案区划代码
     UPDATE [basedata].[PartyOrganization]
       SET DivisionNumber = @NewDivisionNumber, CreatedBy = @NewUserNumber, ModifiedBy = @NewUserNumber
     WHERE CreatedBy = @UserNumber;

    -- 更新党员档案
     UPDATE [basedata].[PartyMember]
        SET CreatedBy = @NewUserNumber, ModifiedBy = @NewUserNumber
      WHERE CreatedBy = @UserNumber

    COMMIT TRANSACTION;

END
```

@UserNumber bigint, 定义参数。

AS

BEGIN

END

中间包含的是



