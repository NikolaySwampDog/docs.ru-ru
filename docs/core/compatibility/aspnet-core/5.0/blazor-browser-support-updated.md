---
title: 'Критическое изменение: Blazor. Обновлен список поддерживаемых веб-браузеров'
description: Сведения о критическом изменении в ASP.NET Core 5.0 — Blazor. Обновлен список поддерживаемых веб-браузеров
ms.author: scaddie
ms.date: 10/01/2020
no-loc:
- Blazor
- Blazor WebAssembly
- Blazor Server
ms.openlocfilehash: 25566a4b30aaa8484ec4bcf26ab1e8fde6af1279
ms.sourcegitcommit: 089068389671f6f9e15fd67dcbfb0145bf72f1fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106497870"
---
# <a name="blazor-updated-browser-support"></a><span data-ttu-id="b278d-103">Blazor: Обновлен список поддерживаемых веб-браузеров</span><span class="sxs-lookup"><span data-stu-id="b278d-103">Blazor: Updated browser support</span></span>

<span data-ttu-id="b278d-104">В ASP.NET Core 5.0 появились [новые функции Blazor](https://github.com/dotnet/aspnetcore/issues/21514), некоторые из которых несовместимы со старыми браузерами.</span><span class="sxs-lookup"><span data-stu-id="b278d-104">ASP.NET Core 5.0 introduces [new Blazor features](https://github.com/dotnet/aspnetcore/issues/21514), some of which are incompatible with older browsers.</span></span> <span data-ttu-id="b278d-105">Список браузеров, поддерживаемых Blazor в ASP.NET Core 5.0, обновлен соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b278d-105">The list of browsers supported by Blazor in ASP.NET Core 5.0 has been updated accordingly.</span></span>

<span data-ttu-id="b278d-106">Обсуждение этого вопроса см. на странице GitHub [dotnet/aspnetcore#26475](https://github.com/dotnet/aspnetcore/issues/26475).</span><span class="sxs-lookup"><span data-stu-id="b278d-106">For discussion, see GitHub issue [dotnet/aspnetcore#26475](https://github.com/dotnet/aspnetcore/issues/26475).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="b278d-107">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="b278d-107">Version introduced</span></span>

<span data-ttu-id="b278d-108">5.0</span><span class="sxs-lookup"><span data-stu-id="b278d-108">5.0</span></span>

## <a name="old-behavior"></a><span data-ttu-id="b278d-109">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="b278d-109">Old behavior</span></span>

<span data-ttu-id="b278d-110">Blazor Server поддерживает Microsoft Internet Explorer 11 с достаточным количеством заполнений.</span><span class="sxs-lookup"><span data-stu-id="b278d-110">Blazor Server supports Microsoft Internet Explorer 11 with sufficient polyfills.</span></span> <span data-ttu-id="b278d-111">Blazor Server и Blazor WebAssembly также работают в [Microsoft Edge прежних версий](https://support.microsoft.com/help/4533505/what-is-microsoft-edge-legacy).</span><span class="sxs-lookup"><span data-stu-id="b278d-111">Blazor Server and Blazor WebAssembly are also functional in [Microsoft Edge Legacy](https://support.microsoft.com/help/4533505/what-is-microsoft-edge-legacy).</span></span>

## <a name="new-behavior"></a><span data-ttu-id="b278d-112">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="b278d-112">New behavior</span></span>

<span data-ttu-id="b278d-113">Blazor Server в ASP.NET Core 5.0 не поддерживается в Microsoft Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="b278d-113">Blazor Server in ASP.NET Core 5.0 isn't supported with Microsoft Internet Explorer 11.</span></span> <span data-ttu-id="b278d-114">Blazor Server и Blazor WebAssembly не полностью работают в Microsoft Edge прежних версий.</span><span class="sxs-lookup"><span data-stu-id="b278d-114">Blazor Server and Blazor WebAssembly aren't fully functional in Microsoft Edge Legacy.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="b278d-115">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="b278d-115">Reason for change</span></span>

<span data-ttu-id="b278d-116">Новые функции Blazor в ASP.NET Core 5.0 несовместимы с этими старыми браузерами, кроме того, уровень их использования снижается.</span><span class="sxs-lookup"><span data-stu-id="b278d-116">New Blazor features in ASP.NET Core 5.0 are incompatible with these older browsers, and use of these older browsers is diminishing.</span></span> <span data-ttu-id="b278d-117">Дополнительные сведения см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="b278d-117">For more information, see the following resources:</span></span>

* [<span data-ttu-id="b278d-118">Поддержка Windows устаревшей версии Microsoft Edge также прекращается 9 марта 2021 г.</span><span class="sxs-lookup"><span data-stu-id="b278d-118">Windows support for Microsoft Edge Legacy is also ending on March 9, 2021</span></span>](https://support.microsoft.com/help/4533505/what-is-microsoft-edge-legacy)
* [<span data-ttu-id="b278d-119">Приложения и службы Microsoft 365 перестанут поддерживать Microsoft Internet Explorer 11 17 августа 2021 г.</span><span class="sxs-lookup"><span data-stu-id="b278d-119">Microsoft 365 apps and services will end support for Microsoft Internet Explorer 11 by August 17, 2021</span></span>](/lifecycle/announcements/m365-ie11-microsoft-edge-legacy)

## <a name="recommended-action"></a><span data-ttu-id="b278d-120">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="b278d-120">Recommended action</span></span>

<span data-ttu-id="b278d-121">Обновите эти старые браузеры до [нового Microsoft Edge, основанного на Chromium](https://www.microsoft.com/edge).</span><span class="sxs-lookup"><span data-stu-id="b278d-121">Upgrade from these older browsers to the [new, Chromium-based Microsoft Edge](https://www.microsoft.com/edge).</span></span> <span data-ttu-id="b278d-122">Для приложений Blazor, которым требуется поддержка этих старых браузеров, используйте ASP.NET Core 3.1.</span><span class="sxs-lookup"><span data-stu-id="b278d-122">For Blazor apps that need to support these older browsers, use ASP.NET Core 3.1.</span></span> <span data-ttu-id="b278d-123">Список поддерживаемых браузеров для Blazor в ASP.NET Core 3.1 не изменился и описан в разделе о [поддерживаемых платформах](/aspnet/core/blazor/supported-platforms?view=aspnetcore-3.1).</span><span class="sxs-lookup"><span data-stu-id="b278d-123">The supported browsers list for Blazor in ASP.NET Core 3.1 hasn't changed and is documented at [Supported platforms](/aspnet/core/blazor/supported-platforms?view=aspnetcore-3.1).</span></span>

## <a name="affected-apis"></a><span data-ttu-id="b278d-124">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="b278d-124">Affected APIs</span></span>

<span data-ttu-id="b278d-125">Отсутствуют</span><span class="sxs-lookup"><span data-stu-id="b278d-125">None</span></span>

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
