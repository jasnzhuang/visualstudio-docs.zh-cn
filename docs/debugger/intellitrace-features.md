---
title: "IntelliTrace 功能 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "调试 [Visual Studio ALM], IntelliTrace"
  - "调试 [Visual Studio ALM], recording execution history"
  - "IntelliTrace, 使用事件进行调试"
  - "IntelliTrace, 使用事件和调用信息进行调试"
  - "IntelliTrace, 禁用"
  - "IntelliTrace, 启用"
  - "IntelliTrace, 导航事件和调用历史记录"
  - "IntelliTrace, recording execution history"
  - "IntelliTrace, 保存会话"
  - "IntelliTrace, 开始调试"
  - "IntelliTrace, 关闭"
  - "IntelliTrace, 打开"
ms.assetid: 5ccc059c-6097-46b4-9d4b-34236c02d549
caps.latest.revision: 67
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 67
---
# IntelliTrace 功能
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

可以使用 IntelliTrace 记录事件和调用应用程序的方法，它让你能够在执行中的不同位置检查其状态（调用堆栈和局部变量值）。  正常启动调试即可，默认启用 IntelliTrace，并且可以在**“事件”**选项卡下的新**“诊断工具”**窗口中看到 IntelliTrace 正在记录的信息。  选择一个事件，然后单击**“激活历史调试”**以查看为此事件记录的调用堆栈和局部变量。  
  
 有关分步说明，请参阅[演练：使用 IntelliTrace](../debugger/walkthrough-using-intellitrace.md)。  
  
 Visual Studio Enterprise 版中提供 IntelliTrace，但 Visual Studio Professional 或 Community 版中不提供。  
  
 要确认 IntelliTrace 已启用，请打开**“工具”\/“选项”\/“IntelliTrace”**选项页。  默认情况下应选中**“启用 IntelliTrace”**。  
  
> [!NOTE]
>  **“IntelliTrace”**选项页上的所有设置都针对 Visual Studio 这个整体，而不针对单个项目或解决方案。  这些设置中的更改适用于 Visual Studio 的所有实例、所有调试会话和所有项目或解决方案。  
  
##  <a name="ChooseEvents"></a> 选择 IntelliTrace 记录的事件  
 可以启用或禁用针对特定 IntelliTrace 事件的记录。  
  
 如果在进行调试，请停止调试。  转到**“工具”\/“选项”\/“IntelliTrace”\/“IntelliTrace 事件”**。  选择想要 IntelliTrace 记录的事件。  
  
##  <a name="GoingFurther"></a> 收集 IntelliTrace 事件和调用信息  
 默认情况下不启用此选项，但 IntelliTrace 可以随事件一起记录方法调用。  要启用方法调用的收集，请转到**“工具”\/“选项”\/“IntelliTrace”\/“常规”**，然后选择**“IntelliTrace 事件和调用信息”**。  
  
 这使你可以查看调用堆栈历史记录以及在代码中的调用间后退和前进。  IntelliTrace 记录的数据包括方法名、方法进入和退出点，以及部分参数值和返回值。  
  
