---
title: Introducción a Azure y .NET
description: Obtenga información sobre los conceptos básicos que necesita saber acerca de Azure y .NET.
ms.date: 06/20/2020
ms.openlocfilehash: c64de800f47035b22cc62b6d08cb7b71246984a7
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174327"
---
# <a name="introduction-to-azure-and-net"></a>Introducción a Azure y .NET

Este documento proporciona información general sobre los conceptos clave y los servicios de .NET con los que los desarrolladores deben estar familiarizados para comenzar a desarrollar aplicaciones con los servicios de Azure.

## <a name="key-concepts"></a>Conceptos clave

**Cuenta de Azure**: la cuenta de Azure es la credencial que usa para iniciar sesión en los servicios de Azure, como [Azure Portal](https://portal.azure.com) o [Cloud Shell](https://shell.azure.com). Si no tiene una cuenta de Azure, puede [crear una gratis](https://azure.microsoft.com/free/dotnet/).

**Suscripción de Azure**: una suscripción es el plan de facturación en el que se crean los recursos de Azure. Las suscripciones pueden ser suscripciones individuales o suscripciones empresariales administradas por su empresa. La cuenta de Azure puede asociarse a varias suscripciones. En este caso, asegúrese de seleccionar la suscripción correcta al crear recursos. Para más información, consulte [Descripción de las cuentas, suscripciones y facturación](/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing).

> [!TIP]
> Si tiene una suscripción de Visual Studio, [tiene créditos mensuales de Azure a la espera de ser activados](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/).

**Grupo de recursos**: los grupos de recursos son una manera de organizar los recursos de Azure en grupos para su administración. Los recursos creados en Azure se almacenarán en un grupo de recursos, algo similar a guardar un archivo en una carpeta en un equipo.

**Hospedaje**: para ejecutar código en Azure, debe estar hospedado en un servicio que admita la ejecución de código proporcionado por el usuario.

**Servicios administrados**: Azure proporciona algunos servicios en los que se proporciona información o datos a Azure y la implementación de Azure toma las acciones oportunas. Un ejemplo es Azure Blob Storage, donde se proporcionan los archivos y Azure se encarga de leerlos, escribirlos y almacenarlos.

**Azure SDK para .NET**: A veces conocido como **bibliotecas de Azure para .NET**, esto hace referencia colectivamente a los [paquetes NuGet](https://www.nuget.org/profiles/azure-sdk) que instala en el proyecto que proporcionan varias interacciones y funcionalidad con los servicios de Azure. En estos paquetes también se incluyen las bibliotecas de administración que se usan para aprovisionar y administrar los recursos.

## <a name="choosing-a-hosting-option"></a>Elección de una opción de hospedaje

El hospedaje en Azure se puede dividir en tres categorías.

* **Infraestructura como servicio (IaaS)** : Con IaaS puede aprovisionar las máquinas virtuales que necesite, junto con la red y los componentes de almacenamiento asociados. A continuación, el usuario implementa el software y las aplicaciones que desee en esas máquinas virtuales. Este modelo es lo más parecido a un entorno local tradicional, salvo que Microsoft administra la infraestructura. El usuario administra las máquinas virtuales individuales, incluidos el sistema operativo, el software personalizado y las actualizaciones de seguridad.

* **Plataforma como servicio (PaaS)** : PaaS proporciona un entorno de hospedaje administrado en el que se implementa la aplicación sin necesidad de administrar las máquinas virtuales o los recursos de red. Por ejemplo, en lugar de crear máquinas virtuales individuales, se crea un recuento de instancias y el servicio aprovisiona, configura y administra los recursos necesarios. Azure App Service es un ejemplo de un servicio de PaaS.
  
* **Funciones como servicio (FaaS)** : conocidas comúnmente como informática sin servidor, FaaS va más allá de PaaS al abstraer las preocupaciones del entorno de hospedaje. En lugar de crear instancias de proceso y después implementar el código en esas instancias, se implementa el código y el servicio lo ejecuta automáticamente. No es necesario administrar los recursos de proceso. La plataforma escala sin problemas el código hasta el nivel necesario para controlar el tráfico y se paga solo cuando se ejecuta el código. Azure Functions es un servicio de FaaS.

Por lo general, cuanto más favorece la aplicación los modelos FaaS y PaaS, más ventajas obtendrá de la ejecución en la nube. A continuación se muestra un resumen de las tres opciones de hospedaje más comunes en Azure y cuándo optar por ellas.

* [Azure App Service](/azure/app-service/app-service-value-prop-what-is): si desea hospedar un servicio o una aplicación web, examine App Service en primer lugar. Para empezar a trabajar con App Service y aplicaciones de ASP.NET, WCF y ASP.NET Core, consulte [Creación de una aplicación web de ASP.NET Core en Azure](/azure/app-service/app-service-web-get-started-dotnet).

* [Azure Functions](/azure/azure-functions/functions-overview): Azure Functions es muy útil para los flujos de trabajo controlados por eventos. Algunos ejemplos son la respuesta a webhooks, el procesamiento de elementos de colas, el almacenamiento de blobs y los temporizadores. Para empezar a trabajar con Azure Functions, consulte [Creación de la primera función mediante Visual Studio](/azure/azure-functions/functions-create-your-first-function-visual-studio).

* [Azure Virtual Machines](/azure/virtual-machines/): si App Service no satisface sus necesidades para hospedar una aplicación existente debido a dependencias específicas, las máquinas virtuales serán el lugar más fácil para empezar. Para empezar a trabajar con Virtual Machines y ASP.NET o WCF, consulte [Implementación de una aplicación ASP.NET en una máquina virtual de Azure](https://tutorials.visualstudio.com/aspnet-vm/intro).

> [!TIP]
> Para más información acerca de cómo elegir un servicio, vea [Elección de un servicio de proceso de Azure para la aplicación](/azure/architecture/guide/technology-choices/compute-decision-tree).

## <a name="choose-a-data-storage-service"></a>Elección de un servicio de almacenamiento de datos

Azure ofrece varios servicios para almacenar los datos según sus necesidades. Los servicios de datos más comunes para los desarrolladores de .NET son:

* [Azure SQL Database](/azure/sql-database/): si desea migrar una aplicación que ya utiliza SQL Server a la nube, Azure SQL Database es un lugar lógico para comenzar. Para empezar, consulte [Tutorial: Compilación de una aplicación ASP.NET en Azure con SQL Database](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase).

* [Azure Cosmos DB](/azure/cosmos-db/): Azure Cosmos DB es una base de datos moderna diseñada para la nube. Cuando se inicia una aplicación nueva que todavía no tiene una dependencia de una base de datos específica, puede evaluar Azure Cosmos DB. Cosmos DB es una buena elección para las nuevas aplicaciones web, móviles, de juegos y de IoT donde la escala automática, el rendimiento predecible, los tiempos de respuesta rápidos y la capacidad de consultar datos sin esquema son importantes. Para comenzar, consulte [Inicio rápido: Compilación de una aplicación web para .NET con Azure Cosmos DB y SQL API en Azure Portal](/azure/cosmos-db/create-sql-api-dotnet).

* [Azure Blob Storage](/azure/storage/): Azure Blob Storage está optimizado para almacenar y recuperar objetos binarios grandes, como imágenes, archivos y secuencias. Los almacenes de objetos permiten la administración de cantidades enormes de datos no estructurados. Para comenzar, consulte [Inicio rápido: Use .NET para crear un blob en el almacenamiento de objetos](/azure/storage/blobs/storage-quickstart-blobs-dotnet).

> [!TIP]
> Para más información, consulte [Elección del almacén de datos apropiado](/azure/architecture/guide/technology-choices/data-store-overview).

## <a name="connect-to-azure-services"></a>Conexión a los servicios de Azure

Si usa Visual Studio, puede agregar compatibilidad con algunos servicios de Azure a sus proyectos. El cuadro de diálogo **Connected Services** de Visual Studio proporciona una manera fácil de agregar todas las referencias necesarias, el código de conexión y las opciones de configuración a los proyectos. Algunos servicios de Azure usados con frecuencia están listos para su uso, como [Storage](/azure/vs-azure-tools-connected-services-storage), la autenticación de [Azure Active Directory](/azure/active-directory/develop/vs-active-directory-add-connected-service), [Azure Key Vault](/azure/key-vault/vs-key-vault-add-connected-service) y servicios de [Cognitive Services](/azure/cognitive-services/) como [Computer Vision](/azure/cognitive-services/computer-vision/vs-computer-vision-connected-service). Más servicios, incluidos servicios de terceros, están disponibles como extensiones en [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?term=connected%20service&target=VS&category=Tools&vsVersion=&subCategory=All&sortBy=Relevance).

## <a name="using-the-azure-sdk-for-net"></a>Uso del SDK de Azure para .NET

Si usa el SDK de Azure para .NET para acceder a los recursos de Azure o administrarlos, tenga en cuenta lo siguiente:

* **Autenticación**: Muchas bibliotecas del SDK usan una infraestructura de autenticación común, mientras que algunas bibliotecas usan mecanismos de autenticación específicos del servicio que están consumiendo. Para obtener más información, consulte el documento [Autenticación con el SDK de Azure para .NET](authentication.md).
* **Registro**: Si se admite, en las bibliotecas cliente se incluye la posibilidad de registrar operaciones de las bibliotecas cliente. Para obtener más información, consulte [Registro con el SDK de Azure para .NET](logging.md).
* **API REST**: El SDK de Azure para .NET es una abstracción construida sobre la [API de REST de Azure](/rest/api/azure/). Si lo desea, puede usar la API de REST de Azure en lugar de o junto con el SDK de Azure para .NET.

## <a name="diagnosing-problems-in-the-cloud"></a>Diagnóstico de problemas en la nube
Una vez que se implementa la aplicación en Azure, es posible encontrar casos en los que funciona en desarrollo, pero no en Azure. A continuación se muestran dos buenos lugares para empezar cuando se diagnostican problemas:

* **Depuración remota en Visual Studio**: la mayoría de los servicios de proceso de Azure (incluidos los servicios que se describen en este documento) admiten la depuración remota con Visual Studio y la adquisición de registros. Para explorar las funcionalidades de Visual Studio con la aplicación, abra la ventana de herramientas de Cloud Explorer escribiendo "Cloud Explorer" en la barra de herramientas de inicio rápido de Visual Studio (en la esquina superior derecha) y, a continuación, busque la aplicación en el árbol. Para más información, consulte [Solución de problemas de una aplicación web en Azure App Service con Visual Studio](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug).

* **Application Insights**: [Application Insights](/azure/application-insights/) es una solución de supervisión de rendimiento de aplicaciones (APM) completa que captura datos de diagnóstico, datos de telemetría y datos de rendimiento de las aplicaciones automáticamente. Para empezar a recopilar datos de diagnóstico de la aplicación, consulte [Inicio de la supervisión de la aplicación web ASP.NET](/azure/application-insights/quick-monitor-portal).

## <a name="next-steps"></a>Pasos siguientes

* [Creación de una aplicación web ASP.NET Core en Azure](/azure/app-service/app-service-web-get-started-dotnet)
* [Obtenga información sobre la autenticación en el SDK de Azure para .NET](authentication.md)
* [Diagnóstico de errores en las aplicaciones en la nube](https://devblogs.microsoft.com/aspnet/diagnosing-errors-on-your-cloud-apps/)
* Descargue el libro electrónico gratuito [Guía de inicio rápido de Azure para desarrolladores de .NET](https://www.microsoft.com/net/download/thank-you/azure-quick-start-ebook).
