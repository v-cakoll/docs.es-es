---
title: Parámetros REF CURSOR de Oracle
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 7cd29a6a20015c7ce4475b0211cb07f7ee78b530
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794871"
---
# <a name="oracle-ref-cursors"></a>Parámetros REF CURSOR de Oracle
El proveedor de datos de .NET Framework para Oracle admite el tipo de datos **ref cursor** de Oracle. Cuando utilice el proveedor de datos para trabajar con cursores REF CURSOR de Oracle, debe tener en cuenta los siguientes comportamientos.  
  
> [!NOTE]
> Algunos de ellos difieren de los del proveedor Microsoft OLE DB para Oracle (MSDAORA).  
  
- Por motivos de rendimiento, el proveedor de datos para Oracle no enlaza automáticamente los tipos de datos **ref cursor** , como hace MSDAORA, a menos que se especifiquen explícitamente.  
  
- El proveedor de datos no admite ninguna secuencia de escape ODBC, lo que incluye el escape {resultset} usado para especificar parámetros REF CURSOR.  
  
- Para ejecutar un procedimiento almacenado que devuelve los cursores REF cursor, debe definir los parámetros de <xref:System.Data.OracleClient.OracleParameterCollection> con un <xref:System.Data.OracleClient.OracleType> de **cursor** y un <xref:System.Data.OracleClient.OracleParameter.Direction%2A> de **Output**. El proveedor de datos admite el enlace de cursores REF CURSOR sólo como parámetros de salida; no los admite como parámetros de entrada.  
  
- No se permite la obtención de un <xref:System.Data.OracleClient.OracleDataReader> del valor del parámetro. Los valores son del tipo <xref:System.DBNull> después de la ejecución del comando.  
  
- El único valor de enumeración de **CommandBehavior** que funciona con cursores REF cursor (por <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>ejemplo, al llamar a) es **CloseConnection**; se omiten todos los demás.  
  
- El orden de los CURSOres REF CURSOR en el objeto **OracleDataReader** depende del orden de los parámetros de **OracleParameterCollection**. Se omite la propiedad <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A>.  
  
- No se admite el tipo de datos de la **tabla** PL/SQL. No obstante, los cursores REF CURSOR resultan más eficientes. Si debe utilizar un tipo de datos de **tabla** , use el proveedor de datos OLE DB .net con MSDAORA.  
  
## <a name="in-this-section"></a>En esta sección  
 [Ejemplos de REF CURSOR](ref-cursor-examples.md)  
 Contiene tres ejemplos en los que se muestra el uso de cursores REF CURSOR.  
  
 [Parámetros REF CURSOR en un objeto OracleDataReader](ref-cursor-parameters-in-an-oracledatareader.md)  
 Muestra cómo ejecutar un procedimiento almacenado PL/SQL que devuelve un parámetro REF CURSOR y lee el valor como **OracleDataReader**.  
  
 [Recuperación de datos desde varios parámetros REF CURSOR utilizando un objeto OracleDataReader](retrieving-data-from-multiple-ref-cursors.md)  
 Muestra cómo ejecutar un procedimiento almacenado PL/SQL que devuelve dos parámetros REF CURSOR y Lee los valores mediante un **OracleDataReader**.  
  
 [Relleno de un conjunto de datos utilizando uno o varios parámetros REF CURSOR](filling-a-dataset-using-one-or-more-ref-cursors.md)  
 Muestra cómo ejecutar un procedimiento almacenado PL/SQL que devuelve dos parámetros REF CURSOR y llena un <xref:System.Data.DataSet> con las filas que se devuelven.  
  
## <a name="see-also"></a>Vea también

- [Oracle y ADO.NET](oracle-and-adonet.md)
- [Información general sobre ADO.NET](ado-net-overview.md)
