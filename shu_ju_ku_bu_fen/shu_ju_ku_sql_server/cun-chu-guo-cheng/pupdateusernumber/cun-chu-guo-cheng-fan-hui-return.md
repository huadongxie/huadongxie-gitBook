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



