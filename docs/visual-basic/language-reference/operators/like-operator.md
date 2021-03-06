---
title: "Оператор Like (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Like"
  - "vb.Like"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "? символ, подстановочный знак"
  - "операторы сравнения"
  - "данные [Visual Basic], сортировка"
  - "данные [Visual Basic], сравнения строк"
  - "Like - оператор [Visual Basic]"
  - "операторы [Visual Basic], сопоставление шаблонов"
  - "соответствие шаблону"
  - "подобие"
  - "сравнение строк [Visual Basic], Like - оператор"
  - "сравнение строк [Visual Basic], Like - операторы"
  - "сравнение строк [Visual Basic], сортировка данных"
  - "строки [Visual Basic], сравнение"
  - "строки [Visual Basic], соответствие"
  - "символы, подстановочный знак"
  - "текст [Visual Basic], сравнение"
  - "подстановочные знаки, Like - оператор"
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Оператор Like (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Сравнивает строку c шаблоном.  
  
## Синтаксис  
  
```  
  
result = string Like pattern  
```  
  
## Части  
 `result`  
 Обязательный.  Любая переменная `Boolean`.  В результате получается значение `Boolean`, показывающее, удовлетворяет ли `string` `pattern`.  
  
 `string`  
 Обязательный.  Произвольное выражение типа `String`.  
  
 `pattern`  
 Обязательный.  Любое выражение `String`, согласующееся с правилами соответствия шаблону, описанными в разделе "Примечания".  
  
## Заметки  
 Если значение в `string` удовлетворяет шаблону, содержащемуся в `pattern`, `result` имеет значение `True`.  Если строка не удовлетворяет шаблону, `result` имеет значение `False`.  Если `string` и `pattern` являются пустыми строками, результатом является значение `True`.  
  
## Метод Сравнения  
 Поведение оператора `Like` зависит от [Оператор Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md).  По умолчанию метод сравнения сроки для каждого исходного файла является `Option Compare Binary`.  
  
## Параметры шаблона  
 Встроенный подбор шаблонов представляет собой универсальный инструмент для сравнения строк.  Средства подбора шаблона позволяют сопоставлять каждый символ в `string` с определенным символом, подстановочным знаком, списком знаков или диапазоном знаков.  В следующей таблице показаны знаки, использование которых допустимо в `pattern`, и их соответствия.  
  
|Знаки в `pattern`|Совпадения в `string`|  
|-----------------------|---------------------------|  
|`?`|Любой отдельный знак|  
|`*`|Ноль или более знаков|  
|`#`|Любая цифра \(0–9\)|  
|`[` `charlist` `]`|Любой отдельный знак в `charlist`|  
|`[!` `charlist` `]`|Любой знак, не входящий в `charlist`|  
  
## Список знаков  
 Группа, состоящая из одного или нескольких знаков \(`charlist`\) и заключенная в квадратные скобки \(`[ ]`\), может быть использована для сопоставления с любым отдельным знаком в `string` и может включать практически любой код символа, включая также цифры.  
  
 Восклицательный знак \(`!`\) в начале `charlist` означает, что подбор осуществляется, если какой\-либо знак, за исключением знаков в `charlist`, обнаружен в `string`.  При использовании без квадратных скобок восклицательный знак сопоставляется с самим собой.  
  
## Специальные символы  
 Чтобы найти совпадения для специальных символов: левой квадратной скобки, \(`[`\), знака вопроса \(`?`\), знака решетки \(`#`\) и звездочки \(`*`\), заключите их в скобки.  Правую квадратную скобку \(`]`\) невозможно использовать в группе для сопоставления с самой собой, но ее можно использовать вне группы в качестве отдельного символа.  
  
 Последовательность символов `[]` считается строкой нулевой длины \(`""`\).  Тем не менее, она не может быть частью списка символов, заключенного в квадратные скобки.  Если требуется проверить, содержит ли позиция в `string` одну из групп знаков или не содержит знаков вообще, можно использовать `Like` дважды.  Пример см. в разделе [Практическое руководство. Сравнение строки на соответствие с шаблоном](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md).  
  
## Диапазон символов  
 Используя дефис \(`–`\) для разделения нижней и верхней границ диапазона, в `charlist` можно указывать диапазон знаков.  Например, `[A–Z]` приводит к совпадению, если соответствующая позиция символа в `string` содержит любой знак в пределах диапазона `A`–`Z`, и также `[!H–L]` приводит к совпадению, если соответствующее положение символа содержит любой знак вне диапазона `H`–`L`.  
  
 При определении диапазона символов они должны появляться в возрастающем порядке сортировки, то есть от низших к высшим.  Таким образом, `[A–Z]` является допустимым шаблоном, а `[Z–A]` не является.  
  
### Составные диапазоны знаков  
 Чтобы указать несколько диапазонов для одной позиции символа, поместите их в одни квадратные скобки без разделителей.  Например, `[A–CX–Z]` приводит к совпадению, если соответствующая позиция символа в `string` содержит любой знак в пределах  диапазона `A`–`C` или диапазона `X`–`Z`.  
  
### Использование дефиса  
 Дефис \(`–`\) может стоять либо в начале \(после восклицательного знака, если таковой имеется\), либо в конце `charlist` для сопоставления с самим собой.  При любом другом расположении дефис обозначает диапазон символов, ограниченный знаками по обе стороны от дефиса.  
  
## Последовательность сортировки  
 Значение указанного диапазона зависит от порядка знаков во время выполнения, определенного с помощью `Option` `Compare` и локальных параметров системы, в которой выполняется код.  При `Option` `Compare` `Binary`, диапазон `[A–E]` совпадает с `A`, `B`, `C`, `D`, и `E`.  При `Option` `Compare` `Text`, `[A–E]` совпадает с `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, `D`, `d`, `E`, и `e`.  Диапазон не соответствует `Ê` или `ê`, так как диакритические знаки сортируются после стандартных в порядке сортировки.  
  
## Знаки диграфы  
 В некоторых языках существуют символы алфавита, представляющие собой два отдельных знака.  Например, в некоторых языках знак `æ` используется для представления знаков `a` и `e`, стоящих рядом.  Оператор `Like` распознает, что один диграф и два отдельных знака эквивалентны.  
  
 Если язык, в котором есть диграфы, указан в региональных параметрах системы, то при наличии одного диграфа либо в `pattern`, либо в `string`, он будет сопоставлен с эквивалентной двузначной последовательностью в другой строке.  Аналогично диграф в `pattern`, заключенный в квадратные скобки \(отдельно, в списке или в диапазоне\), соответствует равнозначной последовательности двух знаков в `string`.  
  
## Перегрузка  
 Оператор `Like` может быть *перегружен*; это означает, что класс или структура может переопределить его поведение, если операнд имеет тип соответствующего класса или структуры.  Если в коде используется этот оператор для такого класса или структуры, убедитесь, что его переопределенное поведение вам понятно.  Дополнительные сведения см. в разделе [Процедуры операторов](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Пример  
 В этом примере оператор `Like` используется для сравнения строк с различными шаблонами.  Результаты переходят в переменную `Boolean`, указывающую, насколько каждая строка удовлетворяет шаблону.  
  
 [!code-vb[VbVbalrOperators#30](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/like-operator_1.vb)]  
  
## См. также  
 <xref:Microsoft.VisualBasic.Strings.InStr%2A>   
 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>   
 [Операторы сравнения](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Порядок применения операторов в Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Список операторов, сгруппированных по функциональному назначению](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Оператор Option Compare](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Операторы и выражения](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Практическое руководство. Сравнение строки на соответствие с шаблоном](../../../visual-basic/programming-guide/language-features/operators-and-expressions/how-to-match-a-string-against-a-pattern.md)