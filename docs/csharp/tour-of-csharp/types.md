---
title: 定义类型及其成员 - C# 教程
description: 类型是程序的基石。学习如何在 C# 中创建类、结构体、接口等等。
ms.date: 08/06/2020
---
# 类型和成员

## 类与对象

*类*是 C# 当中最基础的类型之一。所谓类是指将状态（字段）和行为（方法以及其他函数成员）结合在一个单元当中的一种数据结构。类为类的*实例*提供了定义，后者也称*对象*。类支持*继承*与*多态*，通过这些机制*派生类*可以扩展并特化*基类*。

我们通过类的声明来创造新的类。类的声明从头部开始，该头部指明了：

- 类的特性和修饰符
- 类名
- 基类（若继承自一个[基类](#base-classes)的话） 
- 其所实现的接口

紧接着头部的是类的主体部分，其中包含了一系列成员声明，用分隔符 `{` 与 `}` 括起。

下面的代码展示了如何声明一个简单的，名为 `Point` 的类：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="PointClass":::

使用 `new` 运算符，我们可以创建类的实例，它会为新的实例申请内存空间，调用构造函数来初始化实例，并返回指向实例的引用。下列语句创建了两个 `Point` 对象并将其引用存放在了两个变量当中：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="CreatePoints":::

对象不再被用到时，其所占据的空间会自动收回。在 C# 当中显式地释放对象既不必要也不可能。

### 类型参数

泛型类定义了[***类型参数***](../programming-guide/generics/index.md)。类型参数列表用尖括号括起，其中依次书写类型参数的名称。类型参数紧随于类名之后。此后可在类声明主题里使用这些类型参数来定义类的成员。下面的例子里，`Pair` 的类型参数分别是 `TFirst` 和 `TSecond`：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="DefinePairClass":::

声明中要求类型参数的类类型称为*泛型类类型*。结构体、接口和委托类型也可以是泛型的。
使用泛型类的时候，必须为每个类型形参给定类型实参。

:::code language="csharp" source="./snippets/shared/Types.cs" ID="CreatePairObject":::

像上面这种已经给定了类型实参的泛型类型称为*构造类型*。

### 基类

类的声明当中或许会指明基类。基类的名称跟随在类名和类型参数以后，并用冒号隔开。若是省略了继承自什么基类，则默认等同于继承了 `object` 类型。下面的例子里，`Point3D` 的基类是 `Point`。而在开头的第一个例子里，`Point` 的基类则是 `object`：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="Create3DPoint":::

类会继承其基类的成员。所谓继承意味着类会隐式地包含其基类的几乎所有成员。类并不会继承基类的实例、静态构造函数或是析构函数。派生类可以其所继承成员基础上增加成员，但并不能移除其所继承成员的定义。在前面的例子里，`Point3D` 从 `Point` 处继承了成员 `X` 和 `Y`，于是每个 `Point3D` 的示例均包含这三个属性，`X`、`Y`、`Z`。

从一种类类型到其任一基类类型之间都存在着隐式类型转换。一个类类型的变量可以引用本类的实例，也同样可以引用任一派生类的实例。比方说，在之前类声明的基础上，一个 `Point` 类型的变量既可以引用一个 `Point` 也可以引用一个 `Point3D` 对象：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="ImplicitCastToBase":::

## 结构（struct）

用类我们可以定义支持继承和多态的类型。它可以帮助你用一层一层的派生类来构建精细的行为。相比之下，[***结构类型***](../language-reference/builtin-types/struct.md) 则是更简单的类型，其基本目的就是为了存储数据值。结构类型无法声明基类型；它们隐式地继承了 <xref:System.ValueType?displayProperty=nameWithType>。你也不能从 `struct` 类型派生出其他的 `struct` 类型。它们是隐式密封的：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="PointStruct":::

## 接口

[***接口***](../programming-guide/interfaces/index.md) 定义了一种可以由类与结构所实现的约定。接口可以包含方法、属性、事件和索引器。接口通常并不提供其所定义成员的实现——它仅仅是指明了类或结构必须提供的成员，以此来实现接口。

接口可能使用***多重继承***。下面的例子里，`IComboBox` 接口既继承了 `ITextBox` 也继承了 `IListBox`。

:::code language="csharp" source="./snippets/shared/Types.cs" ID="FirstInterfaces":::

类和结构可以实现多个接口。下面的例子里，类 `EditBox` 同时实现了 `IControl` 和 `IDataBound` 两个接口。

:::code language="csharp" source="./snippets/shared/Types.cs" ID="ImplementInterfaces":::

若一个类或结构实现了一个接口，则其实例可以隐式转换为该接口类型，例如：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="UseInterfaces":::

## 枚举（enum）

[***枚举***](../language-reference/builtin-types/enum.md) 类型定义了一系列常量值。下面的 `enum` 声明了一些常量，它们定义了不同的块根类蔬菜：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="EnumDeclaration":::

你也可以定义可以相互结合使用的 `enum`，每个成员代表一个标志位。下面声明了四季作为标志位的集合。可以任意结合其中的几个季节，包括其中的 `All` 值，它包含了全部季节。

:::code language="csharp" source="./snippets/shared/Types.cs" ID="FlagsEnumDeclaration":::

下面的例子展示了前面两个枚举的声明：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="UsingEnums":::

## 可空类型

任意类型的变量都可声明为***不可空***或***可空***两种情况。可空变量除一般值以外还可存储 `null` 值，代表没有值。可空的值类型（结构或是枚举）是由 <xref:System.Nullable%601?displayProperty=nameWithType> 所代表的，而无论可空还是不可空的引用类型均是由其实际的引用类型所代表的。这种区别通过编译器或库所读取到的元数据表现出来。对可空引用解引用前，若不检查其值是否为 `null`，则编译器会发出警告。同样地，尝试将可能为空的值赋给不可空的引用时也会导致编译器发出警告。下面的例子声明了一个***可空的 int*** 变量，并把它初始化为了 `null`，接着将其值设定为了 `5`。它展示了与***可空字符串***相同的概念。要获取更多信息，请看[可空值类型]。

:::code language="csharp" source="./snippets/shared/Types.cs" ID="DeclareNullable":::

## Tuples

C# 支持 [***元组***](../language-reference/builtin-types/value-tuples.md)，可以用简洁的语法将多个数据元素包括在一个轻量级的数据结构中。可以通过在 `(` 和 `)` 之间声明成员的类型和名称来实例化元组，例如：

:::code language="csharp" source="./snippets/shared/Types.cs" ID="DeclareTuples":::

在不使用下一章所介绍的程序构建基块的前提下，若要创建具有多个成员的数据结构，元组可作为一个替代方案。

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](program-building-blocks.md)
