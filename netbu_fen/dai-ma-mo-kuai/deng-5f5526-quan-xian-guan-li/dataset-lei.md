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

**4.1数据适配器的概念和使用**

DataAdapter提供连接DataSet对象和数据源的桥梁。DataAdapter使用Command对象在数据源中执行SQL命令，以便将数据加载到DataSet中，并使DataSet中数据的更改与数据源保持一致。

1．创建SqlDataAdapter

（1）初始化SqlDataAdapter类的新实例。

`string conString = "data source=127.0.0.1;Database=test;user`

`id=sa;password=123456";`

`SqlConnection myConnection = new SqlConnection(conString);`

`SqlCommand cmd = myConnection.CreateCommand();`

`cmd.CommandText = "SELECT * FROM P_Product";`

`DataSet ds = new DataSet();`

`6.     myConnection.Open();`

`7.     SqlDataAdapter adapter = new SqlDataAdapter();`

`8.     adapter.SelectCommand = cmd;`

`9.     adapter.Fill(ds, "ds");`

`10.  myConnection.Close();`

（2）使用指定的SqlCommand 初始化 SqlDataAdapter 类的新实例。

```
1.     string conString = "data source=127.0.0.1;Database=test;user 
id=sa;password=";  
2.     SqlConnection myConnection = new SqlConnection(conString); 
3.     DataSet ds = new DataSet();  
4.     SqlCommand cmd = myConnection.CreateCommand();  
5.     cmd.CommandText = "SELECT * FROM P_Product";  
6.     myConnection.Open();  
7.     SqlDataAdapter adapter = new SqlDataAdapter(cmd); 
8.     adapter.Fill(ds, "ds");  
9.     myConnection.Close();
```

（3）使用selectcommand字符串和 SqlConnection对象初始化SqlDataAdapter 类的新实例。

```
1.     string conString = "data source=127.0.0.1;Database=test;user 
id=sa;password=";  
2.     string strSQL = "SELECT * FROM P_Product";  
3.     SqlConnection myConnection = new SqlConnection(conString); 
4.     DataSet ds = new DataSet();  
5.     myConnection.Open();  
6.     SqlDataAdapter adapter = new SqlDataAdapter(strSQL, myConnection); 
7.     adapter.Fill(ds, "ds");  
8.     myConnection.Close();
```

（4）使用selectcommand字符串和一个连接字符串初始化SqlDataAdapter类的新实例。

`1.     string conString = "data source=127.0.0.1;Database=test;user         
id=sa;password=";`

`2.     string strSQL = "SELECT * FROM P_Product";`

`3.     DataSet ds = new DataSet();`

`4.     SqlDataAdapter adapter = new SqlDataAdapter(strSQL, conString);`

`5.     adapter.Fill(ds, "ds");`2．DataAdapter和SqlConnection、SqlCommand建立关联

方式1：DataAdapter在构造参数时建立。

方式2：通过SelectCommand属性建立。

**1.    SqlDataAdapter adapter = new SqlDataAdapter\(\); **

**2.    adapter.SelectCommand = new SqlCommand\(strSQL, myConnection\); **

#### **4.2数据集的概念**

形象的来说，数据集就是内存中一个**临时数据库**。怎么理解这个概念呢？如果数据库时水池，那么数据集就是你家中的水缸，如果数据库是超级市场，那么数据集就是你家的冰箱。如果你比较懒你可以把一星期的事物采购回家放在冰箱里，这样就避免了每次饿的时候往超市跑。如果你往超市跑，人多了就免不了要排队，即使超市人不多，你还得走一段路；走路也好说，如果路上再碰上突发事件---比如捡了一角钱之类的事情，势必耽误很长时间…..不管怎么说老往超市跑肯定会降低你“吃”的效率的。对于数据库访问也是一样，如果用户的每个请求都从服务器提取数据来满足，那情形跟上面一样，如果服务器请求过多那么你的请求需要排队，即使不排队，在请求时服务器突然发生故障等天灾人祸都会影响你程序的性能。

