---
title: Перегрузка операторов
description: 'Узнайте, как перегружать арифметические операторы в классе или типе записи и на глобальном уровне в F #.'
ms.date: 08/15/2020
ms.openlocfilehash: 64ff87a8706e6a05754b5328a7d95cd6a2b360c1
ms.sourcegitcommit: 80f38cb67bd02f51d5722fa13d0ea207e3b14a8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/26/2021
ms.locfileid: "105610854"
---
# <a name="operator-overloading"></a>Перегрузка операторов

В этом разделе описывается перегрузка арифметических операторов в классе или типе записи, а также на глобальном уровне.

## <a name="syntax"></a>Синтаксис

```fsharp
// Overloading an operator as a class or record member.
static member (operator-symbols) (parameter-list) =
    method-body
// Overloading an operator at the global level
let [inline] (operator-symbols) parameter-list = function-body
```

## <a name="remarks"></a>Примечания

В предыдущем синтаксисе *оператор-Symbol* является одним из `+` ,,, `-` `*` `/` , `=` и т. д. *Параметр-List* задает операнды в том порядке, в котором они отображаются в обычном синтаксисе для этого оператора. *Метод-Body* конструирует результирующее значение.

Перегрузки операторов для операторов должны быть статическими. Перегрузки операторов для унарных операторов, таких как `+` и `-` , должны использовать символ тильды ( `~` ) в *операторе-Symbol* , чтобы указать, что оператор является унарным оператором, а не бинарным оператором, как показано в следующем объявлении.

```fsharp
static member (~-) (v : Vector)
```

В следующем коде показан класс Vector, имеющий только два оператора: один для унарного минуса и один для умножения скаляром. В этом примере требуется две перегрузки для скалярного умножения, так как оператор должен работать независимо от порядка, в котором отображаются Vector и scalar.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4001.fs)]

## <a name="creating-new-operators"></a>Создание новых операторов

Можно перегружать все стандартные операторы, но можно также создавать новые операторы из последовательностей определенных символов. Допустимые символы оператора: `!` , `$` ,,, `%` `&` `*` , `+` , `-` , `.` , `/` , `<` , `=` , `>` , `?` , `@` , `^` , `|` и `~` . `~`Символ имеет особое значение, что делает оператор унарным и не является частью последовательности символов оператора. Не все операторы можно сделать унарными.

В зависимости от того, какая последовательность символов используется, оператор будет иметь определенный приоритет и ассоциативность. Ассоциативность может быть либо слева направо, либо справа налево, и используется всякий раз, когда операторы одного и того же уровня приоритета отображаются в последовательности без скобок.

Символ оператора не `.` влияет на приоритет, поэтому, например, если требуется определить собственную версию умножения, имеющую тот же приоритет и ассоциативность, что и обычное умножение, можно создать такие операторы, как `.*` .

Только операторы `?` и `?<-` могут начинаться с `?` .

`$`Оператор должен быть изолированным и без дополнительных символов.

Таблица, в которой показан приоритет всех операторов в F #, можно найти в [справочнике по символам и операторам](./symbol-and-operator-reference/index.md).

## <a name="overloaded-operator-names"></a>Имена перегруженных операторов

Когда компилятор F # компилирует выражение оператора, он создает метод с именем, созданным компилятором для этого оператора. Это имя, которое отображается на языке MSIL для метода, а также в отражении и IntelliSense. Обычно вам не нужно использовать эти имена в коде F #.

В следующей таблице показаны стандартные операторы и соответствующие им созданные имена.

|Оператор|Созданное имя|
|--------|--------------|
|`[]`|`op_Nil`|
|`::`|`op_Cons`|
|`+`|`op_Addition`|
|`-`|`op_Subtraction`|
|`*`|`op_Multiply`|
|`/`|`op_Division`|
|`@`|`op_Append`|
|`^`|`op_Concatenate`|
|`%`|`op_Modulus`|
|`&&&`|`op_BitwiseAnd`|
|<code>&#124;&#124;&#124;</code>|`op_BitwiseOr`|
|`^^^`|`op_ExclusiveOr`|
|`<<<`|`op_LeftShift`|
|`~~~`|`op_LogicalNot`|
|`>>>`|`op_RightShift`|
|`~+`|`op_UnaryPlus`|
|`~-`|`op_UnaryNegation`|
|`=`|`op_Equality`|
|`<=`|`op_LessThanOrEqual`|
|`>=`|`op_GreaterThanOrEqual`|
|`<`|`op_LessThan`|
|`>`|`op_GreaterThan`|
|`?`|`op_Dynamic`|
|`?<-`|`op_DynamicAssignment`|
|<code>&#124;></code>|`op_PipeRight`|
|<code><&#124;</code>|`op_PipeLeft`|
|`!`|`op_Dereference`|
|`>>`|`op_ComposeRight`|
|`<<`|`op_ComposeLeft`|
|`<@ @>`|`op_Quotation`|
|`<@@ @@>`|`op_QuotationUntyped`|
|`+=`|`op_AdditionAssignment`|
|`-=`|`op_SubtractionAssignment`|
|`*=`|`op_MultiplyAssignment`|
|`/=`|`op_DivisionAssignment`|
|`..`|`op_Range`|
|`.. ..`|`op_RangeStep`|

