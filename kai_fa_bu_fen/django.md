## django {#django}

### 本地化（汉化）

1、开启国际化的支持，需要在settings.py文件中设置

2、生成需要翻译的文件

3、手工翻译 locale 中的 django.po

4、编译一下，这样翻译才会生效： python manage.py compilemessages。

5、mis项目中 有几处设置：1、mis/locale

2\python27\lib\site-packages\django\contrib\admin\locale

2\python27\lib\site-packages\django\quth\admin\locale

#### 字段汉化 {#-0}

1.  在 admin.py文件中 建class LxUser时候
2.  username = models.CharField(_(**&quot;lxUserName&quot;**),max_length=30)

_(**&quot;lxUserName&quot;**) 就是用来汉化的msgid

1.  在django.po文件中 写中文名

msgid &quot;lxUserName&quot;

msgstr &quot;用户姓名&quot;

#### 二级菜单汉化 {#-1}

1.Model.py 文件中的

class Meta:

verbose_name = _(&#039;LxUser&#039;)

verbose_name_plural = _(&#039;LxUser&#039;)

其中LxUser就是 二级菜单中 显示名称的msgid

#### 一级菜单汉化（app） {#app-1}

Apps.py中 lxUnLoad mangentment

**class** LxunloadConfig(AppConfig): name = **&#039;lxUnLoad&#039;** verbose_name = _(**&quot;lxUnLoad mangentment&quot;**)

verbose_name 在 po 文件中配置

### 重新部署模块(app) {#app}

python manage.py migrate

### 新建模块(app) {#app-0}

#### 建全新模块 {#-2}

要先进入项目目录下，cd project_name 然后执行下面的命令（

python manage.py startapp app_name

或 django-admin.py startapp app_name

1、完成后 自动生成以下文件

2、把定义的app（lxUser）加到settings.py中的INSTALL_APPS中

3、修改models.py

对应 adm数据库中的 users表

4、定义url

5,修改 admin.py文件

运行

说明 表名错误了。

处理方法：1、程序自动建表

python manage.py makemigrations

python manage.py migrate

如果出现 no change detected 可以试试 python manage.py makemigrations --empty lxUser 现建一个空的 initial.py。

如果还出错，就自己修改 .py文件中的数据库生成语句。

#### 根据现有数据库建立model {#model}

Python manage.py inspectdb

这样就可以在命令行看到数据库的模型文件了

把模型文件导入到app中

创建一个app

django-admin.py startapp app

python manage.py inspectdb &gt; app/models.py

ok模型文件已经生成好了。下面的工作就和之前一样了