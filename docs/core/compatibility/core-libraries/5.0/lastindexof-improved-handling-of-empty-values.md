---
title: Критическое изменение. Улучшена обработка пустых строк поиска с помощью LastIndexOf
description: Сведения о критическом изменении .NET 5 в основных библиотеках .NET, где LastIndexOf и связанные API теперь возвращают правильные значения при поиске подстроки нулевой длины.
ms.date: 11/01/2020
ms.openlocfilehash: 9dc34300d867fe1bb9264494b3f2261bad2c1eea
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102257431"
---
# <a name="lastindexof-has-improved-handling-of-empty-search-strings"></a><span data-ttu-id="5e833-103">Улучшена обработка пустых строк поиска с помощью LastIndexOf</span><span class="sxs-lookup"><span data-stu-id="5e833-103">LastIndexOf has improved handling of empty search strings</span></span>

<span data-ttu-id="5e833-104"><xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> и связанные API теперь возвращают правильные значения при поиске подстроки нулевой длины (или эквивалентной нулевой длины) в более длинной строке.</span><span class="sxs-lookup"><span data-stu-id="5e833-104"><xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> and related APIs now return correct values when searching for a zero-length (or zero-length equivalent) substring within a larger string.</span></span>

## <a name="change-description"></a><span data-ttu-id="5e833-105">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="5e833-105">Change description</span></span>

<span data-ttu-id="5e833-106">В .NET Framework и .NET Core 1.0–3.1 <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> и связанные API могут возвращать неправильное значение, когда вызывающий объект выполняет поиск подстроки нулевой длины.</span><span class="sxs-lookup"><span data-stu-id="5e833-106">In .NET Framework and .NET Core 1.0 - 3.1, <xref:System.String.LastIndexOf%2A?displayProperty=nameWithType> and related APIs might return an incorrect value when the caller searches for a zero-length substring.</span></span>

```csharp
Console.WriteLine("Hello".LastIndexOf("")); // prints '4' (incorrect)

ReadOnlySpan<char> span = "Hello";
Console.WriteLine(span.LastIndexOf("")); // prints '0' (incorrect)
```

<span data-ttu-id="5e833-107">Начиная с .NET 5 эти API возвращают правильное значение для `LastIndexOf`.</span><span class="sxs-lookup"><span data-stu-id="5e833-107">Starting with .NET 5, these APIs return the correct value for `LastIndexOf`.</span></span>

```csharp
Console.WriteLine("Hello".LastIndexOf("")); // prints '5' (correct)

ReadOnlySpan<char> span = "Hello";
Console.WriteLine(span.LastIndexOf("")); // prints '5' (correct)
```

<span data-ttu-id="5e833-108">В этих примерах `5` является правильным ответом, поскольку и `"Hello".Substring(5)`, и `"Hello".AsSpan().Slice(5)` создают пустую строку, которая является эквивалентной по отношению к искомой пустой подстроке.</span><span class="sxs-lookup"><span data-stu-id="5e833-108">In these examples, `5` is the correct answer because `"Hello".Substring(5)` and `"Hello".AsSpan().Slice(5)` both produce an empty string, which is trivially equal to the empty substring that is sought.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="5e833-109">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="5e833-109">Reason for change</span></span>

<span data-ttu-id="5e833-110">Это изменение было внесено в рамках устранения ошибок, связанных с обработкой строк для .NET 5.</span><span class="sxs-lookup"><span data-stu-id="5e833-110">This change was part of an overall bug fixing effort around string handling for .NET 5.</span></span> <span data-ttu-id="5e833-111">Это также помогает унифицировать поведение платформы Windows и платформ, отличных от Windows.</span><span class="sxs-lookup"><span data-stu-id="5e833-111">It also helps unify our behavior between Windows and non-Windows platforms.</span></span> <span data-ttu-id="5e833-112">Дополнительные сведения см. в статьях [dotnet/runtime#13383](https://github.com/dotnet/runtime/issues/13383) и [dotnet/runtime##13382](https://github.com/dotnet/runtime/issues/13382).</span><span class="sxs-lookup"><span data-stu-id="5e833-112">For more information, see [dotnet/runtime#13383](https://github.com/dotnet/runtime/issues/13383) and [dotnet/runtime##13382](https://github.com/dotnet/runtime/issues/13382).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="5e833-113">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="5e833-113">Version introduced</span></span>

<span data-ttu-id="5e833-114">5.0</span><span class="sxs-lookup"><span data-stu-id="5e833-114">5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="5e833-115">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="5e833-115">Recommended action</span></span>

<span data-ttu-id="5e833-116">Никаких дополнительных действий от вас не требуется.</span><span class="sxs-lookup"><span data-stu-id="5e833-116">You don't need to take any action.</span></span> <span data-ttu-id="5e833-117">Среда выполнения .NET 5 автоматически предоставляет новые варианты поведения.</span><span class="sxs-lookup"><span data-stu-id="5e833-117">The .NET 5 runtime provides the new behaviors automatically.</span></span>

<span data-ttu-id="5e833-118">Отсутствует параметр совместимости для восстановления старого поведения.</span><span class="sxs-lookup"><span data-stu-id="5e833-118">There is no compatibility switch to restore the old behavior.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="5e833-119">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="5e833-119">Affected APIs</span></span>

- <xref:System.String.LastIndexOf%2A?displayProperty=fullName>
- <xref:System.Globalization.CompareInfo.LastIndexOf%2A?displayProperty=fullName>
- <xref:System.MemoryExtensions.LastIndexOf%2A?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `Overload:System.String.LastIndexOf`
- `Overload:System.Globalization.CompareInfo.LastIndexOf`
- `Overload:System.MemoryExtensions.LastIndexOf`

-->
