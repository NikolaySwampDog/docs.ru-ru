---
title: Критическое изменение. Некоторые свойства TableLayoutSettings выдают исключение InvalidEnumArgumentException
description: Сведения о критическом изменении в .NET 6, в результате которого ряд API TableLayoutSettings теперь выдает исключение InvalidEnumArgumentException для недопустимых аргументов.
ms.date: 01/18/2021
ms.openlocfilehash: 2da097122b935ec3a60c2bb009cc8ebbcff6468e
ms.sourcegitcommit: 9c589b25b005b9a7f87327646020eb85c3b6306f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/06/2021
ms.locfileid: "102255728"
---
# <a name="selected-tablelayoutsettings-properties-throw-invalidenumargumentexception"></a><span data-ttu-id="8a9ac-103">Выбранные свойства TableLayoutSettings выдают исключение InvalidEnumArgumentException</span><span class="sxs-lookup"><span data-stu-id="8a9ac-103">Selected TableLayoutSettings properties throw InvalidEnumArgumentException</span></span>

<span data-ttu-id="8a9ac-104">Теперь выбранные свойства <xref:System.Windows.Forms.TableLayoutSettings> выдают <xref:System.ComponentModel.InvalidEnumArgumentException> при попытке присвоить неверное значение.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-104">Selected <xref:System.Windows.Forms.TableLayoutSettings> properties now throw an <xref:System.ComponentModel.InvalidEnumArgumentException> if you attempt to assign an incorrect value.</span></span>

## <a name="change-description"></a><span data-ttu-id="8a9ac-105">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="8a9ac-105">Change description</span></span>

<span data-ttu-id="8a9ac-106">В предыдущих версиях .NET эти свойства выдают <xref:System.ArgumentOutOfRangeException> при попытке присвоить неверное значение.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-106">In previous .NET versions, these properties throw an <xref:System.ArgumentOutOfRangeException> if you attempt to assign an incorrect value.</span></span> <span data-ttu-id="8a9ac-107">Начиная с .NET 6 эти свойства в таких случаях выдают <xref:System.ComponentModel.InvalidEnumArgumentException>.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-107">Starting in .NET 6, these properties throw an <xref:System.ComponentModel.InvalidEnumArgumentException> in such cases.</span></span>

## <a name="reason-for-change"></a><span data-ttu-id="8a9ac-108">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="8a9ac-108">Reason for change</span></span>

<span data-ttu-id="8a9ac-109">Выдача <xref:System.ComponentModel.InvalidEnumArgumentException> соответствует поведению текущего API Windows Forms в аналогичных ситуациях.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-109">Throwing <xref:System.ComponentModel.InvalidEnumArgumentException> is in line with the existing Windows Forms API in similar situations.</span></span> <span data-ttu-id="8a9ac-110">Выдача этого исключения также позволяет сделать более удобным процесс отладки для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-110">Throwing this exception also provides developers with a better debug experience.</span></span>

## <a name="version-introduced"></a><span data-ttu-id="8a9ac-111">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="8a9ac-111">Version introduced</span></span>

<span data-ttu-id="8a9ac-112">.NET 6.0</span><span class="sxs-lookup"><span data-stu-id="8a9ac-112">.NET 6.0</span></span>

## <a name="recommended-action"></a><span data-ttu-id="8a9ac-113">Рекомендованное действие</span><span class="sxs-lookup"><span data-stu-id="8a9ac-113">Recommended action</span></span>

- <span data-ttu-id="8a9ac-114">Обновите код, чтобы предотвратить присвоение неверных значений.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-114">Update the code to prevent assigning incorrect values.</span></span>
- <span data-ttu-id="8a9ac-115">При необходимости обработайте <xref:System.ComponentModel.InvalidEnumArgumentException> при доступе к этим API.</span><span class="sxs-lookup"><span data-stu-id="8a9ac-115">If necessary, handle an <xref:System.ComponentModel.InvalidEnumArgumentException> when accessing these APIs.</span></span>

## <a name="affected-apis"></a><span data-ttu-id="8a9ac-116">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="8a9ac-116">Affected APIs</span></span>

<span data-ttu-id="8a9ac-117">Затронутые свойства перечислены в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8a9ac-117">The following table lists the affected properties:</span></span>

| <span data-ttu-id="8a9ac-118">Свойство</span><span class="sxs-lookup"><span data-stu-id="8a9ac-118">Property</span></span> | <span data-ttu-id="8a9ac-119">Версия изменена</span><span class="sxs-lookup"><span data-stu-id="8a9ac-119">Version changed</span></span> |
|-|-|-|-|
| <xref:System.Windows.Forms.TableLayoutPanel.CellBorderStyle?displayProperty=fullName> | <span data-ttu-id="8a9ac-120">Предварительная версия 1</span><span class="sxs-lookup"><span data-stu-id="8a9ac-120">Preview 1</span></span> |
| <xref:System.Windows.Forms.TableLayoutPanel.GrowStyle?displayProperty=fullName> | <span data-ttu-id="8a9ac-121">Предварительная версия 1</span><span class="sxs-lookup"><span data-stu-id="8a9ac-121">Preview 1</span></span> |

<!--

### Affected APIs

- `P:System.Windows.Forms.TableLayoutPanel.CellBorderStyle`
- `P:System.Windows.Forms.TableLayoutPanel.GrowStyle`

### Category

Windows Forms

-->
