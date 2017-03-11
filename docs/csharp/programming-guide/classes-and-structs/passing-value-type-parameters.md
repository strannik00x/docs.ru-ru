---
title: "Передача параметров типа значения (Руководство по программированию в C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "параметры методов [C#], типы значений"
  - "параметры [C#], значение"
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
caps.latest.revision: 17
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 17
---
# Передача параметров типа значения (Руководство по программированию в C#)
Переменная [типа значения](../../../csharp/language-reference/keywords/value-types.md) содержит данные непосредственно, в противоположность переменной [ссылочного типа](../../../csharp/language-reference/keywords/reference-types.md), которая содержит ссылку на данные.  Передача переменной типа значения методу значение означает передачей копии переменной методу.  Любые изменения к параметру, который выполняется внутри метода, не влияют на исходные данные, хранящиеся в переменной аргумента.  Если необходимо, чтобы метод с именем изменить значение параметра, необходимо передавать по ссылке, использование [ref](../../../csharp/language-reference/keywords/ref.md) OR  [вне](../../../csharp/language-reference/keywords/out.md) ключевое слово.  Для простоты в следующем примере использовано ключевое слово `ref`.  
  
## Передача типов значений по значению  
 В следующем примере демонстрируется передача параметров типа значения с помощью значения.  Переменная `n` передается с помощью значения в метод `SquareIt`.  Любые изменения, выполняемые внутри метода, не влияют на значение переменной.  
  
 [!code-cs[csProgGuideParameters#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_1.cs)]  
  
 Переменная `n` тип значения.  Он содержит данные, значение `5`.  При вызове метода `SquareIt` содержимое переменной `n` копируется в параметр `x`, который возводится в квадрат внутри метода.  IN `Main`, однако значение  `n` это же после вызова  `SquareIt` метод как он был ранее.  Изменение, выполняется внутри метода влияет только на локальную переменную `x`.  
  
## Передача типов значений по ссылке  
 Следующий пример такой же, как и предыдущий, за исключением того, что аргумент передается в качестве a `ref` параметр.  Значение базового аргумента, `n`, если изменяется  `x` изменения в методе.  
  
 [!code-cs[csProgGuideParameters#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_2.cs)]  
  
 В этом примере передается не значение переменной `n` а ссылка на переменную `n`.  Параметр `x` не является типом [int](../../../csharp/language-reference/keywords/int.md); он является ссылкой на тип `int`, в данном случае ссылкой на переменную `n`.  Следовательно, если `x` придает в квадрат внутри метода, что в квадрат, что фактически придано  `x` ссылается на  `n`.  
  
## Перестановка типов значений  
 Распространенным примером изменить значения аргументов метода обмена, где следует передать значение 2 переменной методу, а метод передает их содержимое.  Необходимо передать аргументы для метода обмена по ссылке.  В противном случае перейдите локальные копии параметров в методе, а отсутствие изменения не происходит в вызывающем методе.  Следующий пример меняет целочисленные значения.  
  
 [!code-cs[csProgGuideParameters#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_3.cs)]  
  
 При вызове `SwapByRef` метод, использующий  `ref` ключевое слово в вызов, как показано в следующем примере.  
  
 [!code-cs[csProgGuideParameters#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/csharp/passing-value-type-param_4.cs)]  
  
## См. также  
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Передача параметров](../../../csharp/programming-guide/classes-and-structs/passing-parameters.md)   
 [Передача параметров ссылочного типа](../../../csharp/programming-guide/classes-and-structs/passing-reference-type-parameters.md)