#### 判断用户权限

http://localhost:37772/Admin/SystemUser/ListSubDivision

ListSubDivision\(Int64? id\) 传入了参数。如果是admin类账户 传入的是null

```
                if (id.HasValue && HasDivisionPrivilege(id.Value) == false)
                    throw new ApplicationException("对不起，您要操作的行政区划不在您的操作权限范围内！");
```

这条语句 HasDivisionPrivilege 就不会执行。



