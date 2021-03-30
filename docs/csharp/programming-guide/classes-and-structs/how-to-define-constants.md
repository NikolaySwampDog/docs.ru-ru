---
title: Определение констант в C#
description: Узнайте, как определять константы в C#, которые являются полями, значения которых задаются во время компиляции. Используйте константы для присвоения значимых имен особым значениям.
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, constants
- constants [C#]
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 43f511be-346c-4b8a-995e-aded94542ece
ms.openlocfilehash: 54b8a335279c8bb81bc75d182ec653e434ab45a0
ms.sourcegitcommit: 05d0087dfca85aac9ca2960f86c5efd218bf833f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/27/2021
ms.locfileid: "105636861"
---
# <a name="how-to-define-constants-in-c"></a><span data-ttu-id="f9464-104">Определение констант в C\#</span><span class="sxs-lookup"><span data-stu-id="f9464-104">How to define constants in C\#</span></span>

<span data-ttu-id="f9464-105">Константы — это поля, значения которых устанавливаются во время компиляции и не изменяются.</span><span class="sxs-lookup"><span data-stu-id="f9464-105">Constants are fields whose values are set at compile time and can never be changed.</span></span> <span data-ttu-id="f9464-106">С помощью констант можно присвоить особым значениям значащие имена вместо числовых литералов.</span><span class="sxs-lookup"><span data-stu-id="f9464-106">Use constants to provide meaningful names instead of numeric literals ("magic numbers") for special values.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f9464-107">В C# с помощью директивы препроцессора [#define](../../language-reference/preprocessor-directives.md#defining-symbols) нельзя определять константы так, как это было реализовано в C и C++.</span><span class="sxs-lookup"><span data-stu-id="f9464-107">In C# the [#define](../../language-reference/preprocessor-directives.md#defining-symbols) preprocessor directive cannot be used to define constants in the way that is typically used in C and C++.</span></span>  
  
 <span data-ttu-id="f9464-108">Чтобы определить значения константы целочисленного типа (`int`, `byte` и т. д.), используйте перечисляемый тип.</span><span class="sxs-lookup"><span data-stu-id="f9464-108">To define constant values of integral types (`int`, `byte`, and so on) use an enumerated type.</span></span> <span data-ttu-id="f9464-109">Дополнительные сведения см. в разделе [Перечисление](../../language-reference/builtin-types/enum.md).</span><span class="sxs-lookup"><span data-stu-id="f9464-109">For more information, see [enum](../../language-reference/builtin-types/enum.md).</span></span>  
  
 <span data-ttu-id="f9464-110">Чтобы определить нецелочисленные константы, можно сгруппировать их в статический класс с именем `Constants`.</span><span class="sxs-lookup"><span data-stu-id="f9464-110">To define non-integral constants, one approach is to group them in a single static class named `Constants`.</span></span> <span data-ttu-id="f9464-111">В этом случае перед любыми ссылками на константы будет необходимо указывать имя класса, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f9464-111">This will require that all references to the constants be prefaced with the class name, as shown in the following example.</span></span>  
  
## <a name="example"></a><span data-ttu-id="f9464-112">Пример</span><span class="sxs-lookup"><span data-stu-id="f9464-112">Example</span></span>  

 [!code-csharp[constants](snippets/how-to-define-constants/Program.cs)]  
  
 <span data-ttu-id="f9464-113">Используя квалификатор имени класса, вы гарантируете, что вы сами и другие разработчики будете понимать, что имеете дело с константой, которую нельзя изменить.</span><span class="sxs-lookup"><span data-stu-id="f9464-113">The use of the class name qualifier helps ensure that you and others who use the constant understand that it is constant and cannot be modified.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f9464-114">См. также</span><span class="sxs-lookup"><span data-stu-id="f9464-114">See also</span></span>

- [<span data-ttu-id="f9464-115">Классы и структуры</span><span class="sxs-lookup"><span data-stu-id="f9464-115">Classes and Structs</span></span>](./index.md)
