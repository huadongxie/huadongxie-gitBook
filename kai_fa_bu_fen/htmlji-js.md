文档对象模型（Document Object Model，简称DOM），是[W3C](https://baike.baidu.com/item/W3C)组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM。Document Object Model的历史可以追溯至1990年代后期微软与[Netscape](https://baike.baidu.com/item/Netscape)的“浏览器大战”，双方为了在[JavaScript](https://baike.baidu.com/item/JavaScript)与[JScript](https://baike.baidu.com/item/JScript)一决生死，于是大规模的赋予浏览器强大的功能。微软在网页技术上加入了不少专属事物，既有[VBScript](https://baike.baidu.com/item/VBScript)、[ActiveX](https://baike.baidu.com/item/ActiveX)、以及微软自家的[DHTML](https://baike.baidu.com/item/DHTML)格式等，使不少网页使用非微软平台及浏览器无法正常显示。DOM即是当时蕴酿出来的杰作。

## 背景介绍

DOM= Document Object Model，[文档对象模型](https://baike.baidu.com/item/文档对象模型)，DOM可以以一种独立于平台和语言的方式访问和修改一个文档的内容和结构。换句话说，这是表示和处理一个HTML或XML文档的常用方法。有一点很重要，DOM的设计是以对象管理组织（[OMG](https://baike.baidu.com/item/OMG/3041465)）的规约为基础的，因此可以用于任何编程语言。最初人们把它认为是一种让JavaScript在浏览器间可移植的方法，不过DOM的应用已经远远超出这个范围。Dom技术使得用户页面可以动态地变化，如可以动态地显示或隐藏一个元素，改变它们的属性，增加一个元素等，Dom技术使得页面的交互性大大地增强。

DOM实际上是以面向对象方式描述的文档模型。DOM定义了表示和修改文档所需的对象、这些对象的行为和属性以及这些对象之间的关系。可以把DOM认为是页面上数据和结构的一个树形表示，不过页面当然可能并不是以这种树的方式具体实现。

通过 JavaScript，您可以重构整个 HTML 文档。您可以添加、移除、改变或重排页面上的项目。

要改变页面的某个东西，JavaScript 就需要获得对 HTML 文档中所有元素进行访问的入口。这个入口，连同对 HTML 元素进行添加、移动、改变或移除的方法和属性，都是通过文档对象模型来获得的（DOM）。

在 1998 年，W3C 发布了第一级的 DOM 规范。这个规范允许访问和操作 HTML 页面中的每一个单独的元素。

所有的浏览器都执行了这个标准，因此，DOM 的兼容性问题也难觅踪影了。

**DOM 可被 JavaScript 用来读取、改变 HTML、XHTML 以及 XML 文档。**

DOM 被分为不同的部分（核心、XML及HTML）和级别（DOM Level 1/2/3）：

### DOM

DOM 是遵循 W3C（万维网联盟）的标准。

DOM 定义了访问 HTML 和 XML 文档的标准：

"W3C 文档对象模型 （DOM） 是中立于平台和语言的接口，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。"

W3C DOM 标准被分为 3 个不同的部分：

* 核心 DOM - 针对任何结构化文档的标准模型
* XML DOM - 针对 XML 文档的标准模型
* HTML DOM - 针对 HTML 文档的标准模型

### XML DOM

XML DOM 是：

* 用于 XML 的标准对象模型
* 用于 XML 的标准编程接口
* 中立于平台和语言
* W3C 标准

XML DOM 定义了所有 XML 元素的**对象和属性**，以及访问它们的**方法**（接口）。

换句话说：**XML DOM 是用于获取、更改、添加或删除 XML 元素的标准。**

### HTML DOM

HTML DOM 是：

* HTML 的标准对象模型
* HTML 的标准编程接口
* W3C 标准

HTML DOM 定义了所有 HTML 元素的**对象和属性**，以及访问它们的**方法**（接口）。

换言之，**HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。**

## DOM的分级

根据[W3C](https://baike.baidu.com/item/W3C)DOM规范，DOM是[HTML](https://baike.baidu.com/item/HTML)与[XML](https://baike.baidu.com/item/XML)的应用编程接口（API），DOM将整个页面映射为一个由层次节点组成的文件。有1级、2级、3级共3个级别。

### 1级DOM

1级DOM在1998年10月份成为W3C的提议，由DOM核心与DOM HTML两个模块组成。DOM核心能映射以XML为基础的文档结构，允许获取和操作文档的任意部分。DOM HTML通过添加HTML专用的对象与函数对DOM核心进行了扩展。

### 2级DOM

鉴于1级DOM仅以映射文档结构为目标，DOM 2级面向更为宽广。通过对原有DOM的扩展，2级DOM通过对象接口增加了对鼠标和用户界面事件（DHTML长期支持鼠标与用户界面事件）、范围、遍历（重复执行DOM文档）和层叠样式表（CSS）的支持。同时也对DOM 1的核心进行了扩展，从而可支持XML命名空间。

2级DOM引进了几个新DOM模块来处理新的接口类型：

DOM视图：描述跟踪一个文档的各种视图（使用CSS样式设计文档前后）的接口；

DOM事件：描述事件接口；

DOM样式：描述处理基于CSS样式的接口；

DOM遍历与范围：描述遍历和操作文档树的接口；

### 3级DOM

3级DOM通过引入统一方式载入和保存文档和文档验证方法对DOM进行进一步扩展，DOM3包含一个名为“DOM载入与保存”的新模块，DOM核心扩展后可支持XML1.0的所有内容，包括XML Infoset、 XPath、和XML Base。

### "0级"DOM

当阅读与DOM有关的材料时，可能会遇到参考0级DOM的情况。需要注意的是并没有标准被称为0级DOM，它仅是DOM历史上一个参考点（0级DOM被认为是在Internet Explorer 4.0 与Netscape Navigator4.0支持的最早的DHTML）。

### 节点

根据 DOM，HTML 文档中的每个成分都是一个节点。

DOM 是这样规定的：

整个文档是一个文档节点

每个 HTML 标签是一个元素节点

包含在 HTML 元素中的文本是文本节点

每一个 HTML 属性是一个属性节点

注释属于注释节点

### Node 层次

节点彼此都有等级关系。

HTML 文档中的所有节点组成了一个文档树（或节点树）。HTML 文档中的每个元素、属性、文本等都代表着树中的一个节点。树起始于文档节点，并由此继续伸出枝条，直到处于这棵树最低级别的所有文本节点为止。

下面这个图片表示一个文档树（节点树）：

![](/assets/https:/baike.baidu.com/pic/DOM/50288/0/810a19d8bc3eb13599df8648a61ea8d3fd1f442c?fr=lemma&ct=single#aid=0&pic=810a19d8bc3eb13599df8648a61ea8d3fd1f442c.png)

### 文档树

```
请看下面这个HTML文档：
<html>
<head>
<title>DOM Tutorial</title>
</head>
<body>
<h1>DOM Lesson one</h1>
<p>Hello world!</p>
</body>
</html>
```

上面所有的节点彼此间都存在关系。

除文档节点之外的每个节点都有父节点。举例，&lt;head&gt; 和 &lt;body&gt; 的父节点是 &lt;html&gt; 节点，文本节点 "Hello world!" 的父节点是 &lt;p&gt; 节点。

大部分元素节点都有子节点。比方说，&lt;head&gt; 节点有一个子节点：&lt;title&gt; 节点。&lt;title&gt; 节点也有一个子节点：文本节点 "DOM Tutorial"。

当节点分享同一个父节点时，它们就是辈（同级节点）。比方说，&lt;h1&gt; 和 &lt;p&gt;是同辈，因为它们的父节点均是 &lt;body&gt; 节点。

节点也可以拥有后代，后代指某个节点的所有子节点，或者这些子节点的子节点，以此类推。比方说，所有的文本节点都是 &lt;html&gt;节点的后代，而第一个文本节点是 &lt;head&gt; 节点的后代。

节点也可以拥有先辈。先辈是某个节点的父节点，或者父节点的父节点，以此类推。比方说，所有的文本节点都可把 &lt;html&gt; 节点作为先辈节点。

## 访问节点

你可通过若干种方法来查找您希望操作的元素：

通过使用 getElementById\(\) 和 getElementsByTagName\(\) 方法

通过使用一个元素节点的 parentNode、firstChild 以及 lastChild 属性  
getElementById\(\) 和 getElementsByTagName\(\) 这两种方法，可查找整个 HTML 文档中的任何 HTML 元素。

这两种方法会忽略文档的结构。假如您希望查找文档中所有的 &lt;p&gt; 元素，getElementsByTagName\(\) 会把它们全部找到，不管 &lt;p&gt;

 元素处于文档中的哪个层次。同时，getElementById\(\) 方法也会返回正确的元素，不论它被隐藏在文档结构中的什么位置。

这两种方法会向您提供任何你所需要的 HTML 元素，不论它们在文档中所处的位置！

getElementById\(\) 可通过指定的 ID 来返回元素：

