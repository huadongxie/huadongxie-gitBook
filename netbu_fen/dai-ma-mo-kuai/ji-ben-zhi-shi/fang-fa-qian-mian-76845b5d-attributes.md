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

AnyClass.Old\(\)' is obsolete: 'Don't use Old method,  use New method'

**开发自定义Attributes**

lx项目中的代码

```
{
    public class AstModuleActionAttribute : Attribute
    {
        public AstModuleActionAttribute(int moduleId);
        public AstModuleActionAttribute(int moduleId = 0, ActionType actionType = ActionType.NoAction);

        public ActionType Action { get; set; }
        public int ModuleId { get; set; }
    }
}
```

\[AstModuleAction\(ModuleInfo.Corporation, ActionType.Create\)\]

在C\#中，我们的attribute类都派生于System.Attribute类\(A class that derives from the abstract class System.Attribute, whether directly or indirectly, is an attribute class. The declaration of an attribute class defines a new kind of attribute that can be placed on a declaration\) ，我们就这么行动吧。

```
public class HelpAttribute : Attribute

{

}
```

不管你是否相信我，就这样我们就已经创建了一个自定义attribute。现在就可以用它来装饰我们的类了，就像我们使用obsolete attribute一样。

注意：按惯例我们是用”Attribute“作为attribute类名的后缀，然而，当我们当我们把attribute绑定到某语言元素时，是不包含“Attribute“后缀的。编译器首先在System.Attribute的继承类中查找该attribute，如果没有找到，编译器会把“Attribute“追加到该attribute的名字后面，然后查找它。

但是迄今为止，该attribute没有任何用处。为了使它有点用处，让我们在它里面加点东西吧。

```
public class HelpAttribute : Attribute
{
    public HelpAttribute(String Descrition_in)
    {
        this.description = Description_in;
    }
    protected String description;
    public String Description 
    {
        get 
        {
            return this.description;

        }            
    }    
}
[Help("this is a do-nothing class")]
public class AnyClass
{
}
```

在上面的例子中，我们在attribute类中添加了一个属性，在最后一节中，我们将在运行时查询该属性。

**定义或控制自定义Attribute的用法**

AttributeUsage类是另一预定义类（译者注：attribute类本身用这个atrributeSystem.AttributeUsage来标记），它将帮助我们控制我们自定义attribute的用法，这就是，我们能为自定义的attribute类定义attributes。

它描述了一个自定义attribute类能被怎样使用。

AttributeUsage提供三个属性，我们能将它们放置到我们的自定义attribute类上， 第一个特性是：  
**ValidOn**

通过这个属性，我们能指定我们的自定义attribute可以放置在哪些语言元素之上。这组我们能把自定义attribute类放置其上的语言元素被放在枚举器AttributeTargets中。我们可以使用bitwise（译者注：这个词不知道怎么翻译好，但他的意思是可以这么用：\[AttributeUsage\(\(AttributeTargets\)4, AllowMultiple =false, Inherited =false \)\],4代表就是“class”元素，其它诸如1代表“assembly”，16383代表“all”等等）或者”.”操做符绑定几个AttributeTargets值。（译者注：默认值为AttributeTargets.All\)

**AllowMultiple**

该属性标识我们的自定义attribte能在同一语言元素上使用多次。（译者注：该属性为bool类型，默认值为false，意思就是该自定义attribute在同一语言元素上只能使用一次）

**Inherited**

我们可以使用该属性来控制我们的自定义attribute类的继承规则。该属性标识我们的自定义attribute是否可以由派生类继承。（（译者注：该属性为bool类型，默认值为false，意思是不能继承）

让我们来做点实际的东西吧，我们将把AttributeUsageattribute 放置在我们的help attribute 上并在它的帮助下，我们来控制help attribute的用法。

```
public class HelpAttribute : Attribute

{

    public HelpAttribute(String Description_in)

    {

        this.description = Description_in;

    }

    protected String description;

    public String Description

    {

        get 

        {

            return this.description;

        }            

    }    

}
```

首先我们注意AttributeTargets.Class. 它规定这个help attribute 只能放置在语言元素”class”之上。这就意味着，下面的代码将会产生一个错误。

```
[Help("this is a do-nothing class")]

public class AnyClass

{

    [Help("this is a do-nothing method")]    //error

    public void AnyMethod()

    {

    }

}
```

我们可以使用AttributeTargets.All来允许Help attribute 可以放置在任何预定义的语言元素上，那些可能的语言元素如下:

