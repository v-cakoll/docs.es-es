---
title: Introducción a Azure Blob Storage mediante F#
description: Almacene datos no estructurados en la nube con Azure BLOB Storage.
author: sylvanc
ms.date: 09/20/2016
ms.openlocfilehash: 79f6a559ac603b0544916764126a988d3f3f43d7
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2020
ms.locfileid: "77092634"
---
# <a name="get-started-with-azure-blob-storage-using-f"></a>Introducción a Azure BLOB Storage mediante F\#

Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".

En este artículo se muestra cómo realizar tareas comunes con el almacenamiento de blobs. Los ejemplos se escriben F# mediante el uso de la biblioteca de cliente de Azure Storage para .net. Entre las tareas descritas se incluyen cómo cargar, enumerar, descargar y eliminar BLOBs.

Para obtener información general conceptual sobre el almacenamiento de blobs, consulte [la guía de .net para BLOB Storage](/azure/storage/blobs/storage-quickstart-blobs-dotnet).

## <a name="prerequisites"></a>Prerequisites

Para usar esta guía, primero debe [crear una cuenta de almacenamiento de Azure](/azure/storage/common/storage-account-create). También necesitará la clave de acceso de almacenamiento para esta cuenta.

## <a name="create-an-f-script-and-start-f-interactive"></a>Creación de F# un script e F# Inicio interactivo

Los ejemplos de este artículo se pueden usar en una F# aplicación o en un F# script. Para crear un F# script, cree un archivo con la extensión `.fsx`, por ejemplo `blobs.fsx`, en el F# entorno de desarrollo.

A continuación, use un [Administrador de paquetes](package-management.md) como [Paket](https://fsprojects.github.io/Paket/) o [NuGet](https://www.nuget.org/) para instalar los paquetes de `WindowsAzure.Storage` y `Microsoft.WindowsAzure.ConfigurationManager`, y haga referencia a `WindowsAzure.Storage.dll` y `Microsoft.WindowsAzure.Configuration.dll` en el script mediante una directiva de `#r`.

### <a name="add-namespace-declarations"></a>Incorporación de declaraciones de espacio de nombres

Agregue las siguientes instrucciones `open` en la parte superior del archivo `blobs.fsx`:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L1-L5)]

### <a name="get-your-connection-string"></a>Obtención de la cadena de conexión

Necesita una cadena de conexión Azure Storage para este tutorial. Para obtener más información sobre las cadenas de conexión, consulte Configuración de las [cadenas de conexión de almacenamiento](/azure/storage/storage-configure-connection-string).

En el tutorial, escriba la cadena de conexión en el script, como se indica a continuación:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L11-L11)]

Sin embargo, esto **no se recomienda** para los proyectos reales. La clave de la cuenta de almacenamiento es similar a la contraseña raíz de la cuenta de almacenamiento. Siempre debe proteger la clave de la cuenta de almacenamiento. Evite distribuirla a otros usuarios, codificarla de forma rígida o guardarla en un archivo de texto que sea accesible a otros usuarios. Puede volver a generar la clave mediante Azure portal si cree que puede estar en peligro.

En el caso de las aplicaciones reales, la mejor manera de mantener la cadena de conexión de almacenamiento se encuentra en un archivo de configuración. Para capturar la cadena de conexión de un archivo de configuración, puede hacer lo siguiente:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L13-L15)]

El uso del Administrador de configuración Azure es opcional. También puede usar una API, como el tipo de `ConfigurationManager` del .NET Framework.

### <a name="parse-the-connection-string"></a>Análisis de la cadena de conexión

Para analizar la cadena de conexión, use:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L21-L22)]

Esto devuelve un `CloudStorageAccount`.

### <a name="create-some-local-dummy-data"></a>Crear algunos datos ficticios locales

Antes de empezar, cree algunos datos locales ficticios en el directorio del script. Más adelante se cargan estos datos.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L28-L30)]

### <a name="create-the-blob-service-client"></a>Creación del cliente de Blob service

