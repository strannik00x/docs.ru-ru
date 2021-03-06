---
title: "/doc (параметры компилятора C#) | Документы Майкрософт"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- FileProperties.BuildAction
- /doc
dev_langs:
- CSharp
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
caps.latest.revision: 19
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8addbbfe1e854feee560192292b713da4fc67e6c
ms.contentlocale: ru-ru
ms.lasthandoff: 03/13/2017

---
# <a name="doc-c-compiler-options"></a>/doc (параметры компилятора C#)
Параметр **/doc** позволяет поместить комментарии документации в XML-файл.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
/doc:file  
```  
  
## <a name="arguments"></a>Аргументы  
 `file`  
 Выходной XML-файл, который заполняется комментариями из файлов исходного кода, участвующих в компиляции.  
  
## <a name="remarks"></a>Примечания  
 Комментарии документации могут быть обработаны и добавлены в XML-файл, если они предшествуют объектам файлов исходного кода, перечисленным ниже.  
  
-   Такие определяемые пользователем типы, как [класс](../../../csharp/language-reference/keywords/class.md), [делегат](../../../csharp/language-reference/keywords/delegate.md) или [интерфейс](../../../csharp/language-reference/keywords/interface.md).  
  
-   Такие члены, как поле, [событие](../../../csharp/language-reference/keywords/event.md), [свойство](../../../csharp/programming-guide/classes-and-structs/using-properties.md) или метод.  
  
 Файл исходного кода, содержащий метод "Main", первым выводится в XML-файл.  
  
 Чтобы использовать созданный XML-файл с помощью функции [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense), имя XML-файла должно совпадать с именем сборки, а сам XML-файл должен находиться в одном каталоге со сборкой. Таким образом, если в проект Visual Studio добавляется ссылка на сборку, то XML-файл также будет найден. Дополнительные сведения см. в разделе [Создание XML-примечаний к коду](https://docs.microsoft.com/visualstudio/ide/supplying-xml-code-comments).  
  
 Если при компиляции не используется параметр [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), `file` будет содержать теги \<assembly>\</assembly>, которые указывают имя файла, содержащего манифест сборки для выходного файла компиляции.  
  
> [!NOTE]
>  Параметр /doc применяется ко всем входным файлам или (если он установлен в параметрах проекта) ко всем файлам проекта. Чтобы отключить предупреждения, связанные с комментариями документации для определенного файла или раздела кода, используйте директиву [#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Способы создания документации из комментариев в коде описаны в разделе [Рекомендуемые теги для комментариев документации](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio  
  
1.  Откройте страницу **Свойства** проекта.  
  
2.  Перейдите на вкладку **Сборка**.  
  
3.  Измените свойство **XML-файл документации**.  
  
 Сведения об установке этого параметра компилятора программным способом см. в разделе <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## <a name="see-also"></a>См. также  
 [Параметры компилятора C#](../../../csharp/language-reference/compiler-options/index.md)   
 [NIB. Практическое руководство. Изменение свойств проекта и параметров конфигурации](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)
