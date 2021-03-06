---
title: "Практическое руководство. Загрузка сборок в домен приложения | Документы Майкрософт"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application domains, loading assemblies
- loading assemblies
ms.assetid: 1432aa2d-bd83-4346-bf3b-a1b7920e2aa9
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 7caaa27fed13c33508b7decde1d87e723167d96b
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="how-to-load-assemblies-into-an-application-domain"></a>Практическое руководство. Загрузка сборок в домен приложения
Существует несколько способов загрузки сборки в домен приложения. Рекомендуется использовать метод <xref:System.Reflection.Assembly.Load%2A> `static` (`Shared` в Visual Basic) класса [System.Reflection.Assembly](https://msdn.microsoft.com/en-us/library/system.reflection.aspx). Другими способами загрузки сборок являются:  
  
-   Метод <xref:System.Reflection.Assembly.LoadFrom%2A> класса [Assembly](https://msdn.microsoft.com/en-us/library/system.reflection.aspx) загружает сборку, заданную расположением ее файла. При загрузке сборок с помощью этого метода используется другой контекст загрузки.  
  
-   Методы <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> и <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> загружают сборку в контекст, предназначенный только для отражения. Сборки, загруженные в этом контексте, могут быть проверены, но не выполнены, позволяя производить проверку сборок, предназначенных для других платформ. См. раздел [Практическое руководство. Загрузка сборок в контекст, предназначенный только для отражения](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
> [!NOTE]
>  Контекст только для отражения впервые появился в платформе .NET Framework версии 2.0.  
  
-   Такие методы, как <xref:System.AppDomain.CreateInstance%2A> и <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> класса <xref:System.AppDomain> могут загружать сборки в домен приложения.  
  
-   Метод <xref:System.Type.GetType%2A> класса <xref:System.Type> может загружать сборки.  
  
-   Метод <xref:System.AppDomain.Load%2A> класса <xref:System.AppDomain?displayProperty=fullName> может загружать сборки, но в основном он используется для COM-взаимодействия. Его не следует использовать для загрузки сборок в домен приложения, отличный от домена приложения, из которого он вызывается.  
  
> [!NOTE]
>  Начиная с платформы .NET Framework версии 2.0, среда выполнения не загружает сборки, которые были скомпилированы версиями платформы .NET Framework, чей номер версии выше, чем у текущей среды выполнения. Это применимо к сочетанию основного и дополнительного номеров для номера версии.  
  
 Можно определить способ, которым JIT-скомпилированный код из загруженных сборок будет распределен между доменами приложений. Дополнительные сведения см. в статье [Домены приложений и сборки](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346).  
  
## <a name="example"></a>Пример  
 Следующий код загружает сборку с именем "example.exe" или "example.dll" в текущий домен приложения, получает тип с именем `Example` из сборки, получает метод без параметров `MethodA` для этого типа и выполняет этот метод. Полное описание получения сведений из загруженной сборки см. в разделе [Динамическая загрузка и использование типов](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md).  
  
 [!code-cpp[System.AppDomain.Load#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source2.cpp#2)] [!code-csharp[System.AppDomain.Load#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source2.cs#2)] [!code-vb[System.AppDomain.Load#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source2.vb#2)]  
  
## <a name="see-also"></a>См. также  
 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>   
 [Программирование с использованием доменов приложений](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Отражение](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [Использование доменов приложений](../../../docs/framework/app-domains/use.md)   
 [Практическое руководство. Загрузка сборок в контекст, предназначенный только для отражения](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)   
 [Домены приложений и сборки](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346)
