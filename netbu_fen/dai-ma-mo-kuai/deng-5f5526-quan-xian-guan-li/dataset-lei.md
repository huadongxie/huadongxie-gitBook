代表一个内存中的缓存的数据。

# DataSetClass

## Definition {#Definition}

Namespace:

[System.Data](https://docs.microsoft.com/zh-cn/dotnet/api/system.data?view=netframework-4.7.1)

Assemblies:

System.Data.dll, netstandard.dll, System.Data.Common.dll

Represents an in-memory cache of data.

DataSet类是ADO.NET中最核心的成员之一，也是各种开发基于.Net平台程序语言开发数据库应用程序最常接触的类。每一个DataSet都有很多个DataTables和Relationships。RelationShip应该也是一种表，特殊的是，这个表只是用来联系两个数据表的。每一个DataTable都有很多datarows和datacols, 也包括ParentRelations，ChildRelations 和一些限制条件像主键不可以重复的限制。

  DataSet每一行有一个RowState属性。主要是反映当前行是否已经被删掉了，被更新了，还是本没变。有如下的几个选项:   Deleted, Modified, New, and Unchanged。



  对DataSet的任何操作，都是在计算机缓存中完成的。



  在从数据库完成数据抽取后，DataSet就是数据的存放地，它是各种数据源中的数据在计算机内存中映射成的缓存，所以有时说DataSet可以看成是一个数据容器。

DataSet对象是一个可以用XML形式表示的数据视图，是一种数据关系视图。

DataSet使用方法一般有三种：

###### 1.把数据库中的数据通过DataAdapter对象填充DataSet

DataAdapter填充DataSet的过程分为二步：首先通过DataAdapter的SqlCommand属性从数据库中检索出需要的数据。SqlCommand其实是一个Command对象。然后再通过DataAdapter的Fill方法把检索来的数据填充DataSet。

###### 2.通过DataAdapter对象操作DataSet实现更新数据库

DataAdapter是通过其Update方法实现以DataSet中数据来更新数据库的。当DataSet实例中包含数据发生更改后，此时调用Update方法，DataAdapter 将分析已作出的更改并执行相应的命令（INSERT、UPDATE 或 DELETE），并以此命令来更新数据库中的数据。

###### 3. 把XML数据流或文本加载到DataSet

DataSet中的数据可以从XML数据流或文档创建。加载XML数据流和文档到DataSet中是可使用DataSet对象的ReadXml方法。

 数据绑定分成二类：简单型数据绑定和复杂型数据绑定。适用于简单型数据绑定组件一般有Lable、TextBox等，适用于复杂性数据绑定的组件一般有DataGrid、ListBox、ComboBox等。

简单型数据绑定一般使用这些组件中的DataBindings属性的Add方法把DataSet中某一个DataTable中的某一行和组件的某个属性绑定起来，从而达到显示数据的效果。

比如：textBox1.DataBindings.Add \( "Text" , dsDataSet1, " Customers. CustomerID "\) ;

复杂性数据绑定一般是设定组件的DataSource属性和DisplayMember属性来完成数据绑定的。DataSource属性值一般设定为要绑定的DataSet，DisplayMember属性值一般设定为要绑定的数据表或数据表中的某一列。

比如：dataGrid1.DataSource = dsDataSet1 ;

dataGrid1.DataMember = " Customers " ;

DataSet的属性Tables可以获取该DATASET中表的数量：DataSet.Tables.Count

DataSet的Tables是一个Table数组，指定其中的一个表：DataSet.Tables\[i\];//i为

Table在数组序列中的位置 或 DataSet.Tables\["表名"\];

通过Table的Rows对象组的Count获取该表的记录数：DataSet.Tables\[i\].Rows.Count;

获取列数：DataSet.Tables\[i\].Columns.Count;

