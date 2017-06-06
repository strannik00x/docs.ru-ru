---
title: "Синтаксис строки подключения | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Синтаксис строки подключения
Каждый поставщик данных платформы .NET Framework имеет объект `Connection`, наследующий из <xref:System.Data.Common.DbConnection>, а также из свойства <xref:System.Data.Common.DbConnection.ConnectionString%2A>, зависящего от поставщика.  Конкретный синтаксис строки подключения для каждого поставщика приведен в его свойстве `ConnectionString`.  В следующей таблице представлен список четырех поставщиков данных, поставляемых в составе платформы .NET Framework.  
  
|Поставщик данных .NET Framework|Описание|  
|-------------------------------------|--------------|  
|<xref:System.Data.SqlClient>|Предоставляет доступ к данным для Microsoft SQL Server.  Дополнительные сведения о синтаксисе строки подключения см. в разделе <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.|  
|<xref:System.Data.OleDb>|Предоставляет доступ к данным источников данных OLE DB.  Дополнительные сведения о синтаксисе строки подключения см. в разделе <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>.|  
|<xref:System.Data.Odbc>|Предоставляет доступ к данным источников данных ODBC.  Дополнительные сведения о синтаксисе строки подключения см. в разделе <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A>.|  
|<xref:System.Data.OracleClient>|Предоставляет доступ к данным Oracle версии 8.1.7 или старше.  Дополнительные сведения о синтаксисе строки подключения см. в разделе <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>.|  
  
## Построители строк подключения  
 В ADO.NET 2.0 появились указанные ниже построители строк соединения для поставщиков данных .NET Framework.  
  
-   <xref:System.Data.SqlClient.SqlConnectionStringBuilder>  
  
-   <xref:System.Data.OleDb.OleDbConnectionStringBuilder>  
  
-   <xref:System.Data.Odbc.OdbcConnectionStringBuilder>  
  
