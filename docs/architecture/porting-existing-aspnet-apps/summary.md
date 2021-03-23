---
title: Итоги
description: Сводка и набор ключевых выводы для переноса приложений ASP.NET MVC и веб-API 2 в ASP.NET Core.
author: ardalis
ms.date: 12/16/2020
ms.openlocfilehash: 596ab8621008d1cdc16d841e8faede5f4a1fdd16
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2021
ms.locfileid: "102401531"
---
# <a name="summary"></a>Итоги

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

В этой книге были предоставлены ресурсы, необходимые для принятия решения о том, имеет ли смысл переносить существующие приложения ASP.NET, работающие на платформа .NET Framework, в ASP.NET Core. Вы узнали о [важных вопросах, касающихся](migration-considerations.md) выбора, когда имеет смысл перейти на .NET Core, и когда может быть целесообразно хранить (части) приложения на платформа .NET Framework. Существуют различия между версиями .NET Core, их возможностями и совместимостью с платформа .NET Framework, и вы узнали, [как выбрать правильную версию .NET Core для приложения](choose-net-core-version.md).

Перенос большого приложения часто влечет за собой значительное количество рисков и усилий. Вы узнали, как уменьшить этот риск, применяя одну или несколько [стратегий добавочной миграции](incremental-migration-strategies.md) вместе с несколькими [стратегиями развертывания](deployment-strategies.md) для хранения частично перенесенных приложений, выполняющихся в рабочей среде.

Существует множество [архитектурных различий между ASP.NET и ASP.NET Core](architectural-differences.md). В главе 2 вы узнали о многих из этих различий и о том, как они связаны с миграцией приложения. В этой главе рассказывается обо всех возможностях [запуска приложений](app-startup-differences.md) и низкоуровневого по [промежуточного слоя](middleware-modules-handlers.md) на ВЫСОКОуровневые [веб-API](webapi-differences.md) [и новые](controller-differences.md) функции, позволяющие [значительно улучшить сценарии тестирования](testing-differences.md).

Крупные приложения часто состоят из множества проектов и пакетов, а зависимости могут играть основную роль в определении того, насколько проста или сложна миграция. В [главе 3](migrate-large-solutions.md) было рассмотрено, как [определить последовательность миграции проектов](identify-migration-sequence.md) , а [также понять и обновить зависимости приложения](understand-update-dependencies.md). В нем также подробно описаны дополнительные [стратегии по переносу приложений, сохраняя их в рабочей среде](strategies-migrating-in-production.md).

В [главе 4 показано, как было перенесено реальное ASP.NET приложение-образец MVC в ASP.NET Core](example-migration-eshop.md). Эта глава включала подробное разбиение всех изменений, которые были необходимы для использования существующего приложения и переноса его на ASP.NET Core. Если у вас есть определенные вопросы о процессе переноса и некоторые из его более подробных сведений, обратитесь к нему.

Наконец, [глава 5 подробное описание конкретных сценариев развертывания на IIS](deployment-scenarios.md). Вы узнали, как можно использовать существующий веб-сервер IIS для размещения частей приложения, которые были перенесены в ASP.NET Core, сохраняя целостность общедоступных URL-адресов приложения. Службы IIS включают в себя превосходную поддержку переписывания URL-адресов и маршрутизации запросов, которая позволяет размещать несколько версий сайта параллельно или даже на разных серверах, не изменяя общедоступные URL-адреса, предоставляемые приложением.

>[!div class="step-by-step"]
>[Назад](deployment-scenarios.md)