---
title: "ORDER BY (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: c0b61572-ecee-41eb-9d7f-74132ec8a26c
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ORDER BY (Entity SQL)
Указывает порядок сортировки для объектов, возвращаемых инструкцией SELECT.  
  
## Синтаксис  
  
```  
  
[ ORDER BY   
   {  
      order_by_expression [SKIP n] [LIMIT n]  
      [ COLLATE collation_name ]  
      [ ASC | DESC ]  
   }  
   [ ,…n ]   
]  
```  
  
## Аргументы  
 `order_by_expression`  
 Любое допустимое выражение запроса, задающее свойство, по которому выполняется сортировка. Может быть указано несколько выражений сортировки. Последовательность выражений сортировки в предложении ORDER BY определяет порядок сортировки результирующего набора.  
  
 COLLATE {collation\_name}  
 Указывает, что операция ORDER BY должна выполняться в соответствии с параметрами сортировки, заданными в аргументе `collation_name`. COLLATE применяется только для строковых выражений.  
  
 ASC  
 Указывает, что значения в указанном свойстве должны быть отсортированы в порядке возрастания, от меньшего к большему. Это значение по умолчанию.  
  
 DESC  
 Указывает, что значения в указанном свойстве должны быть отсортированы в порядке убывания, от большего к меньшему.  
  
 LIMIT `n`  
 Будут выбраны только первые `n` элементов.  
  
 SKIP `n`  
 Пропускает первые `n` элементов.  
  
## Заметки  
 Предложение ORDER BY логически применяется к результату предложения SELECT. Предложение ORDER BY может ссылаться на элементы списка выбора по их псевдонимам. Предложение ORDER BY может также ссылаться на другие переменные, находящиеся в области видимости. Однако если предложение SELECT указано с модификатором DISTINCT, то предложение ORDER BY может ссылаться только на псевдонимы из предложения SELECT.  
  
 `SELECT c AS c1 FROM cs AS c ORDER BY c1.e1, c.e2`  
  
 Выражения в предложении ORDER BY должны иметь сравнимый тип, поскольку для упорядочивания производится сравнение элементов \(меньше, больше и т. д.\). Такими типами обычно являются скалярные примитивы \- числа, строки и даты. Типы RowType для сравнимых типов также являются сравнимыми для упорядочивания.  
  
 Если код проходит по упорядоченному набору, отличному от проекции верхнего уровня, то сохранение порядка в выходных данных не гарантируется.  
  
```  
-- In the following sample, order is guaranteed to be preserved:  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
 Получить упорядоченный результат выполнения операции UNION, UNION ALL, EXCEPT или INTERSECT можно следующим образом.  
  
```  
SELECT ...  
FROM ( UNION/EXCEPT/INTERSECT operation )  
ORDER BY ...  
```  
  
## Служебные ключевые слова  
 Следующие ключевые слова при использовании в предложении `ORDER BY` необходимо заключать в кавычки.  
  
-   CROSS  
  
-   FULL  
  
-   KEY  
  
-   LEFT  
  
-   ORDER  
  
-   OUTER  
  
-   RIGHT  
  
-   ROW  
  
-   VALUE  
  
## Упорядочение вложенных запросов  
 Платформа Entity Framework позволяет разместить вложенное выражение в любом месте запроса. Порядок вложенного запроса не сохраняется.  
  
```  
-- The following query will order the results by the last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## Пример  
 В следующем запросе [!INCLUDE[esql](../../../../../../includes/esql-md.md)] оператор ORDER BY задает порядок сортировки для объектов, возвращаемых инструкцией SELECT. Запрос основан на модели AdventureWorks Sales. Для компиляции и запуска этого запроса выполните следующие шаги.  
  
1.  Выполните процедуру из статьи [Как выполнить запрос, возвращающий результаты типа StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Передайте следующий запрос в качестве аргумента методу `ExecuteStructuralTypeQuery`:  
  
 [!code-csharp[DP EntityServices Concepts 2#ORDERBY](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#orderby)]  
  
## См. также  
 [Выражения запросов](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)   
 [Справочник по Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)   
 [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)   
 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)