-   <xref:System.Data.OracleClient.OracleConnectionStringBuilder>  
  
 Построители строк соединения позволяют создавать во время выполнения синтаксически правильные строки соединения, и поэтому в коде не требуется вручную объединять значения строк соединения.  Для получения дополнительной информации см. [Построители строк подключения](../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
## Проверка подлинности Windows  
 Для соединения с источниками данных рекомендуется использовать проверку подлинности Windows \(которую также называют *встроенной безопасностью*\), если эти источники ее поддерживают.  Синтаксис строки подключения зависит от поставщика.  В следующей таблице показан синтаксис проверки подлинности Windows, который используется с поставщиками данных платформы .NET Framework.  
  
|Поставщик|Синтаксис|  
|---------------|---------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  
|`OleDb`|`Integrated Security=SSPI;`|  
|`Odbc`|`Trusted_Connection=yes;`|  
|`OracleClient`|`Integrated Security=yes;`|  
  
> [!NOTE]
>  Значение `Integrated Security=true` вызывает исключение при работе с поставщиком `OleDb`.  
  
## Строки подключения SqlClient  
 Синтаксис для строки подключения <xref:System.Data.SqlClient.SqlConnection> документирован в свойстве <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName>.  Свойство <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> используется для возврата или задания строки подключения для базы данных SQL Server.  Если необходимо подключиться к более ранней версии SQL Server, следует использовать поставщик данных .NET Framework для OleDb \(<xref:System.Data.OleDb>\).  Наиболее распространенные ключевые слова строк соединения также соответствуют свойствам <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  
  
 Все следующие формы синтаксиса используют для соединения с базой данных **AdventureWorks** на локальном сервере проверку подлинности Windows.  
  
```  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  
  
### Имена входа SQL Server  
 Для соединения с SQL Server предпочтительно использовать проверку подлинности Windows.  Однако если требуется проверка подлинности SQL Server, то имя пользователя и пароль указываются с помощью приведенного ниже синтаксиса.  В этом примере символы звездочки представляют допустимое имя пользователя и пароль.  
  
```  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  
  
> [!IMPORTANT]
>  Значением по умолчанию для ключевого слова `Persist` `` `Security Info` является `false`.  Значение `true` или `yes` позволяет получить из строки соединения конфиденциальные данные \(в том числе идентификатор пользователя и пароль\) после открытия соединения.  Если ключевое слово `Persist` `` `Security Info` равно `false`, то ненадежный источник не сможет получить доступ к конфиденциальным данным строки подключения.  
  
 Чтобы подключиться к именованному экземпляру SQL Server, используйте синтаксис *имя\_сервера\\имя\_экземпляра*.  
  
```  
Data Source=MySqlServer\MSSQL1;"  
```  
  
 Кроме того, в свойстве <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> объекта `SqlConnectionStringBuilder` можно задать имя экземпляра при построении строки подключения.  Свойство <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> объекта <xref:System.Data.SqlClient.SqlConnection> доступно только для чтения.  
  
> [!NOTE]
>  Проверка подлинности Windows имеет приоритет над именами входа SQL Server.  Если указать значение Integrated Security\=true, а также ввести имя пользователя и пароль, то имя пользователя и пароль не будут учитываться и будет применяться проверка подлинности Windows.  
  
### Изменения версий системы типов  
 Ключевое слово `Type System Version` в <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName> указывает клиентское представление типов [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  Дополнительные сведения о ключевом слове `Type System Version` см. в разделе <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName>.  
  
## Подключение и присоединение к пользовательским экземплярам SQL Server Express  
 Пользовательские экземпляры являются одной из функций SQL Server Express.  Они дают пользователям под учетной записью с минимальными правами возможность присоединить и запустить базу данных SQL Server без прав администратора.  Пользовательский экземпляр выполняется с учетными данными пользователя Windows, а не службы.  
  
 Дополнительные сведения о работе с пользовательскими экземплярами см. в разделе [Пользовательские экземпляры SQL Server Express](../../../../docs/framework/data/adonet/sql/sql-server-express-user-instances.md).  
  
## Использование ключевого слова TrustServerCertificate  
 Ключевое слово `TrustServerCertificate` применяется только при соединении с экземпляром [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] с допустимым сертификатом.  Если ключевому слову `TrustServerCertificate` присвоено значение `true`, то транспортный уровень будет использовать протокол SSL для шифрования канала и не пойдет по цепочке сертификатов для проверки доверия.  
  
```  
"TrustServerCertificate=true;"   
```  
  
> [!NOTE]
>  Если ключевому слову `TrustServerCertificate` присвоено значение `true` и включено шифрование, то будет использоваться уровень шифрования, заданный на сервере, даже если в строке подключения `Encrypt` задано значение `false`.  В противном случае соединение не будет установлено.  
  
### Включение шифрования  
 Чтобы включить шифрование, когда на сервере не представлен сертификат, в диспетчере конфигурации SQL Server необходимо установить параметры **Принудительное шифрование протокола** и **Доверять сертификату сервера**.  В этом случае шифрование будет использовать самозаверяющий сертификат сервера, не проверяя наличия подтверждаемого сертификата сервера.  
  
 Настройки приложения не могут снизить установленный на SQL Server уровень безопасности, но при необходимости могут повысить его.  Приложение может затребовать шифрование, присвоив ключевым словам `TrustServerCertificate` и `Encrypt` значение `true`, гарантируя тем самым, что шифрование будет выполняться, даже если не представлен сертификат сервера, а на клиенте не настроен параметр **Принудительное шифрование протокола**.  Но если на клиенте не установлен параметр `TrustServerCertificate`, то сертификат сервера, тем не менее, потребуется.  
  
 В следующей таблице перечислены все случаи.  
  
|Параметр «Принудительное шифрование протокола» на клиенте|Параметр «Доверять сертификату сервера» на клиенте|Строка или атрибут «Шифровать\/Использовать шифрование для подключения к данным»|Строка подключения или атрибут «Доверять сертификату сервера»|Результат|  
|---------------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------------------------------------------|-------------------------------------------------------------------|---------------|  
|Нет|Н\/Д|Нет \(по умолчанию\)|Не учитывается|Шифрование отсутствует.|  
|Нет|Н\/Д|Да|Нет \(по умолчанию\)|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
|Нет|Н\/Д|Да|Да|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
|Да|Нет|Не учитывается|Не учитывается|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
|Да|Да|Нет \(по умолчанию\)|Не учитывается|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
|Да|Да|Да|Нет \(по умолчанию\)|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
|Да|Да|Да|Да|Шифрование применяется только при наличии подтверждаемого сертификата сервера, в противном случае попытка соединения завершается неудачно.|  
  
 Дополнительные сведения см. в разделе [Использование шифрования без проверки](http://go.microsoft.com/fwlink/?LinkId=120500) электронной документации по SQL Server.  
  
## Строки соединения OleDb  
 Свойство <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> класса <xref:System.Data.OleDb.OleDbConnection> позволяет получить или задать строку подключения для источника данных OLE DB \(например, Microsoft Access\).  Строку подключения `OleDb` также можно создать во время выполнения с помощью класса <xref:System.Data.OleDb.OleDbConnectionStringBuilder>.  
  
### Синтаксис строки соединения OleDb  
 В строке соединения <xref:System.Data.OleDb.OleDbConnection> необходимо указать имя поставщика.  Следующие строки подключения подключают к базе данных Microsoft Access, использующей поставщик Jet.  Обратите внимание, что ключевые слова `UserID` и `Password` необязательны, если база данных не защищена \(по умолчанию\).  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0; Data Source=d:\Northwind.mdb;User ID=Admin;Password=;   
```  
  
 Если база данных Jet защищена на уровне пользователя, необходимо указать местоположение файла сведений рабочей группы \(MDW\-файла\).  Файл сведений рабочей группы используется для проверки учетных данных, указанных в строке подключения.  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=d:\Northwind.mdb;Jet OLEDB:System Database=d:\NorthwindSystem.mdw;User ID=*****;Password=*****;  
```  
  
> [!IMPORTANT]
>  Сведения о соединении **OleDbConnection** можно указать в UDL\-файле, однако этого следует избегать.  UDL\-файлы не подвергаются шифрованию, и строки соединения хранятся в них в виде простого текста.  Так как UDL\-файл представляет собой внешний файловый ресурс для приложения, его нельзя защитить средствами .NET Framework.  UDL\-файлы не поддерживаются для **SqlClient**.  
  
### Соединение с Access\/Jet с помощью строки замены DataDirectory  
 Строка замены `DataDirectory` поддерживается не только клиентом `SqlClient`.  Ее можно также использовать с поставщиками данных .NET для <xref:System.Data.OleDb> и <xref:System.Data.Odbc>.  В следующем образце строки <xref:System.Data.OleDb.OleDbConnection> приведен синтаксис для подключения к базе данных Northwind.mdb, расположенной в папке приложения app\_data.  В этой папке также хранится системная база данных \(System.mdw\).  
  
```  
"Provider=Microsoft.Jet.OLEDB.4.0;  
Data Source=|DataDirectory|\Northwind.mdb;  
Jet OLEDB:System Database=|DataDirectory|\System.mdw;"  
```  
  
> [!IMPORTANT]
>  Указывать расположение системной базы данных в строке подключения не требуется, если база данных Access\/Jet не защищена.  Защита снята по умолчанию, все пользователи соединяются как встроенный пользователь Admin с пустым паролем.  База данных Jet остается уязвимой для атаки, даже если правильно реализована безопасность на уровне пользователя.  Поэтому в базе данных Access\/Jet не рекомендуется хранить конфиденциальные данные, поскольку схема безопасности на основе файловой системы неизбежно обладает определенной уязвимостью.  
  
### Соединение с Excel  
 Поставщик Microsoft Jet используется для подключения с книгой Excel.  В следующей строке подключения ключевое слово `Extended Properties` задает специфические свойства Excel. "  «HDR\=Yes;» указывает, что первая строка содержит имена столбцов, а не данные, а «IMEX\=1;» дает указания драйверу всегда считывать «смешанные» столбцы данных в виде текста.  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\MyExcel.xls;Extended Properties=""Excel 8.0;HDR=Yes;IMEX=1""  
```  
  
 Обратите внимание, что двойные кавычки, необходимые для ключевого слова `Extended Properties`, также должны заключаться в двойные кавычки.  
  
### Синтаксис строки подключения с поставщиком Data Shape  
 При соединении с поставщиком Microsoft Data Shape используются оба ключевых слова: `Provider` и `Data Provider`.  В следующем примере поставщик Data Shape используется для подключения к экземпляру SQL Server.  
  
```  
"Provider=MSDataShape;Data Provider=SQLOLEDB;Data Source=(local);Initial Catalog=pubs;Integrated Security=SSPI;"   
```  
  
## Строки подключения ODBC  
 Свойство <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A> класса <xref:System.Data.Odbc.OdbcConnection> позволяет получить или задать строку подключения для источника данных OLE DB.  Строки подключения ODBC также поддерживаются построителем <xref:System.Data.Odbc.OdbcConnectionStringBuilder>.  
  
 Следующая строка подключения использует текстовый драйвер Microsoft.  
  
```  
Driver={Microsoft Text Driver (*.txt; *.csv)};DBQ=d:\bin  
```  
  
### Использование строки замены DataDirectory для соединения с Visual FoxPro  
 Следующий образец строки подключения <xref:System.Data.Odbc.OdbcConnection> демонстрирует использование `DataDirectory` для соединения с файлом Microsoft Visual FoxPro.  
  
```  
"Driver={Microsoft Visual FoxPro Driver};  
SourceDB=|DataDirectory|\MyData.DBC;SourceType=DBC;"  
```  
  
## Строки подключения Oracle  
 Свойство <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> класса <xref:System.Data.OracleClient.OracleConnection> позволяет получить или задать строку подключения для источника данных OLE DB.  Строки подключения Oracle также поддерживаются построителем <xref:System.Data.OracleClient.OracleConnectionStringBuilder>.  
  
```  
Data Source=Oracle9i;User ID=*****;Password=*****;  
```  
  
 Дополнительные сведения о синтаксисе строки подключения ODBC см. в разделе <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>.  
  
## См. также  
 [Строки подключения](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Подключение к источнику данных](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Центр разработчиков, поставщики ADO.NET Managed Provider и набор данных](http://go.microsoft.com/fwlink/?LinkId=217917)