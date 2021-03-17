---
title: Пример миграции на .NET 5
description: Демонстрация миграции примеров приложений, предназначенных для платформы .NET Framework, на .NET 5.
ms.date: 01/19/2021
ms.openlocfilehash: 02a45859dfca891598e235e3de1ed968aefb5bf4
ms.sourcegitcommit: 46cfed35d79d70e08c313b9c664c7e76babab39e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2021
ms.locfileid: "102605169"
---
# <a name="example-of-migrating-to-net"></a><span data-ttu-id="cf277-103">Пример миграции на .NET</span><span class="sxs-lookup"><span data-stu-id="cf277-103">Example of migrating to .NET</span></span>

<span data-ttu-id="cf277-104">В этой главе представлены практические рекомендации, которые помогут выполнить миграцию имеющегося приложения с платформы .NET Framework на .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-104">In this chapter, we present practical guidelines to help you perform a migration of your existing application from .NET Framework to .NET.</span></span>

<span data-ttu-id="cf277-105">Мы представим хорошо структурированный процесс, который вы сможете выполнить, а также наиболее важные моменты, которые следует учитывать на каждом этапе.</span><span class="sxs-lookup"><span data-stu-id="cf277-105">We present a well-structured process you can follow and the most important things to consider on each step.</span></span>

<span data-ttu-id="cf277-106">Затем мы задокументируем пошаговый процесс миграции для примера классического приложения из версий WinForms и WPF.</span><span class="sxs-lookup"><span data-stu-id="cf277-106">We then document a step-by-step migration process for a sample desktop application, both from WinForms and WPF versions.</span></span>

## <a name="migration-process-overview"></a><span data-ttu-id="cf277-107">Общие сведения о процессе миграции</span><span class="sxs-lookup"><span data-stu-id="cf277-107">Migration process overview</span></span>

<span data-ttu-id="cf277-108">Процесс миграции состоит из четырех последовательных шагов:</span><span class="sxs-lookup"><span data-stu-id="cf277-108">The migration process consists of four sequential steps:</span></span>

1. <span data-ttu-id="cf277-109">**Подготовка**. Изучите зависимости, которые проект должен учитывать при дальнейших действиях.</span><span class="sxs-lookup"><span data-stu-id="cf277-109">**Preparation**: Understand the dependencies the project has to have an idea of what's ahead.</span></span> <span data-ttu-id="cf277-110">На этом шаге вы переведете текущий проект в состояние, которое упрощает точку запуска миграции.</span><span class="sxs-lookup"><span data-stu-id="cf277-110">In this step, you take the current project into a state that simplifies the startup point for the migration.</span></span>

2. <span data-ttu-id="cf277-111">**Миграция файла проекта.** В проектах .NET используется новый формат проекта в стиле пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="cf277-111">**Migrate Project File:** .NET projects use the new SDK-style project format.</span></span> <span data-ttu-id="cf277-112">Создайте новый файл проекта с этим форматом или обновите его, чтобы использовать стиль пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="cf277-112">Create a new project file with this format or update the one you have to use the SDK style.</span></span>

3. <span data-ttu-id="cf277-113">**Исправление кода и сборки.** Создайте код в .NET для устранения различий на уровне API между платформой .NET Framework и .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-113">**Fix code and build:** Build the code in .NET addressing API-level differences between .NET Framework and .NET.</span></span> <span data-ttu-id="cf277-114">При необходимости обновите сторонние пакеты до поддерживаемых версий .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-114">If needed, update third-party packages to the ones that support .NET.</span></span>

4. <span data-ttu-id="cf277-115">**Запуск и тестирование.** Могут возникнуть различия, которые не отображаются до времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="cf277-115">**Run and test:** There might be differences that don't show up until run time.</span></span> <span data-ttu-id="cf277-116">Поэтому не забудьте запустить приложение и проверить, чтобы все работало должным образом.</span><span class="sxs-lookup"><span data-stu-id="cf277-116">So, don't forget to run the application and test that everything works as expected.</span></span>

### <a name="preparation"></a><span data-ttu-id="cf277-117">Подготовка</span><span class="sxs-lookup"><span data-stu-id="cf277-117">Preparation</span></span>

#### <a name="migrate-packagesconfig-file"></a><span data-ttu-id="cf277-118">Миграция файла packages.config</span><span class="sxs-lookup"><span data-stu-id="cf277-118">Migrate packages.config file</span></span>

<span data-ttu-id="cf277-119">В приложении .NET Framework все ссылки на внешние пакеты объявляются в файле *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="cf277-119">In a .NET Framework application, all references to external packages are declared in the *packages.config* file.</span></span> <span data-ttu-id="cf277-120">В .NET больше не нужно использовать файл *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="cf277-120">In .NET, there's no longer the need to use the *packages.config* file.</span></span> <span data-ttu-id="cf277-121">Вместо него используйте свойство [PackageReference](../../core/project-sdk/msbuild-props.md#packagereference) в файле проекта, чтобы указать пакеты NuGet для приложения.</span><span class="sxs-lookup"><span data-stu-id="cf277-121">Instead, use the [PackageReference](../../core/project-sdk/msbuild-props.md#packagereference) property inside the project file to specify the NuGet packages for your app.</span></span>

<span data-ttu-id="cf277-122">Поэтому необходимо перейти от одного формата к другому.</span><span class="sxs-lookup"><span data-stu-id="cf277-122">So, you need to transition from one format to another.</span></span> <span data-ttu-id="cf277-123">Обновление можно выполнить вручную, используя зависимости, содержащиеся в файле *packages.config*. Перенесите их в файл проекта в формате `PackageReference`.</span><span class="sxs-lookup"><span data-stu-id="cf277-123">You can do the update manually, taking the dependencies contained in the *packages.config* file and migrating them to the project file with the `PackageReference` format.</span></span> <span data-ttu-id="cf277-124">Вы также можете использовать Visual Studio: щелкните правой кнопкой мыши файл *packages.config* и выберите пункт **Migrate packages.config to PackageReference** (Перенос packages.config в PackageReference).</span><span class="sxs-lookup"><span data-stu-id="cf277-124">Or, you can let Visual Studio do the work for you: right-click on the *packages.config* file and select the **Migrate packages.config to PackageReference** option.</span></span>

