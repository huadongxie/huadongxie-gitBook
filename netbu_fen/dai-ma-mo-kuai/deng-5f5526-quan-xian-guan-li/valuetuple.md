ValueTuple是C\# 7.0的新特性之一，.Net Framework 4.7以上版本可用。

值元组也是一种数据结构，用于表示特定数量和元素序列，但是是和元组类不一样的，主要区别如下：

* 值元组是结构，是值类型，不是类，而元组（Tuple）是类，引用类型；
* 值元组元素是可变的，不是只读的，也就是说可以改变值元组中的元素值；
* 值元组的数据成员是字段不是属性。

值元组的具体使用如下：

### 1.    如何创建值元组

和元组类一样，.Net Framework值元组也只支持1到7个元组元素，如果有8个元素或者更多，需要使用值元组的嵌套和Rest属性去实现。另外ValueTuple类可以提供创造值元组对象的静态方法。

* 利用构造函数创建元组：

```
var testTuple6 = new ValueTuple<int, int, int, int, int, int>(1, 2, 3, 4, 5, 6);
Console.WriteLine($"Item 1: {testTuple6.Item1}, Item 6: {testTuple6.Item6}"); 

var testTuple10 = new ValueTuple<int, int, int, int, int, int, int, ValueTuple<int, int, int>>(1, 2, 3, 4, 5, 6, 7, new ValueTuple <int, int, int>(8, 9, 10));
Console.WriteLine($"Item 1: {testTuple10.Item1}, Item 10: {testTuple10.Rest.Item3}");
```

利用Tuple静态方法构建元组，最多支持八个元素：

  


