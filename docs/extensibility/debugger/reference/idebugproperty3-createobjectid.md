---
title: IDebugProperty3::CreateObjectID |Microsoft 文档
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: df4e45c442745652b3305fd91146bd31ffe79e4b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
创建此属性的唯一 ID，以确保它是唯一的而所有其他属性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CreateObjectID(  
   void  
);  
```  
  
```csharp  
int CreateObjectID();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 当会话调试管理器想要确保此属性唯一地标识所有其他属性中调用此方法。 调试引擎 (DE) 支持此方法，除非已唯一标识它处理的属性。 如果设备不支持此方法，它将返回`E_NOTIMPL`。  
  
 使用任何唯一的 ID 创建`CreateObjectID`时销毁[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)调用方法; 这还指示用于唯一地标识此属性的需求的末尾。  
  
> [!NOTE]
>  没有方法来检索此唯一 ID，因此 DE 可以进行随意的唯一 Id 时`CreateObjectID`调用方法。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)