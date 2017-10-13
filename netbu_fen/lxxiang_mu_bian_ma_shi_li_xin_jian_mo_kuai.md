## lx项目编码实例 -新建模块 {#lx}

### 设计数据库表

基础数据.社会单位档案 表名：SocialUnit

### 代码生成器 {#-0}

显示所有文件

### 生成Model {#model}

SocialUnit.cs

保存到：D:\TXLC\源代码\Tx.Party\Tx.Party.Common\Models\basedata

SocialUnit.Designer.cs

保存到：D:\TXLC\源代码\Tx.Party\Tx.Party.Common\Models\basedata

### 生成DAO {#dao}

SocialUnitDAO.cs 保存到D:\TXLC\源代码\Tx.Party\Tx.Party.DataAccess\basedata

SocialUnitDAO.Designer.cs 保存到D:\TXLC\源代码\Tx.Party\Tx.Party.DataAccess\basedata

### 生成服务 {#-1}

SocialUnitService.cs 保存到 D:\TXLC\源代码\Tx.Party\Tx.Party.Services\basedata

ISocialUnitService.cs 保存到 D:\TXLC\源代码\Tx.Party\Tx.Party.Services\basedata

在d:\txlc\源代码\tx.party\tx.party.mvcui\app\_start\unityconfig.cs 中注册服务 container.RegisterType&lt;ISocialUnitService, SocialUnitService&gt;\(\);

### 生成控制器 {#-2}

SocialUnitController.cs 保存到 D:\TXLC\源代码\Tx.Party\Tx.Party.MvcUI\Areas\basedata\Controllers

SocialUnitId 部分字段名会生成错误，手工修改

namespace Tx.Party.MvcUI.Areas.basedata.Controllers

命名空间也会出错，改成这个正确的。

### 创建视图 {#-3}

1. 列表[视图](/netbu_fen/mvcbian_cheng_mo_shi/mvc-shi-tu.md)

创建成功后会生成 一个文件夹和一个文件

1. 手工修改这个cshtml文件

此模块和 Role.cshtml风格接近 从 Role.cshtml中copy 代码来修改。

新增view

编辑视图

和新增用的是同一个页面、区别在于：

if \(top.\_currentDialog.editType == 'add'\) {

$\('input\[name="Opened"\]'\).prop\('checked', true\);

}

if \(top.\_currentDialog.editType == 'edit'\) {

$\('\#form1'\).form\('load', '@Url.Content\("~/basedata/SocialUnit/LoadSocialUnit"\)'\);

};

### 启用 {#-4}



