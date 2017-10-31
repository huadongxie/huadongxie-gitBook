### 简介

    Merge关键字是一个神奇的DML关键字。它在SQL Server 2008被引入，它能将Insert,Update,Delete简单的并为一句。MSDN对于Merge的解释非常的短小精悍:”根据与源表联接的结果，对目标表执行插入、更新或删除操作。例如，根据在另一个表中找到的差异在一个表中插入、更新或删除行，可以对两个表进行同步。”,通过这个描述，我们可以看出Merge是关于对于两个表之间的数据进行操作的。

    可以想象出，需要使用Merge的场景比如:

*     数据同步
*     数据转换
*     基于源表对目标表做Insert,Update,Delete操作

### 使用Merge关键字的好处

    首先是更加短小精悍的语句，在SQL Server 2008之前没有Merge的时代，基于源表对目标表进行操作需要分别写好几条Insert,Update,Delete。而使用Merge,仅仅需要使用一条语句就好。下面我们来看一个例子。

```
MERGE 目标表 
USING 源表 
ON 匹配条件 
WHEN MATCHED THEN 
语句 
WHEN NOT MATCHED THEN 
语句;
其中最后语句分号不可以省略，且源表既可以是一个表也可以是一个子查询语句
WHEN NOT MATCHED BY TARGET
表示目标表不匹配，BY TARGET是默认的，所以上面我们直接使用WHEN NOT MATCHED THEN
WHEN NOT MATCHED BY SOURCE
表示源表不匹配，即目标表中存在，源表中不存在的情况。
```

**主要用法：**

merge无法多次更新同一行，也无法更新和删除同一行  


当源表和目标表不匹配时：若数据是源表有目标表没有，则进行插入操作若数据是源表没有而目标表有，则进行更新或者删除数据操作当源表和目标表匹配时：进行更新操作或者删除操作when matched 这个子句可以有两个，当有两个时，第一个子句必须是when matched and condition且两个matched子句只会执行一个，且两个子句必须是一个update和一个delete操作when not matched by source和上面类似

merge icr\_codemap\_bak as a  
using icr\_codemap as b  
on a.COLNAME = b.COLNAME and a.ctcode = b.ctcode  
when matched and b.pbcode &lt;&gt; a.pbcode  
then update set a.pbcode = b.pbcode  
when not matched  
then insert values\(b.colname,b.ctcode,b.pbcode,b.note\)  
;

可以比对字段不一致进行更新

[https://technet.microsoft.com/zh-cn/library/bb510625.aspx](https://technet.microsoft.com/zh-cn/library/bb510625.aspx)  这个是MSDN的网址

在 Merge Matched 操作中，只能允许执行 UPDATE 或者 DELETE 语句。  
在 Merge Not Matched 操作中，只允许执行 INSERT 语句。  
一个 Merge 语句中出现的 Matched 操作，只能出现一次 UPDATE 或者 DELETE 语句，否则就会出现下面的错误 - An action of type 'WHEN MATCHED' cannot appear more than once in a 'UPDATE' clause of a MERGE statement.  
Merge 语句最后必须包含分号，以 ; 结束。

    首先建立源表和目标表，并插入相关的数据,如图1所示。



