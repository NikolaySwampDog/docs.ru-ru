---
title: Предупреждение SYSLIB0010
description: Сведения об устаревших элементах, которые приводят к появлению предупреждения во время компиляции SYSLIB0010.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 824423d58802d4a286bfed98422341097985990f
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2020
ms.locfileid: "94440612"
---
# <a name="syslib0010-unsupported-remoting-apis"></a><span data-ttu-id="e1d17-103">SYSLIB0010. Неподдерживаемые API удаленного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="e1d17-103">SYSLIB0010: Unsupported remoting APIs</span></span>

<span data-ttu-id="e1d17-104">Технология [удаленного взаимодействия .NET](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) является устаревшей, и соответствующая инфраструктура существует только в .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e1d17-104">[.NET remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) is a legacy technology, and the infrastructure exists only in .NET Framework.</span></span> <span data-ttu-id="e1d17-105">Следующие API, связанные с удаленным взаимодействием, помечены как устаревшие, начиная с версии .NET 5.0.</span><span class="sxs-lookup"><span data-stu-id="e1d17-105">The following remoting-related APIs are marked as obsolete, starting in .NET 5.0.</span></span> <span data-ttu-id="e1d17-106">При их использовании во время компиляции создается предупреждение `SYSLIB0010`.</span><span class="sxs-lookup"><span data-stu-id="e1d17-106">Using them in code generates warning `SYSLIB0010` at compile time.</span></span>

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType>

## <a name="workarounds"></a><span data-ttu-id="e1d17-107">Обходные пути</span><span class="sxs-lookup"><span data-stu-id="e1d17-107">Workarounds</span></span>

<span data-ttu-id="e1d17-108">Для взаимодействия с объектами в других приложениях или на других компьютерах рекомендуется использовать WCF или службы RESTFUL на основе HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1d17-108">Consider using WCF or HTTP-based REST services to communicate with objects in other applications or across machines.</span></span> <span data-ttu-id="e1d17-109">Дополнительные сведения см. в разделе [Технологии .NET Framework, недоступные в .NET Core](../porting/net-framework-tech-unavailable.md).</span><span class="sxs-lookup"><span data-stu-id="e1d17-109">For more information, see [.NET Framework technologies unavailable on .NET Core](../porting/net-framework-tech-unavailable.md).</span></span>

[!INCLUDE [suppress-syslib-warning](../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a><span data-ttu-id="e1d17-110">См. также</span><span class="sxs-lookup"><span data-stu-id="e1d17-110">See also</span></span>

- <span data-ttu-id="e1d17-111">[Удаленное взаимодействие .NET](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))</span><span class="sxs-lookup"><span data-stu-id="e1d17-111">[.NET remoting](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))</span></span>