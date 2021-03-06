---
title: "Общие сведения о модели программирования WCF Web HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
caps.latest.revision: 45
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 45
---
# Общие сведения о модели программирования WCF Web HTTP
Модель программирования [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] WEB HTTP предоставляет основные элементы, необходимые для построения служб WEB HTTP с помощью [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP рассчитаны на доступ со стороны широкого диапазона возможных клиентов, включая веб\-браузеры, и обладают следующими уникальными требованиями.  
  
-   **URI и обработка URI.** URI играют центральную роль в проектировании служб WEB HTTP.Для предоставления возможностей обработки URI модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP использует классы <xref:System.UriTemplate> и <xref:System.UriTemplateTable>.  
  
-   **Поддержка операций GET и POST.** Службы WEB HTTP используют команду GET для получения данных, а также различные команды вызова для изменения данных и удаленного вызова.В модели программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP используются атрибуты <xref:System.ServiceModel.Web.WebGetAttribute> и <xref:System.ServiceModel.Web.WebInvokeAttribute> для сопоставления операций службы с командой GET и другими командами HTTP, такими как PUT, POST и DELETE.  
  
-   **Несколько форматов данных.** Веб\-службы обрабатывают много типов данных, помимо сообщений SOAP.Для поддержки нескольких различных форматов данных \(включая документы XML, объекты данных JSON и потоки двоичного содержимого, такие как изображения, видеофайлы или обычный текст\) модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP использует привязку <xref:System.ServiceModel.WebHttpBinding> и поведение <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
 Модель программирования WEB HTTP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] расширяет возможности [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] и делает возможной поддержку веб\-сценариев, включающих службы WEB HTTP, AJAX и JSON, а также каналы синдикации \(ATOM\/RSS\).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] службах AJAX и JSON см. в разделе [Интеграция с AJAX и поддержка JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] синдикации см. в разделе [Общие сведения о синдикации WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md).  
  
 Какие\-либо дополнительные ограничения на типы данных, которые могут быть возвращены из веб\-службы HTTP, отсутствуют.При работе веб\-службы HTTP могут быть возвращены любые сериализуемые данные.Поскольку операции веб\-службы HTTP могут быть вызваны веб\-браузером, имеется ограничение относительно того, какие типы данных могут указываться в URL\-адресах.Дополнительные сведения о том, какие типы поддерживаются по умолчанию, см. в приведенном далее разделе **Параметры и URL\-адреса строки запроса UriTemplate**.Это поведение по умолчанию можно изменить, предоставив собственную реализацию объекта T:System.ServiceModel.Dispatcher.QueryStringConverter, которая определяет, как преобразовывать параметры, заданные в URL\-адресе, в фактические типы параметров.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Dispatcher.QueryStringConverter>  
  
> [!CAUTION]
>  Службы, написанные по модели программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP, не используют сообщения SOAP.Поскольку SOAP не используется, то нельзя использовать средства безопасности, предоставляемые [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)],Однако вы можете использовать безопасность уровня транспорта, разместив службу через HTTPS.[!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] о безопасности см. в разделе [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)  
  
