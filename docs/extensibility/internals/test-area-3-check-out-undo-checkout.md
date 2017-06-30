---
title: "测试区域 3︰ 检查传出撤消签出 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "源代码管理插件、 签出"
  - "源代码管理插件、 撤消签出"
  - "签出源代码管理 [Visual Studio SDK]"
  - "源控件 [Visual Studio SDK]，撤消签出"
ms.assetid: ce00c5a5-d472-4f45-8776-d77a1fbe9d37
caps.latest.revision: 16
ms.author: "gregvanl"
manager: "ghogen"
caps.handback.revision: 16
---
# 测试区域 3︰ 签出/撤消签出
[!INCLUDE[vs2017banner](../../code-quality/includes/vs2017banner.md)]

此源代码管理插件测试一方面涵盖了从版本存储区通过编辑和恢复项 **签出** 和 **撤消签出** 命令。  
  
 **签出**︰ 标记版本存储区中的项签出，将会修改为读\/写的本地副本。  
  
 **撤消签出**︰ 标记为签入版本存储区中的项目，将恢复到前 （具体取决于选项） 签出状态的本地副本。  
  
## 命令菜单访问  
 以下 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成的开发环境菜单路径使用的测试用例。  
  
##### 您可以查看︰  
  
-   **文件**, ，**源代码控制**, ，**签出**。  
  
-   **文件**, ，**签出**。  
  
-   快捷菜单上， **签出**。  
  
-   撤消签出︰ **文件**, ，**源代码控制**, ，**撤消签出**。  
  
## 常见的预期的行为  
  
-   在签出操作之后, 的目标文件和\/或文件夹标记为版本存储区中签出。  
  
-   版本存储区为正确的用户属性签出。  
  
-   签出的日期和时间正确 （每个用户的设置）。  
  
## 测试用例  
 以下是有关签出\/撤消签出测试区域的特定测试用例。  
  
### Case 3a︰ 签出  
 本部分重点介绍的签出命令的操作。  
  
|操作|测试步骤|若要验证的预期的结果|  
|--------|----------|----------------|  
|检查出排他 \(COE\) 客户端项目|1.  创建一个客户端项目。<br />2.  将解决方案添加到源代码管理。<br />3.  以独占方式签出整个项目 \(**文件**, ，**签出**\)。|签出发生。|  
|签出排他锁 \(COE\)，文件系统或本地 IIS Web 项目|1.  设置 Web 服务器连接到文件中的共享 **工具**, ，**选项**, ，**项目**, ，**Web 设置**。<br />2.  创建 Web 项目。<br />3.  将解决方案添加到源代码管理。<br />4.  以独占方式签出整个项目 \(**文件**, ，**源代码管理**, ，**签出**\)。|签出发生。|  
|签出解决方案 （新方法，用于处理其他文件） 中的解决方案项|1.  创建一个空白解决方案。<br />2.  将解决方案添加到源代码管理。<br />3.  签出解决方案。<br />4.  添加多个解决方案项目。<br />5.  签入所有新添加的项。<br />6.  选择多个解决方案项目。<br />7.  签出所选的项 \(快捷菜单上， **签出**\)。|选定的文件已签出。|  
|检查出本地版本 （如果待测试插件支持此功能）|1.  用户 1︰ 创建客户端项目。<br />2.  用户 1︰ 添加到源代码管理解决方案。<br />3.  用户 2︰ 到另一个位置从源代码管理打开的解决方案。<br />4.  用户 2︰ 签出文件。<br />5.  用户 2︰ 修改文件。<br />6.  用户 2︰ 签入文件。<br />7.  用户 1︰ 签出文件的本地版本 \(检查 **签出本地版本** 高级选项中的 **签出** 对话框\)。|文件的本地版本签出。<br /><br /> 由用户 2 的修改不应用于用户 1 文件。|  
  