El tipo de `CloudBlobClient` permite recuperar contenedores y blobs almacenados en el almacenamiento de blobs. Esta es una forma de crear el cliente de servicio:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L36-L36)]

Ahora ya puede escribir código que lee y escribe datos en el Almacenamiento de blobs.

## <a name="create-a-container"></a>Crear un contenedor

En este ejemplo se muestra cómo crear un contenedor si todavía no existe:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L42-L46)]

De manera predeterminada, el nuevo contenedor es privado, lo que significa que debe especificar su clave de acceso de almacenamiento para descargar blobs de él. Si desea poner los archivos del contenedor a disposición de todo el mundo, puede convertir el contenedor en público utilizando el código siguiente:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L48-L49)]

Cualquier usuario de Internet puede ver los blobs de los contenedores públicos, pero solo es posible modificarlos o eliminarlos si se dispone de la clave de acceso apropiada o una firma de acceso compartido.

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor

Azure Blob Storage admite blobs en bloques y en páginas. En la mayoría de los casos, un BLOB en bloques es el tipo recomendado que se va a usar.

Para cargar un archivo en un blob en bloques, obtenga una referencia de contenedor y utilícela para obtener una referencia de blob en bloques. Una vez que tenga una referencia de BLOB, puede cargar cualquier secuencia de datos en ella llamando al método `UploadFromFile`. Esta operación crea el BLOB si no existía anteriormente, o lo sobrescribe si existe.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L55-L59)]

## <a name="list-the-blobs-in-a-container"></a>Enumerar los blobs de un contenedor

Para enumerar los blobs de un contenedor, primero obtenga una referencia de contenedor. Después, puede usar el método `ListBlobs` del contenedor para recuperar los blobs o directorios que contiene. Para tener acceso al conjunto completo de propiedades y métodos para un `IListBlobItem`devuelto, debe convertirlo en un objeto `CloudBlockBlob`, `CloudPageBlob`o `CloudBlobDirectory`. Si se desconoce el tipo, puede realizar una comprobación de tipo para determinar el formato al que se debe convertir. El código siguiente muestra cómo recuperar y consultar el URI de cada elemento del contenedor `mydata` :

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L67-L80)]

También puede asignar nombres a los blobs con la información de la ruta de acceso. De este modo crea una estructura de directorios virtuales que puede organizar y recorrer tal como lo haría en un sistema de archivos tradicional. Tenga en cuenta que la estructura de directorios es solo virtual: los únicos recursos disponibles en el almacenamiento de blobs son contenedores y blobs. Sin embargo, la biblioteca de cliente de almacenamiento ofrece un objeto `CloudBlobDirectory` para hacer referencia a un directorio virtual y simplificar el proceso de trabajar con blobs organizados de este modo.

Por ejemplo, observe el siguiente conjunto de blobs en bloques incluidos en un contenedor denominado `photos`:

\ *photo1. jpg*
*2015/Architecture/Description. txt*\
*2015/Architecture/photo3. jpg*\
*2015/Architecture/photo4. jpg*\
*2016/Architecture/photo5. jpg*\
*2016/Architecture/photo6. jpg*\
*2016/Architecture/Description. txt*\
\ *. jpg de 2016/photo7*

Cuando se llama a `ListBlobs` en un contenedor (como en el ejemplo anterior), se devuelve una lista jerárquica. Si contiene objetos `CloudBlobDirectory` y `CloudBlockBlob`, que representan los directorios y los blobs del contenedor, respectivamente, la salida resultante tiene un aspecto similar al siguiente:

```console
Directory: https://<accountname>.blob.core.windows.net/photos/2015/
Directory: https://<accountname>.blob.core.windows.net/photos/2016/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Opcionalmente, puede establecer el parámetro `UseFlatBlobListing` del método `ListBlobs` en `true`. En este caso, cada BLOB del contenedor se devuelve como un objeto `CloudBlockBlob`. La llamada a `ListBlobs` para devolver una lista plana tiene el siguiente aspecto:

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L82-L89)]

y, en función del contenido actual del contenedor, los resultados son similares a los siguientes:

```console
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2015/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2015/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2016/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2016/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2016/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Descargar blobs

