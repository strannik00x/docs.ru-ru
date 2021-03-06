---
title: "&lt;peerAuthentication&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad545e6f-f06e-4549-ac92-09d758d5c636
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;peerAuthentication&gt;
Задает параметры проверки подлинности для сертификата однорангового узла, используемого одноранговым узлом.  
  
## Синтаксис  
  
```  
  
<peerAuthentication  
      customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
      certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
      revocationMode="NoCheck/Online/Offline"  
      trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|`certificateValidationMode`|Необязательное перечисление.  Задает один из трех режимов для проверки учетных данных.  Это атрибут типа <xref:System.ServiceModel.Security.X509CertificateValidationMode>.  Если свойству присвоено значение `Custom`, также необходимо указать свойство `customCertificateValidator`.|  
|`customCertificateValidatorType`|Необязательная строка.  Задает тип и сборку, используемые для проверки пользовательского типа.  Этот атрибут должен быть задан, когда `certificateValidationMode` имеет значение `Custom`.  Это атрибут типа <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] предоставляет используемый по умолчанию проверяющий элемент управления для сертификата точки, осуществляющий проверку того, находится ли этот сертификат в хранилище "Доверенные лица".  Он также проверяет цепочку сертификатов вплоть до действительного корня.  Можно реализовать пользовательский модуль проверки для задания другого поведения и использовать этот атрибут для указания на пользовательский модуль проверки.|  
|`revocationMode`|Необязательное перечисление.  Задает режим отзыва сертификатов.  Это атрибут типа <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>.  Система проверяет, что одноранговый сертификат не отозван, проводя его поиск в списке отозванных сертификатов.  Эта проверка выполняется либо в сети, либо в кэшированном списке отзыва.  Проверку отзыва сертификатов можно отключить, задав этому атрибуту значение NoCheck.|  
|`trustedStoreLocation`|Необязательное перечисление.  Задает расположение доверенного хранилища, где одноранговый сертификат проверяется системой безопасности [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  Это атрибут типа <xref:System.Security.Cryptography.X509Certificates.StoreLocation>.|  
  
### Дочерние элементы  
 Отсутствует.  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-servicecredentials.md)|Задает текущие учетные данные для однорангового узла.|  
  
## Заметки  
 Элемент `<authentication>` соответствует классу <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>.  Этот элемент задает модуль проверки, который вызывается во время проверки подлинности «от соседа к соседу» в сетке.  Когда новый одноранговый узел пытается установить соединение с соседним узлом, он передает свои учетные данные в отвечающий одноранговый узел.  Для проверки учетных данных удаленной стороны вызывается проверяющий элемент управления отвечающего узла.  Как только в сетке устанавливается одноранговое соединение, оба одноранговых узла выполняют взаимную проверку подлинности. Это означает, что вызываются проверяющие элементы управления на обоих концах.  
  
## См. также  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 [Работа с сертификатами](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [Одноранговая сеть](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/ru-ru/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/ru-ru/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [Защита приложений одноранговых каналов](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)