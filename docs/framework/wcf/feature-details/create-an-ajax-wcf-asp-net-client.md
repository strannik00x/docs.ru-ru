---
title: "Практическое руководство. Создание службы WCF с поддержкой AJAX и клиента ASP.NET для обращения к службе | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 95012df8-2a66-420d-944a-8afab261013e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Практическое руководство. Создание службы WCF с поддержкой AJAX и клиента ASP.NET для обращения к службе
В этом разделе показано, как использовать Visual Studio 2008 для создания службы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] с поддержкой AJAX и клиента ASP.NET, который к ней обращается. Коды для службы и для клиента содержатся в разделе «Пример», который следует за разделом «Процедуры», в котором описаны шаги их создания.  
  
### <a name="to-create-the-aspnet-client-application"></a>Создание клиентского приложения ASP.NET.  
  
1.  Откройте [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Из **файл** выберите пункт **New**, затем **проекта**, затем **Web**и выберите **веб-приложение ASP.NET**.  
  
3.  Назовите проект `SandwichServices` и нажмите кнопку **ОК**.  
  
### <a name="to-create-the-wcf-ajax-enabled-service"></a>Создание службы WCF с поддержкой AJAX  
  
1.  Щелкните правой кнопкой мыши `SandwichServices` проекта в **обозревателе решений** и выберите пункт **добавить**, затем **новый элемент**, а затем **служба WCF с поддержкой AJAX**.  
  
2.  Имя службы `CostService` в **имя** и нажмите кнопку **добавить**.  
  
3.  Откройте файл CostService.svc.cs.  
  
4.  Укажите `Namespace` для <xref:System.ServiceModel.ServiceContractAttribute> как `SandwichService`:  
  
    ```  
    namespace SandwichServices  
    {  
      [ServiceContract(Namespace = "SandwichServices")]  
      [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
       public class CostService  
       {  
         …  
       }  
     }  
    ```  
  
5.  Реализация операций службы. Добавить <xref:System.ServiceModel.OperationContractAttribute> для каждой из операций, чтобы указать, что они являются частью контракта. В следующем примере реализован метод, который возвращает стоимость заданного числа сандвичей.  
  
    ```  
    public class CostService  
    {  
        [OperationContract]  
        public double CostOfSandwiches(int quantity)  
        {  
            return 1.25 * quantity;  
        }  
  
    // Add more operations here and mark them with [OperationContract]  
    }  
    ```  
  
### <a name="to-configure-the-client-to-access-the-service"></a>Настройка клиента для доступа к службе.  
  
1.  Откройте страницу Default.aspx и выберите **разработки** представления.  
  
2.  От **представление** выберите пункт **элементов**.  
  
3.  Разверните **расширений AJAX** узел и перетащите **ScriptManager** на страницу Default.aspx.  
  
4.  Щелкните правой кнопкой мыши **ScriptManager** и выберите **свойства**.  
  
5.  Разверните **службы** коллекции в **свойства** окно, чтобы открыть **редактор коллекции ServiceReference** окна.  
  
6.  Щелкните **добавить**, укажите `CostService.svc` как **путь** и нажмите **ОК**.  
  
7.  Разверните **HTML** узел в **элементов** и перетащите **Input (Button)** на страницу Default.aspx.  
  
8.  Щелкните правой кнопкой мыши **кнопку** и выберите **свойства**.  
  
9. Изменение **значение** на `Price for 3 Sandwiches`.  
  
10. Дважды щелкните **кнопку** для доступа к коду JavaScript.  
  
11. Передайте следующий код JavaScript в `script`настроек элемента.  
  
    ```  
    function Button1_onclick() {  
    var service = new SandwichServices.CostService();  
    service.CostOfSandwiches(3, onSuccess, null, null);  
    }  
  
    function onSuccess(result){  
    alert(result);  
    }  
    ```  
  
### <a name="to-access-the-service-from-the-client"></a>Доступ к службе из клиента  
  
1.  Используйте сочетание клавиш Ctrl+F5 для запуска службы и веб-клиента. Щелкните **цена за 3 Жареных Сандвича** кнопку, чтобы создать ожидаемый результат «3,75».  
  
## <a name="example"></a>Пример  
 Этот пример содержит код службы, содержащийся в файле WCFService.svc.cs, и код клиента, содержащийся в файле Default.aspx.  
  
```  
//The service code contained in the CostService.svc.cs file.  
  
using System;  
using System.Linq;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Activation;  
using System.ServiceModel.Web;  
  
namespace SandwichServices  
{  
    [ServiceContract(Namespace="SandwichServices")]  
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]  
    public class CostService  
    {  
        // Add [WebGet] attribute to use HTTP GET  
        [OperationContract]  
        public double CostOfSandwiches(int quantity)  
        {  
            return 1.25 * quantity;  
        }  
  
        // Add more operations here and mark them with [OperationContract]  
    }  
}  
//The code for hosting the service is contained in the CostService.svc file.  
  
<%@ ServiceHost Language="C#" Debug="true" Service="SandwichServices.CostService" CodeBehind="CostService.svc.cs" %>  
  
//The client code contained in the Default.aspx file.  
  
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="SandwichServices._Default" %>  
  
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
  
<html >  
<head runat="server">  
    <title>Untitled Page</title>  
<script language="javascript" type="text/javascript">  
// <!CDATA[  
  
function Button1_onclick() {  
var service = new SandwichServices.CostService();  
service.CostOfSandwiches(3, onSuccess, null, null);  
}  
  
function onSuccess(result){  
alert(result);  
}  
  
// ]]>  
</script>  
</head>  
<body>  
    <form id="form1" runat="server">  
    <div>  
  
    </div>  
    <asp:ScriptManager ID="ScriptManager1" runat="server">  
        <services>  
            <asp:servicereference Path="CostService.svc" />  
        </services>  
    </asp:ScriptManager>  
    </form>  
    <p>  
        <input id="Button1" type="button" value="Price for 3 Sandwiches" onclick="return Button1_onclick()" /></p>  
</body>  
</html>  
  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->