---
title: "Одноранговая совместная работа | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Одноранговая совместная работа
Одноранговая сеть помощью относительно мощных компьютеров \(pc\), существующих на границе Интернета, не просто основанных клиент\- вычислительных задач.  Самомоднейшее ПК \(PC\) имеет очень быстро процессор, более расширенную память и большой жесткий диск, что полностью использовать при выполнении общих вычислительных задач, как электронная почта и просмотра Интернета.  Самомоднейший ПК легко может действовать как клиент и как сервер \(одноранговый узел \(пользователь\) для многих типов приложений.  
  
-   Одноранговая инфраструктура взаимодействия упрощенная реализация инфраструктуры Microsoft Windows, которая использует службу одноранговой соседние пользователи в Windows Vista и более поздних платформах.  Она лучше всего используется для одноранговый\- разрешенных приложений в рамках подсети, для которой работает служба соседние пользователи, хотя она может обслуживать конечные точки или контакты интернета.  Она включает общий диспетчер контактов, используется Live Messenger и другими В реальном времени\- осведомленными приложениями задать конечные точки, доступность и наличие контакта.  
  
## Приложения взаимодействия  
 Типичное однорангового приложения взаимодействия состоит из следующих шагов:  
  
-   Одноранговый узел, указывающее идентификатор узла, нужны маркетинговые данные в размещение сеанс взаимодействия  
  
-   Отправить запрос размещение сеанс каким\-либо образом, а однорангового узла соглашается управлять действие взаимодействия.  
  
-   Основное приложение пригласит контакты в подсети \(включая запросившая сторона\) к сеансу.  
  
-   Все узлы, которые хотят совместной работы могут добавить узел к их диспетчерам контакта.  
  
-   Большинство одноранговые запросы, отправляют ответы, принятый или отклоненный, обратно к узлу основного приложения в отведенное время.  
  
-   Все узлы, которые хотят работать совместно подпишутся к узлу основного приложения.  
  
-   Пока одноранговые выполняющие их initial действие взаимодействия, однорангового узла может добавлять удаленный одноранговые узлы в диспетчере контактов.  Он также рассматривает все ответы приглашения, чтобы определить, кто в отклонило и без ответа.  Он может отменить приглашения теми, которые не отвечают или некоторые другие действия.  
  
-   На этом этапе однорангового узла может начать сеанс взаимодействия со всеми приглашенными одноранговыми узлами или зарегистрировать приложение в инфраструктуре совместной работы.  Приложения используют P2P одноранговой инфраструктуре совместной работы и пространство имен <xref:System.Net.PeerToPeer.Collaboration> для координации сообщений для игр, досок объявлений производительности конференций и других серверов приложений без наличия.  
  
## Одноранговая безопасность сети  
 В домене Active Directory, являются контроллерами домена, предоставляют службы с использованием проверки подлинности Kerberos.  В без сервера среде узла, одноранговые должны предоставить собственную проверку подлинности.  Для одноранговой сети любой узел может выступать в роли центра сертификации, удаляя требование корневого сертификата в хранилище доверенных корневых каждого узла.  Проверка подлинности реализуется с использованием самозаверяющие сертификаты, отформатированное как сертификат X.509.  Эти сертификаты, созданы каждым узлом, который создает пару открытого ключа и закрытого ключа и сертификата, подписывание с использованием закрытого ключа.  Самостоятельно подписанный сертификат, используемый для проверки подлинности и предоставить сведения о сущности однорангового узла.  Использование проверки подлинности X.509, проверка подлинности одноранговой сети зависит от цепочки сертификатов трассировке обратно к открытому ключу, который является доверенным.  
  
## См. также  
 <xref:System.Net.PeerToPeer.Collaboration>   
 [О пространстве имен System.Net.PeerToPeer.Collaboration](../../../docs/framework/network-programming/about-the-system-net-peertopeer-collaboration-namespace.md)