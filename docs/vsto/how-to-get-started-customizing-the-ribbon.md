---
title: 如何： 开始自定义功能区 |Microsoft 文档
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, adding Ribbon to project
- Ribbon [Office development in Visual Studio], adding
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, adding Ribbon to project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 304cf3e9d445bcb655e27e8e35605549f489155c
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-get-started-customizing-the-ribbon"></a>如何：开始自定义功能区
  若要自定义 Microsoft Office 应用程序的功能区，将添加**功能区 （可视化设计器）**或**功能区 (XML)**项到 Office 项目。  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
### <a name="to-add-a-ribbon-to-a-project"></a>若要向项目中添加功能区  
  
1.  上**项目**菜单上，单击**添加新项**。  
  
2.  在**添加新项**对话框中，选择**功能区 （可视化设计器）**或**功能区 (XML)**。 有关这些模板的详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。  
  
3.  在**名称**框中，键入功能区项的名称。  
  
     名称不能包含以下字符：  
  
    -   井号 （#）  
  
    -   百分号 （%）  
  
    -   And 符 (&)  
  
    -   星号 (*)  
  
    -   竖线 (|)  
  
    -   反斜杠 (\\)  
  
    -   冒号 （:）  
  
    -   双引号 (")  
  
    -   小于 (\<)  
  
    -   大于 (>)  
  
    -   问号 (?)  
  
    -   正斜杠 （/）  
  
    -   前导空格或尾随空格 ()  
  
    -   为 Windows 或 DOS 等 （"nul"、"aux"、"con"、"com1"、"lpt1"） 保留的名称  
  
4.  单击 **“确定”**。  
  
 功能区项出现在**解决方案资源管理器**。 有关后续步骤的信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Accessing the Ribbon at Run Time](../vsto/accessing-the-ribbon-at-run-time.md)   
 [功能区设计器](../vsto/ribbon-designer.md)   
 [功能区 XML](../vsto/ribbon-xml.md)   
 [演练： 使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)  
  
  