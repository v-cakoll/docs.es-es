---
title: Guía de seguridad de DataSet y DataTable
ms.date: 07/14/2020
dev_langs:
- csharp
ms.openlocfilehash: c6b32afeadccc3fd22d6611d282840233280440f
ms.sourcegitcommit: e7748001b1cee80ced691d8a76ca814c0b02dd9b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2020
ms.locfileid: "86382472"
---
# <a name="dataset-and-datatable-security-guidance"></a><span data-ttu-id="d2e1c-102">Guía de seguridad de DataSet y DataTable</span><span class="sxs-lookup"><span data-stu-id="d2e1c-102">DataSet and DataTable security guidance</span></span>

<span data-ttu-id="d2e1c-103">Este artículo se aplica a:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-103">This article applies to:</span></span>

* <span data-ttu-id="d2e1c-104">.NET Framework (todas las versiones)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-104">.NET Framework (all versions)</span></span>
* <span data-ttu-id="d2e1c-105">.NET Core y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="d2e1c-105">.NET Core and later</span></span>
* <span data-ttu-id="d2e1c-106">.NET 5,0 y versiones posteriores</span><span class="sxs-lookup"><span data-stu-id="d2e1c-106">.NET 5.0 and later</span></span>

<span data-ttu-id="d2e1c-107">Los tipos [DataSet](/dotnet/api/system.data.dataset) y [DataTable](/dotnet/api/system.data.datatable) son componentes de .net heredados que permiten representar conjuntos de datos como objetos administrados.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-107">The [DataSet](/dotnet/api/system.data.dataset) and [DataTable](/dotnet/api/system.data.datatable) types are legacy .NET components that allow representing data sets as managed objects.</span></span> <span data-ttu-id="d2e1c-108">Estos componentes se introdujeron en .NET 1,0 como parte de la [infraestructura de ADO.net](/dotnet/framework/data/adonet/dataset-datatable-dataview/)original.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-108">These components were introduced in .NET 1.0 as part of the original [ADO.NET infrastructure](/dotnet/framework/data/adonet/dataset-datatable-dataview/).</span></span> <span data-ttu-id="d2e1c-109">Su objetivo era proporcionar una vista administrada a través de un conjunto de datos relacional, extraabstraendo si el origen subyacente de los datos era XML, SQL u otra tecnología.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-109">Their goal was to provide a managed view over a relational data set, abstracting away whether the underlying source of the data was XML, SQL, or another technology.</span></span>

<span data-ttu-id="d2e1c-110">Para obtener más información sobre ADO.NET, incluidos los paradigmas más modernos de la vista de datos, vea [la documentación de ADO.net](/dotnet/framework/data/adonet/).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-110">For more information on ADO.NET, including more modern data view paradigms, see [the ADO.NET documentation](/dotnet/framework/data/adonet/).</span></span>

## <a name="default-restrictions-when-deserializing-a-dataset-or-datatable-from-xml"></a><span data-ttu-id="d2e1c-111">Restricciones predeterminadas al deserializar un DataSet o DataTable desde XML</span><span class="sxs-lookup"><span data-stu-id="d2e1c-111">Default restrictions when deserializing a DataSet or DataTable from XML</span></span>

<span data-ttu-id="d2e1c-112">En todas las versiones compatibles de .NET Framework, .NET Core y .NET, `DataSet` y `DataTable` se aplican las restricciones siguientes a los tipos de objetos que pueden estar presentes en los datos deserializados.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-112">On all supported versions of .NET Framework, .NET Core, and .NET, `DataSet` and `DataTable` place the following restrictions on what types of objects may be present in the deserialized data.</span></span> <span data-ttu-id="d2e1c-113">De forma predeterminada, esta lista está restringida a:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-113">By default, this list is restricted to:</span></span>

* <span data-ttu-id="d2e1c-114">Tipos primitivos y equivalentes primitivos:,,,,,,,,,,,,,,,,,,, `bool` `char` `sbyte` `byte` `short` `ushort` `int` `uint` `long` `ulong` `float` `double` `decimal` `DateTime` `DateTimeOffset` `TimeSpan` `string` `Guid` `SqlBinary` `SqlBoolean` , `SqlByte` , `SqlBytes` ,,,, `SqlChars` , `SqlDateTime` `SqlDecimal` `SqlDouble` `SqlGuid` `SqlInt16` `SqlInt32` `SqlInt64` `SqlMoney` `SqlSingle` `SqlString` ,,,,, y.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-114">Primitives and primitive equivalents: `bool`, `char`, `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, `decimal`, `DateTime`, `DateTimeOffset`, `TimeSpan`, `string`, `Guid`, `SqlBinary`, `SqlBoolean`, `SqlByte`, `SqlBytes`, `SqlChars`, `SqlDateTime`, `SqlDecimal`, `SqlDouble`, `SqlGuid`, `SqlInt16`, `SqlInt32`, `SqlInt64`, `SqlMoney`, `SqlSingle`, and `SqlString`.</span></span>
* <span data-ttu-id="d2e1c-115">No primitivos usados comúnmente: `Type` , `Uri` y `BigInteger` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-115">Commonly used non-primitives: `Type`, `Uri`, and `BigInteger`.</span></span>
* <span data-ttu-id="d2e1c-116">Tipos _System. Drawing_ usados comúnmente: `Color` , `Point` , `PointF` , `Rectangle` , `RectangleF` , `Size` y `SizeF` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-116">Commonly used _System.Drawing_ types: `Color`, `Point`, `PointF`, `Rectangle`, `RectangleF`, `Size`, and `SizeF`.</span></span>
* <span data-ttu-id="d2e1c-117">`Enum`distintos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-117">`Enum` types.</span></span>
* <span data-ttu-id="d2e1c-118">Matrices y listas de los tipos anteriores.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-118">Arrays and lists of the above types.</span></span>

<span data-ttu-id="d2e1c-119">Si los datos XML entrantes contienen un objeto cuyo tipo no está en esta lista:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-119">If the incoming XML data contains an object whose type is not in this list:</span></span>

* <span data-ttu-id="d2e1c-120">Se inicia una excepción.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-120">An exception is thrown.</span></span>
* <span data-ttu-id="d2e1c-121">Se produce un error en la operación de deserialización.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-121">The deserialization operation fails.</span></span>

<span data-ttu-id="d2e1c-122">Al cargar XML en una `DataSet` instancia de o existente `DataTable` , también se tienen en cuenta las definiciones de columna existentes.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-122">When loading XML into an existing `DataSet` or `DataTable` instance, the existing column definitions are also taken into account.</span></span> <span data-ttu-id="d2e1c-123">Si la tabla ya contiene una definición de columna de un tipo personalizado, ese tipo se agrega temporalmente a la lista de permitidos mientras dure la operación de deserialización de XML.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-123">If the table already contains a column definition of a custom type, that type is temporarily added to the allow list for the duration of the XML deserialization operation.</span></span>