数据集都是作为数据库的临时数据容器，可以实现数据库的断开式访问。此时数据库是数据集的数据源，你可以一次性将需要的数据装进数据集，等操作完了再一并更新到数据库中，这就是数据集断开式访问方式。另外，数据集的数据源并不一定是数据库，数据集的数据源可以是文本、XML文件等，无论数据集包含的数据来自什么数据源，.Net都提供了一致的编程模型，这是数据集强大的地方。

```
定义数据集及其数据表、数据列、数据行的类都在系统的System.Data命名空间下，之间的关系如下图：
```

![](/assets/dateset-1.png)

![](/assets/dataset-2.png)

| **属   性** |
| :--- |


|  | **说  明** |
| :--- | :--- |
| Columns | 数据表中的列的集合，DataColumnCollection类型 |
| Rows | 数据表中行的集合，DataRowCollection类型 |
| DataSet | 获取此数据表所属的数据集 |
| TableName | 获取或设置数据表的主键名称 |
| PrimaryKey | 获取或设置数据表的主键 |
| Constrains | 获取该数据表约束的集合，ContraintCollection类型 |
| **方  法** | **说  明** |
| AcceptChanges | 提交对该数据表进行的所有更改 |
| Clear | 清除数据表所有数据 |
| NewRow | 创建于该数据表具有相同架构的新行 |

```

```

列的定义使用DataColumn类来完成，下面是这个类的重要属性和方法：

属  性

|  | 说  明 |
| :--- | :--- |
| AllowDBNull | 获取或设置一个值，该值指示数据表此列是否允许空值，默认为true |
| AutoIncrement | 设置是否是标识列 |
| AutoIncrementSeed | 标识列初值（也叫种子） |
| AutoIncrementStep | 自动生成列值的递增量 |
| ColumnName | 列名 |
| DataType | 指定列的数据类型，数据类型可以为.Net Framework中的基数据类型，默认为string类型 |
| DefaultValue | 设置或得到该列的默认值 |
| ReadOnly | 设置该列是否为只读，true表示设置该列只读，默认为非只读 |
| Table | 该列所属的DataTable |
| Unique | 设置列的每一行中的值是否必须是唯一的，如果为true表示该列值不能重复，也就是唯一，默认是非唯一 |

**4.3 数据集综合操作**

每一个DataSet都是一个或多个DataTable 对象的集合（DataTable相当于数据库中的表），这些对象由数据行（DataRow）、数据列（DataColumn）、字段名（Column Name）、数据格（Item），以及约束（Constraint）和有关DataTable对象中数据的关系（Relations）与数据显示排序（DataView）信息组成。

DataView用来在观察数据时提供排序和过滤的功能。DataColumn用来对表中的数据值进行一定的规限。比如哪一列数据的默认值是什么、哪一列数据值的范围是什么、哪个是主键、数据值是否是只读等。

由于一个DataSet可能存在多张表，这些表可能存在关联关系，因此用parentRelations和childRelations来表述。ParentRelations表是父表，childRelations是子表，子表是对父表的引用，这样就使得一个表中的某行与另一个表中的某一行甚至整个表相关联。

我们下面就从“增删改查”四方面来讨论这些集合的操作。

增:

关于向数据集里增加DataTable，最简单的就是调用Ilist接口的Add方法，如向数据集里加入名称为“Person”和“Books”两个数据表：

ds.Tables.Add\(＂Person＂\);

ds.Tables.Add\(＂Books＂\);

l       删：

从数据集里删除某个DataTable使用Ilist接口的Remove和RemoveAt方法：

DataSet ds=new DataSet\(\);

DataTabledtPerson=ds.Tables.Add\(＂Person＂\);

ds.Tables.RemoveAt\(0\);      //从数据集里删除索引为0的表，也就是dtPerson

ds.Tables.Remove\(dtPerson\);//从数据集里删除dtPerson

l       改：

数据集里的DataTable只能添加和删除，不能修改。

l       查：

获得数据集里的DataTable,可以使用索引器：

DataSet ds=new DataSet\(\);

ds.Tables.Add\(＂Person＂\);

DataTable dt=ds.Tables\[0\];//按数字索引获得DataTable

DataTable dt=ds.Tables\[＂Person＂\]; //按表名称获得DataTable

