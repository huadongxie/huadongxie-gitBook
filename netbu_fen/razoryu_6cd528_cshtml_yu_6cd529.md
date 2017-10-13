## Razor语法(cshtml语法) {#razor-cshtml}

### Razor文件类型 {#razor}

   Razor可以在vb.NET和C#中使用。分别对应了两种文件类型，.vbhtml和.cshtml 。

### **Razor的标识符** {#razor-0}

**    **@字符被定义为Razor服务器代码块的标识符，后面的表示是服务器代码了。web form中使用&lt;%%&gt;中写服务器代码一个道理。在vs工具里面提供了代码着色和[**智能**](http://lib.csdn.net/base/aiplanning)感应的功能。如下面代码：

@{string userName= &quot;邓星林&quot;;}

&lt;span&gt;@userName&lt;/span&gt;

&lt;span&gt;@DateTime.Now.ToString(&quot;yyyy-MM-hh&quot;)&lt;/span&gt;

### Razor的作用域 {#razor-1}

     在上面一个例子中都已经使用到了大括号{}，不错，大括号里面的就是表示作用域的范围，用形如@{code}来写一段代码块。

@{

string userName= &quot;邓星林&quot;;

@userName

}

在作用域(代码块)中输出也是用@符号的。

###  用Razor和html代码混合编写 {#razor-html}

**   **在Razor中写html代码和html代码中写Razor语句都是可以的，并且还有智能提示。

   a.在作用域内如果是以html标签开始则视为文本输出

   b.如果要输出@，则使用@@

   c.如果要输出非html标签和非Razor语句的代码，则用@:，他的作用是相当于在处于html下面编写一样了，如在@：后面可以加上@就是表示Razor语句的变量

 如：

![复制代码](../assets/fu_zhi_dai_ma.gif)

@{

var str = &quot;abc&quot;;

////下面会输出：this is a mail：dxl0321@qq.com, this is var: abc,this is mail@str,this is @；

@: this is a mail：dxl0321@qq.com, this is var: @str,this is mail@str,this is @@；

//下面输出abc

@str

}

![复制代码](../assets/fu_zhi_dai_ma.gif)

### Razor作用块注释 {#razor-2}

    razor作用块里面本身就是服务器代码了，因此可使用服务器代码的注释，注释有//和/**/分别是单行注释和多行注释。

   另外razor注释还可以使用自身特有的@* 注释的内容 *@，支持单行和多行的。

### Razor类型转换 {#razor-3}

         As系列扩展方法和Is系列扩展方法

          AsInt(), IsInt()

　    　AsBool(),IsBool()

    　　AsFloat(),IsFloat()

　   　AsDecimal(),IsDecimal()

### razor其它 {#razor-4}

  @Href(&quot;~/&quot;)//表示网站的根目录

  @Html.Raw(Module.Content)  输出HTML，如：@Html.Raw(&#039;&lt;font color=&#039;red&#039;&gt;红字&lt;/font&gt;&#039;)，就会显示出红色的”红字“，不用的话会直接显示这段html字符串（&lt;font color=&#039;red&#039;&gt;红色文字&lt;/font&gt;）

在实际中，比如一个网站，整过框架是一样的，而有的地方是很多相同的版块。因此我们需要复用。

### 布局（Layout） {#layout}

**   **layout方式布局就是相当于一个模板一样的，我们在它地址地方去添加代码。相当于定义好了框架，作为一个母版页的，在它下面的页面需要修改不同代码的地方使用@RenderBody()方法

![复制代码](../assets/fu_zhi_dai_ma.gif)

&lt;!DOCTYPE html&gt;

&lt;html lang=&quot;en&quot;&gt;

&lt;head&gt;

&lt;meta charset=&quot;utf-8&quot;/&gt;

&lt;title&gt;我的网站 - @Page.Title&lt;/title&gt;

&lt;/head&gt;

&lt;body&gt;

@RenderBody()

&lt;/body&gt;

&lt;/html&gt;

![复制代码](../assets/fu_zhi_dai_ma.gif)

![复制代码](../assets/fu_zhi_dai_ma.gif)

@{

Layout = &quot;/LayoutPage.cshtml&quot;;

Page.Title = &quot;测试页面哦&quot;;

}

&lt;p&gt;This is a layout test&lt;/p&gt;

###  页面（Page） {#page}

** **page是当需要在一个页面中，输出另外一个razor文件的内容时候用到，比如头部或者尾部这些公共的内容时候需要用到。输出就使用 @RenderPage()方法

如：A页面中也要把B页面的内容输出

A页面：

&lt;p&gt;

@RenderPage(&quot;/b.cshtml&quot;)

&lt;/p&gt;

b页面的代码如下：

&lt;font color=&quot;red&quot;&gt;这是一个子页面&lt;/font&gt;

###  Section区域 {#section}

**    **Section是定义在Layou的中使用的。在Layout的页面中用。在要Layout的父页面中使用@RenderSection(&quot;Section名称 &quot;)

定义：

![复制代码](../assets/fu_zhi_dai_ma.gif)

&lt;!DOCTYPE html&gt;

&lt;html lang=&quot;en&quot;&gt;

&lt;head&gt;

&lt;meta charset=&quot;utf-8&quot;/&gt;

&lt;title&gt;我的网站 - @Page.Title&lt;/title&gt;

&lt;/head&gt;

&lt;body&gt;

 @RenderSection(&quot;SubMenu&quot;)

@RenderBody()

&lt;/body&gt;

&lt;/html&gt;

![复制代码](../assets/fu_zhi_dai_ma.gif)

在它的子页面中使用

@section SubMenu{

Hello This is a section implement in About View.

}

 如果在子页面中没有去实现了SubMenu了，则会抛出异常。我们可以它的**重载@RenderSection(&quot;SubMenu&quot;, false)**

![复制代码](../assets/fu_zhi_dai_ma.gif)

@if (IsSectionDefined(&quot;SubMenu&quot;))

{

@RenderSection(&quot;SubMenu&quot;, false)

}

else

{

&lt;p&gt;SubMenu Section is not defined!&lt;/p&gt;

}

![复制代码](../assets/fu_zhi_dai_ma.gif)

　    　AsDateTime(),IsDateTime()

　  　ToString()

@{

var i = “10”;

}

&lt;p&gt; i = @i.AsInt() &lt;/p&gt; &lt;!-- 输出 i = 10 --&gt;

### **Helper** {#helper}

**   **helper就是可以定义可重复使用的帮助器方法，不仅可以在同一个页面不同地方使用，还可以在不同的页面使用。

如在cshtml中那么写：

![复制代码](../assets/fu_zhi_dai_ma.gif)

@helper sum(int a,int b)

{

var result=a+b;　　@result

}

&lt;div &gt;

&lt;p&gt;@@helper的语法&lt;/p&gt; &lt;p&gt;2+3=@sum(2,3)&lt;/p&gt; &lt;p&gt;5+9=@sum(5,9)&lt;/p&gt;&lt;/div&gt;

![复制代码](../assets/fu_zhi_dai_ma.gif)

我们通常会把一类Helper放在一个单独的cshtml文件中，而文件名就相当于一个类名。

我把sum放在HelpMath.cshtml文件中，则我们在那上面cshtml中的使用方法是:

&lt;p&gt;2+3=@HelpMath.sum(2,3)&lt;/p&gt;

&lt;p&gt;5+9=@HelpMath.sum(5,9)&lt;/p&gt;

另外，系统还为我们提供了一些列的Helper，用来简化Html的书写。这些Helper放在@Html中，我们可以方便的使用：

&lt;p&gt;

@Html.TextBox(&quot;txtName&quot;)

&lt;/p&gt;

 本文页面来源地址：[http://www.cnblogs.com/dengxinglin/p/3352078.html](http://www.cnblogs.com/dengxinglin/p/3352078.html)