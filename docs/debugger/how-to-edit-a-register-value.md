---
title: "如何：编辑寄存器值 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.register.edit"
dev_langs: 
  - "FSharp"
  - "VB"
  - "CSharp"
  - "C++"
  - "JScript"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "注册值"
  - "“寄存器”窗口, 编辑寄存器值"
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
caps.latest.revision: 24
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 24
---
# 如何：编辑寄存器值
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

只有在**“选项”**对话框中的**“调试”**节点下启用了地址级调试后，“寄存器”窗口才可用。  
  
### 更改寄存器值  
  
1.  在**“寄存器”**窗口中，使用 Tab 键或鼠标可以将插入点移到要更改的值的位置。  在开始键入之前，光标必须位于要覆盖的值之前。  
  
2.  键入新值。  
  
    > [!CAUTION]
    >  更改寄存器值（特别是 EIP 和 EBP 寄存器中的值）可能会影响程序的执行。  
  
    > [!CAUTION]
    >  编辑浮点值时，由于要将小数部分从十进制转换为二进制，因此所得的结果可能存在微小误差。  甚至看起来无关紧要的编辑都能引起浮点变量中某些最不重要的数据位发生变化。  
  
## 请参阅  
 [如何：使用“寄存器”窗口](../debugger/how-to-use-the-registers-window.md)