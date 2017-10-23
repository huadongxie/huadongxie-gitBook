C\# 中的冒号后面的this这种调用在古老的vs2003就根本没见过，后来用2005也不这样用

  
其实他的用法就是C\#简化调用产生的

1.就目前我发现只用于有参构造函数调用另一有参构造函数，无需在构造函数累不调用构造函数用：this就可以了

2.单独的this一般都是标识当前资源对象的

3.有时用于所引器

4.用于扩展类

1.this是标识当前资源对象的，而base是基于父级的。

2.base发挥了期灵魂级的作用——多态

3.base子类可以访问父类成员

4.base调用父类方法必须重写父类方法

5.base子类构造函数直接访问：base父类构造方法

6.base同样不能用于静态方法

```
internal class DbOperation  
 {  
     public DbOperation(string connectionString, string commandText, TraceSource traceSource)  
         : this(connectionString, commandText, traceSource, SqlClientFactory.Instance.AsIDbProviderFactory())  
     {  
           
     }  
  
     public DbOperation(string connectionString, string commandText, TraceSource traceSource, IDbProviderFactory dbProviderFactory)  
     {  
         ConnectionString = connectionString;  
         CommandText = commandText;  
         Trace = traceSource;  
         _dbProviderFactory = dbProviderFactory;  
     }  
 }  
```



```
public abstract class HttpBasedTransport : ClientTransportBase  
    {  
        protected HttpBasedTransport(IHttpClient httpClient, string transportName)  
            : base(httpClient, transportName)  
        { }  
    } 
```



