---
title: Структура проекта для приложений Blazor
description: Сведения о сравнении структур проектов ASP.NET Web Forms и Blazor.
author: danroth27
ms.author: daroth
no-loc:
- Blazor
- WebAssembly
ms.date: 11/20/2020
ms.openlocfilehash: ba7113c88db728f30812821deaf7c06a80663d1f
ms.sourcegitcommit: 05d0087dfca85aac9ca2960f86c5efd218bf833f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/30/2021
ms.locfileid: "98189093"
---
# <a name="project-structure-for-blazor-apps"></a>Структура проекта для приложений Blazor

Несмотря на существенные различия в структуре проекта, в ASP.NET Web Forms и Blazor применяются многие схожие концепции. Здесь мы рассмотрим структуру проекта Blazor и сравним ее с проектом ASP.NET Web Forms.

Чтобы создать свое первое приложение Blazor, следуйте инструкциям в статье о [начале работы с Blazor](/aspnet/core/blazor/get-started). Вы можете выполнить инструкции, чтобы создать приложение Blazor Server или приложение Blazor WebAssembly, размещенное в ASP.NET Core. За исключением логики размещения для конкретной модели, большая часть кода в обоих проектах одинакова.

## <a name="project-file"></a>Файл проекта

Приложения Blazor Server — это проекты .NET. Файл проекта для приложения Blazor Server максимально прост:

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

</Project>
```

Файл проекта для приложения Blazor WebAssembly выглядит немного более детальным (конкретные номера версии могут отличаться):

```xml
<Project Sdk="Microsoft.NET.Sdk.BlazorWebAssembly">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly" Version="5.0.0" />
    <PackageReference Include="Microsoft.AspNetCore.Components.WebAssembly.DevServer" Version="5.0.0" PrivateAssets="all" />
    <PackageReference Include="System.Net.Http.Json" Version="5.0.0" />
  </ItemGroup>

</Project>
```

Проект Blazor WebAssembly ориентирован на `Microsoft.NET.Sdk.BlazorWebAssembly` вместо пакета SDK `Microsoft.NET.Sdk.Web`, так как они выполняются в браузере в среде выполнения .NET на основе WebAssembly. Вы не можете установить .NET в веб-браузер, как на сервере или на компьютере разработчика. Следовательно, проект ссылается на платформу Blazor, используя отдельные ссылки на пакеты.

Для сравнения проект ASP.NET Web Forms по умолчанию включает в себя почти 300 строк XML-кода в файле *. CSPROJ*, большинство которых явно задает в проекте различные файлы кода и содержимого. С выпуском `.NET 5` приложения `Blazor Server` и `Blazor WebAssembly` могут легко совместно использовать одну единую среду выполнения.

Отдельные ссылки на сборки, хотя они и поддерживаются, не так сильно распространены в проектах .NET. Большинство зависимостей проектов обрабатываются как ссылки на пакеты NuGet. В проектах .NET требуется ссылаться только на зависимости пакетов верхнего уровня. Транзитивные зависимости включаются автоматически. Вместо того чтобы использовать для ссылок на пакеты файл *packages.config*, который обычно находится в проектах ASP.NET Web Forms, ссылки на пакеты добавляются в файл проекта с помощью элемента `<PackageReference>`.

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
</ItemGroup>
```

## <a name="entry-point"></a>Точка входа

Точка входа приложения Blazor Server определяется в файле *Program.cs*, как реализовано в консольном приложении. При выполнении приложение создает и запускает экземпляр хост-сайта с использованием значений по умолчанию, характерных для веб-приложений. Хост-сайт управляет жизненным циклом приложения Blazor Server и настраивает службы на уровне узла. Примерами таких служб являются конфигурация, ведение журнала, внедрение зависимостей и HTTP-сервер. Этот код в основном является стандартным, и часто его оставляют без изменений.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

Приложения Blazor WebAssembly также определяют точку входа в файле *Program.cs*. Сам код выглядит немного иначе. Этот код аналогичен тому, который настраивает хост приложений для предоставления приложению тех же служб уровня узла. Однако хост приложений WebAssembly не настраивает HTTP-сервер, так как он выполняется непосредственно в браузере.

Приложения Blazor имеют класс `Startup` вместо файла *Global.asax*, чтобы определить логику запуска для приложения. Класс `Startup` используется для настройки приложения и всех связанных с ним служб. В приложении Blazor Server класс `Startup` используется в целях настройки конечной точки для соединения в режиме реального времени, используемого Blazor между клиентскими браузерами и сервером. В приложении Blazor WebAssembly класс `Startup` определяет корневые компоненты приложения и то, где они должны отрисовываться. Мы подробнее рассмотрим класс `Startup` в разделе [Запуск приложения](./app-startup.md).

