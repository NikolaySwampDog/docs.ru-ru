---
title: Типы структур — справочник по C#
ms.date: 02/24/2020
f1_keywords:
- struct_CSharpKeyword
helpviewer_keywords:
- struct keyword [C#]
- struct type [C#]
- structure type [C#]
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
ms.openlocfilehash: 6113912f176d2d7b68c77ff2e78a361b373ca31a
ms.sourcegitcommit: 44a7cd8687f227fc6db3211ccf4783dc20235e51
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/26/2020
ms.locfileid: "77634641"
---
# <a name="structure-types-c-reference"></a><span data-ttu-id="a2581-102">Типы структур (справочник по C#)</span><span class="sxs-lookup"><span data-stu-id="a2581-102">Structure types (C# reference)</span></span>

<span data-ttu-id="a2581-103">*Тип структуры*  представляет собой [тип значения](value-types.md), который может инкапсулировать данные и связанные функции.</span><span class="sxs-lookup"><span data-stu-id="a2581-103">A *structure type* (or *struct type*) is a [value type](value-types.md) that can encapsulate data and related functionality.</span></span> <span data-ttu-id="a2581-104">Для определения типа структуры используется ключевое слово `struct`:</span><span class="sxs-lookup"><span data-stu-id="a2581-104">You use the `struct` keyword to define a structure type:</span></span>

[!code-csharp[struct example](~/samples/csharp/language-reference/builtin-types/StructType.cs#StructExample)]

<span data-ttu-id="a2581-105">Типы структуры имеют *семантики значений*.</span><span class="sxs-lookup"><span data-stu-id="a2581-105">Structure types have *value semantics*.</span></span> <span data-ttu-id="a2581-106">То есть переменная типа структуры содержит экземпляр этого типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-106">That is, a variable of a structure type contains an instance of the type.</span></span> <span data-ttu-id="a2581-107">По умолчанию значения переменных копируются при назначении, передаче аргумента в метод и возврате результата метода.</span><span class="sxs-lookup"><span data-stu-id="a2581-107">By default, variable values are copied on assignment, passing an argument to a method, and returning a method result.</span></span> <span data-ttu-id="a2581-108">В случае переменной типа структуры копируется экземпляр типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-108">In the case of a structure-type variable, an instance of the type is copied.</span></span> <span data-ttu-id="a2581-109">Дополнительные сведения см. в разделе [Типы значений](value-types.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-109">For more information, see [Value types](value-types.md).</span></span>

<span data-ttu-id="a2581-110">Как правило, типы структуры используются для проектирования небольших ориентированных на данные типов, которые предоставляют минимум поведения или не предоставляют его вовсе.</span><span class="sxs-lookup"><span data-stu-id="a2581-110">Typically, you use structure types to design small data-centric types that provide little or no behavior.</span></span> <span data-ttu-id="a2581-111">Например, платформа .NET использует типы структуры для представления числа (как [целого](integral-numeric-types.md), так и [вещественного](floating-point-numeric-types.md)), [логического значения](bool.md), [символа Юникода](char.md), [экземпляра времени](xref:System.DateTime).</span><span class="sxs-lookup"><span data-stu-id="a2581-111">For example, .NET uses structure types to represent a number (both [integer](integral-numeric-types.md) and [real](floating-point-numeric-types.md)), a [Boolean value](bool.md), a [Unicode character](char.md), a [time instance](xref:System.DateTime).</span></span> <span data-ttu-id="a2581-112">Если вы сконцентрированы на поведении типа, рекомендуется определить [класс](../keywords/class.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-112">If you're focused on the behavior of a type, consider defining a [class](../keywords/class.md).</span></span> <span data-ttu-id="a2581-113">Типы классов имеют *семантики ссылок*.</span><span class="sxs-lookup"><span data-stu-id="a2581-113">Class types have *reference semantics*.</span></span> <span data-ttu-id="a2581-114">То есть переменная типа класса содержит ссылку на экземпляр этого типа, а не сам экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a2581-114">That is, a variable of a class type contains a reference to an instance of the type, not the instance itself.</span></span>

## <a name="limitations-with-the-design-of-a-structure-type"></a><span data-ttu-id="a2581-115">Ограничения при проектировании типа структуры</span><span class="sxs-lookup"><span data-stu-id="a2581-115">Limitations with the design of a structure type</span></span>

<span data-ttu-id="a2581-116">При проектировании типа структуры вы будете располагать теми же возможностями, что и для типа [класса](../keywords/class.md), за исключением следующих аспектов:</span><span class="sxs-lookup"><span data-stu-id="a2581-116">When you design a structure type, you have the same capabilities as with a [class](../keywords/class.md) type, with the following exceptions:</span></span>

- <span data-ttu-id="a2581-117">Вы не можете объявить конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="a2581-117">You cannot declare a parameterless constructor.</span></span> <span data-ttu-id="a2581-118">Каждый тип структуры уже предоставляет неявный конструктор без параметров, который создает [значение по умолчанию](default-values.md) типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-118">Every structure type already provides an implicit parameterless constructor that produces the [default value](default-values.md) of the type.</span></span>

- <span data-ttu-id="a2581-119">Вы не можете инициализировать поле экземпляра или свойство при его объявлении.</span><span class="sxs-lookup"><span data-stu-id="a2581-119">You cannot initialize an instance field or property at its declaration.</span></span> <span data-ttu-id="a2581-120">Однако можно инициализировать [статическое](../keywords/static.md) поле или поле [константы](../keywords/const.md) или статическое свойство при его объявлении.</span><span class="sxs-lookup"><span data-stu-id="a2581-120">However, you can initialize a [static](../keywords/static.md) or [const](../keywords/const.md) field or a static property at its declaration.</span></span>

- <span data-ttu-id="a2581-121">Конструктор типа структуры должен инициализировать все поля экземпляров данного типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-121">A constructor of a structure type must initialize all instance fields of the type.</span></span>

- <span data-ttu-id="a2581-122">Тип структуры не может наследовать от другого типа класса или структуры и не может быть базовым для класса.</span><span class="sxs-lookup"><span data-stu-id="a2581-122">A structure type cannot inherit from other class or structure type and it cannot be the base of a class.</span></span> <span data-ttu-id="a2581-123">Однако тип структуры может реализовывать [интерфейсы](../keywords/interface.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-123">However, a structure type can implement [interfaces](../keywords/interface.md).</span></span>

- <span data-ttu-id="a2581-124">Вы не можете объявить [метод завершения](../../programming-guide/classes-and-structs/destructors.md) в типе структуры.</span><span class="sxs-lookup"><span data-stu-id="a2581-124">You cannot declare a [finalizer](../../programming-guide/classes-and-structs/destructors.md) within a structure type.</span></span>

## <a name="instantiation-of-a-structure-type"></a><span data-ttu-id="a2581-125">Создание экземпляра типа структуры</span><span class="sxs-lookup"><span data-stu-id="a2581-125">Instantiation of a structure type</span></span>

<span data-ttu-id="a2581-126">В C# необходимо инициализировать объявленную переменную, прежде чем ее можно будет использовать.</span><span class="sxs-lookup"><span data-stu-id="a2581-126">In C#, you must initialize a declared variable before it can be used.</span></span> <span data-ttu-id="a2581-127">Так как переменная типа структуры не может быть `null` (если только это не переменная [типа значения, допускающего значение NULL](nullable-value-types.md)), необходимо создать экземпляр соответствующего типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-127">Because a structure-type variable cannot be `null` (unless it's a variable of a [nullable value type](nullable-value-types.md)), you must instantiate an instance of the corresponding type.</span></span> <span data-ttu-id="a2581-128">Для этого можно использовать несколько способов.</span><span class="sxs-lookup"><span data-stu-id="a2581-128">There are several ways to do that.</span></span>

<span data-ttu-id="a2581-129">Как правило, экземпляр типа структуры создается посредством вызова соответствующего конструктора с помощью оператора [`new`](../operators/new-operator.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-129">Typically, you instantiate a structure type by calling an appropriate constructor with the [`new`](../operators/new-operator.md) operator.</span></span> <span data-ttu-id="a2581-130">Каждый тип структуры имеет по крайней мере один конструктор.</span><span class="sxs-lookup"><span data-stu-id="a2581-130">Every structure type has at least one constructor.</span></span> <span data-ttu-id="a2581-131">Это неявный конструктор без параметров, который создает [значение по умолчанию](default-values.md) данного типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-131">That's an implicit parameterless constructor, which produces the [default value](default-values.md) of the type.</span></span> <span data-ttu-id="a2581-132">Можно использовать оператор или литерал [по умолчанию](../operators/default.md) для создания значения по умолчанию для типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-132">You can also use the [default](../operators/default.md) operator or literal to produce the default value of a type.</span></span>

<span data-ttu-id="a2581-133">Если все поля экземпляров типа структуры доступны, можно также создать его экземпляр без оператора `new`.</span><span class="sxs-lookup"><span data-stu-id="a2581-133">If all instance fields of a structure type are accessible, you can also instantiate it without the `new` operator.</span></span> <span data-ttu-id="a2581-134">В этом случае необходимо инициализировать все поля экземпляров перед первым использованием экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a2581-134">In that case you must initialize all instance fields before the first use of the instance.</span></span> <span data-ttu-id="a2581-135">Следующий пример показывает, как это сделать:</span><span class="sxs-lookup"><span data-stu-id="a2581-135">The following example shows how to do that:</span></span>

[!code-csharp[without new](~/samples/csharp/language-reference/builtin-types/StructType.cs#WithoutNew)]

<span data-ttu-id="a2581-136">В случае [встроенных типов значения](value-types.md#built-in-value-types) используйте соответствующие литералы, чтобы указать значение типа.</span><span class="sxs-lookup"><span data-stu-id="a2581-136">In the case of the [built-in value types](value-types.md#built-in-value-types), use the corresponding literals to specify a value of the type.</span></span>

## <a name="passing-structure-type-variables-by-reference"></a><span data-ttu-id="a2581-137">Передача переменных типа структуры по ссылке</span><span class="sxs-lookup"><span data-stu-id="a2581-137">Passing structure-type variables by reference</span></span>

<span data-ttu-id="a2581-138">При передаче переменной типа структуры в метод в качестве аргумента или возврате значения типа структуры из метода копируется весь экземпляр типа структуры.</span><span class="sxs-lookup"><span data-stu-id="a2581-138">When you pass a structure-type variable to a method as an argument or return a structure-type value from a method, the whole instance of a structure type is copied.</span></span> <span data-ttu-id="a2581-139">Это может повлиять на производительность кода в высокопроизводительных сценариях, где используются большие типы структуры.</span><span class="sxs-lookup"><span data-stu-id="a2581-139">That can affect the performance of your code in high-performance scenarios that involve large structure types.</span></span> <span data-ttu-id="a2581-140">Копирования значений можно избежать, передав переменную типа структуры по ссылке.</span><span class="sxs-lookup"><span data-stu-id="a2581-140">You can avoid value copying by passing a structure-type variable by reference.</span></span> <span data-ttu-id="a2581-141">Используйте модификаторы параметра метода [`ref`](../keywords/ref.md#passing-an-argument-by-reference), [`out`](../keywords/out-parameter-modifier.md) или [`in`](../keywords/in-parameter-modifier.md), чтобы указать, что аргумент должен передаваться по ссылке.</span><span class="sxs-lookup"><span data-stu-id="a2581-141">Use the [`ref`](../keywords/ref.md#passing-an-argument-by-reference), [`out`](../keywords/out-parameter-modifier.md), or [`in`](../keywords/in-parameter-modifier.md) method parameter modifiers to indicate that an argument must be passed by reference.</span></span> <span data-ttu-id="a2581-142">Чтобы возвратить результат метода по ссылке, используйте [ref returns](../../programming-guide/classes-and-structs/ref-returns.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-142">Use [ref returns](../../programming-guide/classes-and-structs/ref-returns.md) to return a method result by reference.</span></span> <span data-ttu-id="a2581-143">Дополнительные сведения см. в статье [Написание безопасного и эффективного кода C#](../../write-safe-efficient-code.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-143">For more information, see [Write safe and efficient C# code](../../write-safe-efficient-code.md).</span></span>

## <a name="conversions"></a><span data-ttu-id="a2581-144">Преобразования</span><span class="sxs-lookup"><span data-stu-id="a2581-144">Conversions</span></span>

<span data-ttu-id="a2581-145">Для любого типа структуры существует [упаковка-преобразование и распаковка-преобразование](../../programming-guide/types/boxing-and-unboxing.md) в типы <xref:System.ValueType?displayProperty=nameWithType> и <xref:System.Object?displayProperty=nameWithType> и из них.</span><span class="sxs-lookup"><span data-stu-id="a2581-145">For any structure type, there exist [boxing and unboxing](../../programming-guide/types/boxing-and-unboxing.md) conversions to and from the <xref:System.ValueType?displayProperty=nameWithType> and <xref:System.Object?displayProperty=nameWithType> types.</span></span> <span data-ttu-id="a2581-146">Существуют упаковка-преобразование и распаковка-преобразование между типом структуры и любым интерфейсом, который он реализует.</span><span class="sxs-lookup"><span data-stu-id="a2581-146">There exist also boxing and unboxing conversions between a structure type and any interface that it implements.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="a2581-147">Спецификация языка C#</span><span class="sxs-lookup"><span data-stu-id="a2581-147">C# language specification</span></span>

<span data-ttu-id="a2581-148">Дополнительные сведения см. в разделе [Структуры](~/_csharplang/spec/structs.md) в [спецификации языка C#](~/_csharplang/spec/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2581-148">For more information, see the [Structs](~/_csharplang/spec/structs.md) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a2581-149">См. также</span><span class="sxs-lookup"><span data-stu-id="a2581-149">See also</span></span>

- [<span data-ttu-id="a2581-150">справочник по C#</span><span class="sxs-lookup"><span data-stu-id="a2581-150">C# reference</span></span>](../index.md)
- [<span data-ttu-id="a2581-151">Рекомендации по проектированию — выбор между классом и структурой</span><span class="sxs-lookup"><span data-stu-id="a2581-151">Design guidelines - Choosing between class and struct</span></span>](../../../standard/design-guidelines/choosing-between-class-and-struct.md)
- [<span data-ttu-id="a2581-152">Рекомендации по проектированию — проектирование структуры</span><span class="sxs-lookup"><span data-stu-id="a2581-152">Design guidelines - Struct design</span></span>](../../../standard/design-guidelines/struct.md)
- [<span data-ttu-id="a2581-153">Классы и структуры</span><span class="sxs-lookup"><span data-stu-id="a2581-153">Classes and structs</span></span>](../../programming-guide/classes-and-structs/index.md)