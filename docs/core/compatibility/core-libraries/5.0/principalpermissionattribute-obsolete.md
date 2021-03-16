---
title: Критическое изменение. PrincipalPermissionAttribute устарел и является ошибочным
description: Сведения о критическом изменении .NET 5 в основных библиотеках .NET, где конструктор PrincipalPermissionAttribute устарел и вызывает ошибку во время компиляции.
ms.date: 11/01/2020
ms.openlocfilehash: 7568883935633e98b884b553efccf50504448b77
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102257236"
---
# <a name="principalpermissionattribute-is-obsolete-as-error"></a><span data-ttu-id="caf23-103">PrincipalPermissionAttribute устарел и является ошибочным</span><span class="sxs-lookup"><span data-stu-id="caf23-103">PrincipalPermissionAttribute is obsolete as error</span></span>

<span data-ttu-id="caf23-104">Конструктор <xref:System.Security.Permissions.PrincipalPermissionAttribute> устарел и вызывает ошибку времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="caf23-104">The <xref:System.Security.Permissions.PrincipalPermissionAttribute> constructor is obsolete and produces a compile-time error.</span></span> <span data-ttu-id="caf23-105">Нельзя создать экземпляр этого атрибута или применить его к методу.</span><span class="sxs-lookup"><span data-stu-id="caf23-105">You cannot instantiate this attribute or apply it to a method.</span></span>

## <a name="change-description"></a><span data-ttu-id="caf23-106">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="caf23-106">Change description</span></span>

<span data-ttu-id="caf23-107">В .NET Framework и .NET Core можно добавлять заметки к методам с помощью атрибута <xref:System.Security.Permissions.PrincipalPermissionAttribute>.</span><span class="sxs-lookup"><span data-stu-id="caf23-107">On .NET Framework and .NET Core, you can annotate methods with the <xref:System.Security.Permissions.PrincipalPermissionAttribute> attribute.</span></span> <span data-ttu-id="caf23-108">Пример:</span><span class="sxs-lookup"><span data-stu-id="caf23-108">For example:</span></span>

```csharp
[PrincipalPermission(SecurityAction.Demand, Role = "Administrators")]
public void MyMethod()
{
    // Code that should only run when the current user is an administrator.
}
```

<span data-ttu-id="caf23-109">Начиная с .NET 5 к методу нельзя применить атрибут <xref:System.Security.Permissions.PrincipalPermissionAttribute>.</span><span class="sxs-lookup"><span data-stu-id="caf23-109">Starting in .NET 5, you cannot apply the <xref:System.Security.Permissions.PrincipalPermissionAttribute> attribute to a method.</span></span> <span data-ttu-id="caf23-110">Конструктор атрибута устарел и вызывает ошибку во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="caf23-110">The constructor for the attribute is obsolete and produces a compile-time error.</span></span> <span data-ttu-id="caf23-111">В отличие от других устаревших предупреждений, эту ошибку нельзя обойти.</span><span class="sxs-lookup"><span data-stu-id="caf23-111">Unlike other obsoletion warnings, you can't suppress the error.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="caf23-112">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="caf23-112">Reason for change</span></span>

<span data-ttu-id="caf23-113">Тип <xref:System.Security.Permissions.PrincipalPermissionAttribute>, как и другие типы, являющиеся подклассом <xref:System.Security.Permissions.SecurityAttribute>, является частью инфраструктуры .NET по управлению доступом для кода (CAS).</span><span class="sxs-lookup"><span data-stu-id="caf23-113">The <xref:System.Security.Permissions.PrincipalPermissionAttribute> type, like other types that subclass <xref:System.Security.Permissions.SecurityAttribute>, is part of .NET's Code Access Security (CAS) infrastructure.</span></span> <span data-ttu-id="caf23-114">В .NET Framework 2.x-4.x среда выполнения применяет заметки <xref:System.Security.Permissions.PrincipalPermissionAttribute> к записи метода, даже если приложение выполняется с полным доверием.</span><span class="sxs-lookup"><span data-stu-id="caf23-114">In .NET Framework 2.x - 4.x, the runtime enforces <xref:System.Security.Permissions.PrincipalPermissionAttribute> annotations on method entry, even if the application is running under a full-trust scenario.</span></span> <span data-ttu-id="caf23-115">В .NET Core и .NET 5 и более поздних версий не поддерживаются атрибуты CAS, и среда выполнения их игнорирует.</span><span class="sxs-lookup"><span data-stu-id="caf23-115">.NET Core and .NET 5 and later don't support CAS attributes, and the runtime ignores them.</span></span>