* Module, 
* Class, 
* Struct, 
* Enum, 
* Constructor, 
* Method, 
* Property, 
* Field,
* Event, 
* Interface, 
* Parameter, 
* Delegate, 
* All = Assembly \| Module \| Class \| Struct \| Enum \| Constructor \| Method \| Property \| Field \| Event \| Interface \| Parameter \| Delegate,
* ClassMembers = Class \| Struct \| Enum \| Constructor \| Method \| Property \| Field \| Event \| Delegate \| Interface \)

* ~现在考虑下  
  AllowMultiple =  
  false  
  . 这就规定该  
  attribute 不能在同一语言元素上放置多次  
  .我们有四种可能的绑定:

  ```
  [AttributeUsage(AttributeTargets.Class, AllowMultiple =true, Inherited =false)] 
  [AttributeUsage(AttributeTargets.Class, AllowMultiple =false, Inherited =true)] 
  [AttributeUsage(AttributeTargets.Class, AllowMultiple =true, Inherited =true)]
  ```

  **第一种情况**

  如果我们查询（我们将在后面来了解如何在运行时来查询attributes）派生类中的help attribute，我们将不可能查询到因为”Inherited”被设为了false。

  **第二种情况**

  第二种情况没有什么不同，因为其”Inherited”也被设为了false。

  **第三种情况**

  为了解释第三种和第四种情况，让我们为派生类也绑定同一attribute。

现在我们查询相关的help attribute ，我们将仅仅可以得到派生类的attribute，为什么这样是因为help attribute虽然允许被继承，但不能多次在同一语言元素上使用，所以基类中的help attribute被派生类的help attribute 重写了。

**第四种情况**

在第四种情况中，当我们查询派生类的help attribute 时，我们可以得到两个attributes，当然是因为help attribute既允许被继承，又允许在同一语言元素上多次使用的结果。

注意：AttributeUsageattribute 仅应用在那种是System.Attribute派生的attriubte类而且绑定值该attriubte类的AllowMultiple和Inherited均为false上才是有效的。

**可选参数vs.命名参数**

可选参数是attribute类构造函数的参数。它们是强制的，必须在每次在attribute绑定至某语言元素时提供一个值。而另一方面，命名参数倒是真正的可选参数，不是在attribute构造函数的参数。

为了更加详细的解释，让我们在Help类中添加另外的属性。

```
public class HelpAttribute : Attribute

{

    public HelpAttribute(String Description_in)

    {

        this.description = Description_in;

        this.verion = "No Version is defined for this class";

    }

    protected String description;

    public String Description

    {

        get 

        {

            return this.description;

        }

    }

    protected String version;

    public String Version

    {

        get 

        {

            return this.version;

        }

        //if we ever want our attribute user to set this property, 

        //we must specify set method for it 

        set 

        {

            this.verion = value;

        }

    }

}

[Help("This is Class1")]

public class Class1

{

}



[Help("This is Class2", Version = "1.0")]

public class Class2

{

}



[Help("This is Class3", Version = "2.0", 

 Description = "This is do-nothing class")]

public class Class3

{

}
```

当我们在Class1中查询Help attribute已经它的属性，我们将得到：

Help.Description : This is Class1

Help.Version :No Version is defined for this class

因为我们没有为Version这个属性定义任何任何值，所以在构造函数中设定的值被我们查询出来了。如果没有定义任何值，那么就会赋一个该类型的默认值（例如：如果是int型，默认值就是0）。

现在，查询Class2的结果是：

Help.Description : This is Class2

Help.Version :  1.0

我们不能为了可选参数而使用多个构造函数，应该用已命名参数来代替。我们之所以称它们为已命名的，是因为当我们在构造函数为它们提供值时，我们必须命名它们。例如，在第二个类中，我们如是定义Help。

\[Help\("This is Class2", Version ="1.0"\)\]

在AttributeUsage 例子中, 参数”ValidOn”是可选参数，而“Inherited“和“AllowMultiple“ 是命名参数。

**Attributes 标记**

假设，我们想把Help attribute 绑定至元素assembly。第一个问题是我们要把Help attribute 放在哪儿才能让编译器确定该attribute是绑定至整个assembly呢？考虑另一种情况，我们想把attribute绑定至一个方法的返回类型上，怎样才能让编译器确定我们是把attribute绑定至方法的返回类型上，而不是整个方法呢？

为了解决诸如此类的含糊问题，我们使用attribute标识符，有了它的帮助，我们就可以确切地申明我们把attribute 绑定至哪一个语言元素。

例如:

\[assembly: Help\("this a do-nothing assembly"\)\]

这个在Help attribute 前的assembly标识符确切地告诉编译器，该attribute被绑定至整个assembly。可能的标识符有：

* assembly
* module
* type
* method
* property
* event
* field
* param
* return

**在运行时查询Attributes**

现在我们明白怎么创建attribtes和把它们绑定至语言元素。是时候来学习类的使用者该如何在运行时查询这信息。

