---
title: "Как получить доступ к службе из приложения рабочего процесса | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 925ef8ea-5550-4c9d-bb7b-209e20c280ad
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Как получить доступ к службе из приложения рабочего процесса
В этом разделе описывается вызов службы рабочего процесса из консольного приложения рабочего процесса.Он связан с разделом [Как создать службу рабочего процесса с помощью действий обмена сообщениями](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md).Хотя в этом разделе описывается вызов службы рабочего процесса из приложения рабочего процесса, эти же методы можно использовать для вызова любых служб [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] из приложения рабочего процесса.  
  
### Создание проекта консольного приложения рабочего процесса  
  
1.  Запустите [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Загрузите проект MyWFService, созданный в разделе [Как создать службу рабочего процесса с помощью действий обмена сообщениями](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md).  
  
3.  Щелкните правой кнопкой мыши решение **MyWFService** в **обозревателе решений** и выберите **Добавить**, а затем **Создать проект**.Выберите **Рабочий процесс** в области **Установленные шаблоны** и выберите в списке типов проекта **Консольное приложение рабочего процесса**.Назовите проект MyWFClient и используйте расположение по умолчанию, как показано на следующем рисунке.  
  
     ![Диалоговое окно "Добавить новый проект"](../../../../docs/framework/wcf/feature-details/media/addnewprojectdlg.JPG "AddNewProjectDlg")  
  
     Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление нового проекта**.  
  
4.  После создания проекта в конструкторе откроется файл Workflow1.xaml.Нажмите вкладку **Область элементов**, чтобы открыть область элементов, и щелкните вешку, чтобы оставить окно области элементов открытым.  
  
5.  Чтобы собрать и запустить службу, нажмите сочетание клавиш CTRL\+F5.Как и раньше, будет запущен ASP.NET Development Server, а в обозревателе Internet Explorer откроется страница справки WCF.Запомните URI этой страницы, поскольку его будет необходимо использовать в следующем шаге.  
  
     ![IE со страницей и URI справки WCF](../../../../docs/framework/wcf/feature-details/media/iewcfhelppagewuri.JPG "IEWCFHelpPageWURI")  
  
6.  В **обозревателе решений** щелкните правой кнопкой мыши проект **MyWFClient** и выберите команду **Добавить ссылку на службу**.Нажмите кнопку **Обнаружение** для поиска текущего решения для любой из служб.Нажмите треугольник рядом с Service1.xamlx в списке «Службы».Нажмите треугольник рядом с Service1, чтобы открыть список контрактов, реализованных службой Service1.Разверните узел **Service1** в списке **Службы**.В списке **Операции** отобразится операция с именем Echo, как показано на следующем рисунке.  
  
     ![Диалоговое окно "Добавить ссылку на службу"](../../../../docs/framework/wcf/feature-details/media/addservicereference.JPG "AddServiceReference")  
  
     Оставьте без изменений пространство имен, заданное по умолчанию, и нажмите **ОК**, чтобы закрыть диалоговое окно **Добавить ссылку на службу**.Отобразится следующее диалоговое окно.  
  
     ![Диалоговое окно уведомления при добавлении ссылки на службу](../../../../docs/framework/wcf/feature-details/media/asrdlg.JPG "ASRDlg")  
  
     Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно.Затем, чтобы построить решение, нажмите сочетание клавиш CTRL\+SHIFT\+B.Обратите внимание, что к области элементов был добавлен новый раздел с именем **MyWFClient.ServiceReference1.Activities**.Разверните этот раздел и обратите внимание на действие с именем Echo, которое было добавлено, как показано на следующем рисунке.  
  
     ![Действие Echo в панели элементов](../../../../docs/framework/wcf/feature-details/media/echoactivity.JPG "EchoActivity")  
  
7.  Перетащите действие <xref:System.ServiceModel.Activities.Sequence> в область конструктора.Оно находится в разделе области элементов **Поток управления**.  
  
8.  При установке фокуса на <xref:System.ServiceModel.Activities.Sequence> щелкните ссылку **Переменные** и добавьте строковую переменную с именем `inString`.Задайте для переменной значение по умолчанию `«Hello, world»`, а также строковую переменную с именем `outString`, как показано на следующей схеме.  
  
     ![Добавление переменной](../../../../docs/framework/wcf/feature-details/media/instringvar.JPG "inStringVar")  
  
9. Перетащите действие с именем **Echo** в <xref:System.ServiceModel.Activities.Sequence>.В окне свойств выполните привязку аргумента к переменной `inString` и аргумента `out_string` к переменной outString, как показано на следующем рисунке.При этом операции будет передано значение переменной `inString`, а затем будет принято возвращаемое значение и помещено в переменную `outString`.  
  
     ![Привязка аргументов к переменным](../../../../docs/framework/wcf/feature-details/media/argumentbind.JPG "ArgumentBind")  
  
10. Перетащите действие **WriteLine** и расположите его под действием **Echo**, чтобы отобразить строку, возвращаемую вызовом службы.Действие **WriteLine** находится в узле **Примитивы** в области элементов.Выполните привязку аргумента **Text** действия **WriteLine** с переменной `outString`, введя в текстовом поле `outString` в действии **WriteLine**.После этого рабочий процесс должен выглядеть так, как показано на следующем рисунке.  
  
     ![Полный рабочий процесс клиента](../../../../docs/framework/wcf/feature-details/media/completeclientwf.JPG "CompleteClientWF")  
  
11. Щелкните правой кнопкой мыши решение MyWFService и выберите **Установка автозагружаемых проектов...**Щелкните переключатель **Несколько запускаемых проектов** и выберите **Начать** для всех проектов в столбце **Действие**, как показано на следующем рисунке.  
  
     ![Параметры запускаемых проектов](../../../../docs/framework/wcf/feature-details/media/startupprojects.JPG "StartupProjects")  
  
12. Используйте сочетание клавиш Ctrl\+F5 для запуска службы и клиента.ASP.NET Development Server размещает службу, в обозревателе Internet Explorer отображается страница справки WCF, а клиентское приложение рабочего процесса запускается в окне консоли и отображает строку, возвращаемую службой \(«Hello, world»\).  
  
## См. также  
 [Службы рабочего процесса](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Как создать службу рабочего процесса с помощью действий обмена сообщениями](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)   
 [Использование службы WCF из рабочего процесса в веб\-проекте](http://go.microsoft.com/fwlink/?LinkId=207725)