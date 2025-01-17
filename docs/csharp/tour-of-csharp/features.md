---
title: Обзор C# — основные области языка
description: Вы еще не знакомы с C#? Изучите основы этого языка. В этой статье содержится обзор основных особенностей языка.
ms.date: 08/06/2020
ms.openlocfilehash: e62ed4e360fdf3b30142474494ff4f038c77a772
ms.sourcegitcommit: e16315d9f1ff355f55ff8ab84a28915be0a8e42b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2021
ms.locfileid: "105111339"
---
# <a name="major-language-areas"></a>Основные области языка

## <a name="arrays-collections-and-linq"></a>Массивы, коллекции и LINQ

В C# и .NET имеется множество различных типов коллекций. Синтаксис массивов определяется языком. Универсальные типы коллекций перечислены в пространстве имен <xref:System.Collections.Generic?displayProperty=fullName>. К специализированным коллекциям относятся <xref:System.Span%601?displayProperty=nameWithType> для доступа к непрерывной памяти в кадре стека и <xref:System.Memory%601?displayProperty=nameWithType> для доступа к непрерывной памяти в управляемой куче. Все коллекции, включая массивы, <xref:System.Span%601> и <xref:System.Memory%601>, используют общий принцип итерации. Используется интерфейс <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>. Этот единый принцип означает, что любой из типов коллекций можно использовать с запросами LINQ или другими алгоритмами. Методы пишутся с помощью <xref:System.Collections.Generic.IEnumerable%601>, и алгоритмы работают с любой коллекцией.

### <a name="arrays"></a>Массивы

[***Массив** _](../programming-guide/arrays/index.md) — это структура данных, содержащая несколько переменных, доступ к которым осуществляется по вычисляемым индексам. Все содержащиеся в массиве переменные, также называемые _*_элементами массива_*_, относятся к одному типу. Он называется _ *_типом элементов_** массива.

Сами массивы имеют ссылочный тип, и объявление переменной массива только выделяет память для ссылки на экземпляр массива. Фактические экземпляры массива создаются динамически во время выполнения с помощью оператора `new`. Операция `new` указывает ***длину*** нового экземпляра массива, которая остается неизменной в течение всего времени существования этого экземпляра. Элементы массива имеют индексы в диапазоне от `0` до `Length - 1`. Оператор `new` автоматически инициализирует все элементы массива значением по умолчанию. Например, для всех числовых типов устанавливается нулевое значение, а для всех ссылочных типов — значение `null`.

Следующий пример кода создает массив из `int` элементов, затем инициализирует этот массив и выводит содержимое массива.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="ArraysSample":::

Этот пример создает и использует ***одномерный массив** _. Кроме этого, C# поддерживает _*_многомерные массивы_*_. Число измерений массива, которое именуется _ *_рангом_** для типа массива, всегда на единицу больше числа запятых, включенных в квадратные скобки типа массива. Следующий пример кода поочередно создает одномерный, двухмерный и трехмерный массивы.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="DeclareArrays":::

Массив `a1` содержит 10 элементов, массив `a2` — 50 элементов (10 × 5), и наконец `a3` содержит 100 элементов (10 × 5 × 2).
Элементы массива могут иметь любой тип, в том числе тип массива. Массив с элементами типа массива иногда называют ***массивом массивов***, так как элементы такого массива не обязаны иметь одинаковую длину. Следующий пример создает массив массивов `int`.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="ArrayOfArrays":::

В первой строке создается массив с тремя элементами, каждый из которых имеет тип `int[]` и начальное значение `null`. В следующих строках эти три элемента инициализируются ссылками на отдельные экземпляры массивов различной длины.

Оператор `new` позволяет задать начальные значения элементов массива, используя ***инициализатор массива***. Так называется список выражений, записанных между разделителями `{` и `}`. Следующий пример создает и инициализирует массив `int[]` с тремя элементами.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="InitializeArray":::

Длина массива определяется по числу выражений между скобками `{` и `}`. Инициализацию массива можно сократить, так как тип массива не обязательно объявлять повторно.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="InitializeShortened":::

Оба приведенных выше примера дают результат, эквивалентный следующему коду:

:::code language="csharp" source="./snippets/shared/Features.cs" ID="InitializeGenerated":::

Оператор `foreach` можно использовать для перечисления элементов любой коллекции. Следующий код перечисляет массив из предыдущего примера:

:::code language="csharp" source="./snippets/shared/Features.cs" ID="EnumerateArray":::

Оператор `foreach` использует интерфейс <xref:System.Collections.Generic.IEnumerable%601>, поэтому может работать с любой коллекцией.

## <a name="string-interpolation"></a>Интерполяция строк

[***Интерполяция строк***](../language-reference/tokens/interpolated.md) в C# позволяет форматировать строки, определяя выражения, результаты которых помещаются в строку формата. Например, в следующем примере выводится температура в указанный день из набора данных о погоде:

:::code language="csharp" source="./snippets/shared/Features.cs" ID="StringInterpolation":::

Интерполированная строка объявляется с помощью токена `$`. При интерполяции строк вычисляются выражения между `{` и `}`, результат преобразуется в `string`, а затем текст в квадратных скобках заменяется строковым результатом выражения. `:` в первом выражении `{weatherData.Date:MM-DD-YYYY}` указывает *строку формата*. В предыдущем примере указывается, что дата должна выводиться в формате "ММ-ДД-ГГГГ".

## <a name="pattern-matching"></a>Регулярные выражения

В языке C# есть выражения [***сопоставления шаблонов***](../pattern-matching.md) для запроса состояния объекта и выполнения кода в зависимости от него. Чтобы определить, какое действие следует предпринять, можно проверить типы и значения свойств и полей. Выражение `switch` является основным для сопоставления шаблонов.