### Case 3b︰ 断开连接签出  
 在断开连接模式下操作允许用户一定程度的持续的源控件支持时不直接连接至的版本存储区。 这是通过本地缓存的已登记的解决方案和项目的所有相关信息。  
  
 在连接到源代码管理存储区时，才会发生独占签出操作。 是否连接或断开连接，可以在任何时候，发生共享的签出操作。 因此，当从版本存储区仅断开连接 **签出共享** \(CO\) 启用命令。 断开连接时， **撤消签出** 被禁用，因为无法检索旧版本以替换用户所做的更改。  
  
 当用户重新连接到的版本存储，签出状态的所有已登记的解决方案和项目进行同步。 这将为用户执行签出执行必要的更新到存储区。 一旦发生同步，用户将能够继续使用像平常一样 （连接）。  
  
#### 预期的行为  
  
-   不能使用 **签出以独占方式** 命令从版本存储区断开连接时。  
  
-   不能使用 **撤消签出** 命令从版本存储区断开连接时。  
  
-   **共享签出** 命令有效。  
  
|操作|测试步骤|若要验证的预期的结果|  
|--------|----------|----------------|  
|断开连接时，签出文件，然后将连接用于同步|1.  断开受控的项目使用更改源代码管理对话框中的连接 \(**文件**, ，**源代码管理**, ，**更改源代码管理**l\)。<br />2.  签出文件。<br />3.  单击签出 （断开连接） 在警告对话框中。<br />4.  编辑文件。<br />5.  使用更改源代码管理对话框中进行连接。<br />6.  获取所编辑文件的最新版本。|常见的预期的行为|  
  
### 案例 3 c︰ 查询编辑\/查询保存 \(QEQS\)  
 在源代码管理下的项进行跟踪的编辑，更改，并保存，以帮助用户轻松管理他们的文件。 "签入"的受控的项编辑时，QEQS 截获尝试的编辑，并询问用户是否希望签出文件对其进行编辑。 具体取决于 **工具**, ，**选项** 设置时，用户是强制签出文件以便编辑或有权编辑内存中的副本和更高版本签出。 如果用户的 **工具**, ，**选项** 设置未设置以显示签出对话框中并只需签出，然后按用户进行他编辑，该文件自动签出，只要有可能。  
  
#### 预期的行为  
  
-   在签出操作之后, 的目标文件和\/或文件夹标记为版本存储区中签出。  
  
-   版本存储区为正确的用户属性签出。  
  
-   签出日期和时间正确 （每个用户的设置）。  
  
-   目标文件或文件夹的本地副本是可写的。  
  
|操作|测试步骤|若要验证的预期的结果|  
|--------|----------|----------------|  
|编辑签入的文本文件|1.  创建新的项目包含一个文本文件。<br />2.  将解决方案添加到源代码管理。<br />3.  设置 **工具**, ，**选项**, ，**源代码管理**, ，**允许文件期间磁盘上以只读方式编辑** 为未选中。<br />4.  设置 **工具**, ，**选项**, ，**源代码管理**, ，**提示输入签出** 中 **签入时编辑文件** 组合框。<br />5.  设置 **工具**, ，**选项**, ，**源代码管理**, ，**提示输入签出** 中 **时签入文件将保存** 组合框。<br />6.  在编辑器中打开文本文件，尝试在文件中键入新文本。 如果此步骤成功，则继续下一步。<br />7.  单击 **取消** 中 **签以进行编辑** 对话框。 如果此步骤成功，则继续下一步。<br />8.  设置 **工具**, ，**选项**, ，**源代码管理**, ，**允许文件期间磁盘上以只读方式编辑** 为选中状态。<br />9. 在编辑器中打开项目文件，尝试在文件中键入新文本。 如果此步骤成功，则继续下一步。<br />10. 单击 **编辑** 中 **签以进行编辑** 对话框。 如果此步骤成功，则继续下一步。<br />11. 编辑文本文件并尝试将其保存。|`Result of step 6:`<br /><br /> 编辑对话框中将显示，则签出。<br /><br /> `Result of step 7:`<br /><br /> 该文件保持不变。<br /><br /> `Result of step 9:`<br /><br /> 编辑对话框中将显示，则签出。<br /><br /> `Result of step 10:`<br /><br /> 您可以编辑内存中的项目文件。<br /><br /> `Result of step 11:`<br /><br /> 在保存、 签出上的保存对话框中会出现。|  
|编辑签入的解决方案文件|重复在以前所述的步骤测试，但更改解决方案的属性，而不是修改一个文本文件，修改解决方案。|与前面的测试相同|  
|编辑签入的项目文件|重复在以前所述的步骤测试，但更改项目属性，而不是修改一个文本文件，修改项目。|与前面的测试相同。|  
  