> [!WARNING]
>  Установка расширения WebDAV для служб IIS может привести к тому, что веб\-службы HTTP будут возвращать ошибку HTTP 405, поскольку расширение WebDAV пытается обрабатывать все запросы PUT.Для решения этой проблемы расширение WebDAV можно удалить либо отключить его для данного веб\-узла.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS и WebDav](http://learn.iis.net/page.aspx/357/webdav-for-iis-70/)  
  
## Обработка универсального кода ресурса \(URI\) с помощью UriTemplate и UriTemplateTable  
 Шаблоны URI предоставляют эффективный синтаксис представления больших наборов URI или схожих по структуре URI.Например, следующий шаблон представляет набор всех трехсегментных URI, начинающихся с "a" и заканчивающихся на "c", независимо от значения промежуточного сегмента: a\/{segment}\/c.  
  
 Данный шаблон описывает универсальные коды ресурса, подобные следующим:  
  
-   a\/x\/c  
  
-   a\/y\/c  
  
-   a\/z\/c  
  
-   и т. д.  
  
 В этом шаблоне запись в фигурных скобках \("{segment}"\) обозначает переменный сегмент, а не литеральное значение.  
  
 Платформа .NET Framework предусматривает API для работы с шаблонами URI, который называется <xref:System.UriTemplate>.`UriTemplates` дает возможность выполнять следующие действия:  
  
-   Для создания соответствующего шаблону *полностью закрытого URI* можно вызвать один из методов `Bind` с набором параметров.Это означает, что все переменные в шаблоне URI заменяются фактическими значениями.  
  
-   Можно вызвать `Match`\(\) с потенциальным URI, который использует шаблон для разбиения потенциального URI на составные части и возвращает словарь, содержащий различные части URI, помеченные в соответствии с переменными в шаблоне.  
  
-   `Bind`\(\) и `Match`\(\) являются инверсиями, поэтому можно вызвать `Match`\( `Bind`\( x \) \) и вернуться к той среде, в которой была начата работа.  
  
 Очень часто \(особенно на стороне сервера, где необходимо направить запрос операции службы на основе URI\), бывает необходимо отслеживать набор объектов <xref:System.UriTemplate> в структуре данных, которые могут независимо обращаться к каждому из включенных шаблонов.<xref:System.UriTemplateTable> представляет набор шаблонов URI и выбирает самый подходящий заданный набор шаблонов и потенциальный URI.Этот набор не связан ни с одним конкретным сетевым стеком \(включая [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]\), поэтому его можно использовать везде, где необходимо.  
  
 Для связывания операций службы с набором URI, который описывается шаблоном <xref:System.UriTemplate>, модель службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] использует шаблон <xref:System.UriTemplate> и таблицу шаблонов <xref:System.UriTemplateTable>.Операция службы связывается с шаблоном <xref:System.UriTemplate> с помощью атрибута <xref:System.ServiceModel.Web.WebGetAttribute> или <xref:System.ServiceModel.Web.WebInvokeAttribute>.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] об <xref:System.UriTemplate> и <xref:System.UriTemplateTable> см. в разделе [UriTemplate и UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md).  
  
## Атрибуты WebGet и WebInvoke  
 Службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP используют команды получения \(например, HTTP GET\), а также различные команды вызова \(например, HTTP POST, PUT и DELETE\).Модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP позволяет разработчикам службы управлять шаблоном URI и командой, связанной с операциями службы, с помощью атрибутов <xref:System.ServiceModel.Web.WebGetAttribute> и <xref:System.ServiceModel.Web.WebInvokeAttribute>.Атрибуты <xref:System.ServiceModel.Web.WebGetAttribute> и <xref:System.ServiceModel.Web.WebInvokeAttribute> позволяют управлять привязкой отдельных операций к URI и методам HTTP, связанным с этими URI.Например, добавление атрибутов <xref:System.ServiceModel.Web.WebGetAttribute> и <xref:System.ServiceModel.Web.WebInvokeAttribute> продемонстрировано в следующем примере кода.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,   
                               string newName );  
}  
```  
  
 Предыдущий код позволяет создавать следующие HTTP\-запросы.  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 Атрибут <xref:System.ServiceModel.Web.WebInvokeAttribute> по умолчанию имеет значение POST, но его можно использовать и для других команд.  
  
```  
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It“ -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 Полный образец кода службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], использующей модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP, см. в разделе [Как создать простую веб\-службу WCF HTTP](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-wcf-web-http-service.md).  
  
## Параметры строки запроса UriTemplate и URL\-адреса  
 Веб\-службы можно вызвать из веб\-браузера, введя URL\-адрес, связанный с операцией службы.Эти операции службы могут принимать параметры строки запроса, которые необходимо указывать в URL\-адресе в строковом формате.В таблице ниже представлены типы, которые могут передаваться внутри URL\-адреса и используемого формата.  
  
