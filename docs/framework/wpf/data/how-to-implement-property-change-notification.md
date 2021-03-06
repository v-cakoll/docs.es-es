---
title: 'Cómo: Implementar la notificación de cambio de propiedad'
description: Habilite las propiedades para notificar automáticamente a un origen de enlace cuando el valor de propiedad cambie en Windows Presentation Foundation (WPF).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: 6c298930b7b1f812e94ea6add8f53c67d3453530
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620786"
---
# <a name="how-to-implement-property-change-notification"></a>Cómo: Implementar la notificación de cambio de propiedad
Para admitir <xref:System.Windows.Data.BindingMode.OneWay> o <xref:System.Windows.Data.BindingMode.TwoWay> enlazar para permitir que las propiedades de destino de enlace reflejen automáticamente los cambios dinámicos del origen de enlace (por ejemplo, para que el panel de vista previa se actualice automáticamente cuando el usuario edita un formulario), la clase debe proporcionar las notificaciones de cambio de propiedad correctas. En este ejemplo se muestra cómo crear una clase que implementa <xref:System.ComponentModel.INotifyPropertyChanged> .  
  
## <a name="example"></a>Ejemplo  
 Para implementar <xref:System.ComponentModel.INotifyPropertyChanged> , debe declarar el <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> evento y crear el `OnPropertyChanged` método. Por lo tanto, para cada propiedad para las que desee cambiar las notificaciones, calle a `OnPropertyChanged` cuando se actualice la propiedad.  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 Para ver un ejemplo de cómo `Person` se puede usar la clase para admitir el <xref:System.Windows.Data.BindingMode.TwoWay> enlace, vea [control cuando el texto de TextBox actualiza el origen](how-to-control-when-the-textbox-text-updates-the-source.md).  
  
## <a name="see-also"></a>Vea también

- [Información general sobre orígenes de enlaces](binding-sources-overview.md)
- [Información general sobre el enlace de datos](../../../desktop-wpf/data/data-binding-overview.md)
- [Temas "Cómo..."](data-binding-how-to-topics.md)
