---
description: Справочник по C#. Ключевое слово ref
title: Справочник по C#. Ключевое слово ref
ms.date: 03/29/2021
f1_keywords:
- ref_CSharpKeyword
helpviewer_keywords:
- parameters [C#], ref
- ref keyword [C#]
ms.openlocfilehash: 3392e560eaf0bac39cf4e9707574fd2bb3d96057
ms.sourcegitcommit: 109507b6c16704ed041efe9598c70cd3438a9fbc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/31/2021
ms.locfileid: "106079444"
---
# <a name="ref-c-reference"></a>ref (Справочник по C#)

Ключевое слово `ref` указывает, что значение передается по ссылке. Оно используется в четырех разных контекстах:

- В сигнатуре и вызове метода для передачи аргумента в метод по ссылке. Дополнительные сведения см. в статье о [передаче аргументов по ссылке](#passing-an-argument-by-reference).
- В сигнатуре метода для возврата значения вызывающему объекту по ссылке. Дополнительные сведения см. в разделе [Значения, возвращаемые по ссылке](#reference-return-values).
- В теле элемента для указания на то, что возвращаемые ссылочные значения хранятся локально в виде ссылки, которая может быть изменена вызывающим объектом. Или чтобы указать, что локальная переменная обращается к другому значению по ссылке. Дополнительные сведения см. в статье о [ссылочных локальных переменных](#ref-locals).
- В объявлении `struct`, чтобы объявить `ref struct` или `readonly ref struct`. Дополнительные сведения см. в описании [структуры `ref`](../builtin-types/struct.md#ref-struct) в статье [Типы структур](../builtin-types/struct.md).

## <a name="passing-an-argument-by-reference"></a>Передача аргументов по ссылке

При использовании в списке параметров метода ключевое слово `ref` указывает на то, что аргумент передается по ссылке, а не по значению. Ключевое слово `ref` позволяет превратить этот формальный параметр в псевдоним для аргумента, который должен представлять собой переменную. Другими словами, любая операция в параметре осуществляется с аргументом.

Для примера предположим, что вызывающая сторона передает выражение локальной переменной или выражение доступа к элементу массива. Тогда вызываемый метод может заменить объект, на который ссылается параметр ref. В этом случае или элемент массива или локальная переменная вызывающей стороны будет ссылаться на новый объект, когда метод возвращает значение.

> [!NOTE]
> Не путайте понятие передачи по ссылке с понятием ссылочных типов. Эти два понятия не совпадают. Параметр метода может быть изменен с помощью `ref` независимо от того, принадлежит ли он к типу значения или ссылочному типу. При передаче по ссылке упаковка-преобразование типа значения не производится.  

Для использования параметра `ref` и при определении метода, и при вызове метода следует явно использовать ключевое слово `ref`, как показано в следующем примере. (За исключением того, что вызывающий метод может опускать `ref` при вызове COM.)

[!code-csharp-interactive[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#1)]

Аргумент, передаваемый в параметр `ref` или `in`, нужно инициализировать перед передачей. В этом и заключается отличие от параметров [out](out-parameter-modifier.md), аргументы которых не нужно явно инициализировать перед передачей.

Члены класса не могут иметь сигнатуры, отличающихся только `ref`, `in` или `out`. Если единственное различие между двумя членами типа состоит в том, что один из них имеет параметр `ref`, а второй — параметр `out` или `in`, возникает ошибка компилятора. Например, следующий код не будет компилироваться.  

```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```

Но методы можно перегружать, если один метод имеет параметр `ref`, `in` или `out`, а другой — передаваемый по значению параметр, как показано в приведенном ниже примере.
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#2)]
  
 В других ситуациях, требующих соответствия сигнатур, таких как скрытие или переопределение, `in`, `ref` и `out` являются частью сигнатуры и не соответствуют друг другу.  
  
 Свойства не являются переменными. Они являются методами и не могут передаваться в параметры `ref`.  
  
 Ключевые слова `ref`, `in` и `out` запрещено использовать для следующих типов методов.  
  
- Асинхронные методы, которые определяются с помощью модификатора [async](async.md).  
- Методы итератора, которые включают оператор [yield return](yield.md) или `yield break`.

[Методы расширения](../../programming-guide/classes-and-structs/extension-methods.md) также имеют ряд ограничений при использовании этих ключевых слов:

- Ключевое слово `out` нельзя использовать в первом аргументе метода расширения.
- Ключевое слово `ref` нельзя использовать в первом аргументе метода расширения, если аргумент не является структурой, или если универсальный тип не ограничен структурой.
- Ключевое слово `in` нельзя использовать, если только первый аргумент не является структурой. Ключевое слово `in` нельзя использовать ни для одного универсального типа, даже если оно ограничено структурой.

## <a name="passing-an-argument-by-reference-an-example"></a>Передача аргументов по ссылке. Пример

В предыдущих примерах типы значений передаются по ссылке. Также можно использовать ключевое слово `ref` для передачи ссылочных типов по ссылке. Передача ссылочного типа по ссылке позволяет вызываемому методу заменять объект, на который указывает ссылочный параметр в вызывающем объекте. Место хранения объекта передается методу в качестве значения ссылочного параметра. Если изменить место хранения параметра (с указанием на новый объект), необходимо изменить место хранения, на который ссылается вызывающий объект. В следующем примере экземпляр ссылочного типа передается как параметр `ref`.
  
[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#3)]

Дополнительные сведения о передаче ссылочных типов по значению и по ссылке см. в разделе [Передача параметров ссылочного типа](../../programming-guide/classes-and-structs/passing-reference-type-parameters.md).
  
## <a name="reference-return-values"></a>Возвращаемые ссылочные значения

Возвращаемые ссылочные значения — это значения, которые метод возвращает вызывающему объекту по ссылке. Это значит, что вызывающий объект может изменять значение, возвращаемое методом, и это изменение будет отражаться в состоянии объекта в вызывающем методе.

Возвращаемое ссылочное значение определяется с помощью ключевого слова `ref`:

- В сигнатуре метода. Например, следующая сигнатура указывает, что метод `GetCurrentPrice` возвращает значение <xref:System.Decimal> по ссылке.

```csharp
public ref decimal GetCurrentPrice()
```

- Между токеном `return` и переменной, возвращенной в инструкции `return` в методе. Пример:

```csharp
return ref DecimalArray[0];
```

Чтобы вызывающий объект имел возможность изменять состояние объекта, возвращаемое ссылочное значение должно храниться в переменной, которая явно определена как [ссылочная локальная переменная](#ref-locals).

Ниже приведен более полный пример возвращаемого ссылочного значения, в котором показаны сигнатура и тело метода.

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

Вызываемый метод может также объявить возвращаемое значение `ref readonly`, чтобы вернуть значение по ссылке, и запретить вызывающему коду изменять возвращаемое значение. Вызывающий метод может обойтись без копирования возвращаемого значения, сохраняя его в локальной переменной [ref readonly](#ref-readonly-locals).

Пример см. в разделе [Пример использования возвращаемых ссылочных значений и ссылочных локальных переменных](#a-ref-returns-and-ref-locals-example).

## <a name="ref-locals"></a>Ссылочные локальные переменные

Ссылочная локальная переменная задает ссылку на значения, возвращаемые с помощью `return ref`. Ссылочная локальная переменная не может инициализироваться как не ссылочное возвращаемое значение. Другими словами, правая часть инициализации должна быть ссылкой. Любые изменения в значении ссылочной локальной переменной отражаются в состоянии объекта, метод которого возвращает значение по ссылке.

Чтобы определить локальное ссылочное значение, ключевое слово `ref` следует указать в двух местах:

- перед объявлением переменной;
- сразу после вызова метода, который возвращает значение по ссылке.

Например, следующая инструкция определяет значение ссылочной локальной переменной, которое возвращается методом `GetEstimatedValue`:

```csharp
ref decimal estValue = ref Building.GetEstimatedValue();
```

Вы можете таким же образом обратиться к значению по ссылке. В некоторых случаях обращение к значению по ссылке повышает производительность, поскольку позволяет избежать потенциально затратной операции копирования. Например, следующая инструкция позволяет определить локальную ссылочную переменную, которая используется для создания ссылки на значение.

```csharp
ref VeryLargeStruct reflocal = ref veryLargeStruct;
```

В обоих примерах ключевое слово `ref` необходимо использовать в обоих местах. В противном случае возникает ошибка компилятора CS8172, "Невозможно инициализировать значением переменную по ссылке".

Начиная с версии C# 7.3, переменная итерации в операторе `foreach` может являться локальной ссылочной переменной или локальной ссылочной переменной только для чтения. Дополнительные сведения см. в статье, посвященной [инструкции foreach](foreach-in.md).

Также, начиная с версии C# 7.3, вы можете переназначать ссылочную локальную переменную или ссылочную локальную переменную только для чтения с помощью [ссылочного оператора присваивания](../operators/assignment-operator.md#ref-assignment-operator).

## <a name="ref-readonly-locals"></a>Ссылочные локальные переменные только для чтения

Ссылочная локальная переменная только для чтения позволяет создать ссылку на значения, возвращаемые методом или свойством, которые имеют в сигнатуре модификатор `ref readonly` и используют `return ref`. Переменная `ref readonly` сочетает свойства локальной переменной `ref` и переменной `readonly`. Это псевдоним для хранилища, которому она присвоена, который не может изменять свое значение.

## <a name="a-ref-returns-and-ref-locals-example"></a>Пример использования возвращаемых ссылочных значений и ссылочных локальных переменных

В следующем примере определяется класс `Book`, содержащий два поля <xref:System.String>: `Title` и `Author`. Также определяется класс `BookCollection`, который включает частный массив объектов `Book`. Отдельные объекты книг возвращаются по ссылке путем вызова метода `GetBookByTitle`.

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#4)]

Если вызывающий объект сохраняет значение, возвращаемое методом `GetBookByTitle`, в качестве ссылочной локальной переменной, изменения, которые этот объект вносит в возвращаемое значение, отражаются в объекте `BookCollection`, как показано в следующем примере.

[!code-csharp[csrefKeywordsMethodParams#6](~/samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/RefParameterModifier.cs#5)]

## <a name="c-language-specification"></a>Спецификация языка C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>См. также

- [Написание безопасного и эффективного кода](../../write-safe-efficient-code.md)
- [Возвращаемые значения ref и локальные переменные ref](../../programming-guide/classes-and-structs/ref-returns.md)
- [Условное выражение REF](../operators/conditional-operator.md#conditional-ref-expression)
- [Передача параметров](../../programming-guide/classes-and-structs/passing-parameters.md)
- [Параметры методов](method-parameters.md)
- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Ключевые слова в C#](index.md)
