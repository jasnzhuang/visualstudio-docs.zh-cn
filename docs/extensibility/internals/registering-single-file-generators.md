---
title: 注册单个文件生成器 |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b9b7d16a9e473028d85540f4447d9981382be0fd
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="registering-single-file-generators"></a>注册单个文件生成器
在中提供一个自定义工具[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，必须将其注册因此[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可以实例化并将其关联与特定项目类型。  
  
### <a name="to-register-a-custom-tool"></a>若要注册一个自定义工具  
  
1.  请注册自定义工具 DLL 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本地注册表或系统注册表项下 HKEY_CLASSES_ROOT。  
  
     例如，下面是托管的 MSDataSetGenerator 自定义工具，它附带的注册信息[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]:  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
    @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
    "ThreadingModel"="Both"  
    "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
    ```  
  
2.  创建所需的注册表项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]下生成器 hive\\*GUID*其中*GUID* GUID 定义由特定语言的项目系统或服务。 密钥的名称将成为自定义工具的编程名称。 自定义工具密钥具有以下值：  
  
    -   (默认)  
  
         可选。 提供自定义工具的用户友好的说明。 此参数是可选的但建议这样做。  
  
    -   CLSID  
  
         必须的。 指定实现的 COM 组件的类库的标识符<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>。  
  
    -   GeneratesDesignTimeSource  
  
         必须的。 指示是否从由此自定义工具生成的文件类型以及可供可视化设计器。 此参数的值需要 （零） 为 0 到可视化设计器不可用的类型或类型可用于可视化设计器 （一个） 1。  
  
    > [!NOTE]
    >  你必须注册为你想自定义工具可为其每个语言分别自定义工具。  
  
     例如，MSDataSetGenerator 注册自身一次为每种语言：  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]  
    @="Microsoft VB Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]  
    @="Microsoft C# Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
    ```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [实现单个文件生成器](../../extensibility/internals/implementing-single-file-generators.md)   
 [公开到可视化设计器的类型](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [简介 BuildManager 对象](http://msdn.microsoft.com/en-us/50080ec2-c1c9-412c-98ef-18d7f895e7fa)