<span data-ttu-id="caf23-116">Это различие в поведении .NET Framework по отношению к .NET Core и .NET 5 может привести к ситуации "ошибочного открытия", когда доступ должен быть заблокирован, а вместо этого он был разрешен.</span><span class="sxs-lookup"><span data-stu-id="caf23-116">This difference in behavior from .NET Framework to .NET Core and .NET 5 can result in a "fail open" scenario, where access should have been blocked but instead has been allowed.</span></span> <span data-ttu-id="caf23-117">Чтобы не допустить ситуации "ошибочного открытия", больше нельзя применять этот атрибут в коде, предназначенном для .NET 5 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="caf23-117">To prevent the "fail open" scenario, you can no longer apply the attribute in code that targets .NET 5 or later.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="caf23-118">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="caf23-118">Version introduced</span></span>

<span data-ttu-id="caf23-119">5.0</span><span class="sxs-lookup"><span data-stu-id="caf23-119">5.0</span></span>

## <a name=""></a><span data-ttu-id="caf23-120"><a id="permission-action">Рекомендуемое действие</a></span><span class="sxs-lookup"><span data-stu-id="caf23-120"><a id="permission-action">Recommended action</a></span></span>

<span data-ttu-id="caf23-121">При возникновении ошибки устаревшего атрибута необходимо выполнить определенные действия.</span><span class="sxs-lookup"><span data-stu-id="caf23-121">If you encounter the obsoletion error, you must take action.</span></span>

- <span data-ttu-id="caf23-122">**При применении атрибута к методу действия MVC ASP.NET:**</span><span class="sxs-lookup"><span data-stu-id="caf23-122">**If you're applying the attribute to an ASP.NET MVC action method:**</span></span>

  <span data-ttu-id="caf23-123">Рассмотрите возможность использования встроенной инфраструктуры авторизации ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="caf23-123">Consider using ASP.NET's built-in authorization infrastructure.</span></span> <span data-ttu-id="caf23-124">В следующем примере кода показано, как добавить к контроллеру атрибут <xref:System.Web.Mvc.AuthorizeAttribute>.</span><span class="sxs-lookup"><span data-stu-id="caf23-124">The following code demonstrates how to annotate a controller with an <xref:System.Web.Mvc.AuthorizeAttribute> attribute.</span></span> <span data-ttu-id="caf23-125">Среда выполнения ASP.NET выполнит авторизацию пользователя перед выполнением действия.</span><span class="sxs-lookup"><span data-stu-id="caf23-125">The ASP.NET runtime will authorize the user before performing the action.</span></span>

  ```csharp
  using Microsoft.AspNetCore.Authorization;

  namespace MySampleApp
  {
      [Authorize(Roles = "Administrator")]
      public class AdministrationController : Controller
      {
          public ActionResult MyAction()
          {
              // This code won't run unless the current user
              // is in the 'Administrator' role.
          }
      }
  }
  ```

  <span data-ttu-id="caf23-126">Дополнительные сведения см. в статьях [Авторизация на основе ролей в ASP.NET Core](/aspnet/core/security/authorization/roles) и [Общие сведения об авторизации в ASP.NET Core](/aspnet/core/security/authorization/introduction).</span><span class="sxs-lookup"><span data-stu-id="caf23-126">For more information, see [Role-based authorization in ASP.NET Core](/aspnet/core/security/authorization/roles) and [Introduction to authorization in ASP.NET Core](/aspnet/core/security/authorization/introduction).</span></span>

- <span data-ttu-id="caf23-127">**При применении атрибута к коду библиотеки вне контекста веб-приложения:**</span><span class="sxs-lookup"><span data-stu-id="caf23-127">**If you're applying the attribute to library code outside the context of a web app:**</span></span>

  <span data-ttu-id="caf23-128">Выполните проверки вручную в начале метода.</span><span class="sxs-lookup"><span data-stu-id="caf23-128">Perform the checks manually at the beginning of your method.</span></span> <span data-ttu-id="caf23-129">Это можно сделать с помощью метода <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="caf23-129">This can be done by using the <xref:System.Security.Principal.IPrincipal.IsInRole(System.String)?displayProperty=nameWithType> method.</span></span>

  ```csharp
  using System.Threading;

  void DoSomething()
  {
      if (Thread.CurrentPrincipal == null
          || !Thread.CurrentPrincipal.IsInRole("Administrators"))
      {
          throw new Exception("User is anonymous or isn't an admin.");
      }

      // Code that should run only when user is an administrator.
  }
  ```

## <a name="affected-apis"></a><span data-ttu-id="caf23-130">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="caf23-130">Affected APIs</span></span>

- <xref:System.Security.Permissions.PrincipalPermissionAttribute?displayProperty=fullName>

<!--

#### Category

- Core .NET libraries
- Security

### Affected APIs

- `T:System.Security.Permissions.PrincipalPermissionAttribute`

-->
