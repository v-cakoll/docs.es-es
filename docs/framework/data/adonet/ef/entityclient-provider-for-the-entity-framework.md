---
title: Proveedor de EntityClient para Entity Framework
ms.date: 03/30/2017
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
ms.openlocfilehash: e3a87d4a936e5bdf633e1f997f66dd98add2a9cb
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854703"
---
# <a name="entityclient-provider-for-the-entity-framework"></a>Proveedor de EntityClient para Entity Framework
El proveedor de EntityClient es un proveedor de datos que usan las aplicaciones de Entity Framework para tener acceso a los datos descritos en un modelo conceptual. Para obtener información sobre los modelos conceptuales, vea [modelado y asignación](modeling-and-mapping.md). EntityClient utiliza otros proveedores de datos .NET Framework para tener acceso al origen de datos. Por ejemplo, EntityClient utiliza el Proveedor de datos .NET Framework para SQL Server (SqlClient) al tener acceso a una base de datos de SQL Server. Para obtener información sobre el proveedor SqlClient, vea [SqlClient para el Entity Framework](sqlclient-for-the-entity-framework.md). El proveedor de EntityClient se implementa en el espacio de nombres <xref:System.Data.EntityClient>.  
  
## <a name="managing-connections"></a>Administrar conexiones  
 El Entity Framework se basa en los proveedores de datos ADO.net específicos del almacenamiento proporcionando un <xref:System.Data.EntityClient.EntityConnection> a un proveedor de datos subyacente y una base de datos relacional. Para construir un <xref:System.Data.EntityClient.EntityConnection> objeto, debe hacer referencia a un conjunto de metadatos que contenga la asignación y los modelos necesarios, y también un nombre de proveedor de datos específico del almacenamiento y una cadena de conexión. Una vez <xref:System.Data.EntityClient.EntityConnection> que se haya implementado, se puede tener acceso a las entidades a través de las clases generadas a partir del modelo conceptual.  
  
 Se puede especificar una cadena de conexión en el archivo app.config.  
  
 El espacio de nombres <xref:System.Data.EntityClient> también incluye la clase <xref:System.Data.EntityClient.EntityConnectionStringBuilder>. Esta clase permite que los programadores creen mediante programación cadenas de conexión sintácticamente correctas, y que analicen y recompilen las cadenas de conexión existentes, utilizando las propiedades y los métodos de la clase. Para obtener más información, vea [Cómo: Cree una cadena](how-to-build-an-entityconnection-connection-string.md)de conexión de EntityConnection.  
  
## <a name="creating-queries"></a>Crear consultas  
 El [!INCLUDE[esql](../../../../../includes/esql-md.md)] lenguaje es un dialecto de SQL independiente del almacenamiento que trabaja directamente con esquemas de entidades conceptuales y admite conceptos de Entity Data Model como la herencia y las relaciones. La <xref:System.Data.EntityClient.EntityCommand> clase se usa para ejecutar un [!INCLUDE[esql](../../../../../includes/esql-md.md)] comando en un modelo de entidad. Cuando se crean objetos de <xref:System.Data.EntityClient.EntityCommand>, se puede especificar un nombre de procedimiento almacenado o un texto de consulta. El Entity Framework funciona con proveedores de datos específicos del almacenamiento para traducir [!INCLUDE[esql](../../../../../includes/esql-md.md)] los genéricos en consultas específicas del almacenamiento. Para obtener más información sobre [!INCLUDE[esql](../../../../../includes/esql-md.md)] cómo escribir consultas, consulte [Entity SQL Language](./language-reference/entity-sql-language.md).  
  
 En el ejemplo siguiente se <xref:System.Data.EntityClient.EntityCommand> crea un objeto y se asigna [!INCLUDE[esql](../../../../../includes/esql-md.md)] un texto de consulta <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> a su propiedad. Esta [!INCLUDE[esql](../../../../../includes/esql-md.md)] consulta solicita los productos ordenados por el precio de venta del modelo conceptual. El código siguiente no tiene conocimiento alguno del modelo de almacenamiento.  
  
 ```csharp
EntityCommand cmd = conn.CreateCommand();
cmd.CommandText = @"SELECT VALUE p
  FROM AdventureWorksEntities.Product AS p
  ORDER BY p.ListPrice";
```
  
## <a name="executing-queries"></a>Ejecutar consultas  
 Cuando se ejecuta una consulta, se analiza y se convierte en un árbol de comandos canónico. Todo el procesamiento subsiguiente se realiza en el árbol de comandos. El árbol de comandos es el medio de comunicación entre <xref:System.Data.EntityClient> y el proveedor de datos de .NET Framework subyacente, <xref:System.Data.SqlClient>como.  
  
 <xref:System.Data.EntityClient.EntityDataReader> muestra los resultados de ejecutar <xref:System.Data.EntityClient.EntityCommand> en un modelo conceptual. Para ejecutar el comando que devuelve el <xref:System.Data.EntityClient.EntityDataReader>, llame a <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>. <xref:System.Data.EntityClient.EntityDataReader> implementa <xref:System.Data.IExtendedDataRecord> para describir resultados estructurados enriquecidos.  
  
## <a name="managing-transactions"></a>Administrar transacciones  
 En Entity Framework, hay dos maneras de utilizar las transacciones: automática y explícita. Las transacciones automáticas usan el espacio de nombres <xref:System.Transactions> y las transacciones explícitas usan la clase <xref:System.Data.EntityClient.EntityTransaction>.  
  
 Para actualizar los datos que se exponen a través de [un modelo conceptual, consulte How to: Administrar transacciones en el Entity Framework](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738523(v=vs.100)).  
  
## <a name="in-this-section"></a>En esta sección  
 [Procedimientos: Compilación de una cadena de conexión de EntityConnection](how-to-build-an-entityconnection-connection-string.md)  
  
 [Procedimientos: Ejecutar una consulta que devuelve resultados PrimitiveType](how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Cómo: Ejecutar una consulta que devuelve resultados StructuralType](how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Cómo: Ejecutar una consulta que devuelve resultados RefType](how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Procedimientos: Ejecutar una consulta que devuelve tipos complejos](how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Cómo: Ejecutar una consulta que devuelve colecciones anidadas](how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Procedimientos: Ejecutar una consulta de Entity SQL con parámetros mediante EntityCommand](how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Procedimientos: Ejecutar un procedimiento almacenado parametrizado usando EntityCommand](how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Procedimientos: Ejecutar una consulta polimórfica](how-to-execute-a-polymorphic-query.md)  
  
 [Cómo: Navegar por las relaciones con el operador Navigate](how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="see-also"></a>Vea también

- [Administrar conexiones y transacciones](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [ADO.NET Entity Framework](index.md)
- [Referencia del lenguaje](./language-reference/index.md)
