---
title: "Asynchronous Programming Model (APM) | Microsoft Docs"
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
  - "ending asynchronous operations"
  - "starting asynchronous operations"
  - "beginning asynchronous operations"
  - "asynchronous programming, ending operations"
  - "asynchronous programming"
  - "stopping asynchronous operations"
  - "asynchronous programming, beginning operations"
ms.assetid: c9b3501e-6bc6-40f9-8efd-4b6d9e39ccf0
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Asynchronous Programming Model (APM)
Асинхронная операция, использующая шаблон разработки <xref:System.IAsyncResult>, реализуется в виде двух методов с именами **Begin** *Имя\_операции* и **End** *Имя\_операции*, которые соответственно начинают и завершают асинхронную операцию *Имя\_операции*. Например, класс <xref:System.IO.FileStream> предоставляет методы <xref:System.IO.FileStream.BeginRead%2A> и <xref:System.IO.FileStream.EndRead%2A> для асинхронного считывания байтов из файла. Эти методы реализуют асинхронную версию метода <xref:System.IO.FileStream.Read%2A>.  
  
> [!NOTE]
>  Начиная с версии .NET Framework 4 библиотека параллельных задач предоставляет новую модель для асинхронного и параллельного программирования. Дополнительные сведения см. в разделах [Task Parallel Library \(TPL\)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md) и [Task\-based Asynchronous Pattern \(TAP\)](../../../docs/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md).\)  
  
 После вызова метода **Begin** *Имя\_операции* приложение может продолжить выполнение инструкций в вызывающем потоке, пока асинхронная операция выполняется в другом потоке. Для каждого вызова метода **Begin** *Имя\_операции* в приложении также должен присутствовать вызов метода **End** *Имя\_операции* для получения результатов операции.  
  
## Начало асинхронной операции  
 Метод **Begin** *Имя\_операции* начинает асинхронную операцию *Имя\_операции* и возвращает объект, реализующий интерфейс <xref:System.IAsyncResult>. В объектах <xref:System.IAsyncResult> хранятся сведения об асинхронных операциях. В таблице ниже приведены сведения об асинхронной операции.  
  
|Член|Описание|  
|----------|--------------|  
|<xref:System.IAsyncResult.AsyncState%2A>|Относящийся к необязательному приложению объект, содержащий сведения об асинхронной операции.|  
|<xref:System.IAsyncResult.AsyncWaitHandle%2A>|Объект <xref:System.Threading.WaitHandle>, который можно использовать, чтобы заблокировать выполнение приложения до завершения асинхронной операции.|  
|<xref:System.IAsyncResult.CompletedSynchronously%2A>|Значение, показывающее, что асинхронная операция выполнена в потоке, который использовался для вызова метода **Begin** *Имя\_операции*, а не в отдельном потоке <xref:System.Threading.ThreadPool>.|  
|<xref:System.IAsyncResult.IsCompleted%2A>|Значение, показывающее, выполнена ли асинхронная операция.|  
  
 Метод **Begin** *Имя\_операции* принимает любые параметры, объявленные в сигнатуре синхронной версии метода, которые передаются по значению или по ссылке. Выходные параметры не входят в сигнатуру метода **Begin** *Имя\_операции*. В сигнатуру метода **Begin** *Имя\_операции* также входят два дополнительных параметра. Первый из них определяет делегат <xref:System.AsyncCallback>, который ссылается на метод, вызываемый при завершении асинхронной операции. Вызывающий объект может указать значение `null` \(`Nothing` в Visual Basic\), если не нужно вызывать метод при завершении операции. Вторым дополнительным параметром является определяемый пользователем объект. Этот объект можно использовать для передачи сведений о состоянии, относящихся к приложению, в метод, который вызывается при завершении асинхронной операции. Если метод **Begin** *Имя\_операции* принимает дополнительные параметры, относящиеся к операции, например массив байтов для хранения байтов, считанных из файла, объект <xref:System.AsyncCallback> и объект состояния приложения являются последними параметрами в сигнатуре метода **Begin** *Имя\_операции*.  
  
 Метод **Begin** *Имя\_операции* немедленно возвращает управление в вызывающий поток. Если метод **Begin** *Имя\_операции* создает исключения, это происходит до запуска асинхронной операции. Если метод **Begin** *Имя\_операции* создает исключения, метод обратного вызова не вызывается.  
  
