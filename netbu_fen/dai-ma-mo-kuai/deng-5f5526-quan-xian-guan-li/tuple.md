Tuple是C\# 4.0时出的新特性，.Net Framework 4.0以上版本可用。

元组是一种数据结构，具有特定数量和元素序列。比如设计一个三元组数据结构用于存储学生信息，一共包含三个元素，第一个是名字，第二个是年龄，第三个是身高。

元组的具体使用如下：

### 1.    如何创建元组

默认情况.Net Framework元组仅支持1到7个元组元素，如果有8个元素或者更多，需要使用Tuple的嵌套和Rest属性去实现。另外Tuple类提供创造元组对象的静态方法。

* 利用构造函数创建元组：

```
var testTuple6 = new Tuple<int, int, int, int, int, int>(1, 2, 3, 4, 5, 6);
Console.WriteLine($"Item 1: {testTuple6.Item1}, Item 6: {testTuple6.Item6}");

var testTuple10 = new Tuple<int, int, int, int, int, int, int, Tuple<int, int, int>>(1, 2, 3, 4, 5, 6, 7, new Tuple<int, int, int>(8, 9, 10));
Console.WriteLine($"Item 1: {testTuple10.Item1}, Item 10: {testTuple10.Rest.Item3}");
```

利用Tuple静态方法构建元组，最多支持八个元素：

```
var testTuple6 = Tuple.Create<int, int, int, int, int, int>(1, 2, 3, 4, 5, 6);
Console.WriteLine($"Item 1: {testTuple6.Item1}, Item 6: {testTuple6.Item6}");

var testTuple8 = Tuple.Create<int, int, int, int, int, int, int, int>(1, 2, 3, 4, 5, 6, 7, 8);
Console.WriteLine($"Item 1: {testTuple8.Item1}, Item 8: {testTuple8.Rest.Item1}");
```

Note：这里构建出来的Tuple类型其实是Tuple&lt;int, int, int, int, int, int, int, Tuple&lt;int&gt;&gt;，因此testTuple8.Rest取到的数据类型是Tuple&lt;int&gt;，因此要想获取准确值需要取Item1属性。

### 2.    表示一组数据

如下创建一个元组表示一个学生的三个信息：名字、年龄和身高，而不用单独额外创建一个类。

```
var studentInfo = Tuple.Create<string, int, uint>("Bob", 28, 175);
Console.WriteLine($"Student Information: Name [{studentInfo.Item1}], Age [{studentInfo.Item2}], Height [{studentInfo.Item3}]");
```

### 3.    从方法返回多个值

当一个函数需要返回多个值的时候，一般情况下可以使用out参数，这里可以用元组代替out实现返回多个值。

```
static Tuple<string, int, uint> GetStudentInfo(string name)
{
    return new Tuple<string, int, uint>("Bob", 28, 175);
}

static void RunTest()
{
    var studentInfo = GetStudentInfo("Bob");
    Console.WriteLine($"Student Information: Name [{studentInfo.Item1}], Age [{studentInfo.Item2}], Height [{studentInfo.Item3}]");
}
```

### 4.    用于单参数方法的多值传递

当函数参数仅是一个Object类型时，可以使用元组实现传递多个参数值。

```
static void WriteStudentInfo(Object student)
{
    var studentInfo = student as Tuple<string, int, uint>;
    Console.WriteLine($"Student Information: Name [{studentInfo.Item1}], Age [{studentInfo.Item2}], Height [{studentInfo.Item3}]");
}

static void RunTest()
{
    var t = new System.Threading.Thread(new System.Threading.ParameterizedThreadStart(WriteStudentInfo));
    t.Start(new Tuple<string, int, uint>("Bob", 28, 175));
    while (t.IsAlive)
    {
        System.Threading.Thread.Sleep(50);
    }
}
```

尽管元组有上述方便使用的方法，但是它也有明显的不足：

* 访问元素的时候只能通过ItemX去访问，使用前需要明确元素顺序，属性名字没有实际意义，不方便记忆；
* 最多有八个元素，要想更多只能通过最后一个元素进行嵌套扩展；
* Tuple是一个引用类型，不像其它的简单类型一样是值类型，它在堆上分配空间，在CPU密集操作时可能有太多的创建和分配工作。

因此在C\# 7.0中引入了一个新的ValueTuple类型，详见下面章节

