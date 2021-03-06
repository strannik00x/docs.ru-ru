---
title: "Как повторно использовать соединение между командой ADO.NET и DataContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e26c7eb-c18a-43b5-a8f0-28fd8b04b0f0
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Как повторно использовать соединение между командой ADO.NET и DataContext
Поскольку [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] является частью семейства технологий [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] и основан на службах, предоставляемых [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)], подключение между командой [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] и <xref:System.Data.Linq.DataContext> можно использовать несколько раз.  
  
## Пример  
 В следующем примере показано повторное использование подключения между командой [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] и <xref:System.Data.Linq.DataContext>.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
## См. также  
 [Дополнительные сведения](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)   
 [ADO.NET и LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/ado-net-and-linq-to-sql.md)   
 [Взаимодействие с базой данных](../../../../../../docs/framework/data/adonet/sql/linq/communicating-with-the-database.md)