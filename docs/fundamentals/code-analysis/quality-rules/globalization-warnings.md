---
title: Правила глобализации (анализ кода)
description: Дополнительные сведения о правилах глобализации для анализа кода
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- rules, globalization
- globalization rules
- globalization [Visual Studio], rules
- managed code analysis rules, globalization rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: 83ecc52c5e20e074c6c1aed68204a574494f42d5
ms.sourcegitcommit: 05d0087dfca85aac9ca2960f86c5efd218bf833f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/30/2021
ms.locfileid: "96593066"
---
# <a name="globalization-rules"></a>Правила глобализации

Правила глобализации поддерживают международные библиотеки и приложения.

## <a name="in-this-section"></a>Содержание раздела

|Правило|Описание|
|----------|-----------------|
|[CA1303. Не передавайте литералы в качестве локализованных параметров](ca1303.md)|Видимый извне метод передает строковый литерал в виде параметра конструктору .NET или методу, и эта строка должна быть локализуемой.|
|[CA1304. Указывайте CultureInfo](ca1304.md)|Метод или конструктор вызывает член, имеющий перегрузку, которая принимает параметр System.Globalization.CultureInfo, вместо того чтобы вызвать перегрузку, принимающую параметр CultureInfo. Если объект CultureInfo или System.IFormatProvider не предоставляется, значение по умолчанию, поставляемое перегруженным членом, может не оказать ожидаемого воздействия во всех языковых стандартах.|
|[CA1305. Указывайте IFormatProvider](ca1305.md)|Метод или конструктор вызывает один или несколько членов, имеющих перегрузки, которые принимают параметр System.IFormatProvider, вместо того чтобы вызвать перегрузку, принимающую параметр IFormatProvider. Если объект System.Globalization.CultureInfo или IFormatProvider не предоставляется, значение по умолчанию, поставляемое перегруженным членом, может не оказать ожидаемого воздействия во всех языковых стандартах.|
|[CA1307. Используйте StringComparison, чтобы ясно указать намерение.](ca1307.md)|В операции сравнения строк используется перегрузка метода, которая не задает параметр StringComparison.|
|[CA1308. Нормализуйте строки в верхний регистр](ca1308.md)|Строки следует нормализовать в верхний регистр. Существует небольшая группа символов, которые после преобразования в нижний регистр не могут участвовать в круговом перемещении.|
|[CA1309. Используйте порядковый параметр StringComparison](ca1309.md)|Операция сравнения строк, не являющаяся лингвистической, не задает для параметра StringComparison ни значения Ordinal, ни значения OrdinalIgnoreCase. После явного задания для параметра значения StringComparison.Ordinal или StringComparison.OrdinalIgnoreCase код часто становится более надежным и правильным, кроме того, увеличивается скорость его выполнения.|
|[CA1310. Используйте StringComparison, чтобы правильно указать намерение.](ca1310.md)|Операция сравнения строк использует перегрузку метода, которая не задает параметр StringComparison и использует сравнение строк для определенного языка и региональных параметров по умолчанию.|
|[CA2101: укажите тип маршалинга для строковых аргументов P/Invoke](ca2101.md)|Элемент вызова неуправляемого кода, разрешающий вызовы с частичным доверием, содержит строковый параметр и не выполняет явное маршалирование этой строки. Это может стать причиной потенциальной уязвимости безопасности.|
