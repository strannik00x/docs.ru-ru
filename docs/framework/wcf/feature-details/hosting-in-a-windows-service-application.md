---
title: "Размещение в приложении службы Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4199998-27f3-4dd9-aee4-0a4addfa9f24
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Размещение в приложении службы Windows
Службы Windows \(ранее называвшиеся службами Windows NT\) обеспечивают модель процессов, особенно подходящую для приложений, которые должны существовать в длительно исполняемом файле и не отображают никакой формы пользовательского интерфейса.  Временем существования процессов приложений служб Windows управляет диспетчер служб, который позволяет запускать, останавливать и приостанавливать приложения служб Windows.  Процесс службы Windows можно настроить на автоматический запуск при запуске компьютера, сделав его подходящей средой размещения для постоянно работающих приложений.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] приложениях служб Windows см. в разделе [Приложения служб Windows](http://go.microsoft.com/fwlink/?LinkId=89450).  
  
 Приложения, содержащие длительно исполняемые службы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], используют многие характеристики совместно со службами Windows.  В частности, службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \- это длительно исполняемые серверные файлы, которые непосредственно не взаимодействуют с пользователем и, следовательно, не реализуют никакой формы пользовательского интерфейса.  По существу размещение служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] в приложениях служб Windows является одной из возможностей создания надежных, длительно работающих приложений [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Перед разработчиками [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] часто встает вопрос, где разместить свое приложение [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \- в приложении службы Windows или в среде размещения IIS или службы активации Windows.  Рассмотреть возможность использования приложений служб Windows необходимо в следующих случаях.  
  
-   Приложение требует явной активации.  Например, службы Windows следует использовать, когда приложение должно запускаться автоматически при запуске сервера, а не динамически при поступлении первого входящего сообщения.  
  
-   Процесс, в котором размещается приложение, после запуска должен оставаться работающим.  После запуска процесс службы Windows остается работающим, если явно не завершается администратором сервера с помощью диспетчера служб.  Приложения, размещенные в IIS или службе активации Windows, могут запускаться и останавливаться динамически для обеспечения оптимального использования системных ресурсов.  Приложения, для которых требуется явное управление в течение времени существования их процесса размещения, должны использовать службы Windows, а не IIS или службу активации Windows.  
  
-   Служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] должна работать на сервере Windows Server 2003 и использовать транспорт, отличный от HTTP.  В Windows Server 2003 среда размещения [!INCLUDE[iis601](../../../../includes/iis601-md.md)] ограничена связью только по протоколу HTTP.  Приложения служб Windows не подвержены такому ограничению и могут использовать любой транспорт, поддерживаемый системой [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], включая net.tcp, net.pipe и net.msmq.  
  
### Размещение WCF в приложении службы Windows  
  
1.  Создайте приложение службы Windows.  Приложения служб Windows можно создавать в управляемом коде, используя классы в пространстве имен <xref:System.ServiceProcess>.  Это приложение должно включать один класс, наследуемый от <xref:System.ServiceProcess.ServiceBase>.  
  
2.  Свяжите время существования служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] с временем существования приложения службы Windows.  Как правило, требуется, чтобы службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], размещенные в приложении службы Windows, становились активными при запуске службы размещения, прекращали прослушивание сообщений при останове службы размещения и завершали процесс размещения, если служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] обнаруживает ошибку.  Это можно обеспечить, выполнив следующие действия.  
  
    -   Переопределите [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>, чтобы открыть один или несколько экземпляров <xref:System.ServiceModel.ServiceHost>.  В одном приложении службы Windows может размещаться несколько служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], которые запускаются и останавливаются вместе.  
  
    -   Переопределите <xref:System.ServiceProcess.ServiceBase.OnStop%2A>, чтобы вызвать <xref:System.ServiceModel.Channels.CommunicationObject.Closed> для любых работающих служб [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] приложения <xref:System.ServiceModel.ServiceHost>, которые были запущены в течение [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>.  
  
    -   Подпишитесь на событие <xref:System.ServiceModel.Channels.CommunicationObject.Faulted> приложения <xref:System.ServiceModel.ServiceHost> и используйте класс <xref:System.ServiceProcess.ServiceController>, чтобы завершить работу приложения службы Windows в случае ошибки.  
  
     Приложения служб Windows, в которых размещаются службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], развертываются и управляются так же, как приложения служб Windows, не использующие [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## См. также  
 <xref:System.ServiceProcess>   
 [Пошаговое руководство. Создание приложения служб Windows в конструкторе компонентов](http://go.microsoft.com/fwlink/?LinkId=94875)   
 [Как разместить службу WCF в управляемой службе Windows](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)   
 [Узел службы Windows](../../../../docs/framework/wcf/samples/windows-service-host.md)   
 [Программная архитектура приложений служб](http://go.microsoft.com/fwlink/?LinkID=94876)   
 [Функции размещения Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=201276)