---
title: 'Критическое изменение. Blazor: Изменена целевая платформа для пакетов NuGet'
description: Сведения о критическом изменении в ASP.NET Core 5.0 — Blazor. Изменена целевая платформа для пакетов NuGet
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 02945c223410860c9336b6046afe54cacce878dd
ms.sourcegitcommit: 089068389671f6f9e15fd67dcbfb0145bf72f1fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106498195"
---
# <a name="blazor-target-framework-of-nuget-packages-changed"></a><span data-ttu-id="c2f38-103">Blazor: Изменена целевая платформа для пакетов NuGet</span><span class="sxs-lookup"><span data-stu-id="c2f38-103">Blazor: Target framework of NuGet packages changed</span></span>

<span data-ttu-id="c2f38-104">Ранее проекты Blazor 3.2 WebAssembly компилировались для целевой платформы .NET Standard 2.1 (`<TargetFramework>netstandard2.1</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="c2f38-104">Blazor 3.2 WebAssembly projects were compiled to target .NET Standard 2.1 (`<TargetFramework>netstandard2.1</TargetFramework>`).</span></span> <span data-ttu-id="c2f38-105">В ASP.NET Core 5.0 целевой платформой для проектов Blazor Server и Blazor WebAssembly является .NET 5.0 (`<TargetFramework>net5.0</TargetFramework>`).</span><span class="sxs-lookup"><span data-stu-id="c2f38-105">In ASP.NET Core 5.0, both Blazor Server and Blazor WebAssembly projects target .NET 5.0 (`<TargetFramework>net5.0</TargetFramework>`).</span></span> <span data-ttu-id="c2f38-106">В соответствии с изменением целевой платформы следующие пакеты Blazor также больше не предназначены для платформы .NET Standard 2.1:</span><span class="sxs-lookup"><span data-stu-id="c2f38-106">To better align with the target framework change, the following Blazor packages no longer target .NET Standard 2.1:</span></span>

* <span data-ttu-id="c2f38-107">[Microsoft.AspNetCore.Components](https://www.nuget.org/packages/Microsoft.AspNetCore.Components);</span><span class="sxs-lookup"><span data-stu-id="c2f38-107">[Microsoft.AspNetCore.Components](https://www.nuget.org/packages/Microsoft.AspNetCore.Components)</span></span>
* [<span data-ttu-id="c2f38-108">Microsoft.AspNetCore.Components.Authorization</span><span class="sxs-lookup"><span data-stu-id="c2f38-108">Microsoft.AspNetCore.Components.Authorization</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.Authorization)
* [<span data-ttu-id="c2f38-109">Microsoft.AspNetCore.Components.Forms</span><span class="sxs-lookup"><span data-stu-id="c2f38-109">Microsoft.AspNetCore.Components.Forms</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.Forms)
* <span data-ttu-id="c2f38-110">[Microsoft.AspNetCore.Components.Web](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.Web).</span><span class="sxs-lookup"><span data-stu-id="c2f38-110">[Microsoft.AspNetCore.Components.Web](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.Web)</span></span>
* [<span data-ttu-id="c2f38-111">Microsoft.AspNetCore.Components.WebAssembly</span><span class="sxs-lookup"><span data-stu-id="c2f38-111">Microsoft.AspNetCore.Components.WebAssembly</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly)
* [<span data-ttu-id="c2f38-112">Microsoft.AspNetCore.Components.WebAssembly.Authentication</span><span class="sxs-lookup"><span data-stu-id="c2f38-112">Microsoft.AspNetCore.Components.WebAssembly.Authentication</span></span>](https://www.nuget.org/packages/Microsoft.AspNetCore.Components.WebAssembly.Authentication)
* [<span data-ttu-id="c2f38-113">Microsoft.JSInterop</span><span class="sxs-lookup"><span data-stu-id="c2f38-113">Microsoft.JSInterop</span></span>](https://www.nuget.org/packages/Microsoft.JSInterop)
* [<span data-ttu-id="c2f38-114">Microsoft.JSInterop.WebAssembly</span><span class="sxs-lookup"><span data-stu-id="c2f38-114">Microsoft.JSInterop.WebAssembly</span></span>](https://www.nuget.org/packages/Microsoft.JSInterop.WebAssembly)
* [<span data-ttu-id="c2f38-115">Microsoft.Authentication.WebAssembly.Msal</span><span class="sxs-lookup"><span data-stu-id="c2f38-115">Microsoft.Authentication.WebAssembly.Msal</span></span>](https://www.nuget.org/packages/Microsoft.Authentication.WebAssembly.Msal)

<span data-ttu-id="c2f38-116">Обсуждение этого вопроса см. на странице GitHub [dotnet/aspnetcore#23424](https://github.com/dotnet/aspnetcore/issues/23424).</span><span class="sxs-lookup"><span data-stu-id="c2f38-116">For discussion, see GitHub issue [dotnet/aspnetcore#23424](https://github.com/dotnet/aspnetcore/issues/23424).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="c2f38-117">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="c2f38-117">Version introduced</span></span>

<span data-ttu-id="c2f38-118">5.0 (предварительная версия 7)</span><span class="sxs-lookup"><span data-stu-id="c2f38-118">5.0 Preview 7</span></span>

## <a name="old-behavior"></a><span data-ttu-id="c2f38-119">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="c2f38-119">Old behavior</span></span>

<span data-ttu-id="c2f38-120">В Blazor 3.1 и 3.2 пакеты были предназначены для платформ .NET Standard 2.1 и .NET Core 3.1.</span><span class="sxs-lookup"><span data-stu-id="c2f38-120">In Blazor 3.1 and 3.2, packages target .NET Standard 2.1 and .NET Core 3.1.</span></span>

## <a name="new-behavior"></a><span data-ttu-id="c2f38-121">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="c2f38-121">New behavior</span></span>

<span data-ttu-id="c2f38-122">В ASP.NET Core 5.0 пакеты предназначены для платформы .NET 5.0.</span><span class="sxs-lookup"><span data-stu-id="c2f38-122">In ASP.NET Core 5.0, packages target .NET 5.0.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="c2f38-123">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="c2f38-123">Reason for change</span></span>

<span data-ttu-id="c2f38-124">Эти изменения были внесены в соответствии с требованиями к целевой платформе .NET.</span><span class="sxs-lookup"><span data-stu-id="c2f38-124">The change was made to better align with .NET target framework requirements.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="c2f38-125">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="c2f38-125">Recommended action</span></span>

<span data-ttu-id="c2f38-126">Для проектов Blazor 3.2 WebAssembly следует задавать .NET 5.0 в качестве целевой платформы в рамках обновления ссылок на пакеты до версии 5.x.x.</span><span class="sxs-lookup"><span data-stu-id="c2f38-126">Blazor 3.2 WebAssembly projects should target .NET 5.0 as part of updating their package references to 5.x.x.</span></span> <span data-ttu-id="c2f38-127">Библиотеки, ссылающиеся на эти пакеты, могут быть предназначены для .NET 5.0 или сразу для нескольких платформ в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="c2f38-127">Libraries that reference one of these packages can either target .NET 5.0 or multi-target depending on their requirements.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="c2f38-128">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="c2f38-128">Affected APIs</span></span>

<span data-ttu-id="c2f38-129">Отсутствуют</span><span class="sxs-lookup"><span data-stu-id="c2f38-129">None</span></span>

<!--

### Category

ASP.NET Core

### Affected APIs

Not detectable via API analysis

-->
