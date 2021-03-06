---
title: "Практическое руководство. Сравнение строки на соответствие с шаблоном (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "операторы сравнения, сравнение строк"
  - "Like - оператор [Visual Basic], соответствие шаблону"
  - "операторы [Visual Basic], сравнение"
  - "соответствие шаблону"
  - "соответствие шаблону, пустая строка"
  - "соответствие шаблону, сравнение строк"
  - "сравнение строк [Visual Basic]"
  - "сравнение строк [Visual Basic], операторы"
  - "строки [Visual Basic], сравнение"
  - "код Visual Basic, операторы"
ms.assetid: 19a83804-b5af-4739-928b-ac93e64e457f
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Практическое руководство. Сравнение строки на соответствие с шаблоном (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

Если нужно узнать, удовлетворяет ли выражение [Тип данных String](../../../../visual-basic/language-reference/data-types/string-data-type.md) шаблону, можно использовать [Оператор Like](../../../../visual-basic/language-reference/operators/like-operator.md).  
  
 `Like` принимает два операнда.  Левый операнд представляет собой строковое выражение, а правый операнд является строкой, содержащей шаблон для соответствия.  `Like` возвращает значение типа `Boolean`, указывающее, удовлетворяет ли строковое выражение шаблону.  
  
 Каждому знаку в строке выражения можно сопоставить определенный символ, подстановочный символ, символ из списка или диапазон символов.  Позиции спецификации в строке шаблона соответствуют расположению знаков, которые сопоставляются со строковым выражением.  
  
### Сравнение символа в строковом выражении с указанным символом  
  
-   Поместите указанный символ непосредственно в строку шаблона.  Некоторые специальные символы должны заключаться в скобки \(`[ ]`\).  Дополнительные сведения см. в разделе [Оператор Like](../../../../visual-basic/language-reference/operators/like-operator.md).  
  
     В следующем примере проверяется состоит ли строка `myString` только из символов `H`.  
  
     [!code-vb[VbVbalrOperators#70](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_1.vb)]  
  
### Сравнение символа в строковом выражении с подстановочным символом  
  
-   Поместите вопросительный знак \(`?`\) в строку шаблона.  Любой допустимый знак в этой позиции говорит об успешном совпадении.  
  
     В следующем примере проверяется, состоит ли строка `myString` только из символов `W`, перед которыми стоят ровно два произвольных символа.  
  
     [!code-vb[VbVbalrOperators#71](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_2.vb)]  
  
### Сравнение символа в строковом выражении на соответствие со списком символов  
  
-   Поместите квадратные скобки \(`[ ]`\) в строку шаблона, а внутри скобок поместите список символов.  Не разделяйте знаки запятыми или любым другим разделителем.  Если в строковом выражении символ совпадает с одним из символом из этого списка, совпадение является успешным.  
  
     Следующий пример проверяет, начинается ли строка `myString`, состоящая из произвольных символов, с одного из следующих символов: `A`, `C` или `E`.  
  
     [!code-vb[VbVbalrOperators#72](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_3.vb)]  
  
     Обратите внимание, что при сравнении учитывается регистр.  
  
### Сравнение символа в строковом выражении с диапазоном символов  
  
-   Поместите квадратные скобки \(`[ ]`\) в строке шаблона и внутри скобок укажите диапазон знаков \(наименьший и наибольший знак\) через дефис \(`–`\).  Любой знак, попадающий в этот диапазон, дает успешное совпадение.  
  
     В следующем примере проверяется, состоит ли строка `myString` из символов `num`, следующих за одним из этих символов: `i`, `j`, `k`, `l`, `m` или `n`.  
  
     [!code-vb[VbVbalrOperators#73](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_4.vb)]  
  
     Обратите внимание, что при сравнении учитывается регистр.  
  
## Сравнение пустых строк  
 `Like` рассматривает последовательность `[]` как строку нулевой длины \(`""`\).  Можно использовать квадратные скобки `[]`, чтобы проверить, является ли строковое выражение пустым. Однако квадратные скобки нельзя использовать, чтобы проверить, является ли строковое выражение пустым в конкретной позиции.  Если пустая позиция является одним из параметров, которые необходимо проверить, можно использовать `Like` несколько раз.  
  
#### Проверка наличия символа строкового выражения в списке символов  
  
1.  Вызовите оператор `Like` дважды для одного строкового выражения и объедините оба вызова с помощью [Оператор Or](../../../../visual-basic/language-reference/operators/or-operator.md) или [Оператор OrElse](../../../../visual-basic/language-reference/operators/orelse-operator.md).  
  
2.  В строке шаблона для первого предложения `Like` включите список символов, заключенный в квадратные скобки \(`[ ]`\).  
  
3.  В строке шаблона для второго предложения `Like` не следует помещать какие\-либо символы в исследуемой позиции.  
  
     В следующем примере проверяется семь цифр телефонного номера `phoneNum`, записанного в следующем формате: сначала идут три символа, затем пробел, дефис \(`–`\), точка \(`.`\) или вообще отсутствует какой\-либо знак, после чего идут остальные 4 цифры номера телефона.  
  
     [!code-vb[VbVbalrOperators#74](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-match-a-string-against-a-pattern_5.vb)]  
  
## См. также  
 [Операторы сравнения](../../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Операторы и выражения](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Оператор Like](../../../../visual-basic/language-reference/operators/like-operator.md)   
 [Тип данных String](../../../../visual-basic/language-reference/data-types/string-data-type.md)