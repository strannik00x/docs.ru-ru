---
title: "Правила разработки типов | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "рекомендации по разработке типов"
  - "правила разработки типов, о рекомендациях по разработке типов"
  - "рекомендации по разработке библиотек [платформа .NET Framework] класса, рекомендации по разработке типов"
  - "типы [платформа .NET Framework] рекомендации по проектированию"
ms.assetid: 6b49314e-8bba-43ea-97ca-4e0255812f95
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Правила разработки типов
С точки зрения среды CLR, имеется только две категории типов — ссылочные типы и типы значений, но для целей обсуждения о разработке платформы, типы разделен на несколько логических групп, каждый из которых имеет свои собственные правила конкретного конструктора.  
  
 Классы являются общем случае ссылочных типов. Они составляют большую часть типов в большинство платформ. Классы должны их популярность набор объектно ориентированные возможности, которые они поддерживают широкий набор функций и их общие применимости. Базовые классы и абстрактные классы являются специальные логические группы, связанные с расширяемости.  
  
 Интерфейсы — это типы, которые могут быть реализованы, ссылочные типы и типы значений. Таким образом они могут служить корни полиморфных иерархий ссылочных типов и типов значений. Кроме того можно использовать интерфейсы для имитации множественное наследование, который изначально не поддерживается средой CLR.  
  
 Структуры являются общем случае типов значений и должны быть зарезервированы для небольших, простых типов, аналогично примитивы языка.  
  
 Перечисления являются особым случаем типы значений, используемые для определения наборов коротких значений, таких как дни недели, цвета консоли и т. д.  
  
 Статические классы — это типы, предназначенные для контейнеров для статических элементов. Они часто используются для предоставления сочетания клавиш для других операций.  
  
 Делегаты, исключения, атрибуты, массивов и коллекций являются все особые случаи ссылочные типы, предназначенные для конкретных целей, и рекомендации по их проектированию и использованию обсуждаемым ниже в этой книге.  
  
 **✓ сделать** убедитесь, что каждый тип строго определенный набор связанных элементов, не только случайных коллекции другие функции.  
  
## В этом подразделе  
 [Выбор между классом и структурой](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)  
 [Разработка абстрактных классов](../../../docs/standard/design-guidelines/abstract-class.md)  
 [Разработка статичных классов](../../../docs/standard/design-guidelines/static-class.md)  
 [Разработка интерфейса](../../../docs/standard/design-guidelines/interface.md)  
 [Разработка структур](../../../docs/standard/design-guidelines/struct.md)  
 [Разработка перечислений](../../../docs/standard/design-guidelines/enum.md)  
 [Вложенные типы](../../../docs/standard/design-guidelines/nested-types.md)  
 *Частей © 2005, 2009 корпорации Microsoft. Все права защищены.*  
  
 *Воспроизведены разрешении Пирсон образования, Inc. из [Framework рекомендации по проектированию: условные обозначения, стили и шаблоны для повторного использования библиотеки .NET, второе издание](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina и Брэд Абрамс опубликованы 22 октября 2008 г., издательство Addison\-Wesley Professional как часть цикла разработки Microsoft Windows.*  
  
## См. также  
 [Рекомендации по проектированию Framework](../../../docs/standard/design-guidelines/index.md)