> [!TIP]
>  默认情况下不启用此选项，因为它会增加大量开销。  IntelliTrace 不仅需要截获应用程序生成的每个方法调用，当需要在屏幕上显示数据或将数据保留到磁盘时，它还需要处理一组更大的数据。  
>   
>  可以通过限制 IntelliTrace 记录的事件列表以及将收集的模块数保持为最小值来减少性能开销。  有关详细信息，请参阅[控制 IntelliTrace 记录的调用信息量](../debugger/intellitrace-features.md#ControlCallData)。  
  
### 使用导航线  
 可以使用代码窗口左侧显示的导航线。  如果没有看到导航线，则转到**“工具”\/“选项”\/“IntelliTrace”\/“高级”**，然后选择**“处于调试模式时显示导航线”**。  
  
 导航线让你能够在历史调试模式下向前和向后移动方法调用和事件。  有关历史调试的详细信息，请参阅[历史调试](../debugger/historical-debugging.md)。  它拥有多个命令：  
  
|||  
|-|-|  
|**在此设置调试器上下文**|将调试上下文设置为调用出现的调用时间范围。<br /><br /> 此图标仅在当前调用堆栈上显示。|  
|**返回调用站点**|将指针和调试上下文移回调用当前函数的位置。<br /><br /> 如果处于实时调试模式下，则此命令会启用历史调试。  如果向后定位到原始执行中断，则会禁用历史调试并启用实时调试。|  
|**转到上一个调用或 IntelliTrace 事件**|将指针和调试上下文移回上一个调用或事件。<br /><br /> 如果处于实时调试模式下，则此命令会启用历史调试。|  
|**单步执行**|单步执行当前选择的函数。<br /><br /> 只有处于历史调试模式下时才能使用此命令。|  
|**转到下一个调用或 IntelliTrace 事件**|将指针和调试上下文移到存在 IntelliTrace 数据的下一个调用或事件。<br /><br /> 只有处于历史调试模式下时才能使用此命令。|  
|**转到实时模式**|返回实时调试模式。|  
  
### 在 IntelliTrace 中搜索某行或某个方法  
 仅当已启用方法调用信息时才可以搜索方法。  可以搜索 IntelliTrace 历史记录以查找特定行或方法。  暂停调试程序执行时，在函数体内右键单击以查看上下文菜单，然后单击**“在 IntelliTrace 中搜索此行”**或**“在 IntelliTrace 中搜索此方法”**。  
  
###  <a name="ControlCallData"></a> 控制 IntelliTrace 记录的调用信息量  
 默认情况下，IntelliTrace 记录解决方案使用的所有模块的信息。  可以将 IntelliTrace 设置为仅记录你感兴趣的模块的调用信息。  在**“工具”\/”选项”\/“IntelliTrace”\/“模块”**中，可以指定 IntelliTrace 要包括或排除的模块。  IntelliTrace 将仅收集你指定的模块中生成的事件，以及你感兴趣的模块内发生的方法调用。  
  
 若要添加多个模块，请在字符串的开头或结尾使用通配符 \*。  对于模块名称，请使用文件名，而不是程序集名称。  不接受文件路径。  
  
 尝试将模块数保持为最小值。  因为要收集的数据变少，所以可以获得更好的性能。  UI 中的噪音也会减少，因为要浏览的数据变少。  
  
##  <a name="SaveSession"></a> 将 IntelliTrace 数据保存到文件  
 当你正在进行调试且应用程序处于中断状态时，通过转到**“调试”\/“IntelliTrace”\/“保存 IntelliTrace 会话”**，可以保存 IntelliTrace 收集的数据。  如果应用程序仍在运行或如果你已经停止调试，则菜单项会被禁用，且你将无法保存 IntelliTrace 收集的数据。  
  
 通过转到**“工具”\/“选项”\/“IntelliTrace”\/“高级”**并选择**“在此目录中存储 IntelliTrace 记录”**，可以将 IntelliTrace 配置为自动保存到文件。  还可以为生成的文件配置固定大小，这会让 IntelliTrace 在空间不足时覆盖旧数据。  自动保存文件并启用 Visual Studio 承载进程 \(vshost.exe\) 时，Visual Studio 会为每个 IntelliTrace 会话创建两个文件。  
  
> [!TIP]
>  要节省磁盘空间，请在不再需要时禁用自动保存文件。  不会删除任何现有文件。  可以随时从上下文菜单按需保存到文件。  
  
 将 IntelliTrace 数据保存到文件中时，每个 IntelliTrace 从中进行收集的进程都将获得一个 .itrace 文件。  然后，通过转到**“文件”\/“打开”\/“文件”**并从“打开文件”对话框中选择 .itrace 文件，你可以在 Visual Studio 中打开 .itrace 文件。  有关详细信息，请参阅[使用保存的 IntelliTrace 数据调试应用](../debugger/using-saved-intellitrace-data.md)。  
  
## 博客  
 [Visual Studio Enterprise 2015 中的 IntelliTrace](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/intellitrace-in-visual-studio-ultimate-2015.aspx)  
  
 [在 Visual Studio 2015 使用 IntelliTrace 进行实时调试的演练（文本编辑器）](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/16/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-text-editor.aspx)  
  
 [使用 Visual Studio 2015 中的 IntelliTrace 进行实时调试的演练（社交俱乐部）](http://blogs.msdn.com/b/visualstudioalm/archive/2000/1/1/walkthrough-of-live-debugging-using-intellitrace-in-visual-studio-2015-social-club.aspx)  
  
 [Visual Studio Enterprise 2015 中的 IntelliTrace 现在支持附加！](http://blogs.msdn.com/b/visualstudioalm/archive/2015/05/14/intellitrace-in-visual-studio-enterprise-2015-now-supports-attach.aspx)  
  
 [使用 IntelliTrace 独立收集器从 windows 服务中收集数据](http://blogs.msdn.com/b/visualstudioalm/archive/2015/05/14/collect-data-from-a-windows-service-using-the-intellitrace-standalone-collector.aspx)  
  
 [编辑 IntelliTrace 收集计划](http://blogs.msdn.com/b/visualstudioalm/archive/2015/03/09/editing-the-intellitrace-collection-plan.aspx)  
  
 [使用 IntelliTrace 自定义 TraceSource 和调试](http://blogs.msdn.com/b/visualstudioalm/archive/2014/12/17/custom-tracesource-and-debugging-using-intellitrace.aspx)  
  
 [使用 Active Directory 帐户运行的 IntelliTrace 独立收集器和应用程序池](http://blogs.msdn.com/b/visualstudioalm/archive/2014/12/22/intellitrace-standalone-collector-and-application-pools-running-under-active-directory-accounts.aspx)  
  
## 论坛  
 [Visual Studio 调试程序](http://go.microsoft.com/fwlink/?LinkId=262263)  
  
## 视频  
 [IntelliTrace 体验](https://channel9.msdn.com/Series/Visual-Studio-2015-Enterprise-Videos/IntelliTrace-Experience)  
  
 [使用 Microsoft Visual Studio Ultimate 2015 中的 IntelliTrace 进行历史调试](https://channel9.msdn.com/events/Ignite/2015/BRK3716)