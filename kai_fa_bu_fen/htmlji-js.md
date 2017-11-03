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