|Тип|Формат|  
|---------|------------|  
|<xref:System.Byte>|0 \- 255|  
|<xref:System.SByte>|\-128 \- 127|  
|<xref:System.Int16>|\-32768 \- 32767|  
|<xref:System.Int32>|\-2,147,483,648 \- 2,147,483,647|  
|<xref:System.Int64>|\-9,223,372,036,854,775,808 \- 9,223,372,036,854,775,807|  
|<xref:System.UInt16>|0 \- 65535|  
|<xref:System.UInt32>|0 \- 4,294,967,295|  
|<xref:System.UInt64>|0 \- 18,446,744,073,709,551,615|  
|<xref:System.Single>|\-3.402823e38–3.402823e38 \(экспоненциальная запись не требуется\)|  
|<xref:System.Double>|\-1.79769313486232e308–1.79769313486232e308 \(экспоненциальная запись не требуется\)|  
|<xref:System.Char>|Любой отдельный знак|  
|<xref:System.Decimal>|Любое десятичное число в стандартной записи \(без экспоненты\)|  
|<xref:System.Boolean>|True или False \(с учетом регистра\)|  
|<xref:System.String>|Любая строка \(пустая строка не поддерживается, преобразование не производится\)|  
|<xref:System.DateTime>|ММ\/ДД\/ГГГГ<br /><br /> ММ\/ДД\/ГГГГ ЧЧ:ММ:СС \[AM&#124;PM\]<br /><br /> Месяц, день, год<br /><br /> Месяц, день, год, ЧЧ:ММ:СС \[AM&#124;PM\]|  
|<xref:System.TimeSpan>|ДД.ЧЧ:ММ:СС,<br /><br /> где ДД \= дни, ЧЧ \= часы, ММ \= минуты, СС \= секунды.|  
|<xref:System.Guid>|Например, идентификатор GUID:<br /><br /> 936DA01F\-9ABD\-4d9d\-80C7\-02AF85C822A8|  
|<xref:System.DateTimeOffset>|ММ\/ДД\/ГГГГ ЧЧ:ММ:СС ММ:СС,<br /><br /> где ДД \= дни, ЧЧ \= часы, ММ \= минуты, СС \= секунды.|  
|Enumerations|Значение перечисления, которое, например, определяет перечисление, как показано в следующем примере кода.<br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> В строке запроса можно указать любое отдельное значение перечисления \(или соответствующее ему целочисленное значение\).|  
|Типы, содержащие атрибут `TypeConverterAttribute`, который может преобразовывать типы в строковое представление и обратно.|Зависит от преобразователя типов.|  
  
## Форматы и модель программирования WCF WEB HTTP  
 Модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP содержит новые функции для работы с несколькими различными форматами данных.На уровне привязки <xref:System.ServiceModel.WebHttpBinding> может считывать и записывать следующие различные типы данных.  
  
-   XML  
  
-   JSON  
  
-   Непрозрачные двоичные потоки  
  
 Это означает, что модель программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WEB HTTP может обрабатывать любой тип данных, но при этом возможно программирование объектов <xref:System.IO.Stream>.  
  
 [!INCLUDE[netfx35_short](../../../../includes/netfx35-short-md.md)] обеспечивает поддержку данных JSON \(AJAX\), а также RSS\-каналов \(включая ATOM и RSS\).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] об этих возможностях см. в разделах [Форматирование веб\-объектов HTTP WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)[Общие сведения о синдикации WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication-overview.md) и [Интеграция с AJAX и поддержка JSON](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md).  
  
## Модель программирования WCF WEB HTTP и безопасность  
 Поскольку модель веб\-программирования HTTP в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] не поддерживает протоколы WS\-\*, единственным способом защитить веб\-службы HTTP в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] является обеспечение доступа к ней через HTTPS с использованием SSL\-сертификата.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] о настройке SSL с помощью [!INCLUDE[iisver](../../../../includes/iisver-md.md)] см. в разделе [Как реализовать SSL в IIS](http://go.microsoft.com/fwlink/?LinkId=131613)  
  
## Устранение неполадок в модели программирования WCF WEB HTTP  
 Когда службы WCF WEB HTTP вызываются с помощью <xref:System.ServiceModel.Channels.ChannelFactory%601> для создания канала, <xref:System.ServiceModel.Description.WebHttpBehavior> использует адрес <xref:System.ServiceModel.EndpointAddress>, заданный в файле конфигурации, даже в случае, когда в <xref:System.ServiceModel.Channels.ChannelFactory%601> передается другой <xref:System.ServiceModel.EndpointAddress>.  
  
## См. также  
 [Синдикация WCF](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)   
 [Объектная модель программирования WCF Web HTTP](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)   
 [Модель веб\-программирования HTTP WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)