---
title: Распределенная трассировка — .NET
description: Общие сведения о распределенной трассировке .NET.
ms.date: 03/15/2021
ms.openlocfilehash: 274a058bf9daf096958813575901e83a3976a3a4
ms.sourcegitcommit: e16315d9f1ff355f55ff8ab84a28915be0a8e42b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/25/2021
ms.locfileid: "105111118"
---
# <a name="net-distributed-tracing"></a>Распределенная трассировка .NET

Распределенная трассировка — это диагностическая методика, помогающая инженерам локализовать сбои и проблемы с производительностью в приложениях, особенно те, которые могут охватывать несколько компьютеров или процессов. Эта методика отслеживает запросы через приложение, сопоставляя работу различных компонентов приложения и отделяя ее от другой работы, которую приложение может выполнять для параллельных запросов. Например, запрос к обычной веб-службе может быть сначала получен подсистемой балансировки нагрузки, а затем передан процессу веб-сервера, который затем выполняет несколько запросов к базе данных. Использование распределенной трассировки позволяет инженерам определить, завершились ли какие-либо из этих шагов со сбоем, сколько времени занял каждый шаг, и потенциально регистрировать сообщения, выданные при выполнении каждого шага.

## <a name="getting-started-for-net-app-developers"></a>Начало работы для разработчиков приложений .NET

Ключевые библиотеки .NET инструментированы для автоматического создания данных распределенной трассировки, но эти сведения необходимо собрать и сохранить, чтобы позже они были доступными для просмотра.
Обычно разработчики приложений выбирают службу телеметрии, где хранятся эти данные трассировки, а затем используют соответствующую библиотеку для передачи данных телеметрии распределенной трассировки в выбранную службу. [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-dotnet/blob/main/docs/trace/getting-started/README.md) — это независимая от поставщика библиотека, поддерживающая несколько служб, [Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/distributed-tracing) — это полнофункциональная служба, предоставляемая корпорацией Майкрософт; кроме того, существует множество высококачественных сторонних поставщиков APM, предоставляющих интегрированные решения .NET.

- [Общие сведения о концепциях распределенной трассировки](distributed-tracing-concepts.md)
- Руководства
  - [Сбор данных распределенных трассировок с помощью Application Insights](distributed-tracing-collection-walkthroughs.md#collect-traces-using-application-insights)
  - [Сбор данных распределенных трассировок с помощью OpenTelemetry](distributed-tracing-collection-walkthroughs.md#collect-traces-using-opentelemetry)
  - [Сбор данных распределенных трассировок с помощью пользовательской логики](distributed-tracing-collection-walkthroughs.md#collect-traces-using-custom-logic)
  - [Добавление настраиваемого инструментирования распределенной трассировки](distributed-tracing-instrumentation-walkthroughs.md)

Для сторонних служб сбора данных телеметрии следуйте инструкциям по установке, предоставленным поставщиком.

## <a name="getting-started-for-net-library-developers"></a>Начало работы для разработчиков библиотек .NET

Библиотекам .NET не нужно заботиться о том, как в конечном итоге собираются данные телеметрии, — только об их создании. Если вы считаете, что разработчики приложений .NET, использующие вашу библиотеку, захотят просматривать выполняемую ею работу в виде подробных данных в распределенной трассировке, следует добавить инструментирование распределенной трассировки для поддержки этого.

- [Общие сведения о концепциях распределенной трассировки](distributed-tracing-concepts.md)
- Руководства
  - [Добавление настраиваемого инструментирования распределенной трассировки](distributed-tracing-instrumentation-walkthroughs.md)
