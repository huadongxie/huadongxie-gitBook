存储过程有三种返回:

1. 用return返回数字型数据

2. 用返回参数返回结果,可以返回各种数据类型\(通过游标来循环查询结果每一行\)

3. 直接在存储过程中用select返回结果集,可以是任意的select语句,这意味着是任意的返回结果集.

方法一:用return返回数字型数据

1、创建存储过程

```
--SQLSERVER 2005示例数据库
USE AdventureWorks
GO
CREATE PROCEDURE checkstate 
@param VARCHAR(11)
AS
IF (
       SELECT StateProvince
       FROM   Person.vAdditionalContactInfo
       WHERE  ContactID = @param
   ) = 'WA'
    RETURN 1
ELSE
    RETURN 2;
GO
```

2、在存储过程中调用

```
DECLARE @return_status INT;
EXEC @return_status = checkstate '9';  --将存储过程返回值赋给@return_status
SELECT 'Return Status' = @return_status;
GO
```

3、在VS中调用

```
 List<DbParameter> para = new List<DbParameter>();
        para.Add(new SqlParameter("@param", 9));
        SqlParameter pa = new SqlParameter();
        pa.ParameterName = "@return";
        pa.SqlDbType = SqlDbType.Int;
        pa.Direction = ParameterDirection.ReturnValue;
        para.Add(pa);
        int i = DBHelper.ExecuteSql("checkstate", CommandType.StoredProcedure, para);
        Response.Write(para[1].Value.ToString());
```

方法二:用返回参数返回结果,可以返回各种数据类型\(通过游标来循环查询结果每一行\)

1. 创建存储过程

```
--SQLSERVER 2005示例数据库
USE AdventureWorks
GO
CREATE PROCEDURE OutPutValue 
@param VARCHAR(11),
@param2 VARCHAR(11) OUTPUT
AS
IF (
       SELECT StateProvince
       FROM   Person.vAdditionalContactInfo
       WHERE  ContactID = @param
   ) = 'WA'
   SET @param2='Good'
ELSE
   SET @param2='Bad'
GO
```

2. 在存储过程中调用

```
DECLARE @param1 NVARCHAR(100)
DECLARE @param2 NVARCHAR(100)
SET @param1='9'
EXEC OutPutValue '9',@param2 OUTPUT
SELECT @param2

```

3. 在VS中调用

```
 List<DbParameter> para = new List<DbParameter>();
        para.Add(new SqlParameter("@param", "9"));
        SqlParameter pa = new SqlParameter();
        pa.Direction = ParameterDirection.Output;
        pa.ParameterName = "@param2";
        pa.Size = 11;
        para.Add(pa);
        int i = DBHelper.ExecuteSql("OutPutValue ", CommandType.StoredProcedure, para);
        //OutPut返回值
        Response.Write(para[1].Value.ToString());  //输出返回值

```

方法三:直接在存储过程中用select返回结果集,可以是任意的select语句,这意味着是任意的返回结果集

1. 创建存储过程

```
--SQLSERVER 2005示例数据库
USE AdventureWorks
GO
CREATE PROCEDURE ReturnDataTable
AS
BEGIN
SELECT * FROM Person.vAdditionalContactInfo
END 
GO
```

2. 在存储过程中调用

```
EXEC ReturnDataTable

```

3. 在VS中调用

```
//存储过程返回结果集可存放在DataTable
 DataTable dt = DBHelper.GetDataTable("ReturnDataTable", CommandType.StoredProcedure); 
```



