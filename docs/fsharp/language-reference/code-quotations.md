---
title: 代码引用
description: '了解 F # 代码引用，它是一种语言功能，可用于以编程方式生成和使用 F # 代码表达式。'
ms.date: 05/16/2016
ms.openlocfilehash: bb5c03edd180c42667731bb90d7a1f624ed2e522
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855385"
---
# <a name="code-quotations"></a>代码引用

本文介绍*代码引用*，它是一种语言功能，可用于以编程方式生成和使用 F # 代码表达式。 利用此功能，您可以生成一个表示 F # 代码的抽象语法树。 然后，可以根据应用程序的需要遍历和处理抽象语法树。 例如，您可以使用树生成 F # 代码或以某种其他语言生成代码。

> [!NOTE]
> F # 的 docs.microsoft.com API 参考未完成。 如果遇到任何断开的链接，请参阅[F # 核心库文档](https://fsharp.github.io/fsharp-core-docs/)。

## <a name="quoted-expressions"></a>带引号的表达式

*带引号的表达式*是代码中的 F # 表达式，它以不作为程序的一部分进行编译，而是编译为表示 F # 表达式的对象。 可以通过以下两种方式之一来标记带引号的表达式：使用类型信息或不包含类型信息。 如果要包括类型信息，请使用符号 `<@` 并 `@>` 分隔带引号的表达式。 如果不需要类型信息，则使用符号 `<@@` 和 `@@>` 。 下面的代码显示类型化和非类型化的引用。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet501.fs)]

如果不包含类型信息，遍历大型表达式树的速度将更快。 使用类型化符号括起来的表达式的结果类型为 `Expr<'T>` ，其中类型参数具有由 F # 编译器的类型推理算法确定的表达式的类型。 使用不带类型信息的代码引用时，带引号的表达式的类型为非泛型类型[Expr](https://msdn.microsoft.com/library/ed6a2caf-69d4-45c2-ab97-e9b3be9bce65)。 可以调用类型化类的[原始](https://msdn.microsoft.com/library/47fb94f1-e77f-4c68-aabc-2b0ba40d59c2)属性 `Expr` 来获取非类型化 `Expr` 对象。

有多种静态方法可让你以编程方式在类中生成 F # 表达式对象， `Expr` 而无需使用带引号的表达式。

请注意，代码引号必须包含完整的表达式。 `let`例如，对于绑定，需要绑定名称和使用绑定的其他表达式的定义。 在详细语法中，这是跟在关键字后面的表达式 `in` 。 在模块的顶层，这只是模块中的下一个表达式，但在引号中，它是显式必需的。

因此，下面的表达式无效。

```fsharp
// Not valid:
// <@ let f x = x + 1 @>
```

但下面的表达式是有效的。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet502.fs)]

若要计算 F # 引号，必须使用[f # 引号计算](https://github.com/fsprojects/FSharp.Quotations.Evaluator)器。 它提供对计算和执行 F # 表达式对象的支持。

## <a name="expr-type"></a>Expr 类型

类型的实例 `Expr` 表示 F # 表达式。 `Expr`F # 库文档中记录了泛型和非泛型类型。 有关详细信息，请参阅[Fsharp.core 命名空间](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.quotations-namespace-%5bfsharp%5d)和[引号。](https://msdn.microsoft.com/visualfsharpdocs/conceptual/quotations.expr-class-%5bfsharp%5d)

## <a name="splicing-operators"></a>拼接运算符

拼接使你能够将文本代码引用与你以编程方式或从其他代码引用创建的表达式组合在一起。 使用 `%` 和 `%%` 运算符可以将 F # 表达式对象添加到代码引用中。 使用运算符将 `%` 类型化表达式对象插入类型化的引用中; 使用 `%%` 运算符将非类型化的表达式对象插入非类型化的引用。 这两个运算符均为一元前缀运算符。 因此 `expr` ，如果是类型的非类型化表达式 `Expr` ，以下代码是有效的。

```fsharp
<@@ 1 + %%expr @@>
```

如果 `expr` 是类型的类型化的引号 `Expr<int>` ，则以下代码有效。

```fsharp
<@ 1 + %expr @>
```

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示如何使用代码引用将 F # 代码放入 expression 对象，然后打印表示该表达式的 F # 代码。 定义了一个函数， `println` 该函数包含一个递归函数 `print` ，该函数 `Expr` 以友好格式显示类型)  (的 F # 表达式对象。 可以使用[fsharp.core](https://msdn.microsoft.com/library/093944a9-c752-403a-8983-5fcd5dbf92a4)和[DerivedPatterns](https://msdn.microsoft.com/library/d2434a6e-ae7b-4f3d-b567-c162938bc9cd)模块中的几个活动模式来分析表达式对象，这种模式可用于分析表达式对象。 此示例不包括可能出现在 F # 表达式中的所有可能的模式。 任何无法识别的模式都会触发与通配符模式的匹配 (`_`) 并使用方法呈现，该 `ToString` 方法在类型上， `Expr` 使你知道要添加到匹配表达式的活动模式。

### <a name="code"></a>代码

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet601.fs)]

### <a name="output"></a>Output

```fsharp
fun (x:System.Int32) -> x + 1
a + 1
let f = fun (x:System.Int32) -> x + 10 in f 10
```

## <a name="example"></a>示例

### <a name="description"></a>描述

您还可以使用[exprshape.rebuildshapecombination 模块](https://msdn.microsoft.com/library/7685150e-2432-4d39-9338-57292eff18de)中的三个活动模式来遍历具有较少活动模式的表达式树。 当你希望遍历树但你不需要大多数节点中的所有信息时，这些活动模式会很有用。 当使用这些模式时，任何 F # 表达式都将与以下三种模式之一匹配： `ShapeVar` 如果表达式是变量，则为; 如果表达式 `ShapeLambda` 是 lambda 表达式，则为; 如果 `ShapeCombination` 表达式为其他任何内容，则为。 如果使用活动模式遍历表达式树，如前面的代码示例所示，您必须使用更多的模式来处理所有可能的 F # 表达式类型，并且您的代码将更复杂。 有关详细信息，请参阅[exprshape.rebuildshapecombination. ShapeVar&#124;ShapeLambda&#124;ShapeCombination Active Pattern](https://msdn.microsoft.com/visualfsharpdocs/conceptual/exprshape.shapevarhshapelambdahshapecombination-active-pattern-%5bfsharp%5d)。

下面的代码示例可用作更复杂的遍历的基础。 在此代码中，将为包含函数调用的表达式创建表达式树 `add` 。 [SpecificCall](https://msdn.microsoft.com/library/05a77b21-20fe-4b9a-8e07-aa999538198d)活动模式用于检测对 `add` 表达式树中的任何调用。 此活动模式将调用的参数分配给 `exprList` 值。 在这种情况下，只有两个，因此会将其拉出，并以递归方式对参数调用函数。 `mul`通过使用接合运算符 () ，将结果插入到表示对的调用 `%%` 。 `println`上一示例中的函数用于显示结果。

其他活动模式分支中的代码只是重新生成相同的表达式树，因此，结果表达式中的唯一更改是从到的更改 `add` `mul` 。

### <a name="code"></a>代码

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-3/snippet701.fs)]

### <a name="output"></a>Output

```fsharp
1 + Module1.add(2,Module1.add(3,4))
1 + Module1.mul(2,Module1.mul(3,4))
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
