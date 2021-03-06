---
title: Filtrar Conservar y restaurar propiedades en el ámbito de aplicación a través de sesiones de aplicación
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application-scope properties [WPF], persisting
- persisting application-scope properties [WPF]
- properties [WPF], persisting
- restoring application-scope properties [WPF]
- properties [WPF], restoring
- application-scope properties [WPF], restoring
ms.assetid: 55d5904a-f444-4eb5-abd3-6bc74dd14226
ms.openlocfilehash: d9c2dda2745e7528902b6b1c4f46d17264d1a8d8
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666723"
---
# <a name="how-to-persist-and-restore-application-scope-properties-across-application-sessions"></a>Filtrar Conservar y restaurar propiedades en el ámbito de aplicación a través de sesiones de aplicación
En este ejemplo se muestra cómo conservar las propiedades del ámbito de la aplicación cuando una aplicación se cierra y cómo restaurar las propiedades del ámbito de la aplicación cuando se inicia una aplicación.  
  
## <a name="example"></a>Ejemplo  
 La aplicación conserva las propiedades de ámbito de aplicación en, y las restaura desde el almacenamiento aislado. El almacenamiento aislado es un área de almacenamiento protegido que las aplicaciones sin permiso de acceso a archivos pueden usar de forma segura.  El archivo *app. Xaml* define el `App_Startup` método como el controlador para el <xref:System.Windows.Application.Startup?displayProperty=nameWithType> evento y <xref:System.Windows.Application.Exit?displayProperty=nameWithType> el `App_Exit` método como el controlador del evento, como se muestra en las líneas resaltadas del primer ejemplo. En el segundo ejemplo se muestra una parte de los archivos *app.Xaml.CS* y *app. Xaml. VB* que resalta el `App_Startup` código para el método, que restaura las propiedades de ámbito de aplicación `App_Exit` y el método, que guarda el ámbito de aplicación. propiedades.

 [!code-xaml[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml?highlight=1-7)]
  
 [!code-csharp[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs?highlight=17-55)]
 [!code-vb[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb?highlight=14-45)]
