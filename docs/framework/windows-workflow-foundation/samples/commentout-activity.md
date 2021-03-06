---
title: "Действие CommentOut | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 340204c3-f827-45fb-870e-55e2ac457ca5
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Действие CommentOut
В этом образце показан способ записи пользовательского действия, которое удаляет другие действия из пути выполнения, преобразуя эти действия в комментарии.  
  
## Действие CommentOut  
 Для выполнения своей задачи действие CommentOut наследует от базового класса <xref:System.Activities.CodeActivity> и реализует пустой метод <xref:System.Activities.CodeActivity.Execute%2A>.  
  
```  
protected override void Execute(CodeActivityContext context)  
{  
}  
```  
  
 Класс объявляется показанным в следующем примере образом.  
  
```  
[Designer(typeof(CommentOutDesigner))]  
[ContentProperty("Body")]  
public sealed class CommentOut : CodeActivity  
  
```  
  
 Атрибут `Designer` указывает класс, который реализует визуальный интерфейс действия во время разработки.Атрибут `ContentProperty` объявляет, что свойство `“Body”` может быть пропущено в XAML\-представлении экземпляра данного действия.  
  
```  
<Border x:Uid="Border_1" BorderThickness ="1">  
    <sad:WorkflowItemPresenter   
    x:Uid="sad:WorkflowItemPresenter_1" AutomationProperties.AutomationId="Body" Item="{Binding Path=ModelItem.Body, Mode=TwoWay}"  
    AllowedItemType="{x:Type sa:Activity}"  
    HintText="Drop activity here"   
    Margin="5,5,5,5" />  
</Border>  
```  
  
 В классе конструктора XAML используется для создания настраиваемого визуального представления действия.<xref:System.Activities.Presentation.WorkflowItemPresenter> — это класс, реализующий визуальный редактор.  
  
 В область действия `CommentOut` может быть перетянуто одно действие.Если в область необходимо добавить несколько действий, сначала перетащите в нее действие последовательности.  
  
#### Использование этого образца  
  
1.  Откройте решение CommentOut.sln в среде [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Постройте решение, нажав клавиши Ctrl\+Shift\+B.  
  
3.  Запустите образец без отладки, нажав сочетание клавиш CTRL\+F5.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\CommentOut`