---
title: "Практическое руководство. Перебор каталогов с файлами с помощью параллельного класса | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "параллельные циклы, перебор каталогов"
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Практическое руководство. Перебор каталогов с файлами с помощью параллельного класса
Во многих случаях итерация файла является операцией, которая с легкостью выполняется параллельно.  В теме [How to: Iterate File Directories with PLINQ](../../../docs/standard/parallel-programming/how-to-iterate-file-directories-with-plinq.md) показан самый простой способ выполнения этой задачи, подходящий для большинства сценариев.  Однако сложности могут возникнуть, если коду предстоит обработка многих типов исключений, которые могут создаваться при входе в файловую систему.  В следующем примере показан один из возможных способов решения этой проблемы.  Для перебора по всем файлам и папкам определенного каталога используется итерация на основе стека, и код может перехватывать и обрабатывать различных исключения.  Но, конечно же, способ обработки исключений определяет только разработчик.  
  
## Пример  
 В следующем примере директории обрабатываются последовательно, а файлы \- параллельно.  Вероятно, это лучшее решение в ситуации, когда на один каталог приходится большое количество файлов.  Кроме того, возможна параллельная итерация каталога и последовательный доступ к каждому файлу.  Вполне возможно, что параллельное выполнение циклов будет неэффективным, если только не используется специальная система с большим количеством процессоров.  Однако в любом случае необходимо тщательно протестировать приложение, чтобы найти лучшее решение.  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 В этом примере файловый ввод\-вывод синхронный.  При работе с большими файлами или при использовании медленного сетевого соединения, возможно, асинхронный доступ к файлам окажется более эффективным.  Методы асинхронного ввода\-вывода можно использовать совместно с параллельной итерацией.  Дополнительные сведения см. в разделе [TPL and Traditional .NET Framework Asynchronous Programming](../../../docs/standard/parallel-programming/tpl-and-traditional-async-programming.md).  
  
 В этом примере используется локальная переменная `fileCount` для учета общего количества обработанных файлов.  Поскольку переменная может быть использована одновременно несколькими задачами, доступ к ней синхронизирован вызовом метода <xref:System.Threading.Interlocked.Add%2A?displayProperty=fullName>.  
  
 Обратите внимание, если исключение возникает в главном потоке, потоки, запускаемые методом <xref:System.Threading.Tasks.Parallel.ForEach%2A>, могут продолжить работу.  Чтобы остановить эти потоки, можно задать логическую переменную в обработчиках исключений и проверять ее значение при каждой итерации параллельного цикла.  Если значение соответствует возникшему исключению, с помощью переменной <xref:System.Threading.Tasks.ParallelLoopState> остановите или прервите цикл.  Для получения дополнительной информации см. [How to: Stop or Break from a Parallel.For Loop](http://msdn.microsoft.com/ru-ru/de52e4f1-9346-4ad5-b582-1a4d54dc7f7e).  
  
## См. также  
 [Data Parallelism](../../../docs/standard/parallel-programming/data-parallelism-task-parallel-library.md)