```cs
XmlReader xmlReader = GetXmlReader();

// Assume the XML blob contains data for type MyCustomClass.
// The following call to ReadXml fails because MyCustomClass isn't in the allowed types list.

DataTable table = new DataTable("MyDataTable");
table.ReadXml(xmlReader);

// However, the following call to ReadXml succeeds, since the DataTable instance
// already defines a column of type MyCustomClass.

DataTable table = new DataTable("MyDataTable");
table.Columns.Add("MyColumn", typeof(MyCustomClass));
table.ReadXml(xmlReader); // this call will succeed
```

<span data-ttu-id="d2e1c-124">Las restricciones de tipo de objeto también se aplican cuando `XmlSerializer` se usa para deserializar una instancia de `DataSet` o `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-124">The object type restrictions also apply when using `XmlSerializer` to deserialize an instance of `DataSet` or `DataTable`.</span></span> <span data-ttu-id="d2e1c-125">Sin embargo, es posible que no se apliquen al utilizar `BinaryFormatter` para deserializar una instancia de `DataSet` o `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-125">However, they may not apply when using `BinaryFormatter` to deserialize an instance of `DataSet` or `DataTable`.</span></span>

<span data-ttu-id="d2e1c-126">Las restricciones de tipo de objeto no se aplican cuando `DataAdapter.Fill` se usa, como cuando una `DataTable` instancia se rellena directamente desde una base de datos sin usar las API de deserialización XML.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-126">The object type restrictions don't apply when using `DataAdapter.Fill`, such as when a `DataTable` instance is populated directly from a database without using the XML deserialization APIs.</span></span>

### <a name="extend-the-list-of-allowed-types"></a><span data-ttu-id="d2e1c-127">Ampliar la lista de tipos permitidos</span><span class="sxs-lookup"><span data-stu-id="d2e1c-127">Extend the list of allowed types</span></span>

<span data-ttu-id="d2e1c-128">Una aplicación puede extender la lista de tipos permitidos para incluir tipos personalizados además de los tipos integrados enumerados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-128">An app can extend the allowed types list to include custom types in addition to the built-in types listed above.</span></span> <span data-ttu-id="d2e1c-129">Si se extiende la lista de tipos permitidos, el cambio afecta a _todas_ las `DataSet` instancias de y dentro de `DataTable` la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-129">If extending the allowed types list, the change affects _all_ `DataSet` and `DataTable` instances within the app.</span></span> <span data-ttu-id="d2e1c-130">Los tipos no se pueden quitar de la lista de tipos permitidos integrados.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-130">Types cannot be removed from the built-in allowed types list.</span></span>

#### <a name="extend-through-configuration-net-framework-40---48"></a><span data-ttu-id="d2e1c-131">Extender a través de la configuración (.NET Framework 4,0-4,8)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-131">Extend through configuration (.NET Framework 4.0 - 4.8)</span></span>

<span data-ttu-id="d2e1c-132">_App.config_ se puede usar para ampliar la lista de tipos permitidos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-132">_App.config_ can be used to extend the allowed types list.</span></span> <span data-ttu-id="d2e1c-133">Para ampliar la lista de tipos permitidos:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-133">To extend the allowed types list:</span></span>

* <span data-ttu-id="d2e1c-134">Use el `<configSections>` elemento para agregar una referencia a la sección de configuración _System. Data_ .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-134">Use the `<configSections>` element to add a reference to the _System.Data_ configuration section.</span></span>
* <span data-ttu-id="d2e1c-135">`<system.data.dataset.serialization>` / `<allowedTypes>` Se usa para especificar tipos adicionales.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-135">Use `<system.data.dataset.serialization>`/`<allowedTypes>` to specify additional types.</span></span>

<span data-ttu-id="d2e1c-136">Cada `<add>` elemento debe especificar un solo tipo usando su nombre de tipo calificado con el ensamblado.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-136">Each `<add>` element must specify only one type by using its assembly qualified type name.</span></span> <span data-ttu-id="d2e1c-137">Para agregar tipos adicionales a la lista de tipos permitidos, use varios `<add>` elementos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-137">To add additional types to the allowed types list, use multiple `<add>` elements.</span></span>

<span data-ttu-id="d2e1c-138">En el ejemplo siguiente se muestra cómo extender la lista de tipos permitidos agregando el tipo personalizado `Fabrikam.CustomType` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-138">The following sample shows extending the allowed types list by adding the custom type `Fabrikam.CustomType`.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <sectionGroup name="system.data.dataset.serialization" type="System.Data.SerializationSettingsSectionGroup, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="allowedTypes" type="System.Data.AllowedTypesSectionHandler, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
    </sectionGroup>
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes>
      <!-- <add type="assembly qualified type name" /> -->
      <add type="Fabrikam.CustomType, Fabrikam, Version=1.0.0.0, Culture=neutral, PublicKeyToken=2b3831f2f2b744f7" />
      <!-- additional <add /> elements as needed -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

<span data-ttu-id="d2e1c-139">Para recuperar el nombre calificado del ensamblado de un tipo, use la propiedad [Type. AssemblyQualifiedName](/dotnet/api/system.type.assemblyqualifiedname) , como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-139">To retrieve the assembly qualified name of a type, use the [Type.AssemblyQualifiedName](/dotnet/api/system.type.assemblyqualifiedname) property, as demonstrated in the following code.</span></span>

```cs
string assemblyQualifiedName = typeof(Fabrikam.CustomType).AssemblyQualifiedName;
```

<a name="etc"></a>

#### <a name="extend-through-configuration-net-framework-20---35"></a><span data-ttu-id="d2e1c-140">Extender a través de la configuración (.NET Framework 2,0-3,5)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-140">Extend through configuration (.NET Framework 2.0 - 3.5)</span></span>

<span data-ttu-id="d2e1c-141">Si su aplicación tiene como destino .NET Framework 2,0 o 3,5, todavía puede usar el mecanismo de _App.config_ anterior para ampliar la lista de tipos permitidos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-141">If your app targets .NET Framework 2.0 or 3.5, you can still use the above _App.config_ mechanism to extend the allowed types list.</span></span> <span data-ttu-id="d2e1c-142">Sin embargo, el `<configSections>` elemento tendrá un aspecto ligeramente diferente, tal como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-142">However, your `<configSections>` element will look slightly different, as shown in the following code:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <!-- The below <sectionGroup> and <section> are specific to .NET Framework 2.0 and 3.5. -->
    <sectionGroup name="system.data.dataset.serialization" type="System.Data.SerializationSettingsSectionGroup, System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">
      <section name="allowedTypes" type="System.Data.AllowedTypesSectionHandler, System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>
    </sectionGroup>
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes>
      <!-- <add /> elements, as demonstrated in the .NET Framework 4.0 - 4.8 sample code above. -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

