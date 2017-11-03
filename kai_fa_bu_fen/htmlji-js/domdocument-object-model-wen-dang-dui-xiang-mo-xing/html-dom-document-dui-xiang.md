## Document 对象

每个载入浏览器的 HTML 文档都会成为 Document 对象。

Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。

提示：Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问。

## Document 对象集合

| 集合 | 描述 |
| :--- | :--- |
| [all\[\]](http://www.w3school.com.cn/jsref/coll_doc_all.asp) | 提供对文档中所有 HTML 元素的访问。 |
| [anchors\[\]](http://www.w3school.com.cn/jsref/coll_doc_anchors.asp) | 返回对文档中所有 Anchor 对象的引用。 |
| applets | 返回对文档中所有 Applet 对象的引用。 |
| [forms\[\]](http://www.w3school.com.cn/jsref/coll_doc_forms.asp) | 返回对文档中所有 Form 对象引用。 |
| [images\[\]](http://www.w3school.com.cn/jsref/coll_doc_images.asp) | 返回对文档中所有 Image 对象引用。 |
| [links\[\]](http://www.w3school.com.cn/jsref/coll_doc_links.asp) | 返回对文档中所有 Area 和 Link 对象引用。 |

## Document 对象属性

| 属性 | 描述 |
| :--- | :--- |
| body | 提供对 &lt;body&gt; 元素的直接访问。对于定义了框架集的文档，该属性引用最外层的 &lt;frameset&gt;。 |
| [cookie](http://www.w3school.com.cn/jsref/prop_doc_cookie.asp) | 设置或返回与当前文档有关的所有 cookie。 |
| [domain](http://www.w3school.com.cn/jsref/prop_doc_domain.asp) | 返回当前文档的域名。 |
| [lastModified](http://www.w3school.com.cn/jsref/prop_doc_lastmodified.asp) | 返回文档被最后修改的日期和时间。 |
| [referrer](http://www.w3school.com.cn/jsref/prop_doc_referrer.asp) | 返回载入当前文档的文档的 URL。 |
| [title](http://www.w3school.com.cn/jsref/prop_doc_title.asp) | 返回当前文档的标题。 |
| [URL](http://www.w3school.com.cn/jsref/prop_doc_url.asp) | 返回当前文档的 URL。 |

## Document 对象方法

| 方法 | 描述 |
| :--- | :--- |
| [close\(\)](http://www.w3school.com.cn/jsref/met_doc_close.asp) | 关闭用 document.open\(\) 方法打开的输出流，并显示选定的数据。 |
| [getElementById\(\)](http://www.w3school.com.cn/jsref/met_doc_getelementbyid.asp) | 返回对拥有指定 id 的第一个对象的引用。 |
| [getElementsByName\(\)](http://www.w3school.com.cn/jsref/met_doc_getelementsbyname.asp) | 返回带有指定名称的对象集合。 |
| [getElementsByTagName\(\)](http://www.w3school.com.cn/jsref/met_doc_getelementsbytagname.asp) | 返回带有指定标签名的对象集合。 |
| [open\(\)](http://www.w3school.com.cn/jsref/met_doc_open.asp) | 打开一个流，以收集来自任何 document.write\(\) 或 document.writeln\(\) 方法的输出。 |
| [write\(\)](http://www.w3school.com.cn/jsref/met_doc_write.asp) | 向文档写 HTML 表达式 或 JavaScript 代码。 |
| [writeln\(\)](http://www.w3school.com.cn/jsref/met_doc_writeln.asp) | 等同于 write\(\) 方法，不同的是在每个表达式之后写一个换行符。  |



