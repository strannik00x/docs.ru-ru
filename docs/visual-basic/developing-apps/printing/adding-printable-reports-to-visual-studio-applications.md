---
title: "Добавление печатаемых отчетов в приложения Visual Studio | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "печать [Visual Studio], отчеты"
  - "отчеты, печать в Visual Studio"
ms.assetid: 93928405-ef41-495e-bce2-9d43d5a7080a
caps.latest.revision: 27
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 27
---
# Добавление печатаемых отчетов в приложения Visual Studio
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Studio поддерживает множество решений для составления отчетов, помогая реализовывать генерацию информативных и привлекательных отчетов в приложениях Visual Basic.  Можно создавать и добавлять отчеты с помощью элементов управления ReportViewer, Crystal Reports или служб отчетов SQL Server.  
  
> [!NOTE]
>  Службы SQL Server Reporting Services — это часть SQL Server 2005, а не Visual Studio.  Если SQL Server 2005 не установлен, то, соответственно, службы Reporting Services также не установлены.  
  
## Обзор технологии Microsoft Reporting в приложениях Visual Basic  
 Выберите один из следующих подходов к использованию технологии Microsoft Reporting в приложении:  
  
-   Добавление одного или нескольких экземпляров элемента управления ReportViewer в приложение Windows Visual Basic.  
  
-   Программная интеграция служб отчетов SQL Server посредством обращений к веб\-службе Report Server.  
  
-   Использование элемента управления ReportViewer в сочетании со службами отчетов Microsoft SQL Server 2005, когда элемент управления используется как средство просмотра отчетов, а сервер отчетов — как обработчик отчетов.  \(Обратите внимание, для совместного использования сервера отчетов и элемента управления ReportViewer необходима версия служб отчетов, входящая в состав SQL Server 2005.\)  
  
## Использование элементов управления ReportViewer  
 Самый простой способ внедрения функциональных возможностей создания отчетов в приложения Windows Visual Basic —добавить элемент управления ReportViewer в форму приложения.  Этот элемент управления непосредственно наделяет приложение возможностями обработки отчетов и предоставляет встроенный конструктор отчетов, позволяющий составлять отчеты, используя данные из любого объекта данных ADO.NET.  Полнофункциональный API обеспечивает программный доступ к элементу управления и отчетам, позволяя настраивать функциональность, доступную во время выполнения.  
  
 ReportViewer — это отдельный, свободно распространяемый элемент управления данными, предоставляющий встроенные возможности обработки и просмотра отчетов.  Элемент управления ReportViewer имеет смысл выбрать, если требуются следующие функциональные возможности:  
  
-   Обработка отчетов в клиентском приложении.  Обработанный отчет отображается в области просмотра, предоставляемой элементом управления.  
  
-   Привязка данных к таблицам данных ADO.NET.  Можно создавать отчеты, потребляющие экземпляры объектов <xref:System.Data.DataTable>, предоставленные элементу управления.  Можно также осуществлять непосредственную привязку к бизнес\-объектам.  
  
-   Свободно распространяемые элементы управления, которые можно включить в приложение.  
  
-   Функциональные возможности времени выполнения, такие как навигация по страницам, печать, поиск и форматы экспорта.  Поддержку этих операций обеспечивает панель инструментов ReportViewer.  
  
 Для использования элемента управления ReportViewer можно перетащить его из раздела **Данные** области элементов Visual Studio на форму в приложении Windows Visual Basic.  
  
### Создание отчетов в Visual Studio для элементов управления ReportViewer  
 Чтобы создать отчет, выполняемый в ReportViewer, добавьте в проект шаблон **Отчет**.  Visual Studio создаст файл определения отчета клиента \(RDLC\), добавит файл в проект и откроет встроенный конструктор отчетов в рабочей области Visual Studio.  
  
 Конструктор отчетов среды Visual Studio интегрируется с окном **Источники данных**.  При перетаскивании поля из окна **Источники данных** в отчет конструктор отчетов копирует метаданные об источнике данных в файл определения отчета.  Эти метаданные используются элементом управления ReportViewer для автоматического создания кода привязки данных.  
  
 В конструкторе отчетов среды Visual Studio отсутствует функция предварительного просмотра отчета.  Для предварительного просмотра отчета запустите приложение и просмотрите внедренный в его отчет.  
  
||  
|-|  
|Добавление в приложение базовых функций составления отчетов|  
|1.  Перетащите элемент управления ReportViewer со вкладки **Данные** в **Области элементов** в форму.<br />2.  В меню **Проект** выберите пункт **Добавить новый элемент**.  В диалоговом окне **Добавление нового элемента** выберите значок **Отчет** и нажмите кнопку **Добавить**.<br />     В среде разработки откроется конструктор отчетов, и в проект будет добавлен файл отчета \(RDLC\).<br />3.  Перетащите элементы отчета из **Области элементов** на макет отчета и упорядочьте их, как требуется.<br />4.  Перетащите поля из окна **Источники данных** на элементы отчета в макете отчета.|  
  
