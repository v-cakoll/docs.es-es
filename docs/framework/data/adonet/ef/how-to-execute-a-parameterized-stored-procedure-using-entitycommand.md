---
title: Procedimiento para ejecutar un procedimiento almacenado parametrizado mediante EntityCommand
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
ms.openlocfilehash: 27e756d8e44580d9205cc075367bce5a45536c69
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854682"
---
# <a name="how-to-execute-a-parameterized-stored-procedure-using-entitycommand"></a>Procedimiento para ejecutar un procedimiento almacenado parametrizado mediante EntityCommand
En este tema se muestra cómo ejecutar un procedimiento almacenado parametrizado usando la clase <xref:System.Data.EntityClient.EntityCommand>.  
  
### <a name="to-run-the-code-in-this-example"></a>Para ejecutar el código de este ejemplo  
  
1. Agregue el [modelo School](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)) al proyecto y configure el proyecto para que use el Entity Framework. Para obtener más información, consulte [Cómo Use el Asistente para](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))Entity Data Model.  
  
2. En la página de código de la aplicación, agregue las instrucciones `using` siguientes (`Imports` en Visual Basic):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3. Importe el procedimiento almacenado `GetStudentGrades` y especifique entidades `CourseGrade` como tipo de valor devuelto. Para obtener información sobre cómo importar un procedimiento almacenado, consulte [cómo: Importar un procedimiento](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896231(v=vs.100))almacenado.  
  
## <a name="example"></a>Ejemplo  
 El código siguiente ejecuta el procedimiento almacenado `GetStudentGrades` donde `StudentId` es un parámetro necesario. Los resultados los lee después una clase <xref:System.Data.EntityClient.EntityDataReader>.  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## <a name="see-also"></a>Vea también

- [Proveedor de EntityClient para Entity Framework](entityclient-provider-for-the-entity-framework.md)
