---
title: Практическое руководство. Реализация облегченного класса с автоматически реализуемыми свойствами (руководство по программированию на C#)
description: Узнайте, как создать неизменяемый упрощенный класс в C#, который инкапсулирует автоматически реализуемые свойства. Существует два подхода к реализации.
ms.date: 07/20/2015
helpviewer_keywords:
- auto-implemented properties [C#]
- properties [C#], auto-implemented
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 1dc5a8ad-a4f7-4f32-8506-3fc6d8c8bfed
ms.openlocfilehash: 1d80cb2391a94c21360117c8217ecc4514fd666e
ms.sourcegitcommit: e3cf8227573e13b8e1f4e3dc007404881cdafe47
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/11/2021
ms.locfileid: "103190272"
---
# <a name="how-to-implement-a-lightweight-class-with-auto-implemented-properties-c-programming-guide"></a><span data-ttu-id="4471c-104">Практическое руководство. Реализация облегченного класса с автоматически реализуемыми свойствами (руководство по программированию на C#)</span><span class="sxs-lookup"><span data-stu-id="4471c-104">How to implement a lightweight class with auto-implemented properties (C# Programming Guide)</span></span>

<span data-ttu-id="4471c-105">В этом примере показано, как создать неизменяемый упрощенный класс, служащий исключительно для инкапсуляции набора автоматически реализуемых свойств.</span><span class="sxs-lookup"><span data-stu-id="4471c-105">This example shows how to create an immutable lightweight class that serves only to encapsulate a set of auto-implemented properties.</span></span> <span data-ttu-id="4471c-106">Используйте такую конструкцию вместо структуры, когда требуется использовать семантику ссылочного типа.</span><span class="sxs-lookup"><span data-stu-id="4471c-106">Use this kind of construct instead of a struct when you must use reference type semantics.</span></span>

<span data-ttu-id="4471c-107">Неизменяемое свойство можно создать следующими способами:</span><span class="sxs-lookup"><span data-stu-id="4471c-107">You can make an immutable property in the following ways:</span></span>

- <span data-ttu-id="4471c-108">Объявить только метод доступа [get](../../language-reference/keywords/get.md), который делает свойство неизменяемым везде, кроме конструктора типа.</span><span class="sxs-lookup"><span data-stu-id="4471c-108">Declare only the [get](../../language-reference/keywords/get.md) accessor, which makes the property immutable everywhere except in the type's constructor.</span></span>

- <span data-ttu-id="4471c-109">Объявить метод доступа [init](../../language-reference/keywords/init.md) вместо `set`, который делает свойство изменяемым только в конструкторе или с помощью [инициализатора объектов](object-and-collection-initializers.md).</span><span class="sxs-lookup"><span data-stu-id="4471c-109">Declare an [init](../../language-reference/keywords/init.md) accessor instead of a `set` accessor, which makes the property settable only in the constructor or by using an [object initializer](object-and-collection-initializers.md).</span></span>

- <span data-ttu-id="4471c-110">Объявить метод доступа [set](../../language-reference/keywords/set.md) как [private](../../language-reference/keywords/private.md).</span><span class="sxs-lookup"><span data-stu-id="4471c-110">Declare the [set](../../language-reference/keywords/set.md) accessor to be [private](../../language-reference/keywords/private.md).</span></span>  <span data-ttu-id="4471c-111">Свойство можно задать в типе, но оно является неизменяемым для потребителей.</span><span class="sxs-lookup"><span data-stu-id="4471c-111">The property is settable within the type, but it is immutable to consumers.</span></span>

  <span data-ttu-id="4471c-112">При объявлении закрытого метода доступа `set` для инициализации свойства нельзя использовать инициализатор объекта.</span><span class="sxs-lookup"><span data-stu-id="4471c-112">When you declare a private `set` accessor, you cannot use an object initializer to initialize the property.</span></span> <span data-ttu-id="4471c-113">Необходимо использовать конструктор или фабричный метод.</span><span class="sxs-lookup"><span data-stu-id="4471c-113">You must use a constructor or a factory method.</span></span>

<span data-ttu-id="4471c-114">В следующем примере показано, как свойство с методом доступа get, отличается от свойства с методами доступа get и private set.</span><span class="sxs-lookup"><span data-stu-id="4471c-114">The following example shows how a property with only get accessor differs than one with get and private set.</span></span>

```csharp
class Contact
{
    public string Name { get; }
    public string Address { get; private set; }

    public Contact(string contactName, string contactAddress)
    {
        // Both properties are accessible in the constructor.
        Name = contactName;
        Address = contactAddress;
    }

    // Name isn't assignable here. This will generate a compile error.
    //public void ChangeName(string newName) => Name = newName;

    // Address is assignable here.
    public void ChangeAddress(string newAddress) => Address = newAddress
}
```

## <a name="example"></a><span data-ttu-id="4471c-115">Пример</span><span class="sxs-lookup"><span data-stu-id="4471c-115">Example</span></span>

<span data-ttu-id="4471c-116">В следующем примере показаны два способа реализации неизменяемого класса с автоматически реализуемыми свойствами.</span><span class="sxs-lookup"><span data-stu-id="4471c-116">The following example shows two ways to implement an immutable class that has auto-implemented properties.</span></span> <span data-ttu-id="4471c-117">Каждый способ объявляет одно из свойств с закрытым методом доступа `set` и одно из свойств только с методом доступа `get`.</span><span class="sxs-lookup"><span data-stu-id="4471c-117">Each way declares one of the properties with a private `set` and one of the properties with a `get` only.</span></span>  <span data-ttu-id="4471c-118">Первый класс использует конструктор только для инициализации свойства, а второй класс использует статический фабричный метод, вызывающий конструктор.</span><span class="sxs-lookup"><span data-stu-id="4471c-118">The first class uses a constructor only to initialize the properties, and the second class uses a static factory method that calls a constructor.</span></span>

```csharp
// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// constructor to initialize its properties.
class Contact
{
    // Read-only property.
    public string Name { get; }

    // Read-write property with a private set accessor.
    public string Address { get; private set; }

    // Public constructor.
    public Contact(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }
}

// This class is immutable. After an object is created,
// it cannot be modified from outside the class. It uses a
// static method and private constructor to initialize its properties.
public class Contact2
{
    // Read-write property with a private set accessor.
    public string Name { get; private set; }

    // Read-only property.
    public string Address { get; }

    // Private constructor.
    private Contact2(string contactName, string contactAddress)
    {
        Name = contactName;
        Address = contactAddress;
    }

    // Public factory method.
    public static Contact2 CreateContact(string name, string address)
    {
        return new Contact2(name, address);
    }
}

public class Program
{
    static void Main()
    {
        // Some simple data sources.
        string[] names = {"Terry Adams","Fadi Fakhouri", "Hanying Feng",
                            "Cesar Garcia", "Debra Garcia"};
        string[] addresses = {"123 Main St.", "345 Cypress Ave.", "678 1st Ave",
                                "12 108th St.", "89 E. 42nd St."};

        // Simple query to demonstrate object creation in select clause.
        // Create Contact objects by using a constructor.
        var query1 = from i in Enumerable.Range(0, 5)
                    select new Contact(names[i], addresses[i]);

        // List elements cannot be modified by client code.
        var list = query1.ToList();
        foreach (var contact in list)
        {
            Console.WriteLine("{0}, {1}", contact.Name, contact.Address);
        }

        // Create Contact2 objects by using a static factory method.
        var query2 = from i in Enumerable.Range(0, 5)
                        select Contact2.CreateContact(names[i], addresses[i]);

        // Console output is identical to query1.
        var list2 = query2.ToList();

        // List elements cannot be modified by client code.
        // CS0272:
        // list2[0].Name = "Eugene Zabokritski";

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}

/* Output:
    Terry Adams, 123 Main St.
    Fadi Fakhouri, 345 Cypress Ave.
    Hanying Feng, 678 1st Ave
    Cesar Garcia, 12 108th St.
    Debra Garcia, 89 E. 42nd St.
*/
```

<span data-ttu-id="4471c-119">Компилятор создает резервные поля для каждого автоматически реализуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="4471c-119">The compiler creates backing fields for each auto-implemented property.</span></span> <span data-ttu-id="4471c-120">Эти поля недоступны непосредственно из исходного кода.</span><span class="sxs-lookup"><span data-stu-id="4471c-120">The fields are not accessible directly from source code.</span></span>

## <a name="see-also"></a><span data-ttu-id="4471c-121">См. также</span><span class="sxs-lookup"><span data-stu-id="4471c-121">See also</span></span>

- [<span data-ttu-id="4471c-122">Свойства</span><span class="sxs-lookup"><span data-stu-id="4471c-122">Properties</span></span>](./properties.md)
- [<span data-ttu-id="4471c-123">struct</span><span class="sxs-lookup"><span data-stu-id="4471c-123">struct</span></span>](../../language-reference/builtin-types/struct.md)
- [<span data-ttu-id="4471c-124">Инициализаторы объектов и коллекций</span><span class="sxs-lookup"><span data-stu-id="4471c-124">Object and Collection Initializers</span></span>](./object-and-collection-initializers.md)
