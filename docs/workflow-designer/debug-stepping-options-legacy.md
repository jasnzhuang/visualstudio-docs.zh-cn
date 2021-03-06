---
title: 工作流设计器-调试单步执行选项 （旧版）
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
helpviewer_keywords:
- branch stepping
- stepping, options in workflow debugging
- debugging, stepping options
- debugging workflows, stepping options
- instance stepping
ms.assetid: 3e9e3041-68c7-4f16-9bd6-da5e5144744b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f46c0ab382a0e189c595e6e0f8aeb69c71814faf
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="debug-stepping-options-legacy"></a>调试单步执行选项（旧版）

本主题介绍如何调试具有并发活动旧的 Windows 工作流设计器中的 Windows Workflow Foundation (WF) 应用程序。 当你需要以面向.NET Framework 版本 3.5 或 WinFX 时，请使用旧工作流设计器。

在调试具有并发执行，如的旧活动**ParallelActivity**或**ConditionedActivityGroup**，可以使用以下两个选项之一来逐句通过代码.

-   **分支单步执行。** 使用此单步执行模式可以逐句通过和调试复合活动的特定分支，例如**ParallelActivity**或**ConditionalActivityGroup**活动。 如果使用此选项进行调试，则看不到由于工作流中并发执行其他活动而导致的控件变化。 调试器只逐句通过当前选定分支中的活动，而工作流中的其他活动可以并发执行。 例如，默认情况下，在最左边的分支**ParallelActivity**活动和的第一个子活动**ConditionedActivityGroup**活动用于单步执行。 如果用户要调试任何其他分支或子活动，则必须在分支或子活动上放置显式断点。 触发断点时，在该分支中继续单步执行。

-   **实例单步执行。** 使用此单步执行模式可以在工作流中逐句通过和调试并发执行的活动。 使用此选项，可以看到在工作流中运行并发执行活动时控件发生的变化。

默认情况下会选择分支单步执行选项，用户在调试旧工作流时可以在这两个选项之间切换。

在调试旧状态机工作流时，应选择实例单步执行选项。

## <a name="see-also"></a>请参阅

- [调试旧版工作流](../workflow-designer/debugging-legacy-workflows.md)
- [如何：更改调试单步执行选项（旧版）](../workflow-designer/how-to-change-the-debug-stepping-option-legacy.md)