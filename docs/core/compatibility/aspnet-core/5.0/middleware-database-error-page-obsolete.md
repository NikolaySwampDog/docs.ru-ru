---
title: 'Критическое изменение. ПО промежуточного слоя: Страница ошибок базы данных помечена как устаревшая'
description: Сведения о критическом изменении в ASP.NET Core 5.0 — ПО промежуточного слоя. Страница ошибок базы данных помечена как устаревшая
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 8bc8852d7fb54b0d558342ee3c69085117512a1a
ms.sourcegitcommit: 089068389671f6f9e15fd67dcbfb0145bf72f1fb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106497623"
---
# <a name="middleware-database-error-page-marked-as-obsolete"></a><span data-ttu-id="e6dca-103">ПО промежуточного слоя: Страница ошибок базы данных помечена как устаревшая</span><span class="sxs-lookup"><span data-stu-id="e6dca-103">Middleware: Database error page marked as obsolete</span></span>

<span data-ttu-id="e6dca-104">[DatabaseErrorPageMiddleware](/dotnet/api/microsoft.aspnetcore.diagnostics.entityframeworkcore.databaseerrorpagemiddleware?view=aspnetcore-3.0) и связанные с ним методы расширения были помечены как устаревшие в ASP.NET Core 5.0.</span><span class="sxs-lookup"><span data-stu-id="e6dca-104">The [DatabaseErrorPageMiddleware](/dotnet/api/microsoft.aspnetcore.diagnostics.entityframeworkcore.databaseerrorpagemiddleware?view=aspnetcore-3.0) and its associated extension methods were marked as obsolete in ASP.NET Core 5.0.</span></span> <span data-ttu-id="e6dca-105">ПО промежуточного слоя и методы расширения будут удалены в ASP.NET Core 6.0.</span><span class="sxs-lookup"><span data-stu-id="e6dca-105">The middleware and extension methods will be removed in ASP.NET Core 6.0.</span></span> <span data-ttu-id="e6dca-106">Эти функции вместо этого будут предоставляться `DatabaseDeveloperPageExceptionFilter` и методами расширения.</span><span class="sxs-lookup"><span data-stu-id="e6dca-106">The functionality will instead be provided by `DatabaseDeveloperPageExceptionFilter` and its extension methods.</span></span>