#### <a name="verify-every-dependency-compatibility-in-net"></a><span data-ttu-id="cf277-125">Проверка совместимости всех зависимостей в .NET</span><span class="sxs-lookup"><span data-stu-id="cf277-125">Verify every dependency compatibility in .NET</span></span>

<span data-ttu-id="cf277-126">После переноса ссылок на пакеты необходимо проверить каждую ссылку на совместимость.</span><span class="sxs-lookup"><span data-stu-id="cf277-126">Once you've migrated the package references, you must check each reference for compatibility.</span></span> <span data-ttu-id="cf277-127">Изучить зависимости всех пакетов NuGet, используемых вашим приложением, можно на сайте [nuget.org](https://www.nuget.org/). Если пакет имеет зависимости .NET Standard, он будет работать в .NET 5.0, так как .NET [поддерживает](../../standard/net-standard.md#net-implementation-support) все версии .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="cf277-127">You can explore the dependencies of each NuGet package your application is using on [nuget.org](https://www.nuget.org/). If the package has .NET Standard dependencies, then it's going to work on .NET 5.0 because .NET [supports](../../standard/net-standard.md#net-implementation-support) all versions of .NET Standard.</span></span> <span data-ttu-id="cf277-128">На следующем изображении показаны зависимости для пакета `Castle.Windsor`:</span><span class="sxs-lookup"><span data-stu-id="cf277-128">The following image shows the dependencies for the `Castle.Windsor` package:</span></span>

![Снимок экрана зависимостей NuGet для пакета Castle.Windsor](./media/example-migration-core/nuget-dependencies.png)

<span data-ttu-id="cf277-130">Для проверки совместимости пакета можно использовать средство <https://fuget.org>, предоставляющее более подробные сведения о версиях и зависимостях.</span><span class="sxs-lookup"><span data-stu-id="cf277-130">To check the package compatibility, you can use the tool <https://fuget.org> that offers a more detailed information about versions and dependencies.</span></span>

<span data-ttu-id="cf277-131">Возможно, проект ссылается на старые версии пакетов, которые не поддерживают .NET. Вы можете найти более новые версии, поддерживающие платформу.</span><span class="sxs-lookup"><span data-stu-id="cf277-131">Maybe the project is referencing older package versions that don't support .NET, but you might find newer versions that do support it.</span></span> <span data-ttu-id="cf277-132">Поэтому рекомендуется обновить пакеты до более новых версий.</span><span class="sxs-lookup"><span data-stu-id="cf277-132">So, updating packages to newer versions is generally a good recommendation.</span></span> <span data-ttu-id="cf277-133">Однако следует учитывать, что обновление версии пакета может повлечь за собой некоторые критические изменения, которые требуют обновления кода.</span><span class="sxs-lookup"><span data-stu-id="cf277-133">However, you should consider that updating the package version can introduce some breaking changes that would force you to update your code.</span></span>

<span data-ttu-id="cf277-134">Что, если вы не нашли совместимую версию?</span><span class="sxs-lookup"><span data-stu-id="cf277-134">What happens if you don't find a compatible version?</span></span> <span data-ttu-id="cf277-135">Что делать, если вы не хотите обновлять версию пакета из-за этих критических изменений?</span><span class="sxs-lookup"><span data-stu-id="cf277-135">What if you just don't want to update the version of a package because of these breaking changes?</span></span> <span data-ttu-id="cf277-136">Не беспокойтесь, так как приложение .NET может зависеть от пакетов .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cf277-136">Don't worry because it's possible to depend on .NET Framework packages from a .NET application.</span></span> <span data-ttu-id="cf277-137">Обязательно протестируйте сборку, так как она может вызвать ошибки во время выполнения, если внешний пакет вызывает API, недоступный в .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-137">Don't forget to test it extensively because it can cause run-time errors if the external package calls an API that isn't available on .NET.</span></span> <span data-ttu-id="cf277-138">Это отлично подходит для тех случаев, когда вы используете старый пакет, который не будет обновляться, и вы можете просто перенастроить его на работу в .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-138">This is great for when you're using an old package that isn't going to be updated and you can just retarget to work on the .NET.</span></span>

#### <a name="check-for-api-compatibility"></a><span data-ttu-id="cf277-139">Проверка на совместимость API</span><span class="sxs-lookup"><span data-stu-id="cf277-139">Check for API compatibility</span></span>

<span data-ttu-id="cf277-140">Так как поверхность API в платформах .NET Framework и .NET похожа, но не идентична, необходимо проверить, какие интерфейсы API доступны в .NET, а какие нет.</span><span class="sxs-lookup"><span data-stu-id="cf277-140">Since the API surface in .NET Framework and .NET is similar but not identical, you must check which APIs are available on .NET and which aren't.</span></span> <span data-ttu-id="cf277-141">Средство "Анализатор переносимости .NET" можно использовать для отображения API-интерфейсов, отсутствующих в .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-141">You can use the .NET Portability Analyzer tool to surface APIs used that aren't present on .NET.</span></span> <span data-ttu-id="cf277-142">Он просматривает двоичный уровень приложения, извлекает все вызываемые API, а затем выводит список недоступных в целевой платформе интерфейсов API (в данном случае это .NET 5.0).</span><span class="sxs-lookup"><span data-stu-id="cf277-142">It looks at the binary level of your app, extracts all the APIs that are called, and then lists which APIs aren't available on your target framework (.NET 5.0 in this case).</span></span>

<span data-ttu-id="cf277-143">Дополнительные сведения об этом средстве можно найти по адресу:</span><span class="sxs-lookup"><span data-stu-id="cf277-143">You can find more information about this tool at:</span></span>

<https://docs.microsoft.com/dotnet/standard/analyzers/portability-analyzer>

<span data-ttu-id="cf277-144">Интересной особенностью этого средства является то, что оно выявляет лишь отличия от вашего собственного кода, а не кода из внешних пакетов, который невозможно изменить.</span><span class="sxs-lookup"><span data-stu-id="cf277-144">An interesting aspect of this tool is that it only surfaces the differences from your own code and not code from external packages, which you can't change.</span></span> <span data-ttu-id="cf277-145">Помните, что большинство этих пакетов следует обновить для работы с .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-145">Remember you should have updated most of these packages to make them work with .NET.</span></span>

### <a name="migrate-with-try-convert-tool"></a><span data-ttu-id="cf277-146">Миграция с помощью средства Try Convert</span><span class="sxs-lookup"><span data-stu-id="cf277-146">Migrate with Try Convert tool</span></span>

<span data-ttu-id="cf277-147">Средство [Try Convert](https://github.com/dotnet/try-convert/releases) — отличный способ миграции проекта.</span><span class="sxs-lookup"><span data-stu-id="cf277-147">The [Try Convert](https://github.com/dotnet/try-convert/releases) tool is a great way to migrate a project.</span></span> <span data-ttu-id="cf277-148">Это глобальное средство, которое пытается обновить файл проекта со старого стиля до нового стиля пакета SDK и настраивает применимые проекты на работу с .NET 5.</span><span class="sxs-lookup"><span data-stu-id="cf277-148">It's a global tool that attempts to upgrade your project file from the old style to the new SDK style, and retargets applicable projects to .NET 5.</span></span> <span data-ttu-id="cf277-149">После установки можно выполнить следующие команды:</span><span class="sxs-lookup"><span data-stu-id="cf277-149">Once installed, you can run the following commands:</span></span>

```dotnetcli
try-convert -p "<path to your project file>"
```

<span data-ttu-id="cf277-150">Или сделайте так:</span><span class="sxs-lookup"><span data-stu-id="cf277-150">Or:</span></span>

```dotnetcli
try-convert -w "<path to your solution>"
```

> [!NOTE]
> <span data-ttu-id="cf277-151">Средство try-convert запускается автоматически в рамках [помощника по обновлению .NET](https://aka.ms/dotnet-upgrade-assistant).</span><span class="sxs-lookup"><span data-stu-id="cf277-151">The try-convert tool is run automatically as part of the [.NET Upgrade Assistant tool](https://aka.ms/dotnet-upgrade-assistant).</span></span> <span data-ttu-id="cf277-152">Рекомендуется запустить помощник по обновлению, а не просто средство Try Convert.</span><span class="sxs-lookup"><span data-stu-id="cf277-152">Consider running the full Upgrade Assistant and not just Try Convert.</span></span>

<span data-ttu-id="cf277-153">После того как средство предпримет попытку преобразования, перезагрузите файлы в Visual Studio для запуска и тестирования.</span><span class="sxs-lookup"><span data-stu-id="cf277-153">After the tool attempts the conversion, reload your files in Visual Studio to run and test.</span></span> <span data-ttu-id="cf277-154">Существует вероятность неуспешного выполнения попытки преобразования из-за особенностей проекта.</span><span class="sxs-lookup"><span data-stu-id="cf277-154">There's a possibility that Try Convert won't be able to perform the conversion due to the specifics of your project.</span></span> <span data-ttu-id="cf277-155">В этом случае вы можете ознакомиться с приведенными ниже шагами.</span><span class="sxs-lookup"><span data-stu-id="cf277-155">In that case, you can refer the below steps.</span></span>

#### <a name="migrate-manually"></a><span data-ttu-id="cf277-156">Миграция вручную</span><span class="sxs-lookup"><span data-stu-id="cf277-156">Migrate manually</span></span>

1. <span data-ttu-id="cf277-157">Создание проекта .NET</span><span class="sxs-lookup"><span data-stu-id="cf277-157">Create the new .NET project</span></span>

<span data-ttu-id="cf277-158">В большинстве случаев необходимо обновить имеющийся проект до нового формата .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-158">In most cases, you'll want to update your existing project to the new .NET format.</span></span> <span data-ttu-id="cf277-159">Однако можно также создать проект, сохранив старый.</span><span class="sxs-lookup"><span data-stu-id="cf277-159">However, you can also create a new project while maintaining the old one.</span></span> <span data-ttu-id="cf277-160">Основной недостаток обновления старого проекта заключается в том, что вы потеряете поддержку конструктора, которая может быть важной для вас и вашей команды разработчиков.</span><span class="sxs-lookup"><span data-stu-id="cf277-160">The main drawback from updating the old project is that you lose designer support, which may be important to you and your development team.</span></span> <span data-ttu-id="cf277-161">Если вы хотите продолжить работу с конструктором, необходимо создать проект .NET параллельно со старым и совместно использовать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="cf277-161">If you want to keep using the designer, you must create a new .NET project in parallel with the old one and share assets.</span></span> <span data-ttu-id="cf277-162">Если необходимо изменить элементы пользовательского интерфейса в конструкторе, можно переключиться на старый проект, чтобы сделать это.</span><span class="sxs-lookup"><span data-stu-id="cf277-162">If you need to modify UI elements in the designer, you can switch to the old project to do that.</span></span> <span data-ttu-id="cf277-163">Так как ресурсы связаны, они также будут обновлены в проекте .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-163">And since assets are linked, they'll be updated in the .NET project as well.</span></span>

<span data-ttu-id="cf277-164">[Проект в стиле пакета SDK](../../core/project-sdk/msbuild-props.md) для .NET гораздо проще, чем формат проекта платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cf277-164">The [SDK-style project](../../core/project-sdk/msbuild-props.md) for .NET is a lot simpler than .NET Framework's project format.</span></span> <span data-ttu-id="cf277-165">Помимо упомянутых выше записей `PackageReference`, это не будет существенно сложнее.</span><span class="sxs-lookup"><span data-stu-id="cf277-165">Apart from the previously mentioned `PackageReference` entries, you won't need to do much more.</span></span> <span data-ttu-id="cf277-166">Новый формат проекта [содержит файлы с определенными расширениями по умолчанию](../../core/project-sdk/overview.md#default-includes-and-excludes), например файлы `.cs` и `.xaml`. Нет необходимости явно включать их в файл проекта.</span><span class="sxs-lookup"><span data-stu-id="cf277-166">The new project format [includes files with certain extensions by default](../../core/project-sdk/overview.md#default-includes-and-excludes), such as `.cs` and `.xaml` files, without the need to explicitly include them in the project file.</span></span>

#### <a name="assemblyinfo-considerations"></a><span data-ttu-id="cf277-167">Рекомендации по AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="cf277-167">AssemblyInfo considerations</span></span>

<span data-ttu-id="cf277-168">В проектах .NET атрибуты создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="cf277-168">Attributes are autogenerated on .NET projects.</span></span> <span data-ttu-id="cf277-169">Если проект содержит файл *AssemblyInfo.cs*, определения будут дублироваться, что приведет к конфликтам компиляции.</span><span class="sxs-lookup"><span data-stu-id="cf277-169">If the project contains an *AssemblyInfo.cs* file, the definitions will be duplicated, which will cause compilation conflicts.</span></span> <span data-ttu-id="cf277-170">Вы можете удалить старый файл *AssemblyInfo.CS* или отключить автоматическое создание, добавив следующую запись в файл проекта .NET:</span><span class="sxs-lookup"><span data-stu-id="cf277-170">You can delete the older *AssemblyInfo.cs* file or disable autogeneration by adding the following entry to the .NET project file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

#### <a name="resources"></a><span data-ttu-id="cf277-171">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="cf277-171">Resources</span></span>

<span data-ttu-id="cf277-172">Внедренные ресурсы включаются автоматически, но ресурсы — нет, поэтому ресурсы необходимо перенести в новый файл проекта.</span><span class="sxs-lookup"><span data-stu-id="cf277-172">Embedded resources are included automatically but resources aren't, so you need to migrate the resources to the new project file.</span></span>

#### <a name="package-references"></a><span data-ttu-id="cf277-173">Ссылки на пакеты</span><span class="sxs-lookup"><span data-stu-id="cf277-173">Package references</span></span>

<span data-ttu-id="cf277-174">С помощью параметра **Migrate packages.config to PackageReference** (Перенос packages.config в PackageReference) можно легко переместить ссылки на внешние пакеты в новый формат, как упоминалось ранее.</span><span class="sxs-lookup"><span data-stu-id="cf277-174">With the **Migrate packages.config to PackageReference** option, you can easily move your external package references to the new format as previously mentioned.</span></span>

#### <a name="update-package-references"></a><span data-ttu-id="cf277-175">Обновление ссылок на пакеты</span><span class="sxs-lookup"><span data-stu-id="cf277-175">Update package references</span></span>

<span data-ttu-id="cf277-176">Обновите версии совместимых пакетов, как показано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="cf277-176">Update the versions of the packages you've found to be compatible, as shown in the previous section.</span></span>

### <a name="fix-the-code-and-build"></a><span data-ttu-id="cf277-177">Исправление кода и сборки</span><span class="sxs-lookup"><span data-stu-id="cf277-177">Fix the code and build</span></span>

#### <a name="microsoftwindowscompatibility"></a><span data-ttu-id="cf277-178">Microsoft.Windows.Compatibility</span><span class="sxs-lookup"><span data-stu-id="cf277-178">Microsoft.Windows.Compatibility</span></span>

<span data-ttu-id="cf277-179">Если приложение зависит от интерфейсов API, которые недоступны в .NET, таких как реестр, списки ACL или WCF, необходимо включить ссылку на пакет `Microsoft.Windows.Compatibility`, чтобы добавить эти интерфейсы API для Windows.</span><span class="sxs-lookup"><span data-stu-id="cf277-179">If your application depends on APIs that aren't available on .NET, such as Registry, ACLs, or WCF, you have to include a reference to the `Microsoft.Windows.Compatibility` package to add these Windows-specific APIs.</span></span> <span data-ttu-id="cf277-180">Они работают на платформе .NET, но не включены в нее, так как не являются кросс-платформенными.</span><span class="sxs-lookup"><span data-stu-id="cf277-180">They work on .NET but aren't included as they aren't cross-platform.</span></span>

<span data-ttu-id="cf277-181">Существует средство, именуемое анализатором API (<https://docs.microsoft.com/dotnet/standard/analyzers/api-analyzer>), помогающее определить интерфейсы API, которые не совместимы с кодом.</span><span class="sxs-lookup"><span data-stu-id="cf277-181">There's a tool called API Analyzer (<https://docs.microsoft.com/dotnet/standard/analyzers/api-analyzer>) that helps you identify APIs that aren't compatible with your code.</span></span>

#### <a name="use-if-directives"></a><span data-ttu-id="cf277-182">Использование директив \#if</span><span class="sxs-lookup"><span data-stu-id="cf277-182">Use \#if directives</span></span>

<span data-ttu-id="cf277-183">Если требуются разные пути выполнения при нацеливании на платформу .NET Framework и .NET, следует использовать константы компиляции.</span><span class="sxs-lookup"><span data-stu-id="cf277-183">If you need different execution paths when targeting .NET Framework and .NET, you should use compilation constants.</span></span> <span data-ttu-id="cf277-184">Добавьте в код несколько директив \#if, чтобы иметь одинаковую базу кода для обеих целей.</span><span class="sxs-lookup"><span data-stu-id="cf277-184">Add some \#if directives to your code to keep the same code base for both targets.</span></span>

#### <a name="technologies-not-available-on-net"></a><span data-ttu-id="cf277-185">Технологии, недоступные в .NET</span><span class="sxs-lookup"><span data-stu-id="cf277-185">Technologies not available on .NET</span></span>

<span data-ttu-id="cf277-186">Некоторые технологии недоступны в .NET, например:</span><span class="sxs-lookup"><span data-stu-id="cf277-186">Some technologies aren't available on .NET, such as:</span></span>

* <span data-ttu-id="cf277-187">Домены приложений</span><span class="sxs-lookup"><span data-stu-id="cf277-187">AppDomains</span></span>
* <span data-ttu-id="cf277-188">Удаленное взаимодействие</span><span class="sxs-lookup"><span data-stu-id="cf277-188">Remoting</span></span>
* <span data-ttu-id="cf277-189">Управление доступом для кода</span><span class="sxs-lookup"><span data-stu-id="cf277-189">Code Access Security</span></span>
* <span data-ttu-id="cf277-190">Сервер WCF</span><span class="sxs-lookup"><span data-stu-id="cf277-190">WCF Server</span></span>
* <span data-ttu-id="cf277-191">Рабочий процесс Windows</span><span class="sxs-lookup"><span data-stu-id="cf277-191">Windows Workflow</span></span>

<span data-ttu-id="cf277-192">Именно поэтому необходимо найти замену этих технологий, если вы используете их в своем приложении.</span><span class="sxs-lookup"><span data-stu-id="cf277-192">That's why you need to find a replacement for these technologies if you're using them in your application.</span></span> <span data-ttu-id="cf277-193">Дополнительные сведения см. в статье [Технологии .NET Framework, недоступные в .NET Core и .NET 5 и более поздних версий](../../core/porting/net-framework-tech-unavailable.md).</span><span class="sxs-lookup"><span data-stu-id="cf277-193">For more information, see the [.NET Framework technologies unavailable on .NET Core and .NET 5+](../../core/porting/net-framework-tech-unavailable.md) article.</span></span>

#### <a name="regenerate-autogenerated-clients"></a><span data-ttu-id="cf277-194">Повторное создание автоматически созданных клиентов</span><span class="sxs-lookup"><span data-stu-id="cf277-194">Regenerate autogenerated clients</span></span>

<span data-ttu-id="cf277-195">Если приложение использует автоматически созданный код, например клиент WCF, может потребоваться повторно создать этот код для .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-195">If your application uses autogenerated code, such as a WCF client, you may need to regenerate this code to target .NET.</span></span> <span data-ttu-id="cf277-196">Иногда можно найти некоторые отсутствующие ссылки, так как они могут быть не включены в набор сборок .NET по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf277-196">Sometimes, you can find some missing references since they may not be included as part of the default .NET assemblies set.</span></span> <span data-ttu-id="cf277-197">С помощью такого средства как <https://apisof.net/> можно легко найти сборку, в которой находится отсутствующая ссылка, и добавить ее из NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf277-197">Using a tool like <https://apisof.net/>, you can easily locate the assembly the missing reference lives in and add it from NuGet.</span></span>

#### <a name="rolling-back-package-versions"></a><span data-ttu-id="cf277-198">Откат версий пакета</span><span class="sxs-lookup"><span data-stu-id="cf277-198">Rolling back package versions</span></span>

<span data-ttu-id="cf277-199">Как мы уже упоминали, лучше обновить каждую версию пакета, чтобы она была совместима с .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-199">As a general rule, we've previously stated that you better update every single package version to be compatible with .NET.</span></span> <span data-ttu-id="cf277-200">Однако вы можете обнаружить, что нацеливание на обновленную и совместимую версию сборки просто нецелесообразно.</span><span class="sxs-lookup"><span data-stu-id="cf277-200">However, you can find that targeting an updated and compatible version of an assembly just doesn't pay off.</span></span> <span data-ttu-id="cf277-201">Если стоимость изменения не является приемлемой, можно рассмотреть возможность отката версий пакета с сохранением тех, которые используются на платформе .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="cf277-201">If the cost of change isn't acceptable, you can consider rolling back package versions keeping the ones you use on .NET Framework.</span></span> <span data-ttu-id="cf277-202">Хотя они и не предназначены для .NET, они должны работать, если не вызывают некоторые неподдерживаемые API.</span><span class="sxs-lookup"><span data-stu-id="cf277-202">Although they may not be targeting .NET, they should work well unless they call some unsupported APIs.</span></span>

### <a name="run-and-test"></a><span data-ttu-id="cf277-203">Запуск и тестирование</span><span class="sxs-lookup"><span data-stu-id="cf277-203">Run and test</span></span>

<span data-ttu-id="cf277-204">После создания приложения без ошибок можно запустить последний шаг миграции, проверив все функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="cf277-204">Once you have your application building with no errors, you can start the last step of the migration by testing every functionality.</span></span>

<span data-ttu-id="cf277-205">На этом заключительном этапе может возникнуть несколько различных проблем в зависимости от сложности приложения и используемых зависимостей и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="cf277-205">In this final step, you can find several different issues depending on the complexity of your application and the dependencies and APIs you're using.</span></span>

<span data-ttu-id="cf277-206">Например, при использовании файлов конфигурации (*app.config*) могут возникнуть ошибки во время выполнения, например отсутствие разделов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cf277-206">For example, if you use configuration files (*app.config*), you may find some errors at run time like Configuration Sections not present.</span></span> <span data-ttu-id="cf277-207">Использование пакета NuGet `Microsoft.Extensions.Configuration` должно исправить эту ошибку.</span><span class="sxs-lookup"><span data-stu-id="cf277-207">Using the `Microsoft.Extensions.Configuration` NuGet package should fix that error.</span></span>

<span data-ttu-id="cf277-208">Другой причиной ошибок является использование методов `BeginInvoke` и `EndInvoke`, так как они не поддерживаются в .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-208">Another reason for errors is the use of the `BeginInvoke` and `EndInvoke` methods because they aren't supported on .NET.</span></span> <span data-ttu-id="cf277-209">Они не поддерживаются в .NET, так как имеют зависимость от удаленного взаимодействия, которое не существует в .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-209">They aren't supported on .NET because they have a dependency on Remoting, which doesn't exist on .NET.</span></span> <span data-ttu-id="cf277-210">Чтобы решить эту проблему, попробуйте использовать ключевое слово `await` (если доступно) или метод <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="cf277-210">To solve this issue, try to use the `await` keyword (when available) or the <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> method.</span></span>

<span data-ttu-id="cf277-211">Анализаторы совместимости можно использовать для выявления интерфейсов API и шаблонов кода в коде, которые могут вызывать проблемы во время выполнения с помощью .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-211">You can use compatibility analyzers to let you identify APIs and code patterns in your code that can potentially cause problems at run time with .NET.</span></span> <span data-ttu-id="cf277-212">Перейдите на страницу <https://github.com/dotnet/platform-compat> и используйте анализатор API .NET для своего проекта.</span><span class="sxs-lookup"><span data-stu-id="cf277-212">Go to <https://github.com/dotnet/platform-compat> and use the .NET API analyzer on your project.</span></span>

## <a name="migrating-a-windows-forms-application"></a><span data-ttu-id="cf277-213">Миграция приложения Windows Forms</span><span class="sxs-lookup"><span data-stu-id="cf277-213">Migrating a Windows Forms application</span></span>

<span data-ttu-id="cf277-214">Чтобы продемонстрировать полный процесс миграции приложения Windows Forms, мы решили перенести пример приложения eShop, доступного по адресу <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopLegacyNTier/src/eShopWinForms>.</span><span class="sxs-lookup"><span data-stu-id="cf277-214">To showcase a complete migration process of a Windows Forms application, we've chosen to migrate the eShop sample application available at <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopLegacyNTier/src/eShopWinForms>.</span></span> <span data-ttu-id="cf277-215">Полный результат миграции можно найти по адресу <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopModernizedNTier/src/eShopWinForms>.</span><span class="sxs-lookup"><span data-stu-id="cf277-215">You can find the complete result of the migration at <https://github.com/dotnet-architecture/eShopModernizing/tree/master/eShopModernizedNTier/src/eShopWinForms>.</span></span>

<span data-ttu-id="cf277-216">Это приложение показывает каталог продуктов и позволяет пользователю перемещаться по ним, фильтровать их и выполнять поиск.</span><span class="sxs-lookup"><span data-stu-id="cf277-216">This application shows a product catalog and allows the user to navigate, filter, and search for products.</span></span> <span data-ttu-id="cf277-217">С точки зрения архитектуры, приложение использует внешнюю службу WCF, которая служит интерфейсом для серверной базы данных.</span><span class="sxs-lookup"><span data-stu-id="cf277-217">From an architecture point of view, the app relies on an external WCF service that serves as a façade to a back-end database.</span></span>

<span data-ttu-id="cf277-218">Главное окно приложения можно увидеть на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="cf277-218">You can see the main application window in the following picture:</span></span>

![Главное окно приложения](./media/example-migration-core/main-application-window.png)

<span data-ttu-id="cf277-220">Открыв файл проекта *.csproj*, вы увидите примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="cf277-220">If you open the *.csproj* project file, you can see something like this:</span></span>

![Снимок экрана содержимого файла csproj](./media/example-migration-core/csproj-file.png)

<span data-ttu-id="cf277-222">Как упоминалось ранее, проект .NET имеет более компактный стиль, поэтому необходимо перенести структуру проекта в новый стиль пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-222">As previously mentioned, .NET project has a more compact style and you need to migrate the project structure to the new .NET SDK style.</span></span>

<span data-ttu-id="cf277-223">В Обозревателе решений щелкните правой кнопкой мыши проект Windows Forms и выберите **Выгрузить проект** > **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="cf277-223">In the Solution Explorer, right click on the Windows Forms project and select **Unload Project** > **Edit**.</span></span>

<span data-ttu-id="cf277-224">Теперь можно обновить файл .csproj.</span><span class="sxs-lookup"><span data-stu-id="cf277-224">Now you can update the .csproj file.</span></span> <span data-ttu-id="cf277-225">Удалите все содержимое, заменив его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cf277-225">You'll delete the entire content and replace it with the following code:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="cf277-226">Сохраните и перезагрузите проект.</span><span class="sxs-lookup"><span data-stu-id="cf277-226">Save and reload the project.</span></span> <span data-ttu-id="cf277-227">Теперь обновление файла проекта завершено и проект нацелен на .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-227">You're now done updating the project file and the project is targeting the .NET.</span></span>

<span data-ttu-id="cf277-228">Скомпилировав проект на этом этапе, вы обнаружите некоторые ошибки, связанные со ссылкой на клиент WCF.</span><span class="sxs-lookup"><span data-stu-id="cf277-228">If you compile the project at this point, you'll find some errors related to the WCF client reference.</span></span> <span data-ttu-id="cf277-229">Поскольку этот код создается автоматически, его необходимо создать заново для .NET.</span><span class="sxs-lookup"><span data-stu-id="cf277-229">Since this code is autogenerated, you must regenerate it to target .NET.</span></span>

![Список ошибок в Visual Studio](./media/example-migration-core/winforms-compilation-errors.png)

<span data-ttu-id="cf277-231">Удалите файл *Reference.cs* и создайте клиент службы.</span><span class="sxs-lookup"><span data-stu-id="cf277-231">Delete the *Reference.cs* file and generate a new Service Client.</span></span>

<span data-ttu-id="cf277-232">Щелкните правой кнопкой мыши **Подключенные службы** и выберите пункт **Добавить подключенную службу**.</span><span class="sxs-lookup"><span data-stu-id="cf277-232">Right-click on **Connected Services** and select the **Add Connected Service** option.</span></span>

![Снимок экрана меню "Подключенные службы" с выбранным параметром "Добавить подключенную службу"](./media/example-migration-core/add-connected-service.png)

<span data-ttu-id="cf277-234">Откроется окно "Подключенные службы".</span><span class="sxs-lookup"><span data-stu-id="cf277-234">The Connected Services window opens.</span></span> <span data-ttu-id="cf277-235">Выберите параметр **Microsoft WCF Web Service**.</span><span class="sxs-lookup"><span data-stu-id="cf277-235">Select the **Microsoft WCF Web Service** option.</span></span>

![Снимок экрана окна "Подключенные службы"](./media/example-migration-core/connected-services-window.png)

<span data-ttu-id="cf277-237">Если у вас есть служба WCF в том же решении, что и в этом примере, вместо указания URL-адреса службы можно выбрать параметр **Обнаружение**.</span><span class="sxs-lookup"><span data-stu-id="cf277-237">If you have the WCF Service in the same solution as we have in this example, you can select the **Discover** option instead of specifying a service URL.</span></span>

![Снимок экрана окна "Настройка ссылки на веб-службу WCF"](./media/example-migration-core/configure-wcf-reference.png)

<span data-ttu-id="cf277-239">После обнаружения службы средство отражает контракт API, реализованный службой.</span><span class="sxs-lookup"><span data-stu-id="cf277-239">Once the service is located, the tool reflects the API contract implemented by the service.</span></span> <span data-ttu-id="cf277-240">Измените имя пространства имен на `eShopServiceReference`, как показано на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="cf277-240">Change the name of the namespace to be `eShopServiceReference` as shown in the following image:</span></span>

![Снимок экрана изменение пространства имен и контракта API](./media/example-migration-core/api-contract-namespace.png)

<span data-ttu-id="cf277-242">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="cf277-242">Select the **Finish** button.</span></span> <span data-ttu-id="cf277-243">Через некоторое время отобразится созданный код.</span><span class="sxs-lookup"><span data-stu-id="cf277-243">After a while, you'll see the generated code.</span></span>

<span data-ttu-id="cf277-244">Вы должны увидеть три автоматически созданных файла:</span><span class="sxs-lookup"><span data-stu-id="cf277-244">You should see three autogenerated files:</span></span>

1. <span data-ttu-id="cf277-245">*Getting Started*: ссылка на GitHub с информацией о WCF.</span><span class="sxs-lookup"><span data-stu-id="cf277-245">*Getting Started*: a link to GitHub to provide some information on WCF.</span></span>
2. <span data-ttu-id="cf277-246">*ConnectedService.json*: параметры конфигурации для подключения к службе.</span><span class="sxs-lookup"><span data-stu-id="cf277-246">*ConnectedService.json*: configuration parameters to connect to the service.</span></span>
3. <span data-ttu-id="cf277-247">*Reference.cs*: фактический код клиента WCF.</span><span class="sxs-lookup"><span data-stu-id="cf277-247">*Reference.cs*: the actual WCF client code.</span></span>

![Снимок экрана окна обозревателя решений с тремя автоматически созданными файлами](./media/example-migration-core/autogenerated-files.png)

<span data-ttu-id="cf277-249">При повторной компиляции отобразится множество ошибок, поступающих из файлов *.cs* в папку *Helper*.</span><span class="sxs-lookup"><span data-stu-id="cf277-249">If you compile again, you'll see many errors coming from *.cs* files inside the *Helper* folder.</span></span> <span data-ttu-id="cf277-250">Эта папка присутствовала в версии .NET Framework, но не была включена в старую версию файла *.csproj*.</span><span class="sxs-lookup"><span data-stu-id="cf277-250">This folder was present in the .NET Framework version but not included in the old *.csproj*.</span></span> <span data-ttu-id="cf277-251">Однако при использовании нового проекта в стиле пакета SDK каждый файл кода, который находится под расположением файла проекта, включается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf277-251">But with the new SDK-style project, every code file present underneath the project file location is included by default.</span></span> <span data-ttu-id="cf277-252">То есть новый проект .NET Core пытается скомпилировать файлы в папке *Helper*.</span><span class="sxs-lookup"><span data-stu-id="cf277-252">That is, the new .NET Core project tries to compile the files inside the *Helper* folder.</span></span> <span data-ttu-id="cf277-253">Так как эта папка не требуется, ее можно безопасно удалить.</span><span class="sxs-lookup"><span data-stu-id="cf277-253">Since that folder isn't needed, you can safely delete it.</span></span>

<span data-ttu-id="cf277-254">Если скомпилировать проект еще раз и выполнить его, образы продукта не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="cf277-254">If you compile the project again and execute it, you won't see the product images.</span></span> <span data-ttu-id="cf277-255">Проблема заключается в том, что теперь путь к файлам немного изменился.</span><span class="sxs-lookup"><span data-stu-id="cf277-255">The problem is that now the path to the files has slightly changed.</span></span> <span data-ttu-id="cf277-256">Чтобы устранить эту проблему, добавьте в путь другой уровень глубины, обновив в файле `CatalogView.cs` строку:</span><span class="sxs-lookup"><span data-stu-id="cf277-256">To fix this issue, you need to add another level of depth in the path, updating in the file `CatalogView.cs` the line:</span></span>

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

<span data-ttu-id="cf277-257">значение</span><span class="sxs-lookup"><span data-stu-id="cf277-257">to</span></span>

```csharp
string image_name = Environment.CurrentDirectory + "\\..\\..\\..\\Assets\\Images\\Catalog\\" + catalogItems.Picturefilename;
```

<span data-ttu-id="cf277-258">Внеся это изменение, проверьте, чтобы приложение запускалось и работало в .NET Core должным образом.</span><span class="sxs-lookup"><span data-stu-id="cf277-258">After this change, you can check that the application launches and runs as expected on .NET Core.</span></span>

## <a name="migrating-a-wpf-application"></a><span data-ttu-id="cf277-259">Миграция приложения WPF</span><span class="sxs-lookup"><span data-stu-id="cf277-259">Migrating a WPF application</span></span>

<span data-ttu-id="cf277-260">Для выполнения миграции мы будем использовать пример приложения `Shop.ClassicWPF`.</span><span class="sxs-lookup"><span data-stu-id="cf277-260">We'll use the `Shop.ClassicWPF` sample application to perform the migration.</span></span> <span data-ttu-id="cf277-261">На следующем изображении показан снимок экрана приложения перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="cf277-261">The following image shows a screenshot of the app before migration:</span></span>

![Пример приложения перед миграцией](./media/example-migration-core/app-before-migration.png)

<span data-ttu-id="cf277-263">Это приложение использует локальную базу данных SQL Server Express для хранения сведений о каталоге продуктов.</span><span class="sxs-lookup"><span data-stu-id="cf277-263">This application uses a local SQL Server Express database to hold the product catalog information.</span></span> <span data-ttu-id="cf277-264">Доступ к этой базе данных осуществляется непосредственно из приложения WPF.</span><span class="sxs-lookup"><span data-stu-id="cf277-264">This database is accessed directly from the WPF application.</span></span>

<span data-ttu-id="cf277-265">Сначала необходимо обновить файл *.csproj* до нового стиля пакета SDK, используемого приложениями .NET Core.</span><span class="sxs-lookup"><span data-stu-id="cf277-265">First, you must update the *.csproj* file to the new SDK style used by .NET Core applications.</span></span> <span data-ttu-id="cf277-266">Выполните те же действия, которые описаны в разделе о миграции Windows Forms: выгрузите проект, откройте файл *.csproj*, обновите его содержимое и перезагрузите проект.</span><span class="sxs-lookup"><span data-stu-id="cf277-266">You'll follow the same steps described in the Windows Forms migration: you'll unload the project, open the *.csproj* file, update its contents, and reload the project.</span></span>

<span data-ttu-id="cf277-267">В этом случае удалите все содержимое файла *.csproj* и замените его следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="cf277-267">In this case, delete all the content of the *.csproj* file and replace it with the following code:</span></span>

```xml
 <Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net5.0-windows</TargetFramework>
    <UseWpf>true</UseWpf>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="cf277-268">Если перезагрузить проект и скомпилировать его, отобразится следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="cf277-268">If you reload the project and compile it, you'll get the following error:</span></span>

![Список ошибок в Visual Studio, в котором отображается единственная ошибка CS0234](./media/example-migration-core/wpf-compilation-error.png)

<span data-ttu-id="cf277-270">Удалив все содержимое файла *.csproj*, вы потеряли спецификацию ссылок на проект, присутствующую в старом проекте.</span><span class="sxs-lookup"><span data-stu-id="cf277-270">Since you've deleted all the *.csproj* contents, you've lost a project reference specification present in the old project.</span></span> <span data-ttu-id="cf277-271">Необходимо просто добавить эту строку в файл *.csproj*, чтобы включить ссылку на проект.</span><span class="sxs-lookup"><span data-stu-id="cf277-271">You just need to add this line to the *.csproj* file to include the project reference back:</span></span>

```xml
<ItemGroup>
    <ProjectReference Include="..\\eShop.SqlProvider\\eShop.SqlProvider.csproj" />
<ItemGroup>
```

<span data-ttu-id="cf277-272">Кроме того, для этого можно использовать Visual Studio, щелкнув правой кнопкой мыши узел **Зависимости** и выбрав пункт **Добавить ссылку на проект**.</span><span class="sxs-lookup"><span data-stu-id="cf277-272">You can also let Visual Studio help you by right-clicking on the **Dependencies** node and selecting **Add Project Reference**.</span></span> <span data-ttu-id="cf277-273">Выберите проект из решения и нажмите кнопку **ОК**:</span><span class="sxs-lookup"><span data-stu-id="cf277-273">Select the project from the solution and click **OK**:</span></span>

![Снимок экрана диалогового окна "Диспетчер ссылок" с выбранным проектом eShop.SqlProvider](./media/example-migration-core/reference-manager.png)

<span data-ttu-id="cf277-275">После добавления отсутствующей ссылки на проект приложение компилируется и запускается в .NET должным образом.</span><span class="sxs-lookup"><span data-stu-id="cf277-275">Once you add the missing project reference, the application compiles and runs as expected on .NET.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="cf277-276">[Назад](windows-migration.md)
>[Вперед](deploy-modern-applications.md)</span><span class="sxs-lookup"><span data-stu-id="cf277-276">[Previous](windows-migration.md)
[Next](deploy-modern-applications.md)</span></span>