#### <a name="extend-programmatically-net-framework-net-core-net-50"></a><span data-ttu-id="d2e1c-143">Extender mediante programación (.NET Framework, .NET Core, .NET 5.0 +)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-143">Extend programmatically (.NET Framework, .NET Core, .NET 5.0+)</span></span>

<span data-ttu-id="d2e1c-144">La lista de tipos permitidos también puede ampliarse mediante programación usando [AppDomain. SetData](/dotnet/api/system.appdomain.setdata) con el sistema de claves conocido _System. Data. DataSetDefaultAllowedTypes_, como se muestra en el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-144">The list of allowed types can also be extended programmatically by using [AppDomain.SetData](/dotnet/api/system.appdomain.setdata) with the well-known key _System.Data.DataSetDefaultAllowedTypes_, as shown in the following code.</span></span>

```cs
Type[] extraAllowedTypes = new Type[]
{
    typeof(Fabrikam.CustomType),
    typeof(Contoso.AdditionalCustomType)
};

AppDomain.CurrentDomain.SetData("System.Data.DataSetDefaultAllowedTypes", extraAllowedTypes);
```

<span data-ttu-id="d2e1c-145">Si se usa el mecanismo de extensión, el valor asociado a la clave _System. Data. DataSetDefaultAllowedTypes_ debe ser de tipo `Type[]` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-145">If using the extension mechanism, the value associated with the key _System.Data.DataSetDefaultAllowedTypes_ must be of type `Type[]`.</span></span>

<span data-ttu-id="d2e1c-146">En .NET Framework, la lista de tipos permitidos se puede extender con _App.config_ y `AppDomain.SetData` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-146">On .NET Framework, the list of allowed types may be extended both with _App.config_ and `AppDomain.SetData`.</span></span> <span data-ttu-id="d2e1c-147">En este caso, `DataSet` y `DataTable` permitirá que un objeto se deserialice como parte de los datos si su tipo está presente en cualquiera de las listas.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-147">In this case, `DataSet` and `DataTable` will allow an object to be deserialized as part of the data if its type is present in either list.</span></span>

### <a name="run-an-app-in-audit-mode-net-framework"></a><span data-ttu-id="d2e1c-148">Ejecutar una aplicación en modo auditoría (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-148">Run an app in audit mode (.NET Framework)</span></span>

<span data-ttu-id="d2e1c-149">En .NET Framework, `DataSet` y `DataTable` proporcionan una capacidad de modo de auditoría.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-149">In .NET Framework, `DataSet` and `DataTable` provide an audit mode capability.</span></span> <span data-ttu-id="d2e1c-150">Cuando está habilitado el modo `DataSet` de auditoría y `DataTable` compara los tipos de objetos entrantes con la lista de tipos permitidos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-150">When audit mode is enabled, `DataSet` and `DataTable` compare the types of incoming objects against the allowed types list.</span></span> <span data-ttu-id="d2e1c-151">Sin embargo, si se muestra un objeto cuyo tipo no está permitido, **no** se produce una excepción.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-151">However, if an object whose type is not allowed is seen, an exception is **not** thrown.</span></span> <span data-ttu-id="d2e1c-152">En su lugar, `DataSet` y `DataTable` notifican a las instancias adjuntas `TraceListener` que un tipo sospechoso está presente, lo que permite `TraceListener` que registre esta información.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-152">Instead, `DataSet` and `DataTable` notify any attached `TraceListener` instances that a suspicious type is present, allowing the `TraceListener` to log this information.</span></span> <span data-ttu-id="d2e1c-153">No se produce ninguna excepción y continúa la operación de deserialización.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-153">No exception is thrown and the deserialization operation continues.</span></span>