<span data-ttu-id="e6dca-107">Обсуждение этого вопроса см. на странице GitHub [dotnet/aspnetcore#24987](https://github.com/dotnet/aspnetcore/issues/24987).</span><span class="sxs-lookup"><span data-stu-id="e6dca-107">For discussion, see the GitHub issue at [dotnet/aspnetcore#24987](https://github.com/dotnet/aspnetcore/issues/24987).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="e6dca-108">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="e6dca-108">Version introduced</span></span>

<span data-ttu-id="e6dca-109">5.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="e6dca-109">5.0 RC 1</span></span>

## <a name="old-behavior"></a><span data-ttu-id="e6dca-110">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="e6dca-110">Old behavior</span></span>

<span data-ttu-id="e6dca-111">`DatabaseErrorPageMiddleware` и связанные с ним методы расширения не устарели.</span><span class="sxs-lookup"><span data-stu-id="e6dca-111">`DatabaseErrorPageMiddleware` and its associated extension methods weren't obsolete.</span></span>

## <a name="new-behavior"></a><span data-ttu-id="e6dca-112">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="e6dca-112">New behavior</span></span>

<span data-ttu-id="e6dca-113">`DatabaseErrorPageMiddleware` и связанные с ним методы расширения устарели.</span><span class="sxs-lookup"><span data-stu-id="e6dca-113">`DatabaseErrorPageMiddleware` and its associated extension methods are obsolete.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="e6dca-114">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="e6dca-114">Reason for change</span></span>

<span data-ttu-id="e6dca-115">`DatabaseErrorPageMiddleware` был перенесен в расширяемый API для [страницы со сведениями об исключении для разработчика](/aspnet/core/fundamentals/error-handling#developer-exception-page).</span><span class="sxs-lookup"><span data-stu-id="e6dca-115">`DatabaseErrorPageMiddleware` was migrated to an extensible API for the [developer exception page](/aspnet/core/fundamentals/error-handling#developer-exception-page).</span></span> <span data-ttu-id="e6dca-116">Дополнительные сведения об расширяемых API см. на странице GitHub [dotnet/aspnetcore#8536](https://github.com/dotnet/aspnetcore/issues/8536).</span><span class="sxs-lookup"><span data-stu-id="e6dca-116">For more information on the extensible API, see GitHub issue [dotnet/aspnetcore#8536](https://github.com/dotnet/aspnetcore/issues/8536).</span></span>

## <a name="recommended-action"></a><span data-ttu-id="e6dca-117">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="e6dca-117">Recommended action</span></span>

<span data-ttu-id="e6dca-118">Выполните следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e6dca-118">Complete the following steps:</span></span>

1. <span data-ttu-id="e6dca-119">Не используйте `DatabaseErrorPageMiddleware` в проектах.</span><span class="sxs-lookup"><span data-stu-id="e6dca-119">Stop using `DatabaseErrorPageMiddleware` in your project.</span></span> <span data-ttu-id="e6dca-120">Например, удалите вызов метода `UseDatabaseErrorPage` из `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="e6dca-120">For example, remove the `UseDatabaseErrorPage` method call from `Startup.Configure`:</span></span>

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDatabaseErrorPage();
        }
    }
    ```

1. <span data-ttu-id="e6dca-121">Добавьте в проект страницу со сведениями об исключении для разработчика.</span><span class="sxs-lookup"><span data-stu-id="e6dca-121">Add the developer exception page to your project.</span></span> <span data-ttu-id="e6dca-122">Например, вызовите метод <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage%2A> в `Startup.Configure`.</span><span class="sxs-lookup"><span data-stu-id="e6dca-122">For example, call the <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage%2A> method in `Startup.Configure`:</span></span>

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
    }
    ```

1. <span data-ttu-id="e6dca-123">Добавьте пакет NuGet [Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore) в файл проекта.</span><span class="sxs-lookup"><span data-stu-id="e6dca-123">Add the [Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore) NuGet package to the project file.</span></span>

1. <span data-ttu-id="e6dca-124">Добавьте фильтр исключений страницы со сведениями об исключении для разработчика базы данных в коллекцию служб.</span><span class="sxs-lookup"><span data-stu-id="e6dca-124">Add the database developer page exception filter to the services collection.</span></span> <span data-ttu-id="e6dca-125">Например, вызовите метод `AddDatabaseDeveloperPageExceptionFilter` в `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="e6dca-125">For example, call the `AddDatabaseDeveloperPageExceptionFilter` method in `Startup.ConfigureServices`:</span></span>

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddDatabaseDeveloperPageExceptionFilter();
    }
    ```

## <a name="affected-apis"></a><span data-ttu-id="e6dca-126">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="e6dca-126">Affected APIs</span></span>

- [<span data-ttu-id="e6dca-127">Microsoft.AspNetCore.Builder.DatabaseErrorPageExtensions.UseDatabaseErrorPage</span><span class="sxs-lookup"><span data-stu-id="e6dca-127">Microsoft.AspNetCore.Builder.DatabaseErrorPageExtensions.UseDatabaseErrorPage</span></span>](/dotnet/api/microsoft.aspnetcore.builder.databaseerrorpageextensions.usedatabaseerrorpage?view=aspnetcore-3.0)
- [<span data-ttu-id="e6dca-128">Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore.DatabaseErrorPageMiddleware</span><span class="sxs-lookup"><span data-stu-id="e6dca-128">Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore.DatabaseErrorPageMiddleware</span></span>](/dotnet/api/microsoft.aspnetcore.diagnostics.entityframeworkcore.databaseerrorpagemiddleware?view=aspnetcore-3.0)

<!--

### Category

ASP.NET Core

### Affected APIs

- `Overload:Microsoft.AspNetCore.Builder.DatabaseErrorPageExtensions.UseDatabaseErrorPage`
- `T:Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore.DatabaseErrorPageMiddleware`

-->