## <a name="static-files"></a>Статические файлы

В отличие от проектов ASP.NET Web Forms, не все файлы проекта Blazor можно запрашивать как статические файлы. Веб-адресации подлежат только файлы в папке *wwwroot*. Эта папка называется "веб-корнем" приложения. Все, что находится за пределами веб-корня приложения, *не подлежит* веб-адресации. Такая настройка обеспечивает дополнительный уровень безопасности, который предотвращает случайное раскрытие файлов проекта через Интернет.

## <a name="configuration"></a>Конфигурация

Конфигурация в приложениях ASP.NET Web Forms обычно реализуется с помощью одного или нескольких файлов *web.config*. У приложений Blazor файлы *web.config* обычно отсутствуют. В противном случае этот файл используется только для настройки параметров, имеющих отношение к IIS, при размещении в службах IIS. Вместо этого приложения Blazor Server используют абстракции конфигурации ASP.NET Core (сейчас приложения Blazor WebAssembly не поддерживают одни и те же абстракции конфигурации, но эта функция может быть добавлена в будущем). Например, приложение Blazor Server по умолчанию хранит некоторые параметры в *appsettings.json*.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

Дополнительные сведения о конфигурации в проектах ASP.NET Core см. в разделе [Конфигурации](./config.md).

## <a name="razor-components"></a>Компоненты Razor

Большинство файлов в проектах Blazor являются файлами *RAZOR*. Razor — это язык для создания шаблонов на основе HTML и C#, который используется для динамического создания пользовательского веб-интерфейса. Файлы *RAZOR* определяют компоненты, составляющие пользовательский интерфейс приложения. В большинстве случаев компоненты для приложений Blazor Server и Blazor WebAssembly идентичны. Компоненты в Blazor аналогичны пользовательским элементам управления в ASP.NET Web Forms.

Каждый файл компонента Razor компилируется в класс .NET при сборке проекта. Созданный класс захватывает состояние компонента, логику отрисовки, методы жизненного цикла, обработчики событий и другую логику. Мы рассмотрим создание компонентов разделе [Создание компонентов пользовательского интерфейса, пригодных для повторного использования, с помощью Blazor](./components.md).

Файлы *_Imports.razor* не являются файлами компонентов Razor. Вместо этого они определяют набор директив Razor для импорта в другие файлы *RAZOR* в той же папке и вложенных в нее папках. Например, файл *_Imports.razor* представляет собой стандартный способ добавления директив `using` для часто используемых пространств имен:

```razor
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop
@using BlazorApp1
@using BlazorApp1.Shared
```

## <a name="pages"></a>Страницы

Где находятся страницы в приложениях Blazor? Blazor не определяет отдельное расширение файла для адресуемых страниц, например, как файлы *ASPX* в приложениях ASP.NET Web Forms. Вместо этого страницы определяются путем назначения маршрутов компонентам. Маршрут обычно назначается с помощью директивы Razor `@page`. Например, компонент `Counter`, созданный в файле *Pages/Counter.razor*, определяет следующий маршрут:

```razor
@page "/counter"
```

Маршрутизация в Blazor обрабатывается на стороне клиента, а не на сервере. При переходе пользователя в браузере Blazor перехватывает навигацию, а затем отрисовывает компонент с соответствующим маршрутом.

Маршруты компонентов сейчас не выводятся расположением файлов компонента, как это имеет место для страниц *ASPX*. Возможно, мы добавим эту функцию в будущем. Каждый маршрут должен быть указан для компонента явно. Хранение маршрутизируемых компонентов в папке *Pages* не имеет особого значения и является просто соглашением.

Маршрутизацию в Blazor мы более подробно рассмотрим в разделе [Страницы, маршрутизация и макеты](./pages-routing-layouts.md).

## <a name="layout"></a>Layout

В приложениях ASP.NET Web Forms общий макет страницы обрабатывается с использованием эталонных страниц (*Site.Master*). В приложениях Blazor макет страницы обрабатывается с использованием компонентов макета (*Shared/MainLayout.razor*). Компоненты макета будут более подробно рассмотрены в разделе [Страницы, маршрутизация и макеты](./pages-routing-layouts.md).

