---
title: 导入声明：open 关键字
description: '了解 F # 导入声明以及如何指定可在不使用完全限定名称的情况下引用其元素的模块或命名空间。'
ms.date: 04/04/2019
ms.openlocfilehash: 2b88427ca92212fb4a7598447dd1a5e12061093a
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855083"
---
# <a name="import-declarations-the-open-keyword"></a>导入声明： `open` 关键字

*导入声明*指定了一个模块或命名空间，在不使用完全限定名称的情况下，可以引用这些元素。

## <a name="syntax"></a>语法

```fsharp
open module-or-namespace-name
```

## <a name="remarks"></a>备注

> [!NOTE]
> F # 的 docs.microsoft.com API 参考未完成。 如果遇到任何断开的链接，请参阅[F # 核心库文档](https://fsharp.github.io/fsharp-core-docs/)。

每次使用完全限定的命名空间或模块路径引用代码都可以创建难以编写、读取和维护的代码。 相反，可以将关键字用于 `open` 经常使用的模块和命名空间，以便在引用该模块或命名空间的成员时，可以使用名称的缩写，而不是完全限定的名称。 此关键字类似于 `using` c # 中的关键字、 `using namespace` Visual C++ 和 `Imports` Visual Basic 中的关键字。

提供的模块或命名空间必须位于同一项目或引用的项目或程序集中。 如果不是，则可以添加对项目的引用，或者使用 `-reference` 命令行选项 (或其缩写 `-r`) 。 有关详细信息，请参阅[编译器选项](compiler-options.md)。

导入声明会使名称位于声明后的代码中，直到封闭命名空间、模块或文件的结尾。

当使用多个导入声明时，它们应该出现在单独的行上。

下面的代码演示 `open` 如何使用关键字来简化代码。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

如果在多个打开的模块或命名空间中出现多义性，则 F # 编译器不会发出错误或警告。 出现歧义时，F # 为最近打开的模块或命名空间赋予首选项。 例如，在下面的代码中， `empty` `Seq.empty` 是指，即使 `empty` 同时位于 `List` 和模块中 `Seq` 。

```fsharp
open List
open Seq
printfn "%A" empty
```

因此，当您打开包含具有相同名称的成员的模块或命名空间（如或）时，请务必小心 `List` `Seq` ; 相反，请考虑使用限定名。 应避免代码依赖于导入声明顺序的任何情况。

## <a name="namespaces-that-are-open-by-default"></a>默认情况下打开的命名空间

一些命名空间非常频繁地在 F # 代码中使用，而无需显式导入声明即可隐式打开它们。 下表显示了默认情况下处于打开状态的命名空间。

|命名空间|说明|
|---------|-----------|
|`Microsoft.FSharp.Core`|包含内置类型（例如和）的基本 F # 类型定义 `int` `float` 。|
|`Microsoft.FSharp.Core.Operators`|包含基本算术运算，例如 `+` 和 `*` 。|
|`Microsoft.FSharp.Collections`|包含不可变的集合类 `List` ，如和 `Array` 。|
|`Microsoft.FSharp.Control`|包含控件构造的类型，例如迟缓计算和异步工作流。|
|`Microsoft.FSharp.Text`|包含格式化 IO 的函数，例如 `printf` 函数。|

## <a name="autoopen-attribute"></a>AutoOpen 特性

`AutoOpen`如果要在引用程序集时自动打开命名空间或模块，则可以将该特性应用于程序集。 您还可以将属性应用于 `AutoOpen` 模块，以便在打开父模块或命名空间时自动打开该模块。 有关详细信息，请参阅[AutoOpenAttribute 类](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.autoopenattribute-class-%5bfsharp%5d)。

## <a name="requirequalifiedaccess-attribute"></a>RequireQualifiedAccess 特性

某些模块、记录或联合类型可以指定 `RequireQualifiedAccess` 属性。 引用这些模块、记录或联合的元素时，必须使用限定名称，而不管是否包含导入声明。 如果在定义常用名称的类型上策略性地使用此属性，则有助于避免名称冲突，从而使代码更能更灵活地应对库中的更改。 有关详细信息，请参阅[RequireQualifiedAccessAttribute 类](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.requirequalifiedaccessattribute-class-%5Bfsharp%5D)。

## <a name="see-also"></a>另请参阅

- [F# 语言参考](index.md)
- [命名空间](namespaces.md)
- [模块](modules.md)
