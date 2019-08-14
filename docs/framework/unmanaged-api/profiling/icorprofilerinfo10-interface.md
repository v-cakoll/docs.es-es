---
title: Interfaz ICorProfilerInfo10
ms.date: 08/06/2019
author: davmason
ms.author: davmason
ms.openlocfilehash: 496959ecac5b16f1faa138aec90c5194d15cb105
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2019
ms.locfileid: "68974015"
---
# <a name="icorprofilerinfo10-interface"></a><span data-ttu-id="b1f16-102">Interfaz ICorProfilerInfo10</span><span class="sxs-lookup"><span data-stu-id="b1f16-102">ICorProfilerInfo10 Interface</span></span>

<span data-ttu-id="b1f16-103">Una subclase de [ICorProfilerInfo9](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-interface.md) que proporciona métodos para modificar el Il de la función, consultar información del tiempo de ejecución y suspender y reanudar el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="b1f16-103">A subclass of [ICorProfilerInfo9](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo9-interface.md) that provides methods to modify function IL, query information from the runtime, and suspend and resume the runtime.</span></span>

## <a name="methods"></a><span data-ttu-id="b1f16-104">Métodos</span><span class="sxs-lookup"><span data-stu-id="b1f16-104">Methods</span></span>  

| <span data-ttu-id="b1f16-105">Método</span><span class="sxs-lookup"><span data-stu-id="b1f16-105">Method</span></span>|<span data-ttu-id="b1f16-106">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="b1f16-106">Description</span></span>|  
| ------------|-----------------|  
|[<span data-ttu-id="b1f16-107">Método EnumerateObjectReferences</span><span class="sxs-lookup"><span data-stu-id="b1f16-107">EnumerateObjectReferences Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-enumerateobjectreferences-method.md)|<span data-ttu-id="b1f16-108">Dado un ObjectID, callback y clientData, enumera cada referencia de objeto (si existe).</span><span class="sxs-lookup"><span data-stu-id="b1f16-108">Given an ObjectID, callback and clientData, enumerates each object reference (if any).</span></span> |
|[<span data-ttu-id="b1f16-109">Método IsFrozenObject</span><span class="sxs-lookup"><span data-stu-id="b1f16-109">IsFrozenObject Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-isfrozenobject-method.md)|<span data-ttu-id="b1f16-110">Dado un ObjectID, determina si el objeto está en un segmento de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="b1f16-110">Given an ObjectID, determines whether the object is in a read-only segment.</span></span> |
|[<span data-ttu-id="b1f16-111">Método GetLOHObjectSizeThreshold</span><span class="sxs-lookup"><span data-stu-id="b1f16-111">GetLOHObjectSizeThreshold Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-getlohobjectsizethreshold-method.md)|<span data-ttu-id="b1f16-112">Obtiene el valor del umbral de montón configurado.</span><span class="sxs-lookup"><span data-stu-id="b1f16-112">Gets the value of the configured LOH threshold.</span></span> |
|[<span data-ttu-id="b1f16-113">Método RequestReJITWithInliners</span><span class="sxs-lookup"><span data-stu-id="b1f16-113">RequestReJITWithInliners Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-requestrejitwithinliners-method.md)| <span data-ttu-id="b1f16-114">ReJITs los métodos solicitados, así como los inlineers de los métodos solicitados.</span><span class="sxs-lookup"><span data-stu-id="b1f16-114">ReJITs the methods requested, as well as any inliners of the methods requested.</span></span>  |
|[<span data-ttu-id="b1f16-115">Método SuspendRuntime</span><span class="sxs-lookup"><span data-stu-id="b1f16-115">SuspendRuntime Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-suspendruntime-method.md)| <span data-ttu-id="b1f16-116">Suspende el tiempo de ejecución sin realizar un GC.</span><span class="sxs-lookup"><span data-stu-id="b1f16-116">Suspends the runtime without performing a GC.</span></span> |
|[<span data-ttu-id="b1f16-117">Método ResumeRuntime</span><span class="sxs-lookup"><span data-stu-id="b1f16-117">ResumeRuntime Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-resumeruntime-method.md)| <span data-ttu-id="b1f16-118">Reanuda el tiempo de ejecución sin realizar un GC.</span><span class="sxs-lookup"><span data-stu-id="b1f16-118">Resumes the runtime without performing a GC.</span></span> |

## <a name="requirements"></a><span data-ttu-id="b1f16-119">Requisitos</span><span class="sxs-lookup"><span data-stu-id="b1f16-119">Requirements</span></span>  
<span data-ttu-id="b1f16-120">**Select** Consulte [sistemas operativos compatibles con .net Core](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).</span><span class="sxs-lookup"><span data-stu-id="b1f16-120">**Platforms:** See [.NET Core supported operating systems](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).</span></span>  
<span data-ttu-id="b1f16-121">**Encabezado**: Corprof. idl, Corprof. h</span><span class="sxs-lookup"><span data-stu-id="b1f16-121">**Header:** CorProf.idl, CorProf.h</span></span>  
<span data-ttu-id="b1f16-122">**Versiones de .net:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b1f16-122">**.NET Versions:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]</span></span> 
## <a name="see-also"></a><span data-ttu-id="b1f16-123">Vea también</span><span class="sxs-lookup"><span data-stu-id="b1f16-123">See also</span></span>
- [<span data-ttu-id="b1f16-124">Interfaces para generación de perfiles</span><span class="sxs-lookup"><span data-stu-id="b1f16-124">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)