> [!WARNING]
> <span data-ttu-id="d2e1c-154">La ejecución de una aplicación en "modo de auditoría" solo debe ser una medida temporal utilizada para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-154">Running an app in "audit mode" should only be a temporary measure used for testing.</span></span> <span data-ttu-id="d2e1c-155">Cuando el modo de auditoría está habilitado `DataSet` y `DataTable` no impone restricciones de tipo, lo que puede incluir un hueco de seguridad dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-155">When audit mode is enabled, `DataSet` and `DataTable` do not enforce type restrictions, which can introduce a security hole inside your app.</span></span> <span data-ttu-id="d2e1c-156">Para obtener más información, vea las secciones titulada [quitar todas las restricciones de tipo](#ratr) y [seguridad con respecto a la entrada que](#swr)no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-156">For more information, see the sections titled [Removing all type restrictions](#ratr) and [Safety with regard to untrusted input](#swr).</span></span>

<span data-ttu-id="d2e1c-157">El modo auditoría se puede habilitar a través de _App.config_:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-157">Audit mode can be enabled through _App.config_:</span></span>

* <span data-ttu-id="d2e1c-158">Vea la sección [extender a través](#etc) de la configuración de este documento para obtener información sobre el valor apropiado que se debe colocar para el `<configSections>` elemento.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-158">See the [Extending through configuration](#etc) section in this document for information on the proper value to put for the `<configSections>` element.</span></span>
* <span data-ttu-id="d2e1c-159">Use `<allowedTypes auditOnly="true">` para habilitar el modo de auditoría, tal como se muestra en el marcado siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-159">Use `<allowedTypes auditOnly="true">` to enable audit mode, as shown in the following markup.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <!-- See the section of this document titled "Extending through configuration" for the appropriate
         <sectionGroup> and <section> elements to put here, depending on whether you're running .NET
         Framework 2.0 - 3.5 or 4.0 - 4.8. -->
  </configSections>
  <system.data.dataset.serialization>
    <allowedTypes auditOnly="true"> <!-- setting auditOnly="true" enables audit mode -->
      <!-- Optional <add /> elements as needed. -->
    </allowedTypes>
  </system.data.dataset.serialization>
</configuration>
```

<span data-ttu-id="d2e1c-160">Una vez habilitado el modo de auditoría, puede usar _App.config_ para conectar su preferido `TraceListener` al `DataSet` nombre integrado del `TraceSource.` origen de seguimiento integrado es _System. Data. DataSet_.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-160">Once audit mode is enabled, you can use _App.config_ to connect your preferred `TraceListener` to the `DataSet` built-in `TraceSource.` The name of the built-in trace source is _System.Data.DataSet_.</span></span> <span data-ttu-id="d2e1c-161">En el ejemplo siguiente se muestra cómo escribir eventos de seguimiento en la consola _y_ en un archivo de registro en disco.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-161">The following sample demonstrates writing trace events to the console _and_ to a log file on disk.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="System.Data.DataSet"
              switchType="System.Diagnostics.SourceSwitch"
              switchValue="Warning">
        <listeners>
          <!-- write to the console -->
          <add name="console"
               type="System.Diagnostics.ConsoleTraceListener" />
          <!-- *and* write to a log file on disk -->
          <add name="filelog"
               type="System.Diagnostics.TextWriterTraceListener"
               initializeData="c:\logs\mylog.txt" />
        </listeners>
      </source>
    </sources>
  </system.diagnostics>
</configuration>
```

<span data-ttu-id="d2e1c-162">Para obtener más información sobre `TraceSource` y `TraceListener` , vea el documento [Cómo: utilizar TraceSource y filtros con agentes de escucha de seguimiento](/dotnet/framework/debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-162">For more information on `TraceSource` and `TraceListener`, see the document [How to: Use TraceSource and Filters with Trace Listeners](/dotnet/framework/debug-trace-profile/how-to-use-tracesource-and-filters-with-trace-listeners).</span></span>

<span data-ttu-id="d2e1c-163">**Nota**: la ejecución de una aplicación en modo auditoría no está disponible en .net Core o en .net 5,0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-163">**Note**: Running an app in audit mode is not available in .NET Core or in .NET 5.0 and later.</span></span>

<a name="ratr"></a>

### <a name="remove-all-type-restrictions"></a><span data-ttu-id="d2e1c-164">Quitar todas las restricciones de tipo</span><span class="sxs-lookup"><span data-stu-id="d2e1c-164">Remove all type restrictions</span></span>

<span data-ttu-id="d2e1c-165">Si una aplicación debe quitar todas las restricciones de limitación de tipos de `DataSet` y `DataTable` :</span><span class="sxs-lookup"><span data-stu-id="d2e1c-165">If an app must remove all type limiting restrictions from `DataSet` and `DataTable`:</span></span>

* <span data-ttu-id="d2e1c-166">Hay varias opciones para suprimir las restricciones de limitación de tipos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-166">There are several options to suppress type limiting restrictions.</span></span>
* <span data-ttu-id="d2e1c-167">Las opciones disponibles dependen del marco de trabajo de destino de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-167">The options available depend on the framework the app targets.</span></span>

> [!WARNING]
> <span data-ttu-id="d2e1c-168">Al quitar todas las restricciones de tipo, se puede introducir un agujero de seguridad dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-168">Removing all type restrictions can introduce a security hole inside the app.</span></span> <span data-ttu-id="d2e1c-169">Al utilizar este mecanismo, asegúrese de que la **not** aplicación no usa `DataSet` o `DataTable` para leer la entrada que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-169">When using this mechanism, ensure the app does **not** use `DataSet` or `DataTable` to read untrusted input.</span></span> <span data-ttu-id="d2e1c-170">Para obtener más información, vea [CVE-2020-1147](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-1147) y la sección siguiente titulada [seguridad con respecto a la entrada que no es de confianza](#swr).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-170">For more information, see [CVE-2020-1147](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-1147) and the following section titled [Safety with regard to untrusted input](#swr).</span></span>

#### <a name="through-appcontext-configuration-net-framework-46---48-net-core-21-and-later-net-50-and-later"></a><span data-ttu-id="d2e1c-171">A través de la configuración de AppContext (.NET Framework 4,6-4,8, .NET Core 2,1 y versiones posteriores, .NET 5,0 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-171">Through AppContext configuration (.NET Framework 4.6 - 4.8, .NET Core 2.1 and later, .NET 5.0 and later)</span></span>

<span data-ttu-id="d2e1c-172">El `AppContext` modificador, `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation` , cuando se establece en, `true` quita todas las restricciones de limitación de tipos de `DataSet` y `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-172">The `AppContext` switch, `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation`, when set to `true` removes all type limiting restrictions from `DataSet` and `DataTable`.</span></span>

<span data-ttu-id="d2e1c-173">En .NET Framework, este modificador se puede habilitar a través de _App.config_, tal y como se muestra en la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-173">In .NET Framework, this switch can be enabled via _App.config_, as shown in the following configuration:</span></span>

```xml
<configuration>
   <runtime>
      <!-- Warning: setting the following switch can introduce a security problem. -->
      <AppContextSwitchOverrides value="Switch.System.Data.AllowArbitraryDataSetTypeInstantiation=true" />
   </runtime>
</configuration>
```

<span data-ttu-id="d2e1c-174">En ASP.NET, el `<AppContextSwitchOverrides>` elemento no está disponible.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-174">In ASP.NET, the `<AppContextSwitchOverrides>` element is not available.</span></span> <span data-ttu-id="d2e1c-175">En su lugar, el conmutador se puede habilitar a través de _Web.config_, como se muestra en la configuración siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-175">Instead, the switch can be enabled via _Web.config_, as shown in the following configuration:</span></span>

```xml
<configuration>
    <appSettings>
        <!-- Warning: setting the following switch can introduce a security problem. -->
        <add key="AppContext.SetSwitch:Switch.System.Data.AllowArbitraryDataSetTypeInstantiation" value="true" />
    </appSettings>
</configuration>
```

<span data-ttu-id="d2e1c-176">Para obtener más información, vea el [\<AppContextSwitchOverrides>](/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element) elemento.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-176">For more information, see the [\<AppContextSwitchOverrides>](/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element) element.</span></span>

<span data-ttu-id="d2e1c-177">En .NET Core, .NET 5 y ASP.NET Core, este valor se controla mediante _runtimeconfig.jsen_, tal y como se muestra en el siguiente JSON:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-177">In .NET Core, .NET 5, and ASP.NET Core, this setting is controlled by _runtimeconfig.json_, as shown in the following JSON:</span></span>

```json
{
  "runtimeOptions": {
    "configProperties": {
      "Switch.System.Data.AllowArbitraryDataSetTypeInstantiation": true
    }
  }
}
```

<span data-ttu-id="d2e1c-178">Para obtener más información, vea ["opciones de configuración en tiempo de ejecución de .net Core"](/dotnet/core/run-time-config/).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-178">For more information, see [".NET Core run-time configuration settings"](/dotnet/core/run-time-config/).</span></span>

<span data-ttu-id="d2e1c-179">`AllowArbitraryDataSetTypeInstantiation`también se puede establecer mediante programación a través de [AppContext. SetSwitch](/dotnet/api/system.appcontext.setswitch) en lugar de usar un archivo de configuración, como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-179">`AllowArbitraryDataSetTypeInstantiation` can also be set programmatically via [AppContext.SetSwitch](/dotnet/api/system.appcontext.setswitch) instead of using a configuration file, as shown in the following code:</span></span>

```cs
// Warning: setting the following switch can introduce a security problem.
AppContext.SetSwitch("Switch.System.Data.AllowArbitraryDataSetTypeInstantiation", true);
```

 <span data-ttu-id="d2e1c-180">Si elige el enfoque de programación anterior, la llamada a `AppContext.SetSwitch` debe realizarse al principio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-180">If you choose the preceding programmatic approach, the call to `AppContext.SetSwitch` should occur early in the apps startup.</span></span>

#### <a name="through-the-machine-wide-registry-net-framework-20---48"></a><span data-ttu-id="d2e1c-181">A través del registro en todo el equipo (.NET Framework 2,0-4,8)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-181">Through the machine-wide registry (.NET Framework 2.0 - 4.8)</span></span>

<span data-ttu-id="d2e1c-182">Si `AppContext` no está disponible, las comprobaciones de limitación de tipos se pueden deshabilitar con el registro de Windows:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-182">If `AppContext` is not available, type limiting checks can be disabled with the Windows registry:</span></span>

* <span data-ttu-id="d2e1c-183">Un administrador debe configurar el registro.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-183">An administrator must configure the registry.</span></span>
* <span data-ttu-id="d2e1c-184">El uso del registro es un cambio en todo el equipo y afectará a _todas las_ aplicaciones que se ejecutan en la máquina.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-184">Using the registry is a machine-wide change and will affect _all_ apps running on the machine.</span></span>

| <span data-ttu-id="d2e1c-185">Tipo</span><span class="sxs-lookup"><span data-stu-id="d2e1c-185">Type</span></span>  |  <span data-ttu-id="d2e1c-186">Value</span><span class="sxs-lookup"><span data-stu-id="d2e1c-186">Value</span></span> |
|---|---|
| <span data-ttu-id="d2e1c-187">**Clave del Registro**</span><span class="sxs-lookup"><span data-stu-id="d2e1c-187">**Registry key**</span></span> | `HKLM\SOFTWARE\Microsoft\.NETFramework\AppContext` |
| <span data-ttu-id="d2e1c-188">**Nombre del valor**</span><span class="sxs-lookup"><span data-stu-id="d2e1c-188">**Value name**</span></span> | `Switch.System.Data.AllowArbitraryDataSetTypeInstantiation` |
| <span data-ttu-id="d2e1c-189">**Tipo de valor**</span><span class="sxs-lookup"><span data-stu-id="d2e1c-189">**Value type**</span></span> | `REG_SZ` |
| <span data-ttu-id="d2e1c-190">**Datos de valor**</span><span class="sxs-lookup"><span data-stu-id="d2e1c-190">**Value data**</span></span> | `true` |

<span data-ttu-id="d2e1c-191">En un sistema operativo de 64 bits, es necesario agregar este valor para la clave de 64 bits (mostrada anteriormente) y la clave de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-191">On a 64-bit operating system, this value my need to be added for both the 64-bit key (shown above) and the 32-bit key.</span></span> <span data-ttu-id="d2e1c-192">La clave de 32 bits se encuentra en `HKLM\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\AppContext` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-192">The 32-bit key is located at `HKLM\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\AppContext`.</span></span>

<span data-ttu-id="d2e1c-193">Para obtener más información sobre el uso del registro para configurar `AppContext` , vea ["AppContext for Library Consumers"](/dotnet/api/system.appcontext#appcontext-for-library-consumers).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-193">For more information on using the registry to configure `AppContext`, see ["AppContext for library consumers"](/dotnet/api/system.appcontext#appcontext-for-library-consumers).</span></span>

<a name="swr"></a>

## <a name="safety-with-regard-to-untrusted-input"></a><span data-ttu-id="d2e1c-194">Seguridad con respecto a la entrada que no es de confianza</span><span class="sxs-lookup"><span data-stu-id="d2e1c-194">Safety with regard to untrusted input</span></span>

<span data-ttu-id="d2e1c-195">While `DataSet` y `DataTable` imponen limitaciones predeterminadas en los tipos que se pueden encontrar durante la deserialización de cargas XML __ `DataSet` y `DataTable` no suelen ser seguras cuando se rellenan con una entrada que no es de confianza.__</span><span class="sxs-lookup"><span data-stu-id="d2e1c-195">While `DataSet` and `DataTable` do impose default limitations on the types that are allowed to be present while deserializing XML payloads, __`DataSet` and `DataTable` are in general not safe when populated with untrusted input.__</span></span> <span data-ttu-id="d2e1c-196">A continuación se muestra una lista no exhaustiva de formas en que `DataSet` una `DataTable` instancia de o podría leer una entrada que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-196">The following is a non-exhaustive list of ways that a `DataSet` or `DataTable` instance might read untrusted input.</span></span>

* <span data-ttu-id="d2e1c-197">Un `DataAdapter` hace referencia a una base de datos de y el `DataAdapter.Fill` método se utiliza para rellenar `DataSet` con el contenido de una consulta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-197">A `DataAdapter` references a database, and the `DataAdapter.Fill` method is used to populate a `DataSet` with the contents of a database query.</span></span>
* <span data-ttu-id="d2e1c-198">El `DataSet.ReadXml` `DataTable.ReadXml` método o se utiliza para leer un archivo XML que contiene información de columnas y filas.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-198">The `DataSet.ReadXml` or `DataTable.ReadXml` method is used to read an XML file containing column and row information.</span></span>
* <span data-ttu-id="d2e1c-199">Una `DataSet` instancia de o `DataTable` se serializa como parte de un punto de conexión de WCF o servicios Web ASP.net (SOAP).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-199">A `DataSet` or `DataTable` instance is serialized as part of a ASP.NET (SOAP) web services or WCF endpoint.</span></span>
* <span data-ttu-id="d2e1c-200">Un serializador como `XmlSerializer` se utiliza para deserializar una `DataSet` `DataTable` instancia de o de una secuencia XML.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-200">A serializer such as `XmlSerializer` is used to deserialize a `DataSet` or `DataTable` instance from an XML stream.</span></span>
* <span data-ttu-id="d2e1c-201">Un serializador como `JsonConvert` se usa para deserializar una `DataSet` `DataTable` instancia de o de un flujo JSON.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-201">A serializer such as `JsonConvert` is used to deserialize a `DataSet` or `DataTable` instance from a JSON stream.</span></span> <span data-ttu-id="d2e1c-202">`JsonConvert`es un método de la conocida [Newtonsoft.Jsde terceros en](https://www.newtonsoft.com/json) la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-202">`JsonConvert` is a method in the popular third-party [Newtonsoft.Json](https://www.newtonsoft.com/json) library.</span></span>
* <span data-ttu-id="d2e1c-203">Un serializador como `BinaryFormatter` se usa para deserializar una `DataSet` `DataTable` instancia de o a partir de una secuencia de bytes sin formato.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-203">A serializer such as `BinaryFormatter` is used to deserialize a `DataSet` or `DataTable` instance from a raw byte stream.</span></span>

<span data-ttu-id="d2e1c-204">En este documento se describen las consideraciones de seguridad para los escenarios anteriores.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-204">This document discusses safety considerations for the preceding scenarios.</span></span>

## <a name="use-dataadapterfill-to-populate-a-dataset-from-an-untrusted-data-source"></a><span data-ttu-id="d2e1c-205">Usar `DataAdapter.Fill` para rellenar a `DataSet` partir de un origen de datos que no es de confianza</span><span class="sxs-lookup"><span data-stu-id="d2e1c-205">Use `DataAdapter.Fill` to populate a `DataSet` from an untrusted data source</span></span>

<span data-ttu-id="d2e1c-206">`DataSet`Se puede rellenar una instancia de `DataAdapter` mediante [el `DataAdapter.Fill` método](/dotnet/api/system.data.common.dataadapter.fill), tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-206">A `DataSet` instance can be populated from a `DataAdapter` by using [the `DataAdapter.Fill` method](/dotnet/api/system.data.common.dataadapter.fill), as shown in the following example.</span></span>

```cs
// Assumes that connection is a valid SqlConnection object.  
string queryString =
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");
```

<span data-ttu-id="d2e1c-207">(El ejemplo de código anterior forma parte de un ejemplo más grande que se encuentra en [rellenar un conjunto de elementos a partir de un DataAdapter](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-207">(The code sample above is part of a larger sample found at [Populating a DataSet from a DataAdapter](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter).)</span></span>

> <span data-ttu-id="d2e1c-208">La mayoría de las aplicaciones pueden simplificar y suponer que su nivel de base de datos es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-208">Most apps can simplify and assume that their database layer is trusted.</span></span> <span data-ttu-id="d2e1c-209">Sin embargo, si es el hábito del [modelado de amenazas](https://www.microsoft.com/securityengineering/sdl/threatmodeling) de las aplicaciones, puede considerar que el modelo de amenazas es un límite de confianza entre la aplicación (cliente) y el nivel de base de datos (servidor).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-209">However, if you are in the habit of [threat modeling](https://www.microsoft.com/securityengineering/sdl/threatmodeling) your apps, your threat model may consider there to be a trust boundary between the application (client) and database layer (server).</span></span> <span data-ttu-id="d2e1c-210">El uso de la [autenticación mutua](/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections) o la [autenticación de AAD](/azure/azure-sql/database/authentication-aad-overview) entre el cliente y el servidor es una manera de ayudar a abordar los riesgos asociados a este.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-210">Using [mutual authentication](/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections) or [AAD authentication](/azure/azure-sql/database/authentication-aad-overview) between client and server is one way to help address the risks associated with this.</span></span> <span data-ttu-id="d2e1c-211">En el resto de esta sección se describe el posible resultado de que un cliente se conecte a un servidor que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-211">The remainder of this section discusses the possible result of a client connecting to an untrusted server.</span></span>

<span data-ttu-id="d2e1c-212">Las consecuencias de señalar un `DataAdapter` en un origen de datos que no es de confianza dependen de la implementación del `DataAdapter` propio.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-212">The consequences of pointing a `DataAdapter` at an untrusted data source depend on the implementation of the `DataAdapter` itself.</span></span>

### <a name="sqldataadapter"></a><span data-ttu-id="d2e1c-213">SqlDataAdapter</span><span class="sxs-lookup"><span data-stu-id="d2e1c-213">SqlDataAdapter</span></span>

<span data-ttu-id="d2e1c-214">En el caso del tipo integrado [SqlDataAdapter](/dotnet/api/microsoft.data.sqlclient.sqldataadapter), la referencia a un origen de datos que no es de confianza podría producir un ataque de denegación de servicio (dos).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-214">For the built-in type [SqlDataAdapter](/dotnet/api/microsoft.data.sqlclient.sqldataadapter), referencing an untrusted data source could result in a denial of service (DoS) attack.</span></span> <span data-ttu-id="d2e1c-215">El ataque de DoS puede dar lugar a que la aplicación deje de responder o se bloquee.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-215">The DoS attack could result in the app becoming unresponsive or crashing.</span></span> <span data-ttu-id="d2e1c-216">Si un atacante puede plantar un archivo DLL junto con la aplicación, es posible que también pueda lograr la ejecución de código local.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-216">If an attacker can plant a DLL alongside the app, they may also be able to achieve local code execution.</span></span>

### <a name="other-dataadapter-types"></a><span data-ttu-id="d2e1c-217">Otros tipos DataAdapter</span><span class="sxs-lookup"><span data-stu-id="d2e1c-217">Other DataAdapter types</span></span>

<span data-ttu-id="d2e1c-218">`DataAdapter`Las implementaciones de terceros deben realizar sus propias evaluaciones sobre qué garantías de seguridad proporcionan en caso de que se produzcan entradas que no son de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-218">Third-party `DataAdapter` implementations must make their own assessments about what security guarantees they provide in the face of untrusted inputs.</span></span> <span data-ttu-id="d2e1c-219">.NET no puede garantizar ninguna garantía de seguridad con respecto a estas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-219">.NET cannot make any safety guarantees regarding these implementations.</span></span>

<a name="dsrdtr"></a>

## <a name="datasetreadxml-and-datatablereadxml"></a><span data-ttu-id="d2e1c-220">DataSet. ReadXml y DataTable. ReadXml</span><span class="sxs-lookup"><span data-stu-id="d2e1c-220">DataSet.ReadXml and DataTable.ReadXml</span></span>

<span data-ttu-id="d2e1c-221">Los `DataSet.ReadXml` `DataTable.ReadXml` métodos y no son seguros cuando se usan con una entrada que no es de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-221">The `DataSet.ReadXml` and `DataTable.ReadXml` methods are not safe when used with untrusted input.</span></span> <span data-ttu-id="d2e1c-222">Se recomienda encarecidamente que los consumidores consideren el uso de una de las alternativas que se describen más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-222">We strongly recommend that consumers instead consider using one of the alternatives outlined later in this document.</span></span>

<span data-ttu-id="d2e1c-223">Las implementaciones de `DataSet.ReadXml` y `DataTable.ReadXml` se crearon originalmente antes de que las vulnerabilidades de serialización fueran una categoría de amenazas bien entendida.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-223">The implementations of `DataSet.ReadXml` and `DataTable.ReadXml` were originally created before serialization vulnerabilities were a well-understood threat category.</span></span> <span data-ttu-id="d2e1c-224">Como resultado, el código no sigue los procedimientos recomendados de seguridad actuales.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-224">As a result, the code does not follow current security best practices.</span></span> <span data-ttu-id="d2e1c-225">Estas API se pueden usar como vectores para que los atacantes realicen ataques de DoS en aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-225">These APIs can be used as vectors for attackers to perform DoS attacks against web apps.</span></span> <span data-ttu-id="d2e1c-226">Estos ataques pueden provocar que el servicio Web deje de responder o que se produzca una terminación inesperada del proceso.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-226">These attacks might render the web service unresponsive or result in unexpected process termination.</span></span> <span data-ttu-id="d2e1c-227">El marco de trabajo no proporciona mitigaciones para estas categorías de ataque y .NET considera este comportamiento "por diseño".</span><span class="sxs-lookup"><span data-stu-id="d2e1c-227">The framework does not provide mitigations for these attack categories and .NET considers this behavior "by design".</span></span>

<span data-ttu-id="d2e1c-228">.NET ha publicado actualizaciones de seguridad para mitigar algunos problemas, como la divulgación de información o la ejecución remota de código en `DataSet.ReadXml` y `DataTable.ReadXml` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-228">.NET has released security updates to mitigate some issues such as information disclosure or remote code execution in `DataSet.ReadXml` and `DataTable.ReadXml`.</span></span> <span data-ttu-id="d2e1c-229">Es posible que las actualizaciones de seguridad de .NET no proporcionen protección completa contra estas categorías de amenaza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-229">The .NET security updates may not provide complete protection against these threat categories.</span></span> <span data-ttu-id="d2e1c-230">Los consumidores deben evaluar sus escenarios individuales y considerar su posible exposición a estos riesgos.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-230">Consumers should assess their individual scenarios and consider their potential exposure to these risks.</span></span>

<span data-ttu-id="d2e1c-231">Los consumidores deben tener en cuenta que las actualizaciones de seguridad de estas API pueden afectar a la compatibilidad de aplicaciones en algunas situaciones.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-231">Consumers should be aware that security updates to these APIs may impact application compatibility in some situations.</span></span> <span data-ttu-id="d2e1c-232">Además, existe la posibilidad de que se detecte una vulnerabilidad novedosa en estas API para la que .NET no puede publicar prácticamente una actualización de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-232">Furthermore, the possibility exists that a novel vulnerability in these APIs will be discovered for which .NET can't practically publish a security update.</span></span>

<span data-ttu-id="d2e1c-233">Se recomienda que los consumidores de estas API:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-233">We recommend that consumers of these APIs either:</span></span>

* <span data-ttu-id="d2e1c-234">Considere la posibilidad de usar una de las alternativas que se describen más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-234">Consider using one of the alternatives outlined later in this document.</span></span>
* <span data-ttu-id="d2e1c-235">Realizar evaluaciones de riesgos individuales en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-235">Perform individual risk assessments on their apps.</span></span>

<span data-ttu-id="d2e1c-236">Es responsabilidad exclusiva del consumidor determinar si se deben utilizar estas API.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-236">It is the consumer's sole responsibility to determine whether to utilize these APIs.</span></span> <span data-ttu-id="d2e1c-237">Los consumidores deben evaluar los riesgos de seguridad, técnicos y legales, incluidos los requisitos normativos, que pueden acompañar al uso de estas API.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-237">Consumers should assess any security, technical, and legal risks, including regulatory requirements, that may accompany using these APIs.</span></span>

## <a name="dataset-and-datatable-via-aspnet-web-services-or-wcf"></a><span data-ttu-id="d2e1c-238">DataSet y DataTable a través de los servicios Web de ASP.NET o WCF</span><span class="sxs-lookup"><span data-stu-id="d2e1c-238">DataSet and DataTable via ASP.NET web services or WCF</span></span>

<span data-ttu-id="d2e1c-239">Es posible aceptar una `DataSet` `DataTable` instancia de o en un servicio Web ASP.net (SOAP), como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-239">It is possible to accept a `DataSet` or a `DataTable` instance in an ASP.NET (SOAP) web service, as demonstrated in the following code:</span></span>

```cs
using System.Data;
using System.Web.Services;

[WebService(Namespace = "http://contoso.com/")]
public class MyService : WebService
{
    [WebMethod]
    public string MyWebMethod(DataTable dataTable)
    {
        /* Web method implementation. */
    }
}
```

<span data-ttu-id="d2e1c-240">Una variación de esto no es aceptar `DataSet` o `DataTable` directamente como parámetro, sino que se puede aceptar como parte del gráfico de objetos serializado SOAP general, tal y como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-240">A variation on this is not to accept `DataSet` or `DataTable` directly as a parameter, but instead to accept it as part of the overall SOAP serialized object graph, as shown in the following code:</span></span>

```cs
using System.Data;
using System.Web.Services;

[WebService(Namespace = "http://contoso.com/")]
public class MyService : WebService
{
    [WebMethod]
    public string MyWebMethod(MyClass data)
    {
        /* Web method implementation. */
    }
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="d2e1c-241">O bien, mediante WCF en lugar de los servicios Web de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-241">Or, using WCF instead of ASP.NET web services:</span></span>

```cs
using System.Data;
using System.ServiceModel;

[ServiceContract(Namespace = "http://contoso.com/")]
public interface IMyContract
{
    [OperationContract]
    string MyMethod(DataTable dataTable);
    [OperationContract]
    string MyOtherMethod(MyClass data);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="d2e1c-242">En todos estos casos, el modelo de amenazas y las garantías de seguridad son los mismos que los de la [sección DataSet. ReadXml y DataTable. ReadXml](#dsrdtr).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-242">In all of these cases, the threat model and security guarantees are the same as the [DataSet.ReadXml and DataTable.ReadXml section](#dsrdtr).</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-xmlserializer"></a><span data-ttu-id="d2e1c-243">Deserialización de un conjunto de DataSet o DataTable a través de XmlSerializer</span><span class="sxs-lookup"><span data-stu-id="d2e1c-243">Deserialize a DataSet or DataTable via XmlSerializer</span></span>

<span data-ttu-id="d2e1c-244">Los desarrolladores pueden usar `XmlSerializer` para deserializar `DataSet` `DataTable` las instancias de y, tal y como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-244">Developers can use `XmlSerializer` to deserialize `DataSet` and `DataTable` instances, as shown in the following code:</span></span>

```cs
using System.Data;
using System.IO;
using System.Xml.Serialization;

public DataSet PerformDeserialization1(Stream stream) {
    XmlSerializer serializer = new XmlSerializer(typeof(DataSet));
    return (DataSet)serializer.Deserialize(stream);
}

public MyClass PerformDeserialization2(Stream stream) {
    XmlSerializer serializer = new XmlSerializer(typeof(MyClass));
    return (MyClass)serializer.Deserialize(stream);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="d2e1c-245">En estos casos, el modelo de amenazas y las garantías de seguridad son los mismos que los de la [sección DataSet. ReadXml y DataTable. ReadXml.](#dsrdtr)</span><span class="sxs-lookup"><span data-stu-id="d2e1c-245">In these cases, the threat model and security guarantees are the same as the [DataSet.ReadXml and DataTable.ReadXml section](#dsrdtr)</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-jsonconvert"></a><span data-ttu-id="d2e1c-246">Deserialización de un conjunto de DataSet o DataTable a través de JsonConvert</span><span class="sxs-lookup"><span data-stu-id="d2e1c-246">Deserialize a DataSet or DataTable via JsonConvert</span></span>

<span data-ttu-id="d2e1c-247">La popular biblioteca de Newtonsoft de terceros [JSON.net](https://www.newtonsoft.com/json) se puede usar para deserializar `DataSet` `DataTable` las instancias de y, tal y como se muestra en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-247">The popular third-party Newtonsoft library [JSON.NET](https://www.newtonsoft.com/json) can be used to deserialize `DataSet` and `DataTable` instances, as shown in the following code:</span></span>

```cs
using System.Data;
using Newtonsoft.Json;

public DataSet PerformDeserialization1(string json) {
    return JsonConvert.DeserializeObect<DataSet>(data);
}

public MyClass PerformDeserialization2(string json) {
    return JsonConvert.DeserializeObect<MyClass>(data);
}

public class MyClass
{
    // Property of type DataTable, automatically serialized and
    // deserialized as part of the overall MyClass payload.
    public DataTable MyDataTable { get; set; }
}
```

<span data-ttu-id="d2e1c-248">La deserialización de un `DataSet` `DataTable` objeto o de este modo desde un BLOB JSON que no es de confianza no es segura.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-248">Deserializing a `DataSet` or `DataTable` in this manner from an untrusted JSON blob is not safe.</span></span> <span data-ttu-id="d2e1c-249">Este patrón es vulnerable a ataques de denegación de servicio.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-249">This pattern is vulnerable to a denial of service attack.</span></span> <span data-ttu-id="d2e1c-250">Este tipo de ataque podría bloquear la aplicación o representar que no responde.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-250">Such an attack could crash the app or render it unresponsive.</span></span>

<span data-ttu-id="d2e1c-251">**Nota**: Microsoft no garantiza ni admite la implementación de bibliotecas de terceros como _Newtonsoft.Jsen_.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-251">**Note**: Microsoft does not warrant or support the implementation of third-party libraries like _Newtonsoft.Json_.</span></span> <span data-ttu-id="d2e1c-252">Esta información se proporciona para la integridad y es precisa en el momento de redactar este documento.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-252">This information is provided for completeness and is accurate as of the time of this writing.</span></span>

## <a name="deserialize-a-dataset-or-datatable-via-binaryformatter"></a><span data-ttu-id="d2e1c-253">Deserializar un conjunto de DataSet o DataTable a través de BinaryFormatter</span><span class="sxs-lookup"><span data-stu-id="d2e1c-253">Deserialize a DataSet or DataTable via BinaryFormatter</span></span>

<span data-ttu-id="d2e1c-254">Los desarrolladores nunca deben usar `BinaryFormatter` , `NetDataContractSerializer` , `SoapFormatter` o formateadores ***no seguros*** relacionados para deserializar una `DataSet` `DataTable` instancia de o de una carga que no sea de confianza:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-254">Developers must never use `BinaryFormatter`, `NetDataContractSerializer`, `SoapFormatter`, or related ***unsafe*** formatters to deserialize a `DataSet` or `DataTable` instance from an untrusted payload:</span></span>

* <span data-ttu-id="d2e1c-255">Esto es susceptible a un ataque de ejecución de código remoto completo.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-255">This is susceptible to a full remote code execution attack.</span></span>
* <span data-ttu-id="d2e1c-256">El uso de un personalizado `SerializationBinder` no es suficiente para evitar este tipo de ataque.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-256">Using a custom `SerializationBinder` is not sufficient to prevent such an attack.</span></span>

## <a name="safe-replacements"></a><span data-ttu-id="d2e1c-257">Reemplazos seguros</span><span class="sxs-lookup"><span data-stu-id="d2e1c-257">Safe replacements</span></span>

<span data-ttu-id="d2e1c-258">En el caso de las aplicaciones que:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-258">For apps that either:</span></span>

* <span data-ttu-id="d2e1c-259">Acepte `DataSet` o `DataTable` a través de un punto de conexión SOAP de. asmx o un extremo de WCF.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-259">Accept `DataSet` or `DataTable` through an .asmx SOAP endpoint or a WCF endpoint.</span></span>
* <span data-ttu-id="d2e1c-260">Deserializa los datos que no son de confianza en una instancia de `DataSet` o `DataTable` .</span><span class="sxs-lookup"><span data-stu-id="d2e1c-260">Deserialize untrusted data into an instance of `DataSet` or `DataTable`.</span></span>

<span data-ttu-id="d2e1c-261">Considere la posibilidad de reemplazar el modelo de objetos para utilizar [Entity Framework](/ef).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-261">Consider replacing the object model to use [Entity Framework](/ef).</span></span> <span data-ttu-id="d2e1c-262">Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="d2e1c-262">Entity Framework:</span></span>

* <span data-ttu-id="d2e1c-263">Es un marco de trabajo rico y moderno orientado a objetos que puede representar datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-263">Is a rich, modern, object-oriented framework that can represent relational data.</span></span>
* <span data-ttu-id="d2e1c-264">Aporta [un amplio ecosistema](/ef/core/providers/) de proveedores de bases de datos para facilitar la creación de proyectos de consultas de base de datos a través de los modelos de objetos de Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-264">Brings [a diverse ecosystem](/ef/core/providers/) of database providers to make it easy to project database queries via your Entity Framework object models.</span></span>
* <span data-ttu-id="d2e1c-265">Ofrece protecciones integradas al deserializar datos de orígenes que no son de confianza.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-265">Offers built-in protections when deserializing data from untrusted sources.</span></span>

<span data-ttu-id="d2e1c-266">En el caso de las aplicaciones que usan `.aspx` extremos SOAP, considere la posibilidad de cambiar esos puntos de conexión para usar [WCF](/dotnet/framework/wcf/).</span><span class="sxs-lookup"><span data-stu-id="d2e1c-266">For apps that use `.aspx` SOAP endpoints, consider changing those endpoints to use [WCF](/dotnet/framework/wcf/).</span></span> <span data-ttu-id="d2e1c-267">WCF es un sustituto más completo de `.asmx` servicios Web.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-267">WCF is a more fully featured replacement for `.asmx` web services.</span></span> <span data-ttu-id="d2e1c-268">Los extremos de WCF [se pueden exponer a través de SOAP](/dotnet/framework/wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients) para la compatibilidad con los autores de llamadas existentes.</span><span class="sxs-lookup"><span data-stu-id="d2e1c-268">WCF endpoints [can be exposed via SOAP](/dotnet/framework/wcf/feature-details/how-to-expose-a-contract-to-soap-and-web-clients) for compatibility with existing callers.</span></span>