## Завершение асинхронной операции  
 Метод **End** *Имя\_операции* завершает асинхронную операцию *Имя\_операции*. Возвращаемое значение метода **End** *Имя\_операции* имеет тот же тип, что и значение его синхронной версии, и определяется асинхронной операцией. Например, метод <xref:System.IO.FileStream.EndRead%2A> возвращает число байтов, считанных из потока <xref:System.IO.FileStream>, а метод <xref:System.Net.Dns.EndGetHostByName%2A> возвращает объект <xref:System.Net.IPHostEntry>, содержащий сведения о сервере. Метод **End** *Имя\_операции* принимает любые параметры out или ref, объявленные в сигнатуре синхронной версии метода. В дополнение к параметрам из синхронного метода метод **End** *Имя\_операции* также включает параметр <xref:System.IAsyncResult>. Вызывающие объекты должны передавать экземпляр, возвращаемый соответствующим вызовом метода **Begin** *Имя\_операции*.  
  
 Если асинхронная операция, представленная объектом <xref:System.IAsyncResult>, не завершилась к моменту вызова метода **End** *Имя\_операции*, метод **End** *Имя\_операции* блокирует выполнение вызывающего потока до момента завершения асинхронной операции. Исключения, создаваемые асинхронной операцией, возникают из метода **End** *Имя\_операции*. Результат многократного вызова метода **End** *Имя\_операции* с одним экземпляром <xref:System.IAsyncResult> не определен. Аналогично, вызов метода **End** *Имя\_операции* с объектом <xref:System.IAsyncResult>, который не был возвращен соответствующим методом Begin, также имеет неопределенный эффект.  
  
> [!NOTE]
>  В случае реализации этих неопределенных сценариев рекомендуется вызывать исключение <xref:System.InvalidOperationException>.  
  
> [!NOTE]
>  В случае реализации этого шаблона разработки необходимо уведомить вызывающий объект о завершении асинхронной операции, установив свойство <xref:System.IAsyncResult.IsCompleted%2A> в значение true, вызвав асинхронный метод обратного вызова \(если он указан\) и отправив сигнал <xref:System.IAsyncResult.AsyncWaitHandle%2A>.  
  
 Разработчики приложений имеют выбор способов доступа к результатам асинхронной операции. Правильный выбор зависит от того, содержит ли приложение инструкции, которые могут выполняться, пока не завершена операция. Если приложение не может выполнять дополнительную работу, пока не получены результаты асинхронной операции, его необходимо заблокировать до момента, когда станут доступны результаты. Чтобы заблокировать работу до завершения асинхронной операции, используйте один из описанных ниже способов.  
  
-   Вызов метода **End** *Имя\_операции* из главного потока приложения блокирует выполнение приложения до завершения операции. Пример, демонстрирующий этот способ, см. в разделе [Blocking Application Execution by Ending an Async Operation](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-by-ending-an-async-operation.md).  
  
-   Используйте свойство <xref:System.IAsyncResult.AsyncWaitHandle%2A>, чтобы заблокировать выполнение приложения до завершения одной или нескольких операций. Пример, демонстрирующий этот способ, см. в разделе [Blocking Application Execution Using an AsyncWaitHandle](../../../docs/standard/asynchronous-programming-patterns/blocking-application-execution-using-an-asyncwaithandle.md).  
  
 В приложениях, которые не нужно блокировать до завершения асинхронной операции, можно использовать один из описанных ниже способов.  
  
-   Запрашивайте состояние выполнения операции, периодически проверяя свойство <xref:System.IAsyncResult.IsCompleted%2A>, и вызовите метод **End** *Имя\_операции*, когда операция будет завершена. Пример, демонстрирующий этот способ, см. в разделе [Polling for the Status of an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/polling-for-the-status-of-an-asynchronous-operation.md).  
  
-   Используйте делегат <xref:System.AsyncCallback> для указания метода, который должен вызываться при завершении операции. Пример, демонстрирующий этот способ, см. в разделе [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).  
  
## См. также  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)   
 [Using an AsyncCallback Delegate and State Object](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-and-state-object.md)