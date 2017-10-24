**介绍**

Attributes是一种新的描述信息，我们既可以使用attributes来定义设计期信息（例如 帮助文件，文档的URL），还可以用attributes定义运行时信息（例如，使XML中的元素与类的成员字段关联起来）。我们也可以用attributes来创建一个“自描述”的组件。在这篇指南中我们将明白怎么创建属性并将其绑定至各种语言元素上，另外我们怎样在运行时环境下获取到attributes的一些信息。

**定义**

[MSDN 中做如下定义\(ms-help://MS.MSDNQTR.2002APR.1033/csspec/html/vclrfcsharpspec\_17\_2.htm\)](https://docs.microsoft.com/zh-cn/dotnet/api/system.attribute?f1url=https%3A%2F%2Fmsdn.microsoft.com%2Fquery%2Fdev15.query%3FappId%3DDev15IDEF1%26l%3DZH-CN%26k%3Dk%28System.Attribute%29;k%28SolutionItemsProject%29;k%28TargetFrameworkMoniker-.NETFramework,Version%3Dv4.6.2%29;k%28DevLang-csharp%29%26rd%3Dtrue&view=netframework-4.7.1)

_"An attribute is a piece of additional declarative information that is specified for a declaration." _

Namespace:

[System](https://docs.microsoft.com/zh-cn/dotnet/api/system?view=netframework-4.7.1)

Assemblies:

System.Runtime.dll, mscorlib.dll, netstandard.dll

**使用预定义Attributes**

```
public class AnyClass 

{
    [Obsolete("Don't use Old method, use New method", true)]

    static void Old( ) { }

    static void New( ) { }

    public static void Main( ) 
    {
        Old( );
    }
}
```

仔细看下该实例，在该实例中我们用到了”Obsolete”attribute，它标记了一个不该再被使用的语言元素（译者注：这里的元素为方法），该属性的第一个参数是string类型，它解释为什么该元素被荒弃，以及我们该使用什么元素来代替它。实际中，我们可以书写任何其它文本来代替这段文本。第二个参数是告诉编译器把依然使用这被标识的元素视为一种错误，这就意味着编译器会因此而产生一个警告。

当我们试图编译上面的上面的程序，我们会得到如下错误：

AnyClass.Old\(\)' is obsolete: 'Don't use Old method,  use New method'

**开发自定义Attributes**  
现在我们即将了解怎么开发自定义的attributes。这儿有个小小处方，有它我们就可以学会创建自定义的attributes。

在C\#中，我们的attribute类都派生于System.Attribute类\(A class that derives from the abstract class System.Attribute, whether directly or indirectly, is an attribute class. The declaration of an attribute class defines a new kind of attribute that can be placed on a declaration\) ，我们就这么行动吧。

```
public class HelpAttribute : Attribute

{

}


```



