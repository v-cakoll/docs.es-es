---
title: Use 'FileGetObject' en lugar de 'FileGet' al usar el argumento de tipo 'Object'.
ms.date: 07/20/2015
ms.assetid: 090b8088-895a-482a-9362-606596bac304
ms.openlocfilehash: fdad64a4b35aa792c996d25a9fd72a9ce1126fbd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62022550"
---
# <a name="use-filegetobject-instead-of-fileget-when-using-argument-of-type-object"></a>Use 'FileGetObject' en lugar de 'FileGet' al usar el argumento de tipo 'Object'.
El método `FileGet` incluye un argumento de tipo `Object`. Debe usarse`FileGetObject` en lugar de `FileGet` para evitar ambigüedades.  
  
 Tenga en cuenta que la funcionalidad que proporciona `My.Computer.Filesystem` ofrece mayor facilidad de uso y rendimiento que `FileGet` o `FileGetObject`.  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1. Reemplace `FileGet` por `FileGetObject`.  
  
2. Convierta el argumento `Object` a un tipo más específico.  
  
## <a name="see-also"></a>Vea también

- [My.Computer.FileSystem](xref:Microsoft.VisualBasic.FileIO.FileSystem)
