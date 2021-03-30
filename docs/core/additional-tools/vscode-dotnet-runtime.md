---
title: Средство установки .NET для авторов расширений VS Code
description: Обзор средства установки .NET для авторов расширений, которое представляет собой расширение Visual Studio Code для установки среды выполнения .NET.
author: sfoslund
ms.date: 11/18/2020
ms.openlocfilehash: a372d0cc728956920d013dac9bc0da1bcd3edc0b
ms.sourcegitcommit: c7f0beaa2bd66ebca86362ca17d673f7e8256ca6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "104872994"
---
# <a name="net-install-tool-for-extension-authors"></a><span data-ttu-id="b29fd-103">Средство установки .NET для авторов расширений</span><span class="sxs-lookup"><span data-stu-id="b29fd-103">.NET install tool for extension authors</span></span>

<span data-ttu-id="b29fd-104">[Средство установки .NET для авторов расширений](https://github.com/dotnet/vscode-dotnet-runtime) — это расширение Visual Studio Code, которое позволяет получить среду выполнения .NET специально для разработчиков расширений VS Code.</span><span class="sxs-lookup"><span data-stu-id="b29fd-104">The [.NET install tool for extension authors](https://github.com/dotnet/vscode-dotnet-runtime) is a Visual Studio Code extension that allows acquisition of the .NET runtime specifically for VS Code extension authors.</span></span> <span data-ttu-id="b29fd-105">Это средство предназначено для использования в расширениях, написанных на .NET. Для работы с ним требуется загрузить части расширений (например, языковой сервер) с помощью .NET.</span><span class="sxs-lookup"><span data-stu-id="b29fd-105">This tool is intended to be leveraged in extensions that are written in .NET and require .NET to boot pieces of the extension (for example, a language server).</span></span> <span data-ttu-id="b29fd-106">Расширение не предназначено для непосредственного использования пользователями при установке .NET для разработки.</span><span class="sxs-lookup"><span data-stu-id="b29fd-106">The extension is not intended to be used directly by users to install .NET for development.</span></span>

## <a name="getting-started-extension-authors"></a><span data-ttu-id="b29fd-107">Начало работы. Авторы расширений</span><span class="sxs-lookup"><span data-stu-id="b29fd-107">Getting started: extension authors</span></span>

<span data-ttu-id="b29fd-108">Чтобы убедиться, что средство установки .NET для авторов расширений подходит для вашего сценария, ознакомьтесь с [основными задачами этого расширения](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) на нашей странице GitHub.</span><span class="sxs-lookup"><span data-stu-id="b29fd-108">To ensure that the .NET install tool for extension authors is the right fit for your scenario, start by reviewing the [goals of this extension](https://github.com/dotnet/vscode-dotnet-runtime#goals-acquiring-net-core-for-extensions) on our GitHub page.</span></span>

> [!NOTE]
> <span data-ttu-id="b29fd-109">С помощью этого средства можно установить только среду выполнения .NET. В настоящее время оно не поддерживает установку пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="b29fd-109">This tool can be used to install the .NET runtime only, it currently does not have the capability to install the .NET SDK.</span></span>

<span data-ttu-id="b29fd-110">Убедившись, что средство установки .NET для авторов расширений соответствует вашим требованиям, можете установить зависимость от него в [манифесте расширения](https://code.visualstudio.com/api/references/extension-manifest) и начать использовать команды, предоставляемые в [API VS Code](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command).</span><span class="sxs-lookup"><span data-stu-id="b29fd-110">Once you have verified that the .NET install tool for extension authors fits your needs, you can take a dependency on it in your [extension manifest](https://code.visualstudio.com/api/references/extension-manifest) and begin using the commands we expose with the [VS Code API](https://code.visualstudio.com/api/extension-guides/command#programmatically-executing-a-command).</span></span> <span data-ttu-id="b29fd-111">Список команд, предоставляемых этим расширением, можно найти [на нашей странице GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/main/Documentation/commands.md).</span><span class="sxs-lookup"><span data-stu-id="b29fd-111">You can find the list of commands this extension exposes on our [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/blob/main/Documentation/commands.md).</span></span>

<span data-ttu-id="b29fd-112">Ознакомьтесь с этим [примером расширения](https://github.com/dotnet/vscode-dotnet-runtime/tree/main/sample), чтобы увидеть, как применяются эти инструкции.</span><span class="sxs-lookup"><span data-stu-id="b29fd-112">Check out this [sample extension](https://github.com/dotnet/vscode-dotnet-runtime/tree/main/sample) to see these steps in action.</span></span>

<span data-ttu-id="b29fd-113">Дополнительные примеры см. в следующих разделах с описанием расширений с открытым кодом, которые используют это средство:</span><span class="sxs-lookup"><span data-stu-id="b29fd-113">For more examples, check out these open source extensions that currently leverage this tool:</span></span>

- [<span data-ttu-id="b29fd-114">Средства Azure Resource Manager (ARM) для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b29fd-114">Azure Resource Manager (ARM) Tools for Visual Studio Code</span></span>](https://github.com/microsoft/vscode-azurearmtools)

- [<span data-ttu-id="b29fd-115">Записные книжки для .NET Interactive</span><span class="sxs-lookup"><span data-stu-id="b29fd-115">.NET Interactive Notebooks</span></span>](https://github.com/dotnet/interactive/tree/main/src/dotnet-interactive-vscode)

## <a name="getting-started-end-users"></a><span data-ttu-id="b29fd-116">Начало работы. Пользователи</span><span class="sxs-lookup"><span data-stu-id="b29fd-116">Getting started: end users</span></span>

<span data-ttu-id="b29fd-117">Как правило, пользователю не нужно взаимодействовать со средством установки .NET для авторов расширений.</span><span class="sxs-lookup"><span data-stu-id="b29fd-117">In general, the end user should not need to interact with the .NET install tool for extension authors at all.</span></span> <span data-ttu-id="b29fd-118">Если у вас возникли проблемы с расширением, ознакомьтесь со страницей с инструкциями по [устранению неполадок](https://github.com/dotnet/vscode-dotnet-runtime/blob/main/Documentation/troubleshooting-runtime.md) или сообщите о проблеме на нашей странице [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).</span><span class="sxs-lookup"><span data-stu-id="b29fd-118">If you are having problems with the extension, check out our [troubleshooting page](https://github.com/dotnet/vscode-dotnet-runtime/blob/main/Documentation/troubleshooting-runtime.md) or file an issue on our [GitHub](https://github.com/dotnet/vscode-dotnet-runtime/issues).</span></span>
