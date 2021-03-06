---
title: "Расширение системы безопасности | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "безопасность [WCF], расширение"
ms.assetid: a015a040-9fdf-4147-9ea9-f83b570be1d4
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# Расширение системы безопасности
Для размещения новых типов утверждений и пользовательских маркеров можно расширить инфраструктуру безопасности [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Это подробно описывается в следующих подразделах.  
  
## В этом подразделе  
 [Security Architecture](http://msdn.microsoft.com/ru-ru/16593476-d36a-408d-808c-ae6fd483e28f)  
 Пошаговое рассмотрение архитектуры системы безопасности [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Пользовательские учетные данные и проверка учетных данных](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md)  
 Рассматривается, как модель удостоверения используется при проверке пользовательских учетных данных.  
  
 [Пользовательские маркеры](../../../../docs/framework/wcf/extending/custom-tokens.md)  
 Маркеры, выдаваемые службой маркеров безопасности \(STS\), — обычно маркеры SAML.В этом разделе описывается, как создать тип пользовательского маркера.  
  
 [Пользовательская авторизация](../../../../docs/framework/wcf/extending/custom-authorization.md)  
 Объясняется, как реализовать пользовательскую авторизацию.  
  
 [Переопределение идентификатора службы для проверки подлинности](../../../../docs/framework/wcf/extending/overriding-the-identity-of-a-service-for-authentication.md)  
 Описывается, как переопределить идентификацию службы для проверки подлинности.  
  
 [Практическое руководство. Создание пользовательского средства проверки идентификации клиентов](../../../../docs/framework/wcf/extending/how-to-create-a-custom-client-identity-verifier.md)  
 Демонстрирует, как проверить идентификацию пользовательской конечной точки.  
  
 [Как использовать отдельные сертификаты X.509 для подписывания и шифрования](../../../../docs/framework/wcf/extending/how-to-use-separate-x-509-certificates-for-signing-and-encryption.md)  
 Обычно сообщения подписываются и шифруются одним сертификатом.В этом разделе объясняется, как при необходимости использовать два сертификата.  
  
 [Практическое руководство. Изменение поставщика служб шифрования для закрытого ключа сертификата X.509](../../../../docs/framework/wcf/extending/change-cryptographic-provider-x509-certificate-private-key.md)  
 Объясняется, как изменить поставщика служб шифрования, предоставлявшего закрытый ключ сертификата X.509, и как интегрировать поставщика в инфраструктуру [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
## Ссылка  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
## Связанные подразделы  
 [Безопасность](../../../../docs/framework/wcf/feature-details/security.md)  
  
 [Базовое программирование WCF](../../../../docs/framework/wcf/basic-wcf-programming.md)  
  
## См. также  
 [Общие сведения о безопасности](../../../../docs/framework/wcf/feature-details/security-overview.md)