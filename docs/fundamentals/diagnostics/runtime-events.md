---
title: События времени выполнения
description: Проверьте события диагностики, созданные средой выполнения .NET (CoreCLR), которые могут использоваться с ETW, LTTng или Евентпипе.
ms.date: 11/13/2020
ms.topic: reference
helpviewer_keywords:
- runtime events (CoreCLR)
- ETW, EventPipe runtime events (CoreCLR)
ms.openlocfilehash: 33fa7275ce40934ce043b4d0dba5749c37515755
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "96594050"
---
# <a name="net-runtime-events"></a>События среды выполнения .NET

Среда выполнения .NET (CoreCLR) выдает различные события, которые могут использоваться для диагностики проблем с приложением .NET, которые можно использовать с помощью различных механизмов, таких как `ETW` , `LTTng` и `EventPipe` .

Этот документ служит ссылкой на события, запускаемые средой выполнения .NET Core.

Сведения о событиях времени выполнения в .NET Framework см. в разделе [события ETW среды CLR](../../framework/performance/clr-etw-events.md).

## <a name="in-this-section"></a>В этом разделе

[События состязания](runtime-contention-events.md)\
Эти события собираются сведения о конфликтах блокировки монитора.

[События сборки мусора](runtime-garbage-collection-events.md)\
Эти события собирают сведения, относящиеся к сборке мусора. Они помогают в диагностике и отладке, включая определение того, сколько раз выполнялась сборка мусора, сколько памяти было освобождено во время сборки мусора и т. д.

[События исключений](runtime-exception-events.md)\
Эти события времени выполнения захватывают сведения о возникших исключениях.

[События взаимодействия](runtime-interop-events.md)\
Эти события времени выполнения захватывают сведения о создании заглушек на стандартном промежуточном языке (CIL).

[События загрузчика и связывателя](runtime-loader-binder-events.md)\
Эти события собираются сведения, связанные с загрузкой и выгрузкой сборок и модулей.

[События методов](runtime-method-events.md)\
Эти события собирают сведения, связанные с методами. Полезные данные этих событий необходимы для разрешения символов. Кроме того, эти события содержат полезные сведения, например сколько раз вызывался метод.

[События потока](runtime-thread-events.md)\
Эти события собирают сведения о рабочих потоках и потоках ввода-вывода.

[События типа](runtime-type-events.md)\
Эти события собираются сведения о системе типов.