## <a name="bootstrap-blazor"></a>Начальная загрузка Blazor

Для начальной загрузки Blazor приложение должно:

- указывать, где на странице следует отрисовывать корневой компонент (*App.Razor*);
- добавить соответствующий сценарий платформы Blazor.

В приложении Blazor Server страница узла корневого компонента определена в файле *_Host.cshtml*. Этот файл определяет страницу Razor, а не компонент. Страницы Razor используют синтаксис Razor для определения адресуемой сервером страницы, которая во многом аналогична странице *ASPX*. Метод `Html.RenderComponentAsync<TComponent>(RenderMode)` используется для определения места, где требуется отрисовать компонент корневого уровня. Параметр `RenderMode` указывает способ отрисовки компонента. В следующей таблице указаны поддерживаемые параметры `RenderMode`.

|Параметр                        |Описание       |
|------------------------------|------------------|
|`RenderMode.Server`           |Интерактивная отрисовка после установки соединения с браузером|
|`RenderMode.ServerPrerendered`|Сначала предварительная отрисовка, а затем интерактивная отрисовка.|
|`RenderMode.Static`           |Отрисовка в виде статического содержимого.|

Ссылка сценария на *_framework/blazor.server.js* обеспечивает подключение к серверу в режиме реального времени и последующую обработку всего взаимодействия с пользователем и обновлений пользовательского интерфейса.

```razor
@page "/"
@namespace BlazorApp1.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>BlazorApp1</title>
    <base href="~/" />
    <link rel="stylesheet" href="css/bootstrap/bootstrap.min.css" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>
        @(await Html.RenderComponentAsync<App>(RenderMode.ServerPrerendered))
    </app>

    <script src="_framework/blazor.server.js"></script>
</body>
</html>
```

В приложении Blazor WebAssembly страница узла представляет собой простой статический HTML-файл по пути *wwwroot/index.html*. Элемент `<div>` с идентификатором `app` используется для указания того, где должен быть отрисован корневой компонент.

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>BlazorApp2</title>
    <base href="/" />
    <link href="css/bootstrap/bootstrap.min.css" rel="stylesheet" />
    <link href="css/app.css" rel="stylesheet" />
    <link href="blazor-web.styles.css" rel="stylesheet" />
</head>

<body>
    <div id="app">Loading...</div>

    <div id="blazor-error-ui">
        An unhandled error has occurred.
        <a href="" class="reload">Reload</a>
        <a class="dismiss">🗙</a>
    </div>
    <script src="_framework/blazor.webassembly.js"></script>
</body>

</html>

```

Подлежащий отрисовке корневой компонент указан в методе `Program.Main` приложения с гибкой возможностью регистрации служб посредством внедрения зависимостей. Дополнительные сведения см. в статье [Внедрение зависимостей Blazor ASP.NET Core](/aspnet/core/blazor/fundamentals/dependency-injection?pivots=webassembly).

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        var builder = WebAssemblyHostBuilder.CreateDefault(args);
        builder.RootComponents.Add<App>("#app");

        ....
        ....
    }
}
```

## <a name="build-output"></a>Выходные данные при создании

При сборке проекта Blazor все файлы компонентов и кода Razor компилируются в одну сборку. В отличие от проектов ASP.NET Web Forms, Blazor не поддерживает компиляцию логики пользовательского интерфейса во время выполнения.

## <a name="run-the-app"></a>Запустите приложение

Чтобы запустить приложение Blazor Server, нажмите клавишу `F5` в Visual Studio. Приложения Blazor не поддерживают компиляцию во время выполнения. Чтобы просмотреть результаты изменений разметки кода и компонентов, перестройте и перезапустите приложение с подключенным отладчиком. Если выполнить запуск без подключенного отладчика (`Ctrl+F5`), Visual Studio отслеживает изменения файлов и перезапускает приложение при внесении изменений. Вы вручную обновляете браузер по мере внесения изменений.

Чтобы запустить приложение Blazor WebAssembly, воспользуйтесь одним из перечисленных ниже подходов:

- Запустите клиентский проект непосредственно с помощью сервера разработки.
- Запустите серверный проект при размещении приложения в ASP.NET Core.

Приложения Blazor WebAssembly можно отлаживать как в браузере, так и в Visual Studio. Дополнительные сведения см. в разделе [Отладка ASP.NET Core Blazor WebAssembly](/aspnet/core/blazor/debug).

>[!div class="step-by-step"]
>[Назад](hosting-models.md)
>[Вперед](app-startup.md)
