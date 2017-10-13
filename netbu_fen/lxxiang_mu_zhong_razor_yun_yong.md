## Lx项目中Razor运用 {#lx-razor}

在每个cshtml文件中 首行都会有：

@**{**

ViewBag**.**Title **=** &quot;PartyOrganization&quot;**;**

Layout **=** &quot;~/Views/Shared/_LayoutIndex.cshtml&quot;**;**

**}**

### @section Scripts{ {#section-scripts}

@section Scripts{。。。。。。}

这个语句的意思是,要把大括号中的内容放置到母板页面中RederSection(&quot;scripts&quot;) 这一句所在的位置。

比如 母版页面是 Layout **=** &quot;~/Views/Shared/_LayoutIndex.cshtml&quot;**;**

**在_LayOutIndex.cshtml中 有代码：** @RenderSection**(**&quot;Scripts&quot;**,** required**:** **false)。**

@section Scripts{。。。。。。} 中的代码就会被抽出来放在这个位置。

MVC视图中，Javascripts代码被放于下面的Razor代码中（@section Scripts{}）。

好处：在视图进行JavaScript编程时，是一个很好的实践，在共享视图（_Layout.cshtml），存在节点（@RenderSection(&quot;scripts&quot;, required: false)），在视图执行时，Razor引擎会将Javascripts代码抽调出来，然后在执行的时候，再将这些代码放置在这个地方。

### @RenderBody() {#renderbody}

**在_LayOutIndex.cshtml中 有代码**

**&lt;**body class**=**&quot;easyui-layout&quot; style**=**&quot;margin: 1px;&quot;**&gt;**

**&lt;**div data**-**options**=**&quot;region:&#039;center&#039;&quot; style**=**&quot;border:none;&quot;**&gt;**

@RenderBody**()**

**&lt;/**div**&gt;**

**&lt;/**body**&gt;**

在模板页的占位符，用来渲染那些没有特地命名的段落。

作用和母版页中的服务器控件类似，当创建基于此布局页面的视图时，视图的内容会和布局页面合并，而新创建视图的内容会通过布局页面的@RenderBody()方法呈现在标签之间。

这个方法不需要参数，而且只能出现一次。

### @Html.Partial（） {#html-partial}

**&lt;**div data**-**options**=**&quot;region:&#039;west&#039;,split:true,title:&#039;行政区划&#039;,collapsible:false&quot; style**=**&quot;width: 350px;&quot;**&gt;**

@Html**.**Partial**(**&quot;_DivisionTreePartial&quot;**)**

**&lt;/**div**&gt;**

Partial View指可以应用于View中以作为其中一部分的View的片段(类似于之前的user control), 可以像类一样，编写一次， 然后在其他View中被反复使用。

这儿使用 了@Html.Partial(&quot;_DivisionTreePartial&quot;)引用s。hared目录下的DivisionTreePartial.cshtml文件

### 汇总

运用以上3个Razor方法 ，最终在访问的时候，组合成了一个在浏览器上呈现的页面：

使用_LayoutIndex.cshtml作为模板：嵌入了DivisionPartyOrganization.cshtml和_DivisionTreePartial.cshtml的内容。组合成。