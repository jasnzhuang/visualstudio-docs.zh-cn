---
title: FeatureProperty 元素 |Microsoft 文档
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FeatureProperty element
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a937310ddbb866cbe046ea2975f8d76e75fe2a98
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34766960"
---
# <a name="featureproperty-element"></a>FeatureProperty 元素
  表示将其部署到 SharePoint 时所随附一项功能的自定义属性。 将功能部署后，你可以在代码中访问属性。  
  
## <a name="syntax"></a>语法  
  
```xml  
<FeatureProperty Key = "Key of the property value"  
    Value = "Property value" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|**Key**|所需**xs: string**属性。<br /><br /> 用来存储和检索属性值的密钥。 每个属性必须具有一个用于在功能中是唯一的键。|  
|**值**|所需**xs: string**属性。<br /><br /> 属性值。|  
  
### <a name="child-elements"></a>子元素
 无。  
  
### <a name="parent-elements"></a>父元素
  
|元素|描述|  
|-------------|-----------------|  
|[FeatureProperties](../sharepoint/featureproperties-element.md)|表示部署到 SharePoint 时所包含的一项功能的属性值的集合。|  
  
## <a name="remarks"></a>备注  
 功能属性有关的详细信息，请参阅[提供打包和部署信息在项目项中](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)。  
  
## <a name="element-information"></a>元素信息
  
|||  
|-|-|  
|**命名空间**|http<nolink>: //schemas.microsoft.com/VisualStudio/<br>2010/SharePointTools/SharePointProjectItemModel|  
|**架构名称**|SharePoint 项目项架构|  
|**验证文件**|ProjectItemModelSchema.xsd|  
|**可以为空**|否|  
  
## <a name="see-also"></a>请参阅
 [SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)   
 [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)  
  
  
