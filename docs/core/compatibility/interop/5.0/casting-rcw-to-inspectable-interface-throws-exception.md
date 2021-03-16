---
title: Критическое изменение. Приведение RCW к `InterfaceIsIInspectable` создает исключение
description: Узнайте о критических изменениях взаимодействия в .NET 5, где приведение RCW к интерфейсу `InterfaceIsIInspectable` создает исключение PlatformNotSupportedException.
ms.date: 09/13/2020
ms.openlocfilehash: 9f777ee9396f7822c9ff6bf5209021c07b8b618a
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102256638"
---
# <a name="casting-rcw-to-an-interfaceisiinspectable-interface-throws-platformnotsupportedexception"></a><span data-ttu-id="02ee0-103">Приведение вызываемой оболочки времени выполнения к интерфейсу `InterfaceIsIInspectable` вызывает исключение PlatformNotSupportedException</span><span class="sxs-lookup"><span data-stu-id="02ee0-103">Casting RCW to an `InterfaceIsIInspectable` interface throws PlatformNotSupportedException</span></span>

<span data-ttu-id="02ee0-104">Приведение вызываемой оболочки времени выполнения (RCW) к интерфейсу, помеченному как <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>, теперь вызывает исключение <xref:System.PlatformNotSupportedException>.</span><span class="sxs-lookup"><span data-stu-id="02ee0-104">Casting a runtime callable wrapper (RCW) to an interface marked as <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> now throws a <xref:System.PlatformNotSupportedException>.</span></span> <span data-ttu-id="02ee0-105">Это изменение соответствует [удалению поддержки WinRT из .NET](built-in-support-for-winrt-removed.md).</span><span class="sxs-lookup"><span data-stu-id="02ee0-105">This change is a follow up to the [removal of WinRT support from .NET](built-in-support-for-winrt-removed.md).</span></span>

## <a name="version-introduced"></a><span data-ttu-id="02ee0-106">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="02ee0-106">Version introduced</span></span>

<span data-ttu-id="02ee0-107">5.0 RC2</span><span class="sxs-lookup"><span data-stu-id="02ee0-107">5.0 RC2</span></span>

## <a name="change-description"></a><span data-ttu-id="02ee0-108">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="02ee0-108">Change description</span></span>

<span data-ttu-id="02ee0-109">В версиях от .NET до .NET 5 (предварительная версия 6) приведение RCW к интерфейсу, помеченному как <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>, работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="02ee0-109">In .NET versions prior to .NET 5 preview 6, casting an RCW to an interface marked as <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> works as expected.</span></span> <span data-ttu-id="02ee0-110">В версиях .NET 5 (предварительные версии 6–8 и RC1) можно успешно привести RCW к интерфейсу <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>.</span><span class="sxs-lookup"><span data-stu-id="02ee0-110">In .NET 5 previews 6-8 and RC1, you can successfully cast an RCW to an <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> interface.</span></span> <span data-ttu-id="02ee0-111">Однако при выполнении методов в интерфейсе могут возникнуть нарушения прав доступа, так как базовая поддержка в среде выполнения [была удалена в .NET 5 (предварительная версия 6)](built-in-support-for-winrt-removed.md).</span><span class="sxs-lookup"><span data-stu-id="02ee0-111">However, you might get access violations when you execute methods on the interface, because the underlying support in the runtime [was removed in .NET 5 preview 6](built-in-support-for-winrt-removed.md).</span></span>

<span data-ttu-id="02ee0-112">В .NET 5 RC2 и более поздних версиях приведение RCW к интерфейсу, помеченному как <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>, вызывает исключение <xref:System.PlatformNotSupportedException> во время приведения.</span><span class="sxs-lookup"><span data-stu-id="02ee0-112">In .NET 5 RC2 and later versions, casting an RCW to an interface marked as <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> throws a <xref:System.PlatformNotSupportedException> at cast time.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="02ee0-113">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="02ee0-113">Reason for change</span></span>

<span data-ttu-id="02ee0-114">Поддержка <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> была [удалена в предыдущей предварительной версии .NET 5](built-in-support-for-winrt-removed.md).</span><span class="sxs-lookup"><span data-stu-id="02ee0-114">The support for <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> was [removed in a previous .NET 5 preview](built-in-support-for-winrt-removed.md).</span></span> <span data-ttu-id="02ee0-115">Однако приведение к интерфейсу <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> было пропущено по ошибке.</span><span class="sxs-lookup"><span data-stu-id="02ee0-115">However, casting to an <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> interface was accidentally overlooked.</span></span> <span data-ttu-id="02ee0-116">Поскольку базовая поддержка в среде выполнения больше не существует, выдача исключения <xref:System.PlatformNotSupportedException> обеспечивает корректную обработку сбоя.</span><span class="sxs-lookup"><span data-stu-id="02ee0-116">Since the underlying support in the runtime no longer exists, throwing a <xref:System.PlatformNotSupportedException> enables a graceful failure path.</span></span> <span data-ttu-id="02ee0-117">Создание исключения также позволяет легче обнаружить, что эта функция больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="02ee0-117">Throwing an exception also makes it more discoverable that this feature is no longer supported.</span></span>

## <a name="recommended-action"></a><span data-ttu-id="02ee0-118">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="02ee0-118">Recommended action</span></span>

- <span data-ttu-id="02ee0-119">Если вы можете определить интерфейс в файле метаданных среды выполнения Windows (WinMD), используйте вместо этого средство C#/WinRT.</span><span class="sxs-lookup"><span data-stu-id="02ee0-119">If you can define the interface in a Windows runtime metadata (WinMD) file, use the C#/WinRT tool instead.</span></span>

- <span data-ttu-id="02ee0-120">В противном случае пометьте интерфейс как <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIUnknown> вместо <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> и добавьте три фиктивные записи в начало интерфейса для методов <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>.</span><span class="sxs-lookup"><span data-stu-id="02ee0-120">Otherwise, mark the interface as <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIUnknown> instead of <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable>, and add three dummy entries to the start of the interface for the <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable> methods.</span></span> <span data-ttu-id="02ee0-121">Фрагмент кода приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="02ee0-121">The following code snippet shows an example.</span></span>

  ```csharp
  [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
  interface IMine
  {
      // Do not call these three methods.
      // They're exclusively to fill in the slots in the vtable.
      void GetIIdsSlot();
      void GetRuntimeClassNameSlot();
      void GetTrustLevelSlot();

      // The original members of the IMine interface go here.
      ...
  }
  ```

## <a name="affected-apis"></a><span data-ttu-id="02ee0-122">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="02ee0-122">Affected APIs</span></span>

- <xref:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable?displayProperty=fullName>

<!--

### Affected APIs

- `F:System.Runtime.InteropServices.ComInterfaceType.InterfaceIsIInspectable`

### Category

Interop

-->