### 例三维︰ 自动签出  
 此子区域涵盖签出方案其中 **签出** 对话框不会不显示每个用户的 **工具**, ，**选项**, ，**源代码管理设置**。  
  
#### 预期的行为  
  
-   在签出操作之后, 的目标文件和\/或文件夹标记为版本存储区中签出。  
  
-   版本存储区为正确的用户属性签出。  
  
-   签出日期和时间正确 （每个用户的设置）。  
  
-   目标文件或文件夹的本地副本是可写的。  
  
|操作|测试步骤|若要验证的预期的结果|  
|--------|----------|----------------|  
|无提示签出文件|1.  设置 **工具**, ，**选项**, ，**源代码管理** 到 **在编辑后自动签出文件**。<br />2.  使用的文件创建一个新的项目。<br />3.  将解决方案添加到源代码管理。<br />4.  签出该文件。|文件已签出以无提示方式 （无用户界面）。|  
|项目的的无提示签出|1.  设置 **工具**, ，**选项**, ，**源代码管理** 到 **在编辑后自动签出文件**。<br />2.  创建新项目。<br />3.  将解决方案添加到源代码管理。<br />4.  签出该项目。|文件已签出以无提示方式 （无用户界面）。|  
  
### Case 3e︰ 撤消签出  
 **撤消签出** 用于取消的文件已签出状态，并避免对文件所做的更改签入。  
  
#### 预期的行为  
  
-   默认值基于用户的 **签出本地版本** 设置。 如果用户已经选择签出本地版本，然后撤消签出的默认值是始终恢复为签出的版本。  
  
-   在撤消，中的图标，接受 **解决方案资源管理器** 影响个更新的文件和项目从 **挂起的签入** 窗口。  
  
|操作|测试步骤|若要验证的预期的结果|  
|--------|----------|----------------|  
|撤消签出操作将以独占方式签出的单个文件|1.  创建一个客户端项目。<br />2.  将解决方案添加到源代码管理。<br />3.  以独占方式签出文件。<br />4.  修改该文件。<br />5.  撤消签出 \(**文件**, ，**源代码控制**, ，**撤消签出**\)。|常见的预期的行为。|  
|撤消签出共享的单个文件签出|1.  创建一个客户端项目。<br />2.  将解决方案添加到源代码管理。<br />3.  签出文件共享。<br />4.  修改该文件。<br />5.  撤消签出 \(**文件**, ，**源代码控制**, ，**撤消签出**\)。|常见的预期的行为。|  
|将文件添加到项目后撤消签出的一个项目|1.  创建一个新项目并将其添加到源代码管理。<br />2.  签出该项目。<br />3.  将文件添加到项目。<br />4.  撤消签出的项目。|添加的文件从解决方案资源管理器中的项目。<br /><br /> 项目不能再签出。|  
|从项目中删除文件后撤消签出的一个项目|1.  创建一个新项目并将其添加到源代码管理。<br />2.  签出该项目。<br />3.  从项目中删除一个文件。<br />4.  撤消签出的项目。|已删除的文件显示在解决方案资源管理器中的项目。<br /><br /> 项目不能再签出。|  
  
## 请参阅  
 [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)