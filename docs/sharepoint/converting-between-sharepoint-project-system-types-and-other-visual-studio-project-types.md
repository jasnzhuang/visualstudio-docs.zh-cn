---
title: SharePoint 项目系统类型和其他 Visual Studio 项目类型之间进行转换 |Microsoft 文档
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 64de38fe796ce3c1e0d333a22582ad2973e1c4d2
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34765354"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换
  在某些情况下您可能会在 SharePoint 项目系统中有一个对象，并且你想要使用的 Visual Studio 自动化对象模型或集成对象模型中相应对象的功能，反之亦然。 在这些情况下，你可以使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>SharePoint 项目服务将对象转换为不同的对象模型的方法。  
  
 例如，你可能必须<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象，但你想要使用仅有的方法<xref:EnvDTE.Project>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>对象。 在这种情况下，你可以使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>方法将转换<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>到<xref:EnvDTE.Project>或<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>。  
  
 有关 Visual Studio 自动化对象模型和 Visual Studio 集成对象模型的详细信息，请参阅[的编程模型的 SharePoint 工具扩展的概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)。  
  
## <a name="types-of-conversions"></a>类型的转换
 下表列出了此方法可以 SharePoint 项目系统和其他 Visual Studio 对象模型之间进行转换的类型。  
  
|SharePoint 项目系统类型|自动化和集成对象模型中的相应类型|  
|------------------------------------|-------------------------------------------------------------------------|  
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> 或<br /><br /> 在 Visual Studio 集成对象模型由项目的基础 COM 对象实现任何接口。 这些接口包括<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>， <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> （或派生的接口），和<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>。 由项目实现的主要接口的列表，请参阅[项目模型核心组件](/visualstudio/extensibility/internals/project-model-core-components)。|  
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> 或<br /><br /> A<xref:System.UInt32>标识中的项目成员的值 （也称为 VSITEMID）<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>包含它。 此值可以传递给*itemid*的某些参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>方法。|  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何使用<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A>方法将转换<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>对象传递给<xref:EnvDTE.Project>。  
  
 [!code-csharp[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs#2)]
 [!code-vb[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb#2)]  
  
 此示例需要：  
  
-   具有对引用 SharePoint 项目系统的扩展*EnvDTE.dll*程序集。 有关详细信息，请参阅[扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)。  
  
-   注册的代码`projectService_ProjectAdded`方法以处理<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded>事件<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService>对象。 有关示例，请参阅[如何： 创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。  
  
## <a name="see-also"></a>请参阅
 [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)   
 [如何： 检索 SharePoint 项目服务](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)   
 [SharePoint 工具扩展的编程模型概述](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)  
  
