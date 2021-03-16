---
title: Критическое изменение. Для десериализации символа требуется строка из одного символа
description: Сведения о критическом изменении в .NET 5, где System.Text.Json требует наличия в JSON строки с одним символом при десериализации до целевого символа.
ms.date: 12/15/2020
ms.openlocfilehash: e901f8ee7e7521af948a3bcde5cf969640436f7f
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102256339"
---
# <a name="systemtextjson-requires-single-char-string-to-deserialize-a-char"></a><span data-ttu-id="188e4-103">Для десериализации символа в System.Text.Json требуется строка из одного символа</span><span class="sxs-lookup"><span data-stu-id="188e4-103">System.Text.Json requires single-char string to deserialize a char</span></span>

<span data-ttu-id="188e4-104">Для успешной десериализации <xref:System.Char> с помощью <xref:System.Text.Json>строка JSON должна содержать один символ.</span><span class="sxs-lookup"><span data-stu-id="188e4-104">To successfully deserialize a <xref:System.Char> using <xref:System.Text.Json>, the JSON string must contain a single character.</span></span>

## <a name="change-description"></a><span data-ttu-id="188e4-105">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="188e4-105">Change description</span></span>

<span data-ttu-id="188e4-106">В предыдущих версиях .NET строка из нескольких `char` в JSON успешно десериализуется в свойство `char` или поле.</span><span class="sxs-lookup"><span data-stu-id="188e4-106">In previous .NET versions, a multi-`char` string in the JSON is successfully deserialized to a `char` property or field.</span></span> <span data-ttu-id="188e4-107">Используется только первый `char` строки, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="188e4-107">Only the first `char` of the string is used, as in the following example:</span></span>

```csharp
// .NET Core 3.0 and 3.1: Returns the first char 'a'.
// .NET 5 and later: Throws JsonException because payload has more than one char.
char deserializedChar = JsonSerializer.Deserialize<char>("\"abc\"");
```

<span data-ttu-id="188e4-108">В .NET 5 и более поздних версиях передача любой строки, кроме строки с одним `char`, приводит к вызову исключения <xref:System.Text.Json.JsonException>, если целевым объектом десериализации является `char`.</span><span class="sxs-lookup"><span data-stu-id="188e4-108">In .NET 5 and later, anything other than a single-`char` string causes a <xref:System.Text.Json.JsonException> to be thrown when the deserialization target is a `char`.</span></span> <span data-ttu-id="188e4-109">Следующий пример строки успешно десериализуется во всех версиях .NET:</span><span class="sxs-lookup"><span data-stu-id="188e4-109">The following example string is successfully deserialized in all .NET versions:</span></span>

```csharp
// Correct usage.
char deserializedChar = JsonSerializer.Deserialize<char>("\"a\"");
```

## <a name="version-introduced"></a><span data-ttu-id="188e4-110">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="188e4-110">Version introduced</span></span>

<span data-ttu-id="188e4-111">5.0</span><span class="sxs-lookup"><span data-stu-id="188e4-111">5.0</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="188e4-112">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="188e4-112">Reason for change</span></span>

<span data-ttu-id="188e4-113">Синтаксический анализ для сериализации должен выполняться только тогда, когда предоставленные полезные данные допустимы для целевого типа.</span><span class="sxs-lookup"><span data-stu-id="188e4-113">Parsing for deserialization should only succeed when the provided payload is valid for the target type.</span></span> <span data-ttu-id="188e4-114">Для типа `char` единственным допустимым набором полезных данных является строка с одним `char`.</span><span class="sxs-lookup"><span data-stu-id="188e4-114">For a `char` type, the only valid payload is a single-`char` string.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="188e4-115">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="188e4-115">Recommended action</span></span>

<span data-ttu-id="188e4-116">При десериализации JSON в целевой объект `char` убедитесь, что строка состоит из одного `char`.</span><span class="sxs-lookup"><span data-stu-id="188e4-116">When you deserialize JSON into a `char` target, make sure the string consists of a single `char`.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="188e4-117">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="188e4-117">Affected APIs</span></span>

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`

### Category

Serialization

-->
