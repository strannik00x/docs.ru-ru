---
title: "Активация UDP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b0ccd10-0dfb-4603-93f9-f0857c581cb7
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Активация UDP
Этот образец основан на образце [Транспорт: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).Он расширяет образец [Транспорт: UDP](../../../../docs/framework/wcf/samples/transport-udp.md) для поддержки активации процесса с помощью службы активации Windows \(WAS\).  
  
 Образец состоит из трех основных частей:  
  
-   Активатор протокола UDP — автономный процесс, получающий сообщения UDP от лица приложений, подлежащих активации.  
  
-   Клиент, использующий пользовательский транспорт UDP для отправки сообщений.  
  
-   Служба \(размещенная в рабочем процессе, активированном службой WAS\), получающая сообщения по пользовательскому транспорту UDP.  
  
## Активатор протокола UDP  
 Активатор протокола UDP представляет собой мост между клиентом [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] и службой [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Он обеспечивает передачу данных через протокол UDP на транспортном уровне.У него две основные функции.  
  
-   Адаптер прослушивателя WAS \(LA\), работающий совместно со службой WAS для активирования процессов в ответ на входящие сообщения.  
  
-   Прослушиватель протокола UDP, который принимает сообщения UDP от лица приложений, подлежащих активации.  
  
 Активатор должен работать как автономная программа на компьютере сервера.Обычно адаптеры прослушивателя WAS \(такие как NetTcpActivator и NetPipeActivator\) реализуются в долговременных службах Windows.Однако для простоты и ясности в данном образце активатор протокола реализован как автономное приложение.  
  
### Адаптер прослушивателя WAS  
 Адаптер прослушивателя WAS для протокола UDP реализован в классе `UdpListenerAdapter`.Именно этот модуль во взаимодействии со службой WAS выполняет активацию приложения для протокола UDP.Это производится путем вызова следующих интерфейсов Webhost API:  
  
-   `WebhostRegisterProtocol`  
  
-   `WebhostUnregisterProtocol`  
  
-   `WebhostOpenListenerChannelInstance`  
  
-   `WebhostCloseAllListenerChannelInstances`  
  
 После исходного вызова `WebhostRegisterProtocol` адаптер прослушивателя получает обратный вызов `ApplicationCreated` от службы WAS для всех приложений, зарегистрированных в applicationHost.config \(расположен в %windir%\\system32\\inetsrv\).В этом образце обрабатываются только приложения с включенным протоколом UDP \(с ИД протокола "net.udp"\).Другие реализации могут выполнять эту обработку по\-другому, если такие реализацию реагируют на динамические изменения конфигурации приложения \(например, переход приложения из отключенного состояния во включенное\).  
  
 Получение обратного вызова `ConfigManagerInitializationCompleted` показывает, что служба WAS завершила все уведомления для инициализации протокола.На этом этапе прослушиватель готов к обработке запросов активации.  
  
 При поступлении нового запроса, который является первым для приложения, адаптер прослушивателя вызывает `WebhostOpenListenerChannelInstance` в WAS, запуская рабочий процесс, если он еще не запущен.Затем загружаются обработчики протокола, и можно начинать обмен данными между адаптером прослушивателя и виртуальным приложением.  
  
 Адаптер прослушивателя регистрируется в файле %SystemRoot%\\System32\\inetsrv\\ApplicationHost.config в разделе \<`listenerAdapters`\> следующим образом:  
  
```  
<add name="net.udp" identity="S-1-5-21-2127521184-1604012920-1887927527-387045" />  
```  
  
### Прослушиватель протокола  
 Прослушиватель протокола UDP представляет собой модуль внутри активатора протокола, который ожидает передачи данных на конечной точке определяемой пользователем процедурой от лица виртуального приложения.Он реализован в классе `UdpSocketListener`.Конечная точка представлена как `IPEndpoint`, номер порта для которой извлекается из привязки протокола для сайта.  
  
### Служба управления  
 В данном образце для взаимодействия активатора и рабочего процесса WAS используется [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Служба, находящаяся в активаторе, называется службой управления.  
  
## Обработчики протоколов  
 После того как адаптер прослушивателя вызывает `WebhostOpenListenerChannelInstance`, диспетчер процесса WAS запускает рабочий процесс, если он еще не запущен.Затем диспетчер приложения внутри рабочего процесса загружает обработчик протокола процесса \(PPH\) UDP с запросом этого `ListenerChannelId`.В свою очередь PPH вызывает `IAdphManager`.`StartAppDomainProtocolListenerChannel`, чтобы запустить обработчик протокола AppDomain \(ADPH\) UDP.  
  
## HostedUDPTransportConfiguration  
 Информация регистрируется в файле Web.config следующим образом:  
  
```  
<serviceHostingEnvironment>  
<add name="net.udp" transportConfigurationType="Microsoft.ServiceModel.Samples.Hosting.HostedUdpTransportConfiguration, UdpActivation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=6fa904d2da1848d6" />  
</serviceHostingEnvironment>  
```  
  
## Специальная настройка для этого образца  
 Этот образец может быть построен и запущен только в ОС Windows Vista, Windows Server 2008 или Windows 7.Для запуска этого образца необходимо сначала правильно установить все компоненты.Установите образец в соответствии с приведенными ниже шагами.  
  
#### Настройка этого образца  
  
1.  Установите [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0, выполнив следующую команду.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Постройте проект в ОС Windows Vista.После компиляции на этапе за построением также выполняются следующие операции.  
  
    -   Устанавливается привязка UDP на сайт "Веб\-узел по умолчанию".  
  
    -   Создается виртуальное приложение "ServiceModelSamples", указывающее по физическому пути: "%SystemDrive%\\inetpub\\wwwroot\\servicemodelsamples".  
  
    -   Также включается протокол "net.udp" для данного виртуального приложения.  
  
3.  Запустите приложение пользовательского интерфейса "WasNetActivator.exe".На вкладке **Установка** установите следующие флажки и нажмите кнопку **Установить**, чтобы установить эти компоненты:  
  
    -   Адаптер прослушивателя UDP  
  
    -   Обработчики протокола UDP  
  
4.  Выберите вкладку **Активация** приложения пользовательского интерфейса "WasNetActivator.exe".Нажмите кнопку **Пуск** для запуска адаптера прослушивателя.Теперь все готово для запуска программы.  
  
    > [!NOTE]
    >  Завершив работу с этим образцом, необходимо запустить файл Cleanup.bat, чтобы удалить привязку net.udp с сайта «Веб\-узел по умолчанию».  
  
## Использование образца  
 После компиляции создаются четыре различных двоичных файла.  
  
-   Client.exe: код клиента.Файл App.config компилируется в файл конфигурации клиента Client.exe.config.  
  
-   UDPActivation.dll: библиотека, содержащая все основные реализации UDP.  
  
-   Service.dll: код службы.Он копируется в каталог \\bin виртуального приложения ServiceModelSamples.Файл службы имеет имя Service.svc, а файл конфигурации — Web.config.После компиляции они копируются в следующее местоположение: %SystemDrive%\\Inetpub\\wwwroot\\ServiceModelSamples.  
  
-   WasNetActivator: программа активатора UDP.  
  
-   Убедитесь, что все обязательные элементы правильно установлены.Следующие шаги показывают, как запустить образец:  
  
1.  Убедитесь, что запущены следующие службы Windows:  
  
    -   Служба активации Windows \(WAS\).  
  
    -   Internet Information Services \(IIS\): W3SVC.  
  
2.  Затем запустите активатор WasNetActivator.exe.На вкладке **Активация** в раскрывающемся списке выбран единственный протокол, **Определяемая пользователем процедура**.Нажмите кнопку **Пуск** для запуска активатора.  
  
3.  После запуска активатора можно запустить код клиента, запустив файл Client.exe в командном окне.Далее приводится образец вывода:  
  
    ```  
    Testing Udp Activation.  
    Start the status service.  
    Sending UDP datagrams.  
    Type a word that you want to say to the server: Hello, world!  
        Sending datagram: Hello, world![0]  
        Sending datagram: Hello, world![1]  
        Sending datagram: Hello, world![2]  
        Sending datagram: Hello, world![3]  
        Sending datagram: Hello, world![4]  
    Calling UDP duplex contract (ICalculatorContract).  
        0 + 0 = 0  
        1 + 2 = 3  
        2 + 4 = 6  
        3 + 6 = 9  
        4 + 8 = 12  
    Getting status and dump server traces:  
        Operation 'Hello' is called: Hello, world![0]  
        Operation 'Hello' is called: Hello, world![1]  
        Operation 'Hello' is called: Hello, world![2]  
        Operation 'Hello' is called: Hello, world![3]  
        Operation 'Hello' is called: Hello, world![4]  
        Operation 'Add' is called: 0 + 0  
        Operation 'Add' is called: 1 + 2  
        Operation 'Add' is called: 2 + 4  
        Operation 'Add' is called: 3 + 6  
        Operation 'Add' is called: 4 + 8  
    Press <ENTER> to complete test.  
    ```  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Extensibility\Transport\UdpActivation`  
  
## См. также