**4.3.2 DataTable的Columns集合**

增：

向数据表添加列我们在前面也提到了，添加的方式也是使用Ilist接口的Add（）。以下是最常用的添加列的方式：

dtPerson.Columns.Add\(＂psnNo＂,typeof\(string\)\);

删：

删除数据表中的列也是使用Ilist接口的Remove或RemoveAt方法：

    dtPerson.Columns.RemoveAt\(0\);  //按索引删除列，这里是删除第一列

    dtPerson.Columns.Remove\(＂psnNo＂\); //按列的名称删除列

改：

修改DataTable里面的某一列可以通过索引器先获得，然后再修改：

DataColumnc=dtPerson.Columns\[＂psnName＂\];

c.AllowDBNull=false;

查：

从DataTable里面获得某一列也是使用索引器的方式：

DataColumnc=dtPerson.Columns\[＂psnName＂\]; //按列名获得该列对象

DataColumnc=dtPerson.Columns\[0\];  //按列索引获得该列对象，这里是获得第一列  
**4.3.3 DataTable的Rows集合：**

增：

向DataTable里面增加数据行使用Add\(\)方法，有两种方式。一种方式，加入行之前要先使用DataTable的NewRow方法获得一个空行：

DataRowr=dtPerson.NewRow\(\);

dtPerson.Rows.Add\(r\);

第二种方式，你可以根据表的列结构构造一个对象数组，这种方式要注意你构造的数组要与表的列结构对应：

object\[\]r=new object\[\]{＂001＂，＂帕瓦罗蒂＂，＂男＂，22，＂中国郑州＂}

删:

删除某个数据行，可以使用Ilist接口的Remove和RemoveAt两种方法，还可以使用该行的delete方法，使用RemoveAt或delete方法删除行比较常用：

DataRowr=dtPerson.NewRow\(\);

dtPerson.Rows.Add\(r\);

r.Delete\(\);  //删除r行

dtPerson.Rows.Remove\(r\);  //删除r行

dtPerson.Rows.RemoveAt\(0\);  //按行索引删除行，这里是删除第一行

改:

因为数据集的实际数据就保存在行里，所以修改行数据是数据集里面最常用的一个操作，修改行也是先使用表的索引器先获得行，然后再使用行的索引器进行修改：

DataRow  r=dtPerson.Rows\[0\];

r\[＂psnSex＂\]= ＂女＂; //按列名修改该行的值

r\[0\]=＂＂;     //按列索引修改行，这里是修改该行的第一列数据

查:

获得某个表的某一行使用表的索引器，获得行的某一列值使用行的索引器，使用方式我们在介绍修改行的时候已经介绍过了，你可以通过数据集直接使用索引获得某行某列的值，要注意返回的值是object类型的，要想获得具体的值还需要进行类型转换：

获取Person表第二行psnName列的数据：

string name=ds.Tables\[＂Person＂\].Rows\[1\].Columns\[＂psnName＂\].ToString\(\);

获取Person表第二行列索引为4的列数据，注意索引都从0开始：

stringaddress=ds.Tables\[＂Person＂\].Rows\[1\].Columns\[4\].ToString\(\);

获取数据集中第一个表，第二行第五列的数据：

stringsex=ds.Tables\[0\].Rows\[1\].Columns\[4\].ToString\(\);

当然，也可以通过循环遍历表中所有行的数据：

foreach\(DataRowr in dtPerson.Rows\)

{

    foreach\(DataColumn c in dtPerson.Columns\)

       Console.WriteLine\(＂{0}＂,r\[c.ColumnName\]\);

}  


**4.4 DataView 类**

（1）得到DataView。

DataView dv = ds.Tables\[0\].DefaultView; 

//或  

DataView dv = new DataView\(ds.Tables\["Product"\], "ID &gt; 52", "ID DESC", 

DataViewRowState.CurrentRows\); 

（2）得到DataView的行数据。

foreach \(DataRowView rowview in dv\) 

{ 

    for \(int i = 0; i &lt; dv.Table.Columns.Count; i++\) 

    { 

        Response.Write\(rowview\[i\] + "  
"\);  

    }     

} 