Para descargar blobs, primero recupere una referencia de BLOB y, a continuación, llame al método `DownloadToStream`. En el ejemplo siguiente se usa el método `DownloadToStream` para transferir el contenido del BLOB a un objeto de secuencia que se puede guardar en un archivo local.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L95-L101)]

También puede utilizar el método `DownloadToStream` para descargar el contenido de un BLOB como una cadena de texto.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L103-L106)]

## <a name="delete-blobs"></a>Eliminar blobs

Para eliminar un BLOB, primero obtenga una referencia de BLOB y, a continuación, llame al método `Delete` en ella.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L112-L116)]

## <a name="list-blobs-in-pages-asynchronously"></a>Enumerar blobs en páginas de forma asincrónica

Si enumera un gran número de blobs o desea controlar el número de resultados que devuelve en una operación de listado, puede enumerar blobs en páginas de resultados. En este ejemplo se muestra cómo devolver resultados en páginas asincrónicamente de forma que la ejecución no se bloquee mientras se espera a devolver un conjunto grande de resultados.

En este ejemplo se muestra una lista plana de blobs, pero también puede realizar una lista jerárquica estableciendo el parámetro `useFlatBlobListing` del método `ListBlobsSegmentedAsync` en `false`.

En el ejemplo se define un método asincrónico mediante un bloque `async`. La palabra clave ``let!`` suspende la ejecución del método de ejemplo hasta que se completa la tarea de enumeración.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L122-L160)]

Ahora podemos usar esta rutina asincrónica como se indica a continuación. En primer lugar, cargue algunos datos ficticios (mediante el archivo local creado anteriormente en este tutorial).

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L162-L166)]

Ahora, llame a la rutina. Utilice `Async.RunSynchronously` para forzar la ejecución de la operación asincrónica.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L168-L168)]

## <a name="writing-to-an-append-blob"></a>Escritura en un blob en anexos

Un blob en anexos se optimiza para las operaciones de anexado, como el registro. Como un blob en bloques, un blob en anexos se compone también de bloques, pero en el caso del blob en anexos cuando se agrega un nuevo bloque, siempre se anexa al final del blob. No se puede actualizar o eliminar un bloque existente en un blob en anexos. Los identificadores de bloque para un blob en anexos no está expuestos como lo están en el caso de los blobs en bloques.

Cada bloque en un blob en anexos puede tener un tamaño diferente, hasta un máximo de 4 MB y el blob puede incluir un máximo de 50.000 bloques. El tamaño máximo de un blob en anexos es, por tanto, ligeramente superior a 195 GB (4 MB X 50.000 bloques).

En el ejemplo siguiente se crea un nuevo BLOB en anexos y se anexan algunos datos, simulando una operación de registro simple.

