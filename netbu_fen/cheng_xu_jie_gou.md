## 程序结构

Tx.Party.sln：解决方案，Visual Studio 的解决方案文件是一个文本文件。

附:文件后缀

_sln：解决方案文件，为解决方案资源管理器提供显示管理文件的图形接口所需的信息。_

_.csproj:项目文件，创建应用程序所需的引用、数据连接、文件夹和文件的信息。_

_.aspx：Web 窗体页由两部分组成：视觉元素（HTML、服务器控件和静态文本）和该页的编程逻辑。Visual Studio 将这两个组成部分分别存储在一个单独的文件中。视觉元素在.aspx 文件中创建。_

_.aspx.cs：Web 窗体页的编程逻辑位于一个单独的类文件中，该文件称作代码隐藏类文件（.aspx.cs）。_

_.cs： 类模块代码文件。业务逻辑处理层的代码。_

_.asax：Global.asax 文件（也叫做 ASP.NET 应用程序文件）是一个可选的文件，该文件包含响应 ASP.NET 或 HTTP 模块引发的应用程序级别事件的代码。_

_.config：Web.config 文件向它们所在的目录和所有子目录提供配置信息。_

_.aspx.resx/.resx：资源文件，资源是在逻辑上由应用程序部署的任何非可执行数据。通过在资源文件中存储数据，无需重新编译整个应用程序即可更改数据。_

_.XSD:XML schema的一种.从DTD,XDR发展到XSD_

_.pdb:PDB（程序数据库）文件保持着调试和项目状态信息，从而可以对程序的调试配置进行增量链接。_

_.suo:解决方案用户选项,记录所有将与解决方案建立关联的选项，以便在每次打开时，它都包含您所做的自定义设置。_

_.asmx:asmx 文件包含 WebService 处理指令，并用作 XML Web services 的可寻址入口点_

_.vsdisco（项目发现）文件 基于 XML 的文件，它包含为 Web 服务提供发现信息的资源的链接 \(URL\)。_

_.htc:一个HTML文件,包含脚本和定义组件的一系列HTC特定元素.htc提供在脚本中implement组件的机制_

_.ascx 是用户控件代码文件_

_.aspx webform html脚本文件_

_.cs 是c\#类文件\)_

_.vb 是vb类文件\)_

_.aspx.cs 和你的webform相关的后台c\#代码文件,其实跟.cs是一样的_

_.aspx.vb 和你的webform相关的后台VB代码文件,其实跟.vb是一样的_

_web.config 配置文件_

_.xml xml文件_

_.css 样式表文件_

### 版本信息 {#-0}

Microsoft Visual Studio Solution File：用来说明解决方案文件的版本号，12.00 说明是 VS2015 的解决方案文件。

VisualStudioVersion：打开这个解决方案文件需要的 Visual Studio 版本号

MinimumVisualStudioVersion：能够打开这个解决方案的最低 Visual Studio 版本号。

Microsoft Visual Studio Solution File, Format Version 12.00

# Visual Studio 15

VisualStudioVersion = 15.0.26228.4

MinimumVisualStudioVersion = 10.0.40219.1

### 项目 {#-1}

解决方案中包含若干个项目，每个项目有一个Project的说明。

Project\(项目在解决方案中的编号=显示名称，实际路径，项目唯一标识\)

_Project\("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}"\) = "Tx.Party.Common", "Tx.Party.Common\Tx.Party.Common.csproj", "{3CA77F50-66F8-4284-B78B-178E7E665AB0}"_

_EndProjectEndProject_

项目的唯一标识来自项目文件，在对应的.csproj文件中可以找到

&lt;ProjectGuid&gt;{3CA77F50-66F8-4284-Bza78B-178E7E665AB0}&lt;/ProjectGuid&gt;

### 解决方案文件夹 {#-2}

解决方案文件夹, 则实际路径与显示名称一致。

### Global 配置节 {#global}

由三个部分组成

整个解决方案的配置信息在 SolutionConfigurationPlatforms 中。

每个项目的平台配置信息在 ProjectConfigurationPlatforms 中。

