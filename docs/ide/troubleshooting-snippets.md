---
title: 代码片段疑难解答
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: troubleshooting
helpviewer_keywords:
- IntelliSense Code Snippets, troubleshooting
- troubleshooting IntelliSense Code Snippets
- troubleshooting Visual Basic, IntelliSense Code Snippets
ms.assetid: 7b6dd40e-2f78-4b50-8e68-41fac1bcb81e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dea93f5c575afc96af188ab2e92e2ee12b929549
ms.sourcegitcommit: 04a717340b4ab4efc82945fbb25dfe58add2ee4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="troubleshoot-snippets"></a>代码片段疑难解答

有关 IntelliSense 代码片段的问题通常由以下两个问题引起：代码片段文件损坏或代码片段文件中存在错误的内容。

## <a name="the-snippet-cannot-be-dragged-from-file-explorer-to-a-visual-studio-source-file"></a>代码片段不能从文件资源管理器拖动到 Visual Studio 源文件

-   代码片段文件中的 XML 可能已损坏。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的 XML 编辑器可找到 XML 结构中的问题。

-   代码片段文件可能不符合代码片段架构。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中的 XML 编辑器可找到 XML 结构中的问题。

## <a name="the-code-has-compiler-errors-that-are-not-highlighted"></a>代码具有未突出显示的编译器错误

-   可能缺少项目引用。 检查有关代码片段的文档。 如果在计算机上找不到引用，则需要安装该引用。 插入代码片段时应在项目中添加所需的任何引用。 如果代码片段缺少引用信息，可将此情形作为一个错误报告给代码片段创建者。

-   可能未定义变量。 代码片段中未定义的变量应突出显示。 如果未突出显示，则将此情形作为一个错误报告给代码片段创建者。

## <a name="see-also"></a>请参阅

- [代码片段](../ide/code-snippets.md)
