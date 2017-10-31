在.net 1.1的时代，还没有TransactionScope类，因此很多关于事务的处理，都交给了SqlTransaction和SqlConnection，每个Transaction是基于每个Connection的。这种设计对于跨越多个程序集或者多个方法的事务行为来说，不是非常好，需要把事务和数据库连接作为参数传入。

在.net 2.0后，TransactionScope类的出现，大大的简化了事务的设计。示例代码如下：

```
static void Main(string[] args)
        {
            using (TransactionScope ts = new TransactionScope())
            {
                userBLL u = new userBLL();
                TeacherBLL t = new TeacherBLL();
                u.ADD();
                t.ADD();
                ts.Complete();
            }
        }


```

只需要把需要事务包裹的逻辑块写在using \(TransactionScope ts = new TransactionScope\(\)\)中就可以了。从这种写法可以看出，TransactionScope实现了IDispose接口。除非显示调用ts.Complete\(\)方法。否则，系统不会自动提交这个事务。如果在代码运行退出这个block后，还未调用Complete\(\)，那么事务自动回滚了。在这个事务块中，u.ADD\(\)方法和t.ADD\(\)方法内部都没有用到任何事务类。

TransactionScope是基于当前线程的，在当前线程中，调用Transaction.Current方法可以看到当前事务的信息。具体关于TransactionScope的使用方法，已经它的成员方法和属性，可以查看 [MSDN](http://msdn.microsoft.com/zh-cn/library/system.transactions.transactionscope%28v=vs.80%29.aspx) 。

  
TransactionScope类是可以嵌套使用，如果要嵌套使用，需要在嵌套事务块中指定TransactionScopeOption参数。默认的这个参数为Required。

该参数的具体含义可以参考http://msdn.microsoft.com/zh-cn/library/system.transactions.transactionscopeoption\(v=vs.80\).aspx

```
static void Main(string[] args)
        {
            using (TransactionScope ts = new TransactionScope())
            {
                Console.WriteLine(Transaction.Current.TransactionInformation.LocalIdentifier);
                userBLL u = new userBLL();
                TeacherBLL t = new TeacherBLL();
                u.ADD();
                using (TransactionScope ts2 = new TransactionScope(TransactionScopeOption.Required))
                {
                    Console.WriteLine(Transaction.Current.TransactionInformation.LocalIdentifier);
                    t.ADD();
                    ts2.Complete();
                }
               ts.Complete();
            }
        }


```

当嵌套类的TransactionScope的TransactionScopeOption为Required的时候，则可以看到如下结果，他们的事务的ID都是同一个。并且，只有当2个TransactionScope都complete的时候才能算真正成功。

  


