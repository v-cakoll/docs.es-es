---
title: Aplicaciones sin servidor Application Insights
description: Application Insights es una plataforma de diagnóstico sin servidor que permite a los desarrolladores detectar, evaluar y diagnosticar problemas en aplicaciones Web, aplicaciones móviles, aplicaciones de escritorio y microservicios.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 1f5b99fba448c2c1c12139524ffdcd3708b3c956
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577728"
---
# <a name="telemetry-with-application-insights"></a><span data-ttu-id="33f64-103">Telemetría con Application Insights</span><span class="sxs-lookup"><span data-stu-id="33f64-103">Telemetry with Application Insights</span></span>

<span data-ttu-id="33f64-104">[Application Insights](https://docs.microsoft.com/azure/application-insights) es una plataforma de diagnóstico sin servidor que permite a los desarrolladores detectar, evaluar y diagnosticar problemas en aplicaciones Web, aplicaciones móviles, aplicaciones de escritorio y microservicios.</span><span class="sxs-lookup"><span data-stu-id="33f64-104">[Application Insights](https://docs.microsoft.com/azure/application-insights) is a serverless diagnostics platform that enables developers to detect, triage, and diagnose issues in web apps, mobile apps, desktop apps, and microservices.</span></span> <span data-ttu-id="33f64-105">Puede activar Application Insights para las aplicaciones de función simplemente volteando un modificador en el portal.</span><span class="sxs-lookup"><span data-stu-id="33f64-105">You can turn on Application Insights for function apps simply by flipping a switch in the portal.</span></span> <span data-ttu-id="33f64-106">Application Insights proporciona todas estas funcionalidades sin tener que configurar un servidor o configurar su propia base de datos.</span><span class="sxs-lookup"><span data-stu-id="33f64-106">Application Insights provides all of these capabilities without you having to configure a server or set up your own database.</span></span> <span data-ttu-id="33f64-107">Todas las funcionalidades de Application Insights se proporcionan como un servicio que se integra automáticamente con sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="33f64-107">All of Application Insights' capabilities are provided as a service that automatically integrates with your apps.</span></span>

![Application Insights logotipo](./media/application-insights-logo.png)

<span data-ttu-id="33f64-109">Agregar Application Insights a las aplicaciones existentes es tan sencillo como agregar una clave de instrumentación a la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="33f64-109">Adding Application Insights to existing apps is as easy as adding an instrumentation key to your application's settings.</span></span> <span data-ttu-id="33f64-110">Con Application Insights puede:</span><span class="sxs-lookup"><span data-stu-id="33f64-110">With Application Insights you can:</span></span>

* <span data-ttu-id="33f64-111">Cree gráficos y alertas personalizados basados en métricas como el número de invocaciones de función, el tiempo necesario para ejecutar una función y excepciones.</span><span class="sxs-lookup"><span data-stu-id="33f64-111">Create custom charts and alerts based on metrics such as number of function invocations, the time it takes to run a function, and exceptions</span></span>
* <span data-ttu-id="33f64-112">Analizar errores y excepciones de servidor</span><span class="sxs-lookup"><span data-stu-id="33f64-112">Analyze failures and server exceptions</span></span>
* <span data-ttu-id="33f64-113">Profundice en el rendimiento por operación y mida el tiempo que se tarda en llamar a dependencias de terceros</span><span class="sxs-lookup"><span data-stu-id="33f64-113">Drill into performance by operation and measure the time it takes to call third-party dependencies</span></span>
* <span data-ttu-id="33f64-114">Supervisar el uso de CPU, la memoria y las tasas en todos los servidores que hospedan las aplicaciones de función</span><span class="sxs-lookup"><span data-stu-id="33f64-114">Monitor CPU usage, memory, and rates across all servers that host your function apps</span></span>
* <span data-ttu-id="33f64-115">Visualización de una secuencia en directo de métricas, incluido el recuento de solicitudes y la latencia de las aplicaciones de función</span><span class="sxs-lookup"><span data-stu-id="33f64-115">View a live stream of metrics including request count and latency for your function apps</span></span>
* <span data-ttu-id="33f64-116">Usar [análisis](https://docs.microsoft.com/azure/application-insights/app-insights-analytics) para buscar, consultar y crear gráficos personalizados sobre los datos de la función</span><span class="sxs-lookup"><span data-stu-id="33f64-116">Use [Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics) to search, query, and create custom charts over your function data</span></span>

![Explorador de métricas](./media/metrics-explorer.png)

<span data-ttu-id="33f64-118">Además de la telemetría integrada, también es posible generar telemetría personalizada.</span><span class="sxs-lookup"><span data-stu-id="33f64-118">In addition to built-in telemetry, it's also possible to generate custom telemetry.</span></span> <span data-ttu-id="33f64-119">En el fragmento de código siguiente se crea un cliente de telemetría personalizado mediante la clave de instrumentación establecida para la aplicación de función:</span><span class="sxs-lookup"><span data-stu-id="33f64-119">The following code snippet creates a custom telemetry client using the instrumentation key set for the function app:</span></span>

```csharp
public static TelemetryClient telemetry = new TelemetryClient()
{
    InstrumentationKey = Environment.GetEnvironmentVariable("APPINSIGHTS_INSTRUMENTATIONKEY")
};
```

<span data-ttu-id="33f64-120">El código siguiente mide cuánto tiempo se tarda en insertar una nueva fila en una instancia de [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) :</span><span class="sxs-lookup"><span data-stu-id="33f64-120">The following code measures how long it takes to insert a new row into an [Azure Table Storage](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview) instance:</span></span>

```csharp
var operation = TableOperation.Insert(entry);
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
await table.ExecuteAsync(operation);
telemetry.TrackDependency("AzureTableStorageInsert", "Insert", startTime, timer.Elapsed, true);
```

<span data-ttu-id="33f64-121">Se muestra el gráfico de rendimiento resultante:</span><span class="sxs-lookup"><span data-stu-id="33f64-121">The resulting performance graph is shown:</span></span>

![Telemetría personalizada](./media/custom-telemetry.png)

<span data-ttu-id="33f64-123">La telemetría personalizada revela que el tiempo promedio para insertar una nueva fila es de 32,6 milisegundos.</span><span class="sxs-lookup"><span data-stu-id="33f64-123">The custom telemetry reveals the average time to insert a new row is 32.6 milliseconds.</span></span>

<span data-ttu-id="33f64-124">Application Insights proporciona una manera eficaz y cómoda de registrar la telemetría detallada sobre las aplicaciones sin servidor.</span><span class="sxs-lookup"><span data-stu-id="33f64-124">Application Insights provides a powerful, convenient way to log detailed telemetry about your serverless applications.</span></span> <span data-ttu-id="33f64-125">Tiene control total sobre el nivel de seguimiento y registro que se proporciona.</span><span class="sxs-lookup"><span data-stu-id="33f64-125">You have full control over the level of tracing and logging that is provided.</span></span> <span data-ttu-id="33f64-126">Puede realizar un seguimiento de las estadísticas personalizadas, como los eventos, las dependencias y la vista de página.</span><span class="sxs-lookup"><span data-stu-id="33f64-126">You can track custom statistics such as events, dependencies, and page view.</span></span> <span data-ttu-id="33f64-127">Por último, el eficaz análisis le permite escribir consultas que formulan preguntas importantes y generan gráficos e información avanzada.</span><span class="sxs-lookup"><span data-stu-id="33f64-127">Finally, the powerful analytics enable you to write queries that ask important questions and generate charts and advanced insights.</span></span>

<span data-ttu-id="33f64-128">Para obtener más información, vea [Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring).</span><span class="sxs-lookup"><span data-stu-id="33f64-128">For more information, see [Monitor Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="33f64-129">[Anterior](azure-functions.md)
>[Siguiente](logic-apps.md)</span><span class="sxs-lookup"><span data-stu-id="33f64-129">[Previous](azure-functions.md)
[Next](logic-apps.md)</span></span>