Обратите внимание, что `not` оператор в F # не выдается, `op_Inequality` так как он не является символом-оператором. Это функция, которая создает IL, который Инвертирует логическое выражение.

Другие сочетания символов операторов, которые не перечислены здесь, могут использоваться в качестве операторов и иметь имена, которые объединяются путем объединения имен для отдельных символов из следующей таблицы. Например, +!  превращается в `op_PlusBang`.

|Символ оператора|Имя|
|------------------|----|
|`>`|`Greater`|
|`<`|`Less`|
|`+`|`Plus`|
|`-`|`Minus`|
|`*`|`Multiply`|
|`/`|`Divide`|
|`=`|`Equals`|
|`~`|`Twiddle`|
|`$`|`Dollar`|
|`%`|`Percent`|
|`.`|`Dot`|
|`&`|`Amp`|
|<code>&#124;</code>|`Bar`|
|`@`|`At`|
|`^`|`Hat`|
|`!`|`Bang`|
|`?`|`Qmark`|
|`(`|`LParen`|
|`,`|`Comma`|
|`)`|`RParen`|
|`[`|`LBrack`|
|`]`|`RBrack`|

## <a name="prefix-and-infix-operators"></a>Операторы prefix и инфиксные

Операторы *префикса* должны размещаться перед операндом или операндами, во многом подобно функции. Операторы *инфиксные* должны располагаться между двумя операндами.

В качестве префиксных операторов можно использовать только определенные операторы. Некоторые операторы всегда являются префиксными операторами, другие могут быть инфиксные или префиксом, а остальные всегда инфиксные операторами. Операторы, которые начинаются с `!` оператора, за исключением `!=` and, `~` или повторяющихся последовательностей `~` , всегда являются префиксными операторами. Операторы,,,,,, `+` `-` `+.` `-.` `&` `&&` `%` и `%%` могут быть префиксными операторами или операторами инфиксные. Префиксную версию этих операторов можно отличить от версии инфиксные, добавляя в `~` начале префиксного оператора, когда он определен. `~`Не используется при использовании оператора, только если он определен.

## <a name="example"></a>Пример

В следующем коде показано использование перегрузки операторов для реализации типа дробной части. Дробная часть представляется числителем и знаменателем. Функция `hcf` используется для определения самого высокого общего фактора, который используется для сокращения дробей.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4002.fs)]

**Выходные данные:**

```console
3/4 + 1/2 = 5/4
3/4 - 1/2 = 1/4
3/4 * 1/2 = 3/8
3/4 / 1/2 = 3/2
3/4 + 1 = 7/4
```

## <a name="operators-at-the-global-level"></a>Операторы на глобальном уровне

Операторы также можно определять на глобальном уровне. В следующем коде определяется оператор `+?` .

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4003.fs)]

Выходные данные приведенного выше кода имеют значение `12` .

Таким образом, можно переопределить регулярные арифметические операторы, так как правила области для F # определяют, что новые определенные операторы имеют приоритет над встроенными операторами.

Ключевое слово `inline` часто используется с глобальными операторами, которые часто являются маленькими функциями, которые лучше всего интегрируются в вызывающий код. Использование встроенных функций операторов также позволяет им работать с статически разрешаемыми параметрами типов для формирования статически разрешаемого универсального кода. Дополнительные сведения см. в разделе [встроенные функции](./functions/inline-functions.md) и [статически разрешаемые параметры типа](./generics/statically-resolved-type-parameters.md).

## <a name="see-also"></a>См. также раздел

- [Члены](./members/index.md)
