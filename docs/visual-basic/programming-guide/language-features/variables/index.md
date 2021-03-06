---
title: "Переменные в Visual Basic"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- variables [Visual Basic]
- values [Visual Basic], storing
ms.assetid: 4cfaa06d-4ae3-4307-897b-cf599dc24caa
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2fdc670bf4f17000809e75e32c32edb39abf0fed
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="variables-in-visual-basic"></a>Переменные в Visual Basic
Часто при выполнении вычислений с [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] требуется сохранять значения. Например, может потребоваться вычислить несколько значений, сравнить их и (в зависимости от результата сравнения) выполнить с ними различные операции. Чтобы сравнить значения, их необходимо сохранить.  
  
## <a name="usage"></a>Использование  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], как и большинство языков программирования, использует для хранения значений переменные. *Переменная* имеет имя (слово, которое используется для ссылки на содержащееся в переменной значение). Переменная также имеет тип данных (который определяет, какие данные можно хранить в переменной). Переменная может представлять массив, если она должна хранить индексированный набор близко связанных элементов данных.  
  
 Вывод локального типа позволяет объявлять переменные без явного указания типа данных. Вместо этого компилятор выводит тип переменной из типа инициализирующего выражения. Дополнительные сведения см. в разделах [Вывод локального типа](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) и [Оператор Option Infer](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## <a name="assigning-values"></a>Назначение значений  
 Для выполнения вычислений и присвоения результата переменной используются операторы присваивания, как показано в следующем примере.  
  
 [!code-vb[VbVbalrVariables#1](../../../../visual-basic/programming-guide/language-features/variables/codesnippet/VisualBasic/index_1.vb)]  
  
> [!NOTE]
>  В этом примере знак равенства (`=`) является оператором присваивания, а не оператором равенства. Значение присваивается переменной `applesSold`.  
  
 Подробнее см. в разделе [Практическое руководство. Запись данных в переменную и их извлечение из переменной](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md).  
  
## <a name="variables-and-properties"></a>Переменные и свойства  
 Как и переменная, *свойство* соответствует значению, к которому можно получить доступ. Но оно является более сложным, чем переменная. Свойство использует блоки кода, определяющие способ задания и получения его значения. Подробнее см. в разделе [Различия между свойствами и переменными в Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md).  
  
## <a name="see-also"></a>См. также  
 [Объявление переменной](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Объектные переменные](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Устранение неполадок, связанных с переменными](../../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)   
 [Практическое руководство. Запись данных в переменную и их извлечение из переменной](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)   
 [Различия между свойствами и переменными в Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [Вывод локального типа](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)

