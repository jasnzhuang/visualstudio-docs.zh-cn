---
title: "JsGetUndefinedValue 函数 | Microsoft Docs"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- jsrt/JsGetUndefinedValue
helpviewer_keywords:
- JsGetUndefinedValue function
ms.assetid: e118eaf6-452c-42f2-86b8-e63c7d987cba
caps.latest.revision: 
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3c1788f7edeeb6df1ccf7eb3b6918322a65f2db8
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2017
---
# <a name="jsgetundefinedvalue-function"></a>JsGetUndefinedValue 函数
获取当前脚本上下文中的 `undefined` 值。  
  
## <a name="syntax"></a>语法  
  
```  
STDAPI_(JsErrorCode) JsGetUndefinedValue(  
   _Out_ JsValueRef *undefinedValue  
);  
```  
  
#### <a name="parameters"></a>参数  
 `undefinedValue`  
 `undefined` 值。  
  
## <a name="return-value"></a>返回值  
 如果该操作成功，则为代码 `JsNoError` ，否则为失败代码。  
  
## <a name="remarks"></a>备注  
 需要活动脚本上下文。  
  
## <a name="requirements"></a>要求  
 **标头：** jsrt.h  
  
## <a name="see-also"></a>另请参阅  
 [引用（JavaScript 运行时）](../chakra-hosting/reference-javascript-runtime.md)