为了查询一语言元素上绑定的attributes，我们必须使用反射。反射有能力在运行时发现类型信息。

我们可以使用.NET Framework Reflection APIs 通过对整个assembly元数据的迭代，列举出assembly中所有已定义的类，类型，还有方法。

记住那旧的Helpattribute 和AnyClass类。

```
using System.Reflection;

using System.Diagnostics;



//attaching Help attribute to entire assembly

[assembly : Help("This Assembly demonstrates custom attributes 

 creation and their run-time query.")]



//our custom attribute class

public class HelpAttribute : Attribute

{

    public HelpAttribute(String Description_in)

    {

        //

        // TODO: Add constructor logic here

        this.description = Description_in;

        //

    }

    protected String description;

    public String Description

    {

        get 

        {

            return this.deescription;



        }            

    }    

}

//attaching Help attribute to our AnyClass

[HelpString("This is a do-nothing Class.")]

public class AnyClass

{

//attaching Help attribute to our AnyMethod

    [Help("This is a do-nothing Method.")]

    public void AnyMethod()

    {

    }

//attaching Help attribute to our AnyInt Field

    [Help("This is any Integer.")]

    public int AnyInt;

}

class QueryApp

{

    public static void Main()

    {

    }
```

我们将在接下来的两节中在我们的Main方法中加入attribute查询代码。

**查询程序集的Attributes**

在接下来的代码中，我们先得到当前的进程名称，然后用Assembly类中的LoadForm（）方法加载程序集，再有用GetCustomAttributes（）方法得到被绑定至当前程序集的自定义attributes，接下来用foreach语句遍历所有attributes并试图把每个attribute转型为Help attribute（即将转型的对象使用as关键字有一个优点，就是当转型不合法时，我们将不需担心会抛出异常，代之以空值（null）作为结果），接下来的一行就是检查转型是否有效，及是不是为空，跟着就显示Help attribute的“Description”属性。

```
public static void Main()

    {

        HelpAttribute HelpAttr;


        //Querying Assembly Attributes

        String assemblyName;

        Process p = Process.GetCurrentProcess();

        assemblyName = p.ProcessName + ".exe";


        Assembly a = Assembly.LoadFrom(assemblyName);


        foreach (Attribute attr in a.GetCustomAttributes(true))
        {

            HelpAttr = attr as HelpAttribute;

            if (null != HelpAttr)

            {

                Console.WriteLine("Description of {0}:\n{1}", 

                                  assemblyName,HelpAttr.Description);

            }

        }

}

}
```

程序输出如下：

Description of QueryAttribute.exe:

This Assembly demonstrates custom attributes creation and

their run-time query.

Press any key to continue

**查询类、方法、类成员的Attributes**

下面的代码中，我们惟一不熟悉的就是Main（）方法中的第一行。

Type type =typeof\(AnyClass\);

它用typeof操作符得到了一个与我们AnyClass类相关联的Type型对象。剩下的查询类attributes代码就与上面的例子是相似的，应该不要解释了吧（我是这么想的）。

为查询方法和类成员的attributes,首先我们得到所有在类中存在的方法和成员，然后我们查询与它们相关的所有attributes，这就跟我们查询类attributes一样的方式。

```
class QueryApp

{

    public static void Main()

    {

 

        Type type = typeof(AnyClass);

        HelpAttribute HelpAttr;

 

 

        //Querying Class Attributes

        foreach (Attribute attr in type.GetCustomAttributes(true))

        {

            HelpAttr = attr as HelpAttribute;

            if (null != HelpAttr)

            {

                Console.WriteLine("Description of AnyClass:\n{0}", 

                                  HelpAttr.Description);

            }

        }

        //Querying Class-Method Attributes  

        foreach(MethodInfo method in type.GetMethods())

        {

            foreach (Attribute attr in method.GetCustomAttributes(true))

            {

                HelpAttr = attr as HelpAttribute;

                if (null != HelpAttr)

                {

                    Console.WriteLine("Description of {0}:\n{1}", 

                                      method.Name, 

                                      HelpAttr.Description);

                }

            }

        }

        //Querying Class-Field (only public) Attributes

        foreach(FieldInfo field in type.GetFields())

        {

            foreach (Attribute attr in field.GetCustomAttributes(true))

            {

                HelpAttr= attr as HelpAttribute;

                if (null != HelpAttr)

                {

                    Console.WriteLine("Description of {0}:\n{1}",

                                      field.Name,HelpAttr.Description);

                }

            }

        }

    }

}

```

The output of the following program is.

Description of AnyClass:

This is a do-nothing Class.

Description of AnyMethod:

This is a do-nothing Method.

Description of AnyInt:

This is any Integer.

Press any key to continue

