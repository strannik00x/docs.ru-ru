---
title: "Класс Exception и его свойства | Microsoft Docs"
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
  - "Exception - класс"
  - "исключения, Exception - класс"
ms.assetid: e2e1f8c4-e7b4-467d-9a66-13c90861221d
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Класс Exception и его свойства
Класс <xref:System.Exception> является базовым классом, из которого наследуются исключения.  Большинство объектов исключения являются экземплярами некоторого класса, производного от **Exception**, но в качестве исключения можно создавать любой объект, унаследованный от класса <xref:System.Object>.  Обратите внимание, что не все языки поддерживают генерацию и перехват тех объектов, которые не являются производными класса **Exception**.  Почти во всех случаях рекомендуется создавать и перехватывать только объекты **Exception**.  
  
 Класс **Exception** имеет несколько свойств, облегчающих анализ исключения.  В число этих свойств входят следующие.  
  
-   Свойство <xref:System.Exception.StackTrace%2A>.  
  
     Это свойство содержит трассировку стека, которую можно использовать для определения места возникновения ошибки.  Трассировка стека включает имя файла источника и, при наличии отладочной информации, номер программной строки.  
  
-   Свойство <xref:System.Exception.InnerException%2A>.  
  
     Это свойство может использоваться для создания и сохранения серии исключений во время обработки исключений.  Это свойство можно использовать для создания нового исключения, содержащего ранее перехваченные исключения.  Исходное исключение может быть захвачено вторым исключением в свойстве **InnerException**, что позволяет коду, обрабатывающему второе исключение, проверять дополнительные данные.  
  
     Например, предположим, что существует метод, выполняющий чтение файла и форматирование данных.  Этот код пытается выполнить чтение из файла, но создается исключение FileException.  Данный метод перехватывает FileException и создает исключение BadFormatException.  В этом случае исключение FileException может быть сохранено в свойстве **InnerException** исключения BadFormatException.  
  
     Чтобы улучшить возможности определения вызывающим объектом причин создания исключения, в некоторых случаях рекомендуется использовать метод для перехвата исключения, созданного вспомогательной подпрограммой, с последующей выдачей исключения, содержащего больше сведений о возникшей ошибке.  Может быть создано новое, более информативное исключение, в котором имеется ссылка внутреннего исключения, указывающая на исходное исключение.  Затем это более значимое исключение может быть передано в вызывающий объект.  Обратите внимание, что с помощью этой функциональной возможности можно создавать серии связанных исключений, заканчивающиеся тем исключением, которое было порождено первым.  
  
-   Свойство <xref:System.Exception.Message%2A>.  
  
     Это свойство предоставляет подробные сведения о причине возникновения исключения.  Свойство **Message** выводится на том языке, который указан в свойстве <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName> для потока, который создает исключение.  
  
-   Свойство <xref:System.Exception.HelpLink%2A>.  
  
     Это свойство может содержать URL \(или URN\) к файлу справки, предоставляющему подробные сведения о причине возникновения исключения.  
  
-   Свойство <xref:System.Exception.Data%2A>.  
  
     Это свойство имеет тип IDictionary и может содержать произвольные данные в парах "ключ\-значение".  
  
 В большинстве классов, унаследованных из **Exception**, не реализуются дополнительные элементы или дополнительные функциональности. Они просто унаследованы из класса **Exception**.  Таким образом, наиболее важные сведения об исключении можно найти в иерархии исключений, в имени исключения и в информации, содержащейся в этом исключении.  
  
## См. также  
 [Иерархия исключений](../../../docs/standard/exceptions/exception-hierarchy.md)   
 [Основы обработки исключений](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [Лучшие методики обработки исключений](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Исключения](../../../docs/standard/exceptions/index.md)