[!code-fsharp[BlobStorage](~/samples/snippets/fsharp/azure/blob-storage.fsx#L174-L203)]

Consulte [Descripción Blobs en bloques, en anexos y en páginas](https://msdn.microsoft.com/library/azure/ee691964.aspx) para obtener más información acerca de las diferencias entre los tres tipos de blobs.

## <a name="concurrent-access"></a>simultáneo

Para permitir el acceso simultáneo a un blob desde varios clientes o varias instancias de proceso, puede usar etiquetas **ETag** o **concesiones**.

- **Etag** : proporciona una manera de detectar que otro proceso ha modificado el blob o el contenedor

- **Concesión** : proporciona una manera de obtener acceso exclusivo y renovable de escritura o eliminación a un blob durante un período de tiempo

Para obtener más información, vea [administrar la simultaneidad en Microsoft Azure Storage](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/).

## <a name="naming-containers"></a>Nomenclatura de contenedores

Cada blob del almacenamiento de Azure debe residir en un contenedor. El contenedor forma parte del nombre del blob. Por ejemplo, `mydata` es el nombre del contenedor de estos URI de blob de ejemplo:

- `https://storagesample.blob.core.windows.net/mydata/blob1.txt`
- `https://storagesample.blob.core.windows.net/mydata/photos/myphoto.jpg`

Un nombre de contenedor debe ser un nombre DNS válido y cumplir las reglas de nomenclatura siguientes:

1. Los nombres de contenedor deben comenzar por una letra o un número, y pueden contener solo letras, números y el carácter de guión (-).
1. Todos los caracteres de guión (-) deben estar inmediatamente precedidos y seguidos por una letra o un número; no se permiten guiones consecutivos en nombres de contenedor.
1. Todas las letras del nombre de un contenedor deben aparecer en minúsculas.
1. Los nombres de contenedor deben tener entre 3 y 63 caracteres de longitud.

Tenga en cuenta que el nombre de un contenedor siempre debe estar en minúsculas. Si se incluye una letra mayúscula en un nombre de contenedor o se infringe de algún otro modo las reglas de nomenclatura de contenedores, recibirá un error 400 (solicitud incorrecta).

## <a name="managing-security-for-blobs"></a>Administración de la seguridad para blobs

De forma predeterminada, Azure Storage protege sus datos al limitar el acceso al propietario de la cuenta, quien está en posesión de las claves de acceso a ella. Cuando necesite compartir datos Blob en su cuenta de almacenamiento, es importante hacerlo sin poner en peligro la seguridad de las claves de acceso de la cuenta. Además, puede cifrar los datos Blob para cerciorarse de que es seguro pasar por la red y Azure Storage.

### <a name="controlling-access-to-blob-data"></a>Control del acceso a datos Blob

De forma predeterminada, los datos Blob de su cuenta de almacenamiento solo son accesibles para el propietario de la cuenta de almacenamiento. Para autenticar las solicitudes en el Almacenamiento de blobs, se necesita la clave de acceso de la cuenta de forma predeterminada. Sin embargo, es posible que desee poner determinados datos de BLOB a disposición de otros usuarios.

### <a name="encrypting-blob-data"></a>Cifrado de datos Blob

Azure Storage admite el cifrado de datos de BLOB tanto en el cliente como en el servidor.

## <a name="next-steps"></a>Pasos siguientes

Ahora que está familiarizado con los aspectos básicos del Almacenamiento de blobs, siga estos vínculos para obtener más información.

### <a name="tools"></a>Herramientas

- [ F#\ AzureStorageTypeProvider](https://fsprojects.github.io/AzureStorageTypeProvider/)
Un F# proveedor de tipo que se puede usar para explorar blobs, tablas y colas Azure Storage activos y aplicar fácilmente operaciones CRUD en ellos.

- [FSharp. Azure. Storage](https://github.com/fsprojects/FSharp.Azure.Storage)\
Una F# API para usar Microsoft Azure servicio Table Storage

- [Explorador de Microsoft Azure Storage (Mase)](/azure/vs-azure-tools-storage-manage-with-storage-explorer)\
Una aplicación independiente y gratuita de Microsoft que le permite trabajar visualmente con datos de Azure Storage en Windows, OS X y Linux.

### <a name="blob-storage-reference"></a>Referencia de Almacenamiento de blobs

- [API de Azure Storage para .NET](/dotnet/api/overview/azure/storage)
- [Referencia de la API REST de los servicios de Azure Storage](/rest/api/storageservices/)

### <a name="related-guides"></a>Guías relacionadas

- [Azure Blob Storage Samples for .NET](https://docs.microsoft.com/samples/azure-samples/storage-blob-dotnet-getting-started/storage-blob-dotnet-getting-started/) (Ejemplos de Azure Blob Storage para .NET)
- [Introducción a AzCopy](/azure/storage/common/storage-use-azcopy-v10)
- [Configuración de las cadenas de conexión de Azure Storage](/azure/storage/common/storage-configure-connection-string)
- [Blog del equipo de Azure Storage](https://docs.microsoft.com/archive/blogs/windowsazurestorage/)
- [Inicio rápido: uso de .NET para crear un BLOB en el almacenamiento de objetos](/azure/storage/blobs/storage-quickstart-blobs-dotnet)
