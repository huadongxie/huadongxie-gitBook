BEGIN 和 END 语句用于将多个 Transact-SQL 语句组合为一个逻辑块。在控制流语句必须执行包含两条或多条 Transact-SQL 语句的语句块的任何地方，都可以使用 BEGIN 和 END 语句。

例如，当 IF 语句仅控制一条 Transact-SQL 语句的执行时，不需要使用 BEGIN 或 END 语句：

 IF \(@@ERROR &lt;&gt; 0\)

   SET @ErrorSaveVariable = @@ERROR

如果 @@ERROR 为 0，则仅跳过 SET 语句。

用 BEGIN 和 END 语句可以使 IF 语句在计算结果为 FALSE 时跳过语句块：

IF \(@@ERROR &lt;&gt; 0\)

BEGIN

   SET @ErrorSaveVariable = @@ERROR

   PRINT 'Error encountered, ' + 

         CAST\(@ErrorSaveVariable AS VARCHAR\(10\)\)

END

BEGIN 和 END 语句必须成对使用：任何一个均不能单独使用。BEGIN 语句单独出现在一行中，后跟 Transact-SQL 语句块。最后，END 语句单独出现在一行中，指示语句块的结束。