## Использование служб отчетов в приложениях Visual Basic  
 Службы отчетов — это серверная технология составления отчетов, входящая в состав SQL Server.  Службы отчетов включают в себя дополнительные функции, отсутствующие в элементе управления ReportViewer.  Выбирайте службы отчетов, если требуется любая из следующих возможностей:  
  
-   Масштабное развертывание и обработка отчетов на стороне сервера, которая обеспечивает повышенную производительность для сложных или долго выполняющихся отчетов и с большим объемом операций по составлению отчетов.  
  
-   Интегрированная обработка данных и отчетов с поддержкой пользовательских элементов управления отчетами и разнообразных выходных форматов отрисовки отчетов.  
  
-   Обработка отчетов по расписанию, позволяющая точно указать, когда следует выполнять отчеты.  
  
-   Распространение отчетов на основе подписки по электронной почте или через общие папки.  
  
-   Функции составления специальных отчетов, позволяющие бизнес\-пользователям создавать отчеты по мере необходимости.  
  
-   Управляемые данными подписки, обеспечивающие рассылку настраиваемых выходных данных отчетов динамическому списку получателей.  
  
-   Пользовательские расширения для обработки данных, доставки отчетов, пользовательской проверки подлинности и отрисовки отчетов.  
  
 Сервер отчетов реализован как веб\-служба.  Код приложения должен включать вызовы веб\-службы для доступа к отчетам и другим метаданным.  Веб\-служба предоставляет полный программный доступ к экземпляру сервера отчетов.  
  
 Поскольку службы отчетов представляют собой веб\-технологию, в средстве просмотра по умолчанию отображаются отчеты, визуализированные в формате HTML.  Если вы не хотите использовать HTML как заданный по умолчанию формат представления отчетов, необходимо создать для приложения пользовательское средство просмотра отчетов.  
  
### Создание отчетов в Visual Studio for Reporting Services  
 Для построения отчетов, которые выполняются на сервере отчетов, необходимо создать файлы определения отчетов \(RDL\) в Visual Studio с помощью компонента Business Intelligence Development Studio, входящего в состав SQL Server 2005.  
  
> [!NOTE]
>  Для использования служб отчетов SQL Server и Business Intelligence Development Studio необходимо, чтобы на компьютере было установлено программное обеспечение SQL Server 2005.  
  
 Business Intelligence Development Studio добавляет шаблоны проектов, которые относятся к компонентам SQL Server.  Для создания отчетов можно выбрать шаблон **Проект сервера отчетов** или **Мастер проектов сервера отчетов**.  Можно задать подключения к источникам данных и запросы к различным типам источников данных, включая SQL Server, Oracle, службы аналитики, XML и службы интеграции SQL Server.  Вкладки **Данные**, **Макет** и **Предварительный просмотр** позволяют определить данные, создать макет отчета и предварительно просмотреть отчет в той же рабочей области.  
  
 Определения отчетов, построенные для элемента управления или сервера отчетов, могут быть повторно использованы в любой из этих технологий.  
  
||  
|-|  
|Создание отчета, выполняемого на сервере отчетов|  
|1.  В меню **Файл** выберите команду **Создать**.<br />     Откроется диалоговое окно **Новый проект**.<br />2.  В области **Типы проектов** щелкните **Проекты бизнес\-аналитики**.<br />3.  В области "Шаблоны" выберите **Проект сервера отчетов** или **Мастер проектов сервера отчетов**.|  
  
## Использование элементов управления ReportViewer в сочетании со службами отчетов SQL Server  
 Элементы управления ReportViewer и службы отчетов SQL Server 2005 могут использоваться вместе в одном приложении.  
  
-   Элемент управления ReportViewer предоставляет средство просмотра, используемое для отображения отчетов в приложении.  
  
-   Службы отчетов предоставляют отчеты и выполняют всю обработку на удаленном сервере.  
  
 Элемент управления ReportViewer можно настроить на отображение отчетов, хранящихся и обрабатываемых на удаленном сервере служб отчетов.  Этот тип конфигурации называется *режимом удаленной обработки*.  В режиме удаленной обработки элемент управления запрашивает отчет, который хранится на удаленном сервере отчетов.  Сервер отчетов выполняет всю обработку отчета, обработку данных и отрисовку отчета.  По завершении готовый для просмотра отчет возвращается элементу управления и отображается в области просмотра.  
  
 Отчеты, выполняемые на сервере отчетов, поддерживают дополнительные форматы экспорта, имеют различную реализацию параметризации отчетов, используют типы данных источников, которые поддерживаются сервером отчетов и доступны через модель авторизации на основе ролей на сервере отчетов.  
  
 Чтобы использовать режим удаленной обработки, укажите URL\-адрес и путь к серверу отчетов при настройке элемента управления ReportViewer.