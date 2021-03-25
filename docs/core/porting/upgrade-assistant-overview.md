---
title: Обзор помощника по обновлению .NET
description: Знакомство со средством "помощник по обновлению .NET", которое помогает переходить с платформы .NET Framework и обновляет проекты до .NET 5.
author: ardalis
ms.date: 03/08/2021
ms.openlocfilehash: c667cfce40d4f740bc23606826eb2a058643b7be
ms.sourcegitcommit: 46cfed35d79d70e08c313b9c664c7e76babab39e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/10/2021
ms.locfileid: "102604779"
---
# <a name="overview-of-the-net-upgrade-assistant"></a>Обзор помощника по обновлению .NET

Возможно, у вас есть приложения, которые сейчас выполняются в .NET Framework, и вы хотите перенести их в .NET 5. Средство "помощник по обновлению .NET" может помочь в этом процессе. В этой статье приводится следующее:

- Обзор помощника по обновлению .NET.
- Установка помощника по обновлению .NET.

## <a name="what-is-the-net-upgrade-assistant"></a>Что такое помощник по обновлению .NET

Помощник по обновлению .NET — это средство командной строки, которое можно запускать для различных приложений платформы .NET Framework. Это средство поможет вам в обновлении приложений .NET Framework до .NET 5. После запуска средства **в большинстве случаев для завершения миграции приложения потребуются дополнительные действия**. Средство включает установку анализаторов, которые могут помочь в завершении миграции.

В настоящее время средство поддерживает следующие типы приложений платформы.NET Framework:

- Приложения .NET Framework Windows Forms
- Приложения .NET Framework WPF
- Приложения .NET Framework ASP.NET MVC
- Консольные приложения .NET Framework
- Библиотеки классов .NET Framework

Помощник по обновлению .NET сейчас находится на этапе предварительного выпуска и часто обновляется. Если вы обнаружили проблемы при использовании этого средства, сообщите о них в [репозитории GitHub](https://github.com/dotnet/upgrade-assistant) средства.

## <a name="how-to-install-the-net-upgrade-assistant"></a>Установка помощника по обновлению .NET

В [руководстве по началу работы](https://aka.ms/dotnet-upgrade-assistant-install) описывается установка и использование помощника по обновлению .NET.

### <a name="prerequisites"></a>Предварительные требования

1. Это средство использует MSBuild для работы с файлами проектов. Убедитесь, что установлена последняя версия MSBuild. Простой способ сделать это — [установить Visual Studio 2019](https://visualstudio.microsoft.com/downloads/).
1. Это средство зависит от [try-convert](https://github.com/dotnet/try-convert). Чтобы помощник выполнялся правильно, необходимо установить средство try-convert для преобразования файлов проекта в новый стиль SDK. Если вы уже установили средство **try-convert**, возможно, потребуется обновить его (**upgrade-assistant** зависит от версии _0.7.212201_ или более поздней).
    1. Для установки try-convert: `dotnet tool install -g try-convert`
    1. Для обновления try-convert: `dotnet tool update -g try-convert`

### <a name="installation-steps"></a>Шаги установки

Помощник можно установить в качестве средства .NET CLI, выполнив следующую команду:

```dotnet
dotnet tool install -g upgrade-assistant
```

Аналогично, поскольку помощник по обновлению .NET устанавливается как средство .NET CLI, его можно легко обновить, выполнив следующую команду:

```dotnet
dotnet tool update -g upgrade-assistant
```

Подробные инструкции по установке см. в файле [README](https://github.com/dotnet/upgrade-assistant) проекта.

## <a name="see-also"></a>См. также раздел

- [Обновление приложения WPF до .NET 5 с помощью помощника по обновлению .NET](upgrade-assistant-wpf-framework.md)
- [Обновление приложения Windows Forms до .NET 5 с помощью помощника по обновлению .NET](upgrade-assistant-winforms-framework.md)
- [Обновление приложения ASP.NET MVC до .NET 5 с помощью помощника по обновлению .NET](upgrade-assistant-aspnetmvc.md)
- [Репозиторий GitHub помощника по обновлению .NET](https://github.com/dotnet/upgrade-assistant)
