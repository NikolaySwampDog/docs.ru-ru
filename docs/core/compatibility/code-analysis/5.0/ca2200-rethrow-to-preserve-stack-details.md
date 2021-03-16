---
title: Критическое изменение. CA2200. Повторно порождайте исключения для сохранения сведений стека
description: Узнайте о критическом изменении в .NET 5, вызванном включением правила анализа кода CA2200.
ms.date: 09/03/2020
ms.openlocfilehash: 776a1bcf16c19364017e4652837720080fb7ba72
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102257730"
---
# <a name="warning-ca2200-rethrow-to-preserve-stack-details"></a><span data-ttu-id="7b32e-103">Предупреждение CA2200: Повторно порождайте исключения для сохранения сведений стека</span><span class="sxs-lookup"><span data-stu-id="7b32e-103">Warning CA2200: Rethrow to preserve stack details</span></span>

<span data-ttu-id="7b32e-104">Начиная с .NET 5.0 правило [CA2200](/visualstudio/code-quality/ca2200) анализатора кода .NET включено по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7b32e-104">.NET code analyzer rule [CA2200](/visualstudio/code-quality/ca2200) is enabled, by default, starting in .NET 5.0.</span></span> <span data-ttu-id="7b32e-105">Оно создает предупреждение сборки для всех блоков `catch`, которые повторно выдают исключение, а исключение явным образом указывается в операторе `throw`.</span><span class="sxs-lookup"><span data-stu-id="7b32e-105">It produces a build warning for any `catch` blocks that rethrow an exception and the exception is explicitly specified in the `throw` statement.</span></span>

## <a name="change-description"></a><span data-ttu-id="7b32e-106">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="7b32e-106">Change description</span></span>

<span data-ttu-id="7b32e-107">Начиная с .NET 5, пакет SDK для .NET включает [анализаторы исходного кода .NET](../../../../fundamentals/code-analysis/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b32e-107">Starting in .NET 5, the .NET SDK includes [.NET source code analyzers](../../../../fundamentals/code-analysis/overview.md).</span></span> <span data-ttu-id="7b32e-108">Некоторые из этих правил включены по умолчанию, в том числе [CA2200](/visualstudio/code-quality/ca2200).</span><span class="sxs-lookup"><span data-stu-id="7b32e-108">Several of these rules are enabled, by default, including [CA2200](/visualstudio/code-quality/ca2200).</span></span> <span data-ttu-id="7b32e-109">Если проект содержит код, нарушающий это правило и настроенный на обработку предупреждений как ошибок, это изменение может нарушить сборку.</span><span class="sxs-lookup"><span data-stu-id="7b32e-109">If your project contains code that violates this rule and is configured to treat warnings as errors, this change could break your build.</span></span>

<span data-ttu-id="7b32e-110">Правило CA2200 помечает код, в котором исключения вызываются повторно, а переменная исключения указывается в операторе `throw`.</span><span class="sxs-lookup"><span data-stu-id="7b32e-110">Rule CA2200 flags code where exceptions are rethrown and the exception variable is specified in the `throw` statement.</span></span> <span data-ttu-id="7b32e-111">Часть информации в появившемся исключении представляет собой трассировку стека.</span><span class="sxs-lookup"><span data-stu-id="7b32e-111">When an exception is thrown, part of the information it carries is the stack trace.</span></span> <span data-ttu-id="7b32e-112">Трассировка стека — это список иерархии вызовов методов, который начинается с метода, вызывающего исключение, и завершается методом, перехватывающим исключение.</span><span class="sxs-lookup"><span data-stu-id="7b32e-112">The stack trace is a list of the method call hierarchy that starts with the method that throws the exception and ends with the method that catches the exception.</span></span> <span data-ttu-id="7b32e-113">Если исключение повторно создается заданием исключения в операторе `throw`, трассировка стека перезапускается в текущем методе, а список вызовов метода между исходным методом, создавшим исключение, и текущим методом теряется.</span><span class="sxs-lookup"><span data-stu-id="7b32e-113">If an exception is rethrown by specifying the exception in the `throw` statement, the stack trace restarts at the current method and the list of method calls between the original method that threw the exception and the current method is lost.</span></span> <span data-ttu-id="7b32e-114">Для сохранения исходных данных трассировки стека с исключением следует использовать оператор `throw` без указания исключения.</span><span class="sxs-lookup"><span data-stu-id="7b32e-114">To keep the original stack trace information with the exception, use the `throw` statement without specifying the exception.</span></span>

<span data-ttu-id="7b32e-115">Следующий фрагмент кода не создает предупреждение для правила CA2200.</span><span class="sxs-lookup"><span data-stu-id="7b32e-115">The following code snippet does not produce a warning for rule CA2200.</span></span> <span data-ttu-id="7b32e-116">Однако строка с комментарием *будет* вызывать нарушение.</span><span class="sxs-lookup"><span data-stu-id="7b32e-116">The commented line *would* trigger a violation, however.</span></span>

```csharp
catch (ArithmeticException e)
{
    // throw e;
    throw;
}
```

## <a name="version-introduced"></a><span data-ttu-id="7b32e-117">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="7b32e-117">Version introduced</span></span>

<span data-ttu-id="7b32e-118">5.0</span><span class="sxs-lookup"><span data-stu-id="7b32e-118">5.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="7b32e-119">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="7b32e-119">Recommended action</span></span>

- <span data-ttu-id="7b32e-120">Повторно создайте исключения без явного указания исключения.</span><span class="sxs-lookup"><span data-stu-id="7b32e-120">Rethrow exceptions without specifying the exception explicitly.</span></span> <span data-ttu-id="7b32e-121">Дополнительные сведения см. в правиле [CA2200](/visualstudio/code-quality/ca2200).</span><span class="sxs-lookup"><span data-stu-id="7b32e-121">For more information, see [CA2200](/visualstudio/code-quality/ca2200).</span></span>

- <span data-ttu-id="7b32e-122">Чтобы полностью отключить анализ кода, задайте для параметра `EnableNETAnalyzers` значение `false` в файле проекта.</span><span class="sxs-lookup"><span data-stu-id="7b32e-122">To disable code analysis completely, set `EnableNETAnalyzers` to `false` in your project file.</span></span> <span data-ttu-id="7b32e-123">Дополнительные сведения см. в разделе [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).</span><span class="sxs-lookup"><span data-stu-id="7b32e-123">For more information, see [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).</span></span>

## <a name="affected-apis"></a><span data-ttu-id="7b32e-124">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="7b32e-124">Affected APIs</span></span>

<span data-ttu-id="7b32e-125">Невозможно обнаружить с помощью анализа API.</span><span class="sxs-lookup"><span data-stu-id="7b32e-125">Not detectable via API analysis.</span></span>

<!--

### Affected APIs

Not detectable via API analysis.

### Category

Code analysis

-->
