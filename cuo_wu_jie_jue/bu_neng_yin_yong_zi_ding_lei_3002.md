## 不能引用自定类。

按照要求在App_Code文件夹创建了一个公共类CommonClass.cs，并准备在Login.aspx中调用此公共类的方法，但是在Login.aspx中死活不能引用CommonClass.cs的命名空间，错误提示如下：

错误 CS0234 命名空间“NewsRelease”中不存在类型或命名空间名“App_Code”(是否缺少程序集引用?)

错误 CS0246 未能找到类型或命名空间名“CommonClass”(是否缺少 using 指令或程序集引用?)

查看CommonClass.cs的文件属性，将生成操作改为“编译”即可。