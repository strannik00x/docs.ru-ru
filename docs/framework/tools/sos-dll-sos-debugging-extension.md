---
title: "SOS.dll (расширение отладки SOS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "отладка расширений"
  - "отладка выражений SOS"
  - "SOS.dll"
ms.assetid: 9ac1b522-77ab-4cdc-852a-20fcdc9ae498
caps.latest.revision: 55
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 55
---
# SOS.dll (расширение отладки SOS)
Расширение отладки SOS (SOS.dll) позволяет выполнять отладку управляемых программ в Visual Studio и отладчике Window (WinDbg.exe), предоставляя информацию о внутренней среде CLR. Для работы этой программы в проекте необходимо включить отладку неуправляемого кода. Библиотека "SOS.dll" автоматически устанавливается с .NET Framework. Чтобы использовать SOS.dll в Visual Studio, установите [набор драйверов Windows (WDK)](http://msdn.microsoft.com/windows/hardware/hh852362).  
  
> [!NOTE]
>  Если используется [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], библиотека "SOS.dll" поддерживается в отладчике Windows в Visual Studio, но не в окне интерпретации отладчика Visual Studio.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
![command] [options]   
```  
  
## <a name="commands"></a>Команды  
  
|Команда|Описание|  
|-------------|-----------------|  
|**AnalyzeOOM** (**№ АО**)|Отображает сведения по последнему событию OOM, произошедшему при запросе на выделение памяти в куче для сборки мусора. (В сборке мусора сервера отображает произошедшее событие OOM для каждой кучи сборки мусора.)|  
|**BPMD** [**-nofuturemodule**] [*module name*> *method name*>] [**-md** <`MethodDesc`>] **-list** **-clear** \<*pending breakpoint number*> **-clearall**|Создает точку останова в указанном методе указанного модуля.<br /><br /> Если указанные модуль и метод не загружены, команда ожидает уведомления о загрузке модуля и выполнении JIT-компиляции, прежде чем создавать точку останова.<br /><br /> Список точек ожидания останова можно управлять с помощью **-список**, **-снимите**, и **- clearall** параметры:<br /><br /> **-Список** создает список всех ожидающих точек останова. Если ожидающая точка останова имеет идентификатор модуля, отличный от нуля, эта точка останова связана с функцией в конкретном загруженном модуле. Если ожидающая точка останова имеет нулевой идентификатор модуля, такая точка останова применяется к еще не загруженным модулям.<br /><br /> Используйте **-снимите** или **- clearall** параметр, чтобы удалить из списка ожидающие точки останова.|  
|**CLRStack** [**-a**] [**-l**] [**-p**] [**-n**]|Обеспечивает трассировку стека только для управляемого кода.<br /><br /> **-P** задает отображение аргументов управляемой функции.<br /><br /> **-L** задает отображение сведений о локальных переменных в кадре. Расширение отладки SOS не позволяет извлекать локальные имена, поэтому для локальных имен выводится в формате *локальный адрес*> **=** <*значение*настроек.<br /><br /> **-**(Все) параметр – это ярлык для **-l** и **-p**вместе.<br /><br /> **- N** отключает отображение имен исходных файлов и номеров строк. Если для отладчика указан параметр "SYMOPT_LOAD_LINES", расширение отладки SOS ищет символы для каждого управляемого кадра и в случае успеха отображает соответствующее имя исходного файла и номер строки. **- N** (без номеров строк) для отключения такого поведения можно указать параметр.<br /><br /> Расширение отладки SOS не отображает переходные кадры на платформах x64 и IA-64.|  
|**COMState**|Выдает список моделей контейнера COM для каждого потока и указатель `Context`, если он имеется.|  
|**DumpArray** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-details**] [**-nofields**] *array object address*><br /><br /> -или-<br /><br /> **DA** [**-start** \<*startIndex*>] [**-length** \<*length*>] [**-detail**] [**-nofields**] *array object address*>|Анализирует элементы объекта массива.<br /><br /> **-Запуск** указывает индекс, начиная с которого отображаются элементы.<br /><br /> **-Длина** указывает, сколько элементов для отображения.<br /><br /> **-Сведения о** задает отображение сведений об элементе в **DumpObj** и **DumpVC** форматы.<br /><br /> **- Nofields** параметр отменяет отображение массивов. Это может быть доступна, только если **-подробно** параметра.|  
|**DumpAssembly** \<*адрес сборки*>|Отображает сведения о сборке.<br /><br /> **DumpAssembly** команда выводит список модулей, если они существуют.<br /><br /> Адрес сборки можно получить с помощью **DumpDomain** команды.|  
|**DumpClass** \<*EEClass адрес*>|Отображает сведения о структуре `EEClass`, связанной с типом.<br /><br /> **DumpClass** команда отображает значения статических полей, но значения нестатических полей не отображаются.<br /><br /> Используйте **DumpMT**, **DumpObj**, **Name2EE**, или **Token2EE** команду, чтобы получить `EEClass` адрес структуры.|  
|**DumpDomain** [*адрес домена*настроек]|Перечисляет все <xref:System.Reflection.Assembly> объект, загруженные по указанному <xref:System.AppDomain> адресу объекта.  При вызове без параметров, **DumpDomain** команда перечисляет все <xref:System.AppDomain> объектов в процессе.|  
|**DumpHeap** [**-stat**] [**-strings**] [**-short**] [**-min** \<*size*>] [**-max** \<*size*>] [**-thinlock**] [**-startAtLowerBound**] [**-mt** \<*MethodTable address*>] [**-type** \<*partial type name*>][*start* [*end*]]|Отображает сведения о куче со сборкой мусора и статистику сбора мусора по объектам.<br /><br /> **DumpHeap** команда выводит предупреждение в случае чрезмерной фрагментации в куче сборщика мусора.<br /><br /> **-Stat** ограничивает выводимую информацию статистической сводкой по типам.<br /><br /> **-Строки** ограничивает выводимую информацию статистической сводкой значений строк.<br /><br /> **-Краткое** ограничивает вывод только адресом каждого объекта. Благодаря такому подходу можно легко передавать результат из одной команды отладчика в другую команду с целью автоматизации.<br /><br /> **-Min** задает пропуск объектов, которые меньше, чем `size` параметра, указанного в байтах.<br /><br /> **-Max** задает пропуск объектов, размер которых превышает `size` параметра, указанного в байтах.<br /><br /> **- Thinlock** параметр сообщает о ThinLocks.  Дополнительные сведения см. в разделе **SyncBlk** команды.<br /><br /> Параметр `-startAtLowerBound` приводит к тому, что обход кучи начинается с нижней границы предоставленного диапазона адресов. На стадии планирования куча часто является неанализируемой, поскольку объекты перемещаются. Этот параметр заставляет **DumpHeap** начать проверку с указанной нижней границы. Чтобы задействовать этот параметр, необходимо указать адрес допустимого объекта в качестве нижней границы. Можно отобразить память по адресу неверного объекта, чтобы вручную найти следующую таблицу методов. Если сборка мусора выполняется в момент вызова `memcopy`, также можно найти адрес следующего объекта путем добавления размера к начальному адресу, который указан как параметр.<br /><br /> **- Mt** параметр Вывод только тех объектов, которые соответствуют указанной `MethodTable` структуры.<br /><br /> **-Тип** параметр перечислены только те объекты, для которых имя типа содержит указанную строку для поиска совпадений.<br /><br /> Параметр `start` задает составление списка, начиная с указанного адреса.<br /><br /> Параметр `end` прекращает составление списка на указанном адресе.|  
|**DumpIL** \<*DynamicMethod управляемого объекта*настроек |       *DynamicMethodDesc указатель*настроек |        *MethodDesc указателя*>|Отображает язык CIL, связанный с управляемым методом.<br /><br /> Следует иметь в виду, что динамический язык CIL генерируется иначе, чем язык CIL, загруженный из сборки. Динамический язык CIL ссылается на объекты в массиве управляемых объектов, а не на токены метаданных.|  
|**DumpLog** [**-addr** \<*addressOfStressLog*>] [*Filenam*`e`>]|Записывает в указанный файл содержимое журнала нагрузок, хранящегося в памяти. Если имя не указано, команда создает файл "StressLog.txt" в текущем каталоге.<br /><br /> Хранящийся в памяти журнал нагрузок помогает при диагностике сбоев, вызываемых нагрузкой, без использования блокировки или ввода-вывода. Чтобы включить журнал нагрузки, задайте следующие разделы реестра в реестр\\. NETFramework:<br /><br /> (DWORD) StressLog = 1<br /><br /> (DWORD) LogFacility = 0xffffffff<br /><br /> (DWORD) StressLogSize = 65536<br /><br /> С помощью необязательного параметра `-addr` можно указать журнал нагрузки, отличный от журнала по умолчанию.|  
|**DumpMD** \<*MethodDesc адрес*>|Отображает сведения о структуре `MethodDesc`, находящейся по указанному адресу.<br /><br /> Можно использовать **IP2MD** команду, чтобы получить `MethodDesc` адрес из управляемой функции структуры.|  
|**DumpMT** [**-MD**] *адрес MethodTable*>|Отображает сведения о таблице методов, расположенной по указанному адресу. Указание **-MD** задает вывод списка всех методов, определенных с объектом.<br /><br /> Каждый управляемый объект содержит указатель на таблицу методов.|  
|**DumpMethodSig** <*подпись_метода*настроек *адрес_модуля*`r`>|Отображает сведения о структуре `MethodSig`, находящейся по указанному адресу.|  
|**DumpModule** [**- mt**] *адрес модуля*>|Отображает информацию о модуле, находящемся по указанному адресу. **- Mt** задает отображение типов, определенных в модуле и типы, указанные в модуле<br /><br /> Можно использовать **DumpDomain** или **DumpAssembly** команду, чтобы получить адрес модуля.|  
|**DumpObj** [**- nofields**] *адресу объекта*><br /><br /> -или-<br /><br /> **СДЕЛАТЬ** \<*адресу объекта*>|Отображает сведения об объекте, находящемся по указанному адресу. **DumpObj** команда отображает список полей, `EEClass` структура информации, таблицу методов и размер объекта.<br /><br /> Можно использовать **DumpStackObjects** команду, чтобы получить адрес объекта.<br /><br /> Обратите внимание, что можно запустить **DumpObj** команду для полей типа `CLASS` так, как они также являются объектами.<br /><br /> `-` **Nofields** не предотвращает полей отображаемого объекта, что полезно для таких объектов, как строка.|  
|**DumpRuntimeTypes**|Отображает объекты типы среды выполнения в куче сборщика мусора и выводит список связанных с ними имен типов и таблиц методов.|  
|**DumpStack** [**-EE**] [**-n**] [`top` *stack* [`bottom` *stac*`k`]]|Отображает трассировку стека.<br /><br /> **- EE** предписывает **DumpStack** команду, чтобы отобразить только управляемых функций. Параметры `top` и `bottom` позволяют ограничить состав отображаемых кадров стека на платформах x86.<br /><br /> **- N** отключает отображение имен исходных файлов и номеров строк. Если для отладчика указан параметр "SYMOPT_LOAD_LINES", расширение отладки SOS ищет символы для каждого управляемого кадра и в случае успеха отображает соответствующее имя исходного файла и номер строки. **- N** (без номеров строк) для отключения такого поведения можно указать параметр.<br /><br /> На платформах x86 и x64 **DumpStack** команда создает подробную трассировку стека.<br /><br /> На платформах IA-64 **DumpStack** команда имитирует отладчика **K** команды. На платформах IA-64 параметры `top` и `bottom` игнорируются.|  
|**DumpSig** \<*подпись_метода*настроек *адрес_модуля*>|Отображает сведения о структуре `Sig`, находящейся по указанному адресу.|  
|**DumpSigElem** \<*подпись_метода*настроек *адрес_модуля*>|Отображает единственный элемент объекта сигнатуры. В большинстве случаев следует использовать **DumpSig** для просмотра отдельных объектов сигнатур. Однако, если каким-либо образом повреждена подпись, можно использовать **DumpSigElem** для чтения ее допустимых частей.|  
|**DumpStackObjects** [**-verify**] [`top` *stack* [`bottom` *stack*]]<br /><br /> -или-<br /><br /> **DSO** [**-verify**] [`top` *stack* [`bottom` *stack*]]|Отображает все управляемые объекты, обнаруженные в пределах границ текущего стека.<br /><br /> **-Проверьте** задает проверку каждого нестатического `CLASS` поле объекта.<br /><br /> Используйте **DumpStackObject** команды с командами трассировки стека, такими как **K** команды и **CLRStack** команду для определения значений локальных переменных и параметров.|  
|**DumpVC** \<*адрес MethodTable*настроек *адрес*>|Отображает сведения о полях класса значений, находящегося по указанному адресу.<br /><br /> **MethodTable** параметр позволяет **DumpVC** команду, чтобы правильно интерпретировать поля. В классах значений первое поле не содержит таблицу методов.|  
|**EEHeap** [**-gc**] [**-loader**]|Отображает сведения о памяти процессов, занимаемой внутренними структурами данных среды CLR.<br /><br /> **-Gc** и **-загрузчик** ограничивают выходные данные этой команды в структурах данных сборщика мусора и загрузчика.<br /><br /> Сведения о сборщике мусора включает в себя диапазоны каждого сегмента в управляемой куче.  Если указатель попадает в диапазон сегмента, заданный параметром **-gc**, он является указателем объекта.|  
|**EEStack** [**-short**] [**-EE**]|Выполняется **DumpStack** на все потоки в процессе.<br /><br /> **- EE** передается непосредственно в **DumpStack** команды. **-Краткое** параметр ограничивает выходные данные следующими видами потоков:<br /><br /> Потоки с блокировкой.<br /><br /> Потоки, остановленные для сбора мусора.<br /><br /> Потоки, которые в данный момент находятся в управляемом коде.|  
|**EEVersion**|Отображает версию среды CLR.|  
|**EHInfo** [*MethodDesc адрес*настроек] [*код адрес*настроек]|Отображает блоки обработки исключений в указанном методе.  Данная команда выводит адреса кода и смещения для блока предложений (блока `try`) и блока обработчика (блока `catch`).|  
|**ВОПРОСЫ И ОТВЕТЫ**|Отображает вопросы и ответы.|  
|**FinalizeQueue** [**-подробно**] | [**-allReady**] [**-short**]|Отображает все объекты, зарегистрированные для заключительной обработки.<br /><br /> **-Подробно** задает вывод дополнительной информации о каких-либо `SyncBlocks` , которые необходимо очистить и любой `RuntimeCallableWrappers` (времени выполнения RCW), ожидающих очистки. Поток завершения кэширует и очищает обе эти структуры данных.<br /><br /> Параметр `-allReady` отображает все объекты, которые уже готовы к завершению без учета того, помечены они для сборки мусора или будут помечены следующей сборкой мусора. Объекты, отсутствующие в списке "готовые для завершения", — это завершаемые объекты, которые больше не являются корневым. Применение этого параметра может быть очень затратным, поскольку проверяется, все ли объекты в завершаемых очередях по-прежнему являются корневыми.<br /><br /> Параметр `-short` ограничивает вывод адресом каждого объекта. Если используется в сочетании с **- allReady**, он перечисляет все объекты, имеющие метод завершения, которые больше не являются корневым. При независимом использовании создает список всех объектов в очередях "поддерживающие завершение" и "готовые для завершения".|  
|**FindAppDomain** \<*адресу объекта*>|Определяет домен приложения для объекта, находящегося по указанному адресу.|  
|**FindRoots** **-gen** \<*N*> | **-gen any** |* адрес объекта*>|Вызывает остановку отладчика в отлаживаемом объекте следующей коллекции заданного поколения. Эффект сбрасывается, как только произойдет останов. Чтобы остановиться на следующей коллекции, необходимо повторное выполнение команды. * <object></object> \> * Этой команды используется после прерывания, вызванного **-gen** или **-gen любой** произошла. В этот момент отлаживаемый объект находится в правильном состоянии для **FindRoots** для идентификации корневых папок для объектов из поколений, обречены.|  
|**GCHandles** [**- perdomain**]|Отображает статистику дескрипторов сборщика мусора в составе процесса.<br /><br /> **- Perdomain** упорядочивает статистику по доменам приложений.<br /><br /> Используйте **GCHandles** команды для поиска утечек памяти, вызываемых утечками дескрипторов сборщика мусора. Например, утечка памяти происходит, когда в коде продолжает использоваться большой массив, поскольку на него еще указывает строгий дескриптор сборщика мусора, а сам дескриптор удаляется без освобождения памяти.|  
|**GCHandleLeaks**|Ищет в памяти ссылки на строгие и закрепленные дескрипторы сборщика мусора в рамках процесса и отображает результаты. Если найден дескриптор **GCHandleLeaks** команда отображает адрес ссылки. Если дескриптор в памяти не найден, выдается уведомление.|  
|**GCInfo** \<*MethodDesc адрес*>\<*код адрес*>|Отображает данные, показывающие, содержатся ли управляемые объекты в регистрах или ячейках стека. Если производится сбор мусора, сборщик должен знать расположение ссылок на объекты, чтобы их можно было обновить новыми значениями указателей объектов.|  
|**GCRoot** [**- nostacks**] *адресу объекта*>|Отображает информацию о ссылках (или корневых элементах) объекта, находящегося по указанному адресу.<br /><br /> **GCRoot** команда анализирует всю управляемую кучу и таблицу дескрипторов, находящихся в других дескрипторов объектах или в стеке. Затем каждый стек просматривается в поисках указателей на объекты; также просматривается и очередь метода завершения.<br /><br /> Данная команда не определяет, является ли корень стека допустимым или удален ли он. Используйте **CLRStack** и **U** команды, чтобы дизассемблировать кадр, к которой принадлежит значение локальной переменной или аргумента, чтобы определить, используется ли еще корень стека.<br /><br /> **- Nostacks** ограничивает поиск дескрипторами сборщика мусора и объектами.|  
|**GCWhere**  *<object></object>\>*|Отображает расположение и размер переданного аргумента в куче для сборки мусора. Если аргумент располагается в управляемой куче, но не является адресом допустимого объекта, размер отображается как "0" (нуль).|  
|**help** [*command*>] [`faq`]|Отображает все доступные команды при отсутствии параметров или, если указана команда, — подробные справочные сведения об этой команде.<br /><br /> Параметр `faq` задает отображение ответов на часто задаваемые вопросы.|  
|**HeapStat** [**- inclUnrooted** | **-iu**]|Отображает размеры поколений для каждой кучи и общий объем свободного места в каждом поколении каждой кучи. Если**inclUnrooted** параметр указан, отчет содержит сведения об управляемых объектах в куче сборщика мусора, больше не является корнем.|  
|**HistClear**|Освобождает все ресурсы, используемые семейством команд `Hist`.<br /><br /> Как правило, прямой вызов `HistClear` не требуется, так как каждая команда `HistInit` очищает предыдущие ресурсы.|  
|**HistInit**|Инициализирует структуры SOS из журнала нагрузки, сохраненного в отлаживаемом объекте.|  
|**HistObj***<obj_address>*</obj_address>|Проверяет все записи журнала перемещения нагрузки и отображает цепочку перемещений сборки мусора, которые могли привести к адресу, переданному в качестве аргумента.|  
|**HistObjFind**  *<obj_address>*</obj_address>|Отображает все записи журнала, ссылающиеся на объект по указанному адресу.|  
|**HistRoot***<>\>*|Отображает сведения о повышениях и перемещениях указанного корневого элемента.<br /><br /> Корневое значение можно использовать для отслеживания движения объекта в сборках мусора.|  
|**IP2MD** \<*код адрес*>|Отображает структуру `MethodDesc` по указанному адресу в коде после его JIT-компиляции.|  
|`ListNearObj`(`lno`)*<obj_address>*</obj_address>|Отображает объекты перед указанным адресом и после него. Команда находит в куче для сборки мусора адрес, напоминающий допустимое начало управляемого объекта (в зависимости от таблицы допустимых методов), и объект, следующий за адресом аргумента.|  
|**MinidumpMode** [**0**] [**1**]|Запрещает выполнение небезопасных команд при использовании минидампа.<br /><br /> Передайте **0** для отключения этой функции или **1** для включения этой функции. По умолчанию **MinidumpMode** значение **0**.<br /><br /> Минидампы, созданные с **.dump /m** команда или **.dump** команда ограниченный набор данных, связанных с CLR и позволяют корректно выполнять только часть команд SOS. Выполнение некоторых команд может завершаться сбоем из-за непредвиденных ошибок, вызываемых тем, что требуемые области памяти не сопоставлены или сопоставлены лишь частично. Данный параметр блокирует запуск небезопасных команд для минидампов.|  
|**Name2EE** \<*имя модуля*настроек *имя типа или метода*><br /><br /> -или-<br /><br /> **Name2EE** \<*module name*>**!** \< *имя типа или метода*>|Отображает структуры `MethodTable` и `EEClass` для указанного типа или метода в указанном модуле.<br /><br /> Указанный модуль должен быть загружен в процесс.<br /><br /> Чтобы получить правильное имя типа, просмотрите модуль с помощью [Ildasm.exe (дизассемблер IL)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md). Можно также передать `*` в качестве параметра имени модуля, чтобы просматривались все загруженные управляемые модули. *Имя модуля* параметр также может быть имя отладчика для модуля, таких как `mscorlib` или `image00400000`.<br /><br /> Эта команда поддерживает следующий синтаксис отладчика Windows из `module` > `!` < `type`настроек. Имя типа должно быть полным.|  
|**ObjSize** [*адресу объекта*настроек] | [**-aggregate**] [**-stat**]|Отображает размер указанного объекта. Если не указать никаких параметров, **ObjSize** команда отображает размеры всех объектов, найденных в управляемых потоках, отображает все дескрипторы сборщика мусора в составе процесса и общий размер всех объектов, указываемых этими дескрипторами. **ObjSize** команда включает размер всех дочерних объектов родительского.<br /><br /> **-Статистические** параметр может использоваться в сочетании с **-stat** аргумент для получения подробного представления типов, которые по-прежнему являются корневыми. С помощью **! dumpheap-stat** и **! objsize-статистической обработки - stat**, можно определить, какие объекты больше не являются корневыми и провести диагностику различных проблем с памятью.|  
|**PrintException** [**-вложенных**] [**-строки**] [*адрес объекта исключения*настроек]<br /><br /> -или-<br /><br /> **PE** [**-вложенных**] [*адрес объекта исключения*настроек]|Отображает и форматирует поля всех производных объектов <xref:System.Exception> класс по указанному адресу. Если не указать адрес **PrintException** команда отображает последнее исключение, возникшее в текущем потоке.<br /><br /> **-Вложенных** задает отображение сведений о вложенных объектах исключений.<br /><br /> **-Строки** параметр отображает сведения об источнике, если он доступен.<br /><br /> С помощью этой команды можно форматировать и просматривать поле `_stackTrace`, представляющее собой двоичный массив.|  
|**ProcInfo** [**-env**] [**-time**] [**-mem**]|Отображает переменные среды для статистики процесса, процессорного времени ядра и использования памяти.|  
|**RCWCleanupList** \<*RCWCleanupList адрес*>|Отображает список вызываемых оболочек среды выполнения по указанному адресу, ожидающих очистки.|  
|**SaveModule** \<*базовый адрес*настроек *имя файла*>|Записывает в указанный файл образ, загруженный в память по указанному адресу.|  
|**SOSFlush**|Очищает внутренний кэш SOS.|  
|**StopOnException** [**-производный**] [**-создание** | **-create2**] *исключение*настроек *псевдорегистр номер*>|Предписывает отладчику остановиться при возникновении указанного исключения и продолжать работу при возникновении других исключений.<br /><br /> **-Производный** задает перехват указанного исключения и всех исключений, который является производным от указанного исключения.|  
|**SyncBlk** [**-all** | *syncblk номер*настроек]|Отображает указанную структуру `SyncBlock` или все структуры `SyncBlock`.  Если вы не передаете аргументы, **SyncBlk** команда отображает `SyncBlock` структуру, соответствующую объектам, владельцем которых является поток.<br /><br /> Структура `SyncBlock` представляет собой контейнер для дополнительной информации, которую необязательно создавать для каждого объекта. Она может включать данные COM-взаимодействия и сведения о блокировке для потокобезопасных операций.|  
|**ThreadPool**|Отображает сведения о пуле управляемых потоков, включая число рабочих запросов в очереди, число потоков портов завершения и число таймеров.|  
|**Token2EE** \<*имя модуля*настроек *маркеров*>|Преобразует указанный токен метаданных указанного модуля в структуру `MethodTable` или `MethodDesc`.<br /><br /> В качестве параметра имени модуля можно указать `*`, чтобы узнать, с чем сопоставляется токен в каждом из загруженных управляемых модулей. Можно также задать имя отладчика для модуля, например `mscorlib` или `image00400000`.|  
|**Threads** [**-live**] [**-special**]|Отображает все управляемые потоки в процессе.<br /><br /> **Потоков** команда отображает сокращенный идентификатор отладчика, идентификатор потока среды и идентификатор потока операционной системы  Кроме того **потоков** команда выводит столбец Domain, содержащий домен приложения, в котором выполняется поток, столбец APT, в котором показан режим COM-подразделения и столбец Exception, где указано последнее исключение, возникшее в потоке.<br /><br /> **-Live** задает отображение потоков, связанных с активным потоком.<br /><br /> **-Специальные** параметр отображение всех специальных потоков, созданных средой CLR. К специальным потокам относятся потоки сборки мусора (для параллельной сборки мусора и server мусора), вспомогательные потоки отладчика, потоки метода завершения, <xref:System.AppDomain> выгрузить потоки и потоки таймера пула потоков.|  
|**Состояния потока ** *значение поля состояния***>**|Отображает состояние потока. `value` Параметра является значение `State` в **потоков** вывод отчета.<br /><br /> Пример<br /><br /> `0:003> !Threads     ThreadCount:      2     UnstartedThread:  0     BackgroundThread: 1     PendingThread:    0     DeadThread:       0     Hosted Runtime:   no                                           PreEmptive   GC Alloc           Lock            ID OSID ThreadOBJ    State     GC       Context       Domain   Count APT Exception        0    1  250 0019b068      a020 Disabled 02349668:02349fe8 0015def0     0 MTA        2    2  944 001a6020      b220 Enabled  00000000:00000000 0015def0     0 MTA (Finalizer)     0:003> !ThreadState b220         Legal to Join         Background         CLR Owns         CoInitialized         In Multi Threaded Apartment`|  
|**TraverseHeap** [**- xml**] *имя файла*>|Записывает данные кучи в указанный файл в формате, распознаваемом профилировщиком CLR. **- Xml** предписывает **TraverseHeap** команду для формата файла как XML.<br /><br /> Профилировщик CLR можно загрузить [центра загрузки Майкрософт](http://go.microsoft.com/fwlink/?LinkID=67325).|  
|**U** [**-gcinfo**] [**-ehinfo**] [**-n**] *MethodDesc address*> | *Код адрес*>|Отображает дизассемблированный код с примечаниями для управляемого метода, заданного указателем структуры `MethodDesc` или адресом кода в теле метода. **U** команда отображает весь метод от начала до конца, с примечаниями, преобразующими токены метаданных в имена.<br /><br /> **- Gcinfo** предписывает **U** команду, чтобы отобразить `GCInfo` структуры для метода.<br /><br /> **- Ehinfo** параметр отображает сведения об исключении для метода. Можно также получить эту информацию с **EHInfo** команды.<br /><br /> **- N** отключает отображение имен исходных файлов и номеров строк. Если для отладчика указан параметр "SYMOPT_LOAD_LINES", расширение отладчика SOS ищет символы для каждого управляемого кадра и в случае успеха отображает соответствующее имя исходного файла и номер строки. Можно указать **- n** параметр, чтобы отключить это поведение.|  
|**VerifyHeap**|Проверяет кучу сборщика мусора на наличие признаков повреждения и отображает обнаруженные ошибки.<br /><br /> Повреждения кучи могут быть вызваны неправильно созданными вызовами неуправляемого кода.|  
|**VerifyObj** \<*адресу объекта*>|Проверяет объект, передаваемый в качестве аргумента, на наличие повреждений.|  
|**VMMap**|Выполняет обход виртуального адресного пространства и отображает тип защиты для каждого региона.|  
|**VMStat**|Создает сводное представление виртуального адресного пространства, упорядоченное по типам защиты соответствующих видов памяти (свободная, зарезервированная, выделенная, закрытая, отображаемая, образ). В столбце "TOTAL" содержится результат умножения значения в столбце "AVERAGE" на значение в столбце "BLK COUNT".|  
  
## <a name="remarks"></a>Примечания  
 Расширение отладки SOS позволяет просматривать сведения о коде, выполняемом в среде CLR. Например, с помощью расширения отладки SOS можно получать сведения об управляемой куче, искать повреждения кучи, отображать внутренние типы данных, используемые средой выполнения, и просматривать информацию о любом управляемом коде, запущенном в среде выполнения.  
  
 Чтобы использовать расширение отладки SOS в Visual Studio, установите [набор драйверов Windows (WDK)](http://msdn.microsoft.com/windows/hardware/hh852362). Сведения об интегрированной среде отладки в Visual Studio см. в разделе [среды отладки](http://msdn.microsoft.com/library/windows/hardware/hh406268.aspx) в центре разработчиков Windows.  
  
 Можно также использовать расширение отладки SOS, загрузив их в отладчик WinDbg.exe, которое доступно из [WDK разработчиков средств веб-узел и](http://go.microsoft.com/fwlink/?LinkId=103787)и выполнять команды в WinDbg.exe.  
  
 Чтобы загрузить расширение отладки SOS в отладчик WinDbg.exe, выполните в программе следующую команду.  
  
```  
.loadby sos clr  
```  
  
 Отладчик WinDbg.exe и Visual Studio используют версию библиотеки "SOS.dll", которая соответствует текущей версии "Mscorwks.dll". В .NET Framework версий 1.1 и 2.0 библиотека "SOS.dll" устанавливается в том же каталоге, что и "Mscorwks.dll". По умолчанию следует использовать версию библиотеки "SOS.dll", которая соответствует текущей версии "Mscorwks.dll".  
  
 Чтобы использовать файл дампа, созданный на другом компьютере, убедитесь, что файл "Mscorwks.dll", поступивший вместе с этой установленной копией, указан в пути к символам в данной системе, и загрузите соответствующую версию библиотеки "SOS.dll".  
  
 Чтобы загрузить определенную версию библиотеки "SOS.dll", введите в окне отладчика Windows следующую команду.  
  
```  
.load <full path to sos.dll>  
```  
  
## <a name="examples"></a>Примеры  
 Следующая команда отображает содержимое массива по адресу `00ad28d0`.  Отображаются данные для пяти элементов массива, начиная со второго.  
  
```  
!dumparray -start 2 -length 5 -detail 00ad28d0   
```  
  
 Следующая команда отображает содержимое сборки по адресу `1ca248`.  
  
```  
!dumpassembly 1ca248  
```  
  
 Следующая команда отображает сведения о куче сборщика мусора.  
  
```  
!dumpheap  
```  
  
 Следующая команда записывает содержимое журнала нагрузок в памяти в файл "StressLog.txt" (по умолчанию), расположенный в текущем каталоге.  
  
```  
!DumpLog  
```  
  
 Следующая команда отображает структуру `MethodDesc` по адресу `902f40`.  
  
```  
!dumpmd 902f40  
```  
  
 Следующая команда отображает сведения о модуле по адресу `1caa50`.  
  
```  
!dumpmodule 1caa50  
```  
  
 Следующая команда отображает сведения об объекте по адресу `a79d40`.  
  
```  
!DumpObj a79d40  
```  
  
 Следующая команда отображает поля класса значений по адресу `00a79d9c`, используя таблицу методов по адресу `0090320c`.  
  
```  
!DumpVC 0090320c 00a79d9c  
```  
  
 Следующая команда отображает память процесса, используемую сборщиком мусора.  
  
```  
!eeheap -gc  
```  
  
 Следующая команда отображает все объекты, запланированные для заключительной обработки.  
  
```  
!finalizequeue  
```  
  
 Следующая команда находит домен приложения для объекта по адресу `00a79d98`.  
  
```  
!findappdomain 00a79d98  
```  
  
 Следующая команда отображает все дескрипторы сборщика мусора в текущем процессе.  
  
```  
!gcinfo 5b68dbb8   
```  
  
 Следующая команда отображает структуры `MethodTable` и `EEClass` для метода `Main` класса `MainClass` в модуле `unittest.exe`.  
  
```  
!name2ee unittest.exe MainClass.Main  
```  
  
 Следующая команда отображает сведения о токене метаданных по адресу `02000003` в модуле `unittest.exe`.  
  
```  
!token2ee unittest.exe 02000003  
```  
  
## <a name="see-also"></a>См. также  
 [Средства](../../../docs/framework/tools/index.md)   
 [Командная строка](../../../docs/framework/tools/developer-command-prompt-for-vs.md)