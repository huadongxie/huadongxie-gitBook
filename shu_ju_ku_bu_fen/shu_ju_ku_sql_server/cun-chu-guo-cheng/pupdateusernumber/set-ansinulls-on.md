##### **SET ANSI\_NULLS ON**

当 SET ANSI\_NULLS 为 ON 时，即使 column\_name 中包含空值，使用 WHERE column\_name = NULL 的 SELECT 语句仍返回零行。                             即使column\_name 中包含非空值，使用 WHERE column\_name &lt;&gt; NULL 的 SELECT 语句仍会返回零行。

当 SET ANSI\_NULLS 为 OFF 时，等于 \(=\) 和不等于 \(&lt;&gt;\) 比较运算符不遵从 SQL-92 标准。使用 WHERE

column\_name = NULL 的 SELECT 语句返回 column\_name 中包含空值的行。使用 WHERE column\_name &lt;&gt; NULL

的 SELECT 语句返回列中包含非空值的行。此外，使用 WHERE column\_name &lt;&gt; XYZ\_value 的 SELECT 语句返

回所有不为 XYZ\_value 也不为 NULL 的行。

