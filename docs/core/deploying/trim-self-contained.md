---
title: Обрезка автономных приложений
description: Сведения об обрезке автономных приложений для уменьшения их размера. .NET Core объединяет среду выполнения с автономно публикуемым приложением и обычно содержит больше компонентов среды выполнения, чем необходимо.
author: jamshedd
ms.author: jamshedd
ms.date: 04/03/2020
ms.openlocfilehash: b5e2650d8240648aa05eaa9026a57b926f63b4de
ms.sourcegitcommit: c7f0beaa2bd66ebca86362ca17d673f7e8256ca6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104872877"
---
# <a name="trim-self-contained-deployments-and-executables"></a>Обрезка автономных развертываний и исполняемых файлов

[Модель развертывания с зависимостью от платформы](index.md#publish-framework-dependent) была наиболее успешной моделью развертывания с момента запуска .NET. При таком сценарии разработчик приложения связывает только приложение и сторонние сборки, ожидая, что среда выполнения .NET и библиотеки платформы будут доступны на клиентском компьютере. Эта модель развертывания продолжает доминировать и в .NET Core, но в некоторых случаях модель, зависящая от платформы, не является оптимальной. Альтернативой является публикация [автономного приложения](index.md#publish-self-contained), в котором среда выполнения и платформа .NET Core объединены вместе с приложением и сборками сторонних производителей.

Автономная модель развертывания — это специализированная версия автономной модели развертывания, оптимизированная для уменьшения размера развертывания. Минимизация размера развертывания является критически важным требованием для некоторых сценариев на стороне клиента, например приложений Blazor. В зависимости от сложности приложения указывается только подмножество сборок платформы, а для запуска приложения требуется подмножество кода в каждой сборке. Неиспользуемые компоненты библиотеки не нужны, поэтому их можно удалить из упакованного приложения.

Однако существует риск того, что анализ времени сборки приложения может вызвать сбои во время выполнения из-за невозможности надежного анализа различных проблемных шаблонов кода (в основном сосредоточенных на использовании отражения). Так как надежность не гарантируется, эта модель развертывания предлагается в качестве предварительной версии.

Модуль анализа времени сборки предупреждает разработчиков шаблонов кода о проблемных шаблонах кода, чтобы можно было определить, какой другой код требуется. Код можно снабдить атрибутами, чтобы указать, что еще следует включить в обрезку. Многие шаблоны отражения можно заменить на создание кода во время сборки с помощью [генераторов кода](https://github.com/dotnet/roslyn/blob/main/docs/features/source-generators.md).

Режим обрезки для приложений настраивается с параметром `TrimMode`. Значение по умолчанию (`copyused`) объединяет сборки, на которые имеются ссылки, с приложением. Значение `link` используется с приложениями WebAssembly Blazor и обрезает неиспользуемый код в сборках. Предупреждения анализа обрезки предоставляют сведения о шаблонах кода, в которых невозможен полный анализ зависимостей. Эти предупреждения подавляются по умолчанию и могут быть включены путем установки флага `SuppressTrimAnalysisWarnings` в значение `false`. Дополнительные сведения о доступных параметрах обрезки см. в разделе [Параметры обрезки](trimming-options.md).

> [!NOTE]
> Обрезка является экспериментальной функцией в .NET Core 3.1 и .NET 5.0. Она доступна _только_ для автономно публикуемых приложений.

## <a name="prevent-assemblies-from-being-trimmed"></a>Исключение сборок из процесса обрезки

В некоторых случаях функции обрезки не удается обнаружить ссылки. Например, если в сборке среды выполнения отражение используется либо приложением, либо библиотекой, на которую ссылается приложение, прямые ссылки на эту сборку отсутствуют. Процессу обрезки неизвестно об этих косвенных ссылках, и он исключит библиотеку из папки опубликованных.

Когда код косвенно ссылается на сборку через отражение, можно исключить сборку из процесса обрезки с помощью параметра `<TrimmerRootAssembly>`. В следующем примере показано исключение сборки с именем `System.Security` из процесса обрезки.

```xml
<ItemGroup>
    <TrimmerRootAssembly Include="System.Security" />
</ItemGroup>
```

### <a name="support-for-ssl-certificates"></a>Поддержка SSL-сертификатов

Если ваше приложение, например приложение ASP.NET Core, загружает SSL-сертификаты, следует предотвратить обрезку сборок, которые помогают при загрузке SSL-сертификатов.

Для ASP.NET Core 3.1 файл проекта можно обновить, включив следующее.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>...</PropertyGroup>
  <!--Include the following for .aspnetcore 3.1-->
  <ItemGroup>
    <TrimmerRootAssembly Include="System.Net" />
    <TrimmerRootAssembly Include="System.Net.Security" />
    <TrimmerRootAssembly Include="System.Security" />
  </ItemGroup>
  ...
</Project>
```

При использовании .NET 5.0 можно обновить файл проекта, включив следующее.

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
 <PropertyGroup>...</PropertyGroup>
 <!--Include the following for .net 5.0-->
 <ItemGroup>
    <TrimmerRootAssembly Include="System.Net.Security" />
    <TrimmerRootAssembly Include="System.Security" />
  </ItemGroup>
  ...
</Project>
```

## <a name="trim-your-app---cli"></a>Обрезка приложения с помощью CLI

Выполните обрезку приложения с помощью команды [dotnet publish](../tools/dotnet-publish.md). При публикации приложения задайте следующие свойства.

- Опубликовать как автономное приложение для конкретной среды выполнения: `-r win-x64`
- Включить обрезку: `/p:PublishTrimmed=true`

В следующем примере показана публикация приложения для Windows в качестве автономного и обрезка выходных данных.

```xml
<PropertyGroup>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PublishTrimmed>true</PublishTrimmed>
</PropertyGroup>
```

В следующем примере приложение публикуется в режиме агрессивной обрезки, в котором неиспользованный код в сборках будет обрезан, а предупреждения об обрезке будут включены.

```xml
<PropertyGroup>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
    <PublishTrimmed>true</PublishTrimmed>
    <TrimMode>link</TrimMode>
    <SuppressTrimAnalysisWarnings>false</SuppressTrimAnalysisWarnings>
</PropertyGroup>
```

Дополнительные сведения см. в статье [Публикация приложений .NET Core с помощью .NET Core CLI](deploy-with-cli.md).

## <a name="trim-your-app---visual-studio"></a>Обрезка приложения с помощью Visual Studio

Visual Studio создает многократно используемые профили публикации, которые управляют процессом публикации приложения.

01. В **обозревателе решений** щелкните правой кнопкой мыши проект, который нужно опубликовать. Выберите команду **Опубликовать…** .

    :::image type="content" source="media/trim-self-contained/visual-studio-solution-explorer.png" alt-text="Обозреватель решений с контекстным меню, где выделен пункт Опубликовать":::

    Если у вас еще нет профиля публикации, следуйте инструкциям по его созданию и выберите **Папка** в качестве типа целевого объекта.

01. Нажмите кнопку **Изменить**.

    :::image type="content" source="media/trim-self-contained/visual-studio-publish-edit-settings.png" alt-text="Профиль публикации Visual Studio с кнопкой Изменить":::

01. В диалоговом окне **Параметры профиля** задайте следующие параметры.

    - Параметру **Режим развертывания** задайте значение **Автономное**.
    - В качестве значения параметра **Целевая среда выполнения** укажите платформу, на которую будет выполнена публикация.
    - Выберите **Обрезать неиспользуемые сборки (в предварительной версии)** .

    Нажмите кнопку **Сохранить**, чтобы сохранить параметры и вернуться в диалоговое окно **Публикация**.

    :::image type="content" source="media/trim-self-contained/visual-studio-publish-properties.png" alt-text="Диалоговое окно параметров профиля с выделенными параметрами для режима развертывания, целевой среды выполнения и обрезки неиспользуемых сборок.":::

01. Чтобы опубликовать обрезанное приложение, нажмите кнопку **Опубликовать**.

Дополнительные сведения см. в статье [Публикация приложений .NET Core с помощью Visual Studio](deploy-with-vs.md).

## <a name="trim-your-app---visual-studio-for-mac"></a>Обрезка приложения с помощью Visual Studio для Mac

В Visual Studio для Mac отсутствует возможность обрезки приложения во время публикации. Вам потребуется вручную опубликовать приложение, выполнив инструкции в разделе [Образка приложения с помощью CLI](#trim-your-app---cli). Дополнительные сведения см. в статье [Публикация приложений .NET Core с помощью .NET Core CLI](deploy-with-cli.md).

## <a name="see-also"></a>См. также

- [Развертывание приложений .NET Core](index.md)
- [Публикация приложений .NET Core с помощью .NET Core CLI](deploy-with-cli.md)
- [Публикация приложений .NET Core с помощью Visual Studio](deploy-with-vs.md)
- [Команда dotnet publish](../tools/dotnet-publish.md)
