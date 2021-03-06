---
title: XML 架构资源管理器中的上下文菜单
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: reference
ms.assetid: 42ab17ca-b8c1-40d7-beda-d033f66fe874
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: faf28fc44acd530cbc379c4a400c3488f98405ea
ms.sourcegitcommit: d1824ab926ebbc4a8057163e0edeaf35cec57433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2018
---
# <a name="context-menus-xml-schema-explorer"></a>上下文菜单 （XML 架构资源管理器）

以下上下文菜单项用于执行特定于架构的搜索和其他操作。

## <a name="node-type-schema-set"></a>节点类型： 架构集

下表介绍了可用于架构集节点的选项。

|选项|描述|
|------------|-----------------|
|**显示最可能的根元素**|查找并突出显示并非从其他全局元素引用的所有全局元素。|
|**显示全局类型**|查找并突出显示架构集中的所有全局类型。|
|**显示全局元素**|查找并突出显示架构集中的所有全局元素。|
|**“属性”窗口**|打开**属性**窗口 （如果尚未打开）。 此窗口显示有关节点的信息。|

## <a name="node-type-namespace"></a>节点类型： Namespace
 下表介绍了可用于命名空间节点的选项。

|选项|描述|
|------------|-----------------|
|**显示所有入站的引用**|查找并突出显示导入所选命名空间的文件。|
|**显示所有出站引用**|对于所选命名空间中的每个文件，查找并突出显示下列内容：<br /><br /> 的在中引用所有命名空间导入而无需对帐单`schemaLocation`属性。<br />的中指定所选以外的命名空间中所有文件`schemaLocation`属性中导入和包含语句。|
|**显示全局类型**|查找并突出显示所选命名空间中的所有全局类型。|
|**显示全局元素**|查找并突出显示所选命名空间中的所有全局元素。|
|**“属性”窗口**|打开**属性**窗口 （如果尚未打开）。 此窗口显示有关节点的信息。|

## <a name="node-type-file"></a>节点类型： 文件
 下表介绍了可用于文件节点的选项。

|选项|描述|
|------------|-----------------|
|**显示所有入站的引用**|查找并突出显示在其包含和导入语句的 `schemaLocation` 属性中指定了所选文件的所有文件。|
|**显示所有出站引用**|查找并突出显示下列内容：<br /><br /> 的所有命名空间的所有命名空间属性中指定的导入语句而没有`schemaLocation`属性。<br />的中指定所有文件`schemaLocation`属性的所有导入和包含语句。|
|**显示全局类型**|查找并突出显示此文件中的所有全局类型。|
|**显示全局元素**|查找并突出显示此文件中的所有全局元素。|
|**查看代码**|在 XML 编辑器中打开包含所选节点的文件。 在 XML 架构资源管理器中选定的项也会在 XML 编辑器中选定。|
|**“属性”窗口**|打开**属性**窗口 （如果尚未打开）。 此窗口显示有关节点的信息。|

## <a name="all-global-node-types"></a>所有全局节点类型
 下表介绍了可用于所有全局节点的选项。

|选项|描述|
|------------|-----------------|
|**在关系图视图中显示**|打开图形视图。 如果所选节点未在工作区中，请将其添加到工作区中并将其选定。|
|**在内容模型视图中显示**|打开内容模型视图。 如果所选节点未在工作区中，请将其添加到工作区中并将其选定。|
|**查看代码**|在 XML 编辑器中打开包含所选节点的文件。 在 XML 架构资源管理器中选定的项也会在 XML 编辑器中选定。|
|**“属性”窗口**|打开**属性**窗口 （如果尚未打开）。 此窗口显示有关节点的信息。|

## <a name="node-type-element"></a>节点类型： 元素
 除了上述全局节点选项之外，元素节点的上下文菜单还拥有以下选项：

|选项|描述|
|------------|-----------------|
|**转到类型定义**|导航至所选元素的类型定义。 只有当用于元素的类型为全局类型时，此选项才适用。|
|**转到原始元素**|对于元素引用，导航至元素的实际定义。|
|**显示所有引用**|对于全局元素，查找并突出显示对所选元素的所有引用（具有 `ref="selectedElement"` 的元素）。|
|**显示替换组的成员**|对于替换组的头，查找并突出显示与所选元素同属于一个替换组的所有成员元素。 这样将显示直接和间接的参与者。|
|**显示替换组的头**|对于作为替换组成员的全局元素，查找并突出显示所选元素的所有直接和间接头，如下所示：<br /><br /> 的对所选元素指定替换组头。<br />的指定对其头元素替换组头。|
|**生成示例 XML**|仅可用于全局元素。 生成全局元素的示例 XML 文件。|

## <a name="node-type-global-types"></a>节点类型： 全局类型
 除了上述全局节点选项之外，全局类型节点的上下文菜单还拥有以下选项：

|选项|描述|
|------------|-----------------|
|**显示基类型**|如果所选类型是从全局类型派生的，则导航至所选类型的基类型。|
|**显示所有引用**|查找并突出显示对所选类型的所有引用， 其中包括所选类型和从所选类型派生的各种类型的元素和特性。|
|**显示所有派生类型**|查找并突出显示从所选类型直接和间接派生的所有类型。|
|**显示所有上级**|显示所有父（基）类型。|

## <a name="node-type-attribute"></a>节点类型： 属性
 除了上述全局节点选项之外，特性节点的上下文菜单还拥有以下选项：

|选项|描述|
|------------|-----------------|
|**转到类型定义**|如果用于属性的类型为全局类型，则导航至所选属性的类型定义。|
|**转到原始属性**|对于属性引用，导航至特性的实际定义。|
|**显示所有引用**|对于全局特性，查找并突出显示对所选特性的所有引用（具有 `ref="selectedAttribute"` 的其他特性）。|

## <a name="node-type-attribute-group"></a>节点类型： 属性组
 除了上述全局节点选项之外，特性组节点的上下文菜单还拥有以下选项：

|选项|描述|
|------------|-----------------|
|**转到定义**|对于引用，导航至属性的实际定义。|
|**显示所有成员**|查找并突出显示特性组的所有成员。|
|**显示所有引用**|查找并突出显示对所选特性组的所有引用（具有 `ref="selectedAttributeGroup"` 的特性组）。|

## <a name="node-type-named-group"></a>节点类型： 命名组
 除了上述全局节点选项之外，命名组节点的上下文菜单还拥有以下选项：

|选项|描述|
|------------|-----------------|
|**转到定义**|对于引用，导航至属性的实际定义。|
|**显示所有成员**|查找并突出显示命名组的所有成员。|
|**显示所有引用**|查找并突出显示对所选组的所有引用（具有 `ref="selectedGroup"` 的组）。|

## <a name="see-also"></a>请参阅

- [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)
- [搜索架构集](../xml-tools/searching-the-schema-set.md)