## <a name="delegates-and-lambda-expressions"></a>Делегаты и лямбда-выражения

[***Тип delegate***](../delegates-overview.md) представляет ссылки на методы с конкретным списком параметров и типом возвращаемого значения. Делегаты позволяют использовать методы как сущности, сохраняя их в переменные и передавая в качестве параметров. Принцип работы делегатов близок к указателям функций из некоторых языков. В отличие от указателей функций, делегаты являются объектно-ориентированными и типобезопасными.

Следующий пример кода объявляет и использует тип делегата с именем `Function`.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="DelegateExample":::

Экземпляр `Function` с типом делегата может ссылаться на любой метод, который принимает аргумент `double` и возвращает значение `double`. Метод `Apply` применяет заданный `Function` к элементам `double[]` и возвращает `double[]` с результатами. В методе `Main` используется `Apply` для применения трех различных функций к `double[]`.

Делегат может ссылаться на статический метод (например, `Square` или `Math.Sin` в предыдущем примере) или метод экземпляра (например, `m.Multiply` в предыдущем примере). Делегат, который ссылается на метод экземпляра, также содержит ссылку на конкретный объект. Когда метод экземпляра вызывается через делегат, этот объект превращается в `this` в вызове.

Делегаты могут также создаваться с использованием анонимных функций, то есть создаваемых при объявлении "встроенных методов". Анонимные функции могут использовать локальные переменные соседних методов. В следующем примере не создается класс:

:::code language="csharp" source="./snippets/shared/Features.cs" ID="UseDelegate":::

Делегат не имеет информации или ограничений в отношении того, к какому классу относится метод, на который он ссылается. Достаточно лишь, чтобы метод, на который указывает ссылка, имел такие же параметры и тип возвращаемого значения, что и делегат.

## <a name="async--await"></a>async и await

C# поддерживает асинхронные программы с двумя ключевыми словами: `async` и `await`. Чтобы объявить метод как асинхронный, нужно добавить модификатор `async` в его объявление. Оператор `await` предписывает компилятору асинхронно ожидать результата для завершения выполнения. Управление возвращается вызывающему объекту, а метод возвращает структуру, которая управляет состоянием асинхронной работы. Обычно структурой является <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>, но это также может быть любой тип, поддерживающий шаблон ожидания. Эти возможности позволяют писать код, который считывается как синхронный аналог, но выполняется асинхронно. Например, следующий код скачивает домашнюю страницу [документации Майкрософт](/):

:::code language="csharp" source="./snippets/shared/Features.cs" ID="AsyncExample":::

В этом небольшом примере показаны основные особенности асинхронного программирования:

- Объявление метода включает в себя модификатор `async`.
- Тело метода (`await`) ожидает возврата управления методом `GetByteArrayAsync`.
- Тип, указанный в операторе `return`, соответствует аргументу типа в объявлении `Task<T>` для метода. (Метод, возвращающий `Task`, будет использовать операторы `return` без аргументов.)

## <a name="attributes"></a>Атрибуты

Типы, члены и другие сущности в программе C# поддерживают модификаторы, которые управляют некоторыми аспектами их поведения. Например, доступность метода определяется с помощью модификаторов `public`, `protected`, `internal` и `private`. C# обобщает эту возможность, позволяя пользователям определять собственные типы декларативных сведений, назначать их для сущностей программы и извлекать во время выполнения. В программах эти дополнительные декларативные сведения определяются и используются посредством [***атрибутов***](../programming-guide/concepts/attributes/index.md).

Следующий пример кода объявляет атрибут `HelpAttribute`, который можно поместить в сущности программы для указания связей с соответствующей документацией.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="DefineAttribute":::

Все классы атрибутов являются производными от базового класса <xref:System.Attribute>, который предоставляется в библиотеке .NET. Чтобы задать атрибут, его имя и возможные аргументы указываются в квадратных скобках непосредственно перед объявлением соответствующей сущности. Если имя атрибута заканчивается на `Attribute`, этот суффикс можно опускать при указании ссылки на этот атрибут. Например, атрибут с именем `HelpAttribute` можно использовать так:

:::code language="csharp" source="./snippets/shared/Features.cs" ID="UseAttributes":::

Этот пример кода присоединяет атрибут `HelpAttribute` к классу `Widget`. Также он добавляет другой атрибут `HelpAttribute` для метода `Display` в этом классе. Открытые конструкторы класса атрибута указывают, какие сведения необходимо указать при назначении атрибута некоторой сущности программы. Дополнительные сведения можно предоставить через обращения к открытым свойствам класса атрибута, доступным для чтения и записи (например, как указанная выше ссылка на свойство `Topic`).

Метаданные, определенные атрибутами, можно считывать и использовать во время выполнения с помощью отражения. Когда с помощью этого метода выполняется запрос конкретного атрибута, вызывается конструктор для класса атрибута с указанием сведений, представленных в исходном коде программы, а затем возвращается созданный экземпляр атрибута. Если дополнительные сведения предоставляются через свойства, перед возвращением экземпляра атрибута этим свойствам присваиваются указанные значения.

В следующем примере кода показано, как получить экземпляр класса `HelpAttribute`, связанный с классом `Widget` и его методом `Display`.

:::code language="csharp" source="./snippets/shared/Features.cs" ID="ReadAttributes":::

## <a name="learn-more"></a>Дополнительные сведения

Узнать больше о C# можно с помощью наших [учебников](../tutorials/intro-to-csharp/introduction-to-classes.md).

>[!div class="step-by-step"]
>[Назад](program-building-blocks.md)
