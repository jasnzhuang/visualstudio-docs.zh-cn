---
title: 捕获图形信息 |Microsoft 文档
ms.custom: ''
ms.date: 02/09/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.frame
- vs.graphics.capturewindow
- VS.ToolsOptionsPages.Graphics_Diagnostics.Capture
ms.assetid: 187ce86e-e340-4f6c-8937-8e8f1027a17f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e00dd4d0fae184f092efabb5df4a4f27e76a653a
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="capturing-graphics-information"></a>捕获图形信息
从 Direct3D 应用捕获图形信息，以便使用 Visual Studio 图形分析器来诊断呈现问题和性能问题。  
  
## <a name="capturing-graphics-information"></a>捕获图形信息  
 捕获图形信息的过程分为两步。 首先，在图形诊断下运行应用程序，然后指定要从中捕获详细信息的一个或多个帧。  
  
### <a name="to-run-your-app-under-graphics-diagnostics"></a>在图形诊断下运行应用程序  
  
-   在菜单栏上，选择**调试**，**图形**，**启动图形调试**。 （键盘：按 Alt+F5）  
  
-   上**图形**工具栏上，选择**启动图形调试**按钮。  
  
 当应用程序在图形诊断下运行时，将始终捕获某些类型的图形信息；这包括设备设置、交换链的创建、图形对象和资源的创建以及其他影响多个帧的重要事件。 同时，你可以捕获有关特定帧的详细信息；这包括绘图调用和计算着色器调度，以及支持它们的 Direct3D 对象和资源。  
  
### <a name="to-capture-a-frame"></a>捕获帧  
  
-   在 Visual Studio 中，在**图形**工具栏上，单击**捕获帧**按钮![图形捕获按钮图标](media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics").  
  
-   在键盘上，按 Print Screen 键。
  
    > [!NOTE]
    >  在运行应用时**图形诊断**，Print Screen 键只能捕获图形信息的帧; 不执行其常规功能。 这将一直有效，直到你停止捕获图形信息（通常通过停止调试或正常退出应用程序），即使另一应用程序具有焦点时也是如此。  
  
-   在 Visual Studio 捕获接口中，选择**捕获帧**按钮位于下面**诊断会话**时间线，也可选择**捕获帧**按钮位于下面**每秒帧数**泳道和右侧的任何先前捕获的帧。 两个按钮均突出显示在下方的图像中。  
  
     ![使用 GPU 使用情况工具捕获帧。](media/pix_gpu_usage_tool_capture_frame.png)  
  
     如果你已准备好检查帧已捕获、 启动**Visual Studio 图形分析器**按照**帧...**高于图像缩略图，或通过双击该缩略图的链接。  
  
 可以捕获仅整帧，因此当你启动捕获时，它实际上记录下一个帧的图形信息。 记录将在显示你从中启动捕获的帧后立即开始，在显示捕获的帧后结束。 应用程序在图形诊断下运行时，可以捕获你所需的多个帧。 如果未捕获任何帧，将丢弃图形日志。  
  
 捕获帧时，Visual Studio 将显示诊断会话 (.diagsession) 窗口。 如果你关闭此窗口、 停止调试，或关闭应用程序，你无法捕获任何帧到该日志。 要捕获更多图形信息，必须在图形诊断下再次运行应用以启动新的诊断会话。  
  
### <a name="graphics-diagnostics-capture-options"></a>图形诊断捕获选项  
 你可以通过配置捕获来收集所有图形事件或有限子集的调用堆栈，禁用捕获 HUD，也可以启用或禁用捕获兼容模式。  
  
#### <a name="to-configure-graphics-diagnostics-capture-options"></a>配置图形诊断捕获选项  
  
1.  在菜单栏上，依次选择“工具”、“选项”。 这时会显示一个“选项”对话框。  
  
2.  在左侧的选项类别列表中选择“图形诊断”，然后配置所需的“图形诊断”选项。  
  
     **在捕获过程中收集调用堆栈 （使捕获速度变慢）**  
     选中该复选框以收集调用堆栈。 默认情况下，不会收集调用堆栈。 若要捕获调用堆栈，请确保**捕获过程中收集调用堆栈 (使捕获速度变慢**复选框设置为启用收集，然后设置**绘图、 调度、 现在和性能标记**选项 （默认值），以收集仅最重要的调用堆栈，或**所有操作都**选项以收集所有调用堆栈。 若要停止收集调用堆栈更高版本，请清除**捕获过程中收集调用堆栈 (使捕获速度变慢**复选框。  
  
     **在捕获期间禁用在游戏中的 HUD**  
     选中此框以禁用在图形诊断下运行的应用通常会显示的 HUD 覆盖。 取消选中以显示 HUD 覆盖。  
  
     **在兼容性模式下捕获**  
     选中此框以在兼容模式下捕获图形信息。 在兼容模式下捕获是默认设置。 在兼容模式下，Direct3D 不会报告 GPU 会支持基本功能级别中所定义的功能范围以外的任何其他功能。 这样可以防止使用特定于硬件的 GPU 扩展将应用捕获到这个 GPU 上，同时确保图形日志可以通过任何支持相同或更高功能级别的 GPU 进行播放。 取消选中此框可禁用兼容模式；兼容模式被禁用时所捕获的日志将不能在任何不支持与应用程序在捕获期间使用的其他功能相同的功能的 GPU 上播放。  
  
     **如果找到任何 SDK _layers 错误，停止捕获**  
     选中此框以便在遇到错误时立即停止捕获。  
  
## <a name="capturing-graphics-information-remotely"></a>远程捕获图形信息  
 可以从本地计算机或者远程计算机或设备上运行的应用程序捕获图形信息。 [!INCLUDE[winblue_client_2](../includes/winblue_client_2_md.md)] 计算机和 [!INCLUDE[winblue_winrt_2](../includes/winblue_winrt_2_md.md)] 设备支持远程捕获。 若要从远程运行的应用程序捕获图形信息，请配置你的项目以进行远程调试，然后如之前所述，在图形诊断下运行应用程序。 应用程序在远程计算机上运行，捕获的图形信息将记录在你的开发计算机上。  
  
 配置项目以进行远程调试的方式取决于你开发的应用程序类型以及你使用的编程语言。 有关如何为 UWP 应用配置远程调试的信息，请参阅[远程计算机上运行的 UWP 应用](../run-windows-store-apps-on-a-remote-machine.md)。 有关如何为 Windows 桌面应用程序配置远程调试的信息，请参阅[远程调试](../remote-debugging.md)。  
  
 之后，可以使用远程计算机或设备播放图形信息，而无论信息从何处捕获。 有关详细信息，请参阅[如何： 更改图形诊断播放机](how-to-change-the-graphics-diagnostics-playback-machine.md)。  
  
## <a name="capturing-graphics-information-from-the-command-line"></a>从命令行捕获图形信息  
 可使用命令行工具从应用捕获图形信息。 DXCap.exe 这一工具可以快速捕获和播放图形信息，而不使用 Visual Studio 或编程捕获。 具体而言，你可以使用 DXCap.exe 来实现自动化，或在测试环境中使用。 有关 DXCap.exe 的详细信息，请参阅[命令行捕获工具](command-line-capture-tool.md)  
  
## <a name="see-also"></a>请参阅  
 [演练：捕获图形信息](walkthrough-capturing-graphics-information.md)