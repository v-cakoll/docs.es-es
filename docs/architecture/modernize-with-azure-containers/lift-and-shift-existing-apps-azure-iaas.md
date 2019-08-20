---
title: Elevación y desplazamiento de las aplicaciones .NET existentes a IaaS de Azure (lista para la infraestructura de la nube)
description: Modernice las aplicaciones .NET existentes con los contenedores de Windows y la nube de Azure.
ms.date: 04/28/2018
ms.openlocfilehash: cda316ad01a58f26661395c804547de04e20d052
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "69578398"
---
# <a name="lift-and-shift-existing-net-apps-to-azure-iaas-cloud-infrastructure-ready"></a><span data-ttu-id="3a23d-103">Elevación y desplazamiento de las aplicaciones .NET existentes a IaaS de Azure (lista para la infraestructura de la nube)</span><span class="sxs-lookup"><span data-stu-id="3a23d-103">Lift and shift existing .NET apps to Azure IaaS (Cloud Infrastructure-Ready)</span></span>

> <span data-ttu-id="3a23d-104">Visión: Como primer paso, para reducir la inversión local y el costo total del mantenimiento del hardware y de la red, solo tiene que volver a hospedar las aplicaciones existentes en la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-104">Vision: As a first step, to reduce your on-premises investment and total cost of hardware and networking maintenance, simply rehost your existing applications in the cloud.</span></span>

<span data-ttu-id="3a23d-105">Antes de empezar a migrar las aplicaciones existentes a la plataforma de infraestructura como servicio (IaaS) de Azure, es importante analizar las razones *por* las que desea migrar directamente a IaaS en Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-105">Before getting into *how* to migrate your existing applications to the Azure infrastructure as a service (IaaS) platform, it's important to analyze the reasons *why* you'd want to migrate directly to IaaS in Azure.</span></span> <span data-ttu-id="3a23d-106">El escenario de este nivel de madurez de modernización básicamente es empezar a usar las máquinas virtuales en la nube, en lugar de seguir usando la infraestructura local actual.</span><span class="sxs-lookup"><span data-stu-id="3a23d-106">The scenario at this modernization maturity level essentially is to start using VMs in the cloud, instead of continuing to use your current, on-premises infrastructure.</span></span>

<span data-ttu-id="3a23d-107">Otro punto para analizar es el *motivo por* el que podría querer migrar a la nube de IaaS pura en lugar de agregar simplemente servicios administrados más avanzados en Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-107">Another point to analyze is *why* you might want to migrate to pure IaaS cloud instead of just adding more advanced managed services in Azure.</span></span> <span data-ttu-id="3a23d-108">Determine qué casos pueden requerir IaaS en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="3a23d-108">Determine what cases might require IaaS in the first place.</span></span>

<span data-ttu-id="3a23d-109">La figura 2-1 coloca las aplicaciones preparadas para la infraestructura de nube en los niveles de madurez de modernización:</span><span class="sxs-lookup"><span data-stu-id="3a23d-109">Figure 2-1 positions Cloud Infrastructure-Ready applications in the modernization maturity levels:</span></span>

![Posicionamiento de aplicaciones listas para la infraestructura de nube](./media/image2-1.png)

> <span data-ttu-id="3a23d-111">**Figura 2-1.**</span><span class="sxs-lookup"><span data-stu-id="3a23d-111">**Figure 2-1.**</span></span> <span data-ttu-id="3a23d-112">Posicionamiento de aplicaciones listas para la infraestructura de nube</span><span class="sxs-lookup"><span data-stu-id="3a23d-112">Positioning Cloud Infrastructure-Ready applications</span></span>

## <a name="why-migrate-existing-net-web-applications-to-azure-iaas"></a><span data-ttu-id="3a23d-113">Por qué migrar aplicaciones Web .NET existentes a IaaS de Azure</span><span class="sxs-lookup"><span data-stu-id="3a23d-113">Why migrate existing .NET web applications to Azure IaaS</span></span>

<span data-ttu-id="3a23d-114">La razón principal para migrar a la nube, incluso en el nivel inicial de IaaS, es lograr reducciones de costos.</span><span class="sxs-lookup"><span data-stu-id="3a23d-114">The main reason to migrate to the cloud, even at an initial IaaS level, is to achieve cost reductions.</span></span> <span data-ttu-id="3a23d-115">Mediante el uso de servicios de infraestructura más administrados, su organización puede reducir su inversión en el mantenimiento de hardware, el aprovisionamiento e implementación de servidores o máquinas virtuales y la administración de la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="3a23d-115">By using more managed infrastructure services, your organization can lower its investment in hardware maintenance, server or VM provisioning and deployment, and infrastructure management.</span></span>

<span data-ttu-id="3a23d-116">Después de tomar la decisión de trasladar sus aplicaciones a la nube, el motivo principal por el que podría elegir IaaS en lugar de opciones más avanzadas, como PaaS, es simplemente que el entorno de IaaS le resulte más familiar.</span><span class="sxs-lookup"><span data-stu-id="3a23d-116">After you make the decision to move your apps to the cloud, the main reason why you might choose IaaS instead of more advanced options like PaaS is simply that the IaaS environment will be more familiar.</span></span> <span data-ttu-id="3a23d-117">El cambio a un entorno similar al entorno local actual ofrece una curva de aprendizaje más baja, lo que lo convierte en la ruta más rápida a la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-117">Moving to an environment that's similar to your current, on-premises environment offers a lower learning curve, which makes it the quickest path to the cloud.</span></span>

<span data-ttu-id="3a23d-118">Sin embargo, si se toma la ruta de acceso más rápida a la nube no significa que se saque el máximo partido de hacer que las aplicaciones se ejecuten en la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-118">However, taking the quickest path to the cloud doesn't mean that you will gain the most benefit from having your applications running in the cloud.</span></span> <span data-ttu-id="3a23d-119">Cualquier organización obtendrá las ventajas más importantes de una migración en la nube en los niveles de madurez de la nube y los que ya se han optimizado para la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-119">Any organization will gain the most significant benefits from a cloud migration at the already introduced Cloud-Optimized and Cloud-Native maturity levels.</span></span>

<span data-ttu-id="3a23d-120">También ha resultado evidente que las aplicaciones son más fáciles de modernizar y rediseñar en el futuro cuando ya se están ejecutando en la nube, incluso en IaaS.</span><span class="sxs-lookup"><span data-stu-id="3a23d-120">It also has become evident that applications are easier to modernize and rearchitect in the future when they are already running in the cloud, even on IaaS.</span></span> <span data-ttu-id="3a23d-121">Ya se ha logrado la migración de datos de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a23d-121">Application data migration has already been achieved.</span></span> <span data-ttu-id="3a23d-122">Además, su organización habrá obtenido los conocimientos necesarios para trabajar en la nube y realizar el cambio de funcionamiento en una "referencia cultural de la nube".</span><span class="sxs-lookup"><span data-stu-id="3a23d-122">Also, your organization will have gained skills required for working in the cloud and made the shift to operating in a "cloud culture."</span></span>

## <a name="when-to-migrate-to-iaas-instead-of-to-paas"></a><span data-ttu-id="3a23d-123">Cuándo migrar a IaaS en lugar de a PaaS</span><span class="sxs-lookup"><span data-stu-id="3a23d-123">When to migrate to IaaS instead of to PaaS</span></span>

<span data-ttu-id="3a23d-124">En las secciones siguientes se describen las aplicaciones optimizadas para la nube que se basan principalmente en plataformas y servicios PaaS.</span><span class="sxs-lookup"><span data-stu-id="3a23d-124">The next sections discuss Cloud-Optimized applications that are mostly based on PaaS platforms and services.</span></span> <span data-ttu-id="3a23d-125">Estas aplicaciones ofrecen el máximo beneficio de la migración a la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-125">These apps give you the most benefits from migrating to the cloud.</span></span> 

<span data-ttu-id="3a23d-126">Si su objetivo es simplemente trasladar las aplicaciones existentes a la nube, identifique primero las aplicaciones existentes que no requieren la modificación sustancial para que se ejecuten en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3a23d-126">If your goal is simply to move existing applications to the cloud, first, identify existing applications that would not require substantial modification to run in Azure App Service.</span></span> <span data-ttu-id="3a23d-127">Estas aplicaciones deben ser las primeras candidatas para la optimización para la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-127">These apps should be the first candidates for Cloud-Optimized.</span></span> 

<span data-ttu-id="3a23d-128">A continuación, en el caso de las aplicaciones que todavía no se pueden trasladar a contenedores de Windows y PaaS, como App Service o orquestadores como Azure Kubernetes Service, migre los a las máquinas virtuales sencillas simples (IaaS).</span><span class="sxs-lookup"><span data-stu-id="3a23d-128">Then, for the apps that still cannot move to Windows Containers and PaaS such as App Service or orchestrators like Azure Kubernetes Service, migrate those to simple plain VMs (IaaS).</span></span> 

<span data-ttu-id="3a23d-129">Sin embargo, tenga en cuenta que la configuración, la protección y el mantenimiento correctos de las máquinas virtuales requiere mucho más tiempo y experiencia de TI en comparación con el uso de servicios de PaaS en Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-129">But, keep in mind that correctly configuring, securing, and maintaining VMs requires much more time and IT expertise compared to using PaaS services in Azure.</span></span> <span data-ttu-id="3a23d-130">Si está pensando en Azure Virtual Machines, asegúrese de tener en cuenta el esfuerzo de mantenimiento continuo necesario para aplicar revisiones, actualizar y administrar su entorno de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3a23d-130">If you are considering Azure Virtual Machines, make sure that you take into account the ongoing maintenance effort required to patch, update, and manage your VM environment.</span></span> <span data-ttu-id="3a23d-131">Azure Virtual Machines es IaaS.</span><span class="sxs-lookup"><span data-stu-id="3a23d-131">Azure Virtual Machines is IaaS.</span></span>

## <a name="use-azure-migrate-to-analyze-and-migrate-your-existing-applications-to-azure"></a><span data-ttu-id="3a23d-132">Usar Azure Migrate para analizar y migrar las aplicaciones existentes a Azure</span><span class="sxs-lookup"><span data-stu-id="3a23d-132">Use Azure Migrate to analyze and migrate your existing applications to Azure</span></span>

<span data-ttu-id="3a23d-133">No es necesario migrar a la nube.</span><span class="sxs-lookup"><span data-stu-id="3a23d-133">Migrating to the cloud doesn't have to be difficult.</span></span> <span data-ttu-id="3a23d-134">Pero muchas organizaciones luchan por empezar a obtener visibilidad profunda en el entorno y las estrechas interdependencias entre las aplicaciones, las cargas de trabajo y los datos.</span><span class="sxs-lookup"><span data-stu-id="3a23d-134">But many organizations struggle to get started - to get deep visibility into the environment and the tight interdependencies between applications, workloads, and data.</span></span> <span data-ttu-id="3a23d-135">Sin esa visibilidad, puede ser difícil planear la ruta de acceso hacia delante.</span><span class="sxs-lookup"><span data-stu-id="3a23d-135">Without that visibility, it can be difficult to plan the path forward.</span></span> <span data-ttu-id="3a23d-136">Sin información detallada sobre lo que se necesita para una migración correcta, no puede tener las conversaciones correctas dentro de la organización.</span><span class="sxs-lookup"><span data-stu-id="3a23d-136">Without detailed information on what's required for a successful migration, you can't have the right conversations within your organization.</span></span> <span data-ttu-id="3a23d-137">No sabe lo suficiente sobre las ventajas potenciales de los costos o si las cargas de trabajo solo podrían levantarse y cambiarse o requeriría un retrabajo significativo para migrar correctamente.</span><span class="sxs-lookup"><span data-stu-id="3a23d-137">You don't know enough about the potential cost benefits, or whether workloads could just lift-and-shift or would require significant rework to migrate successfully.</span></span> <span data-ttu-id="3a23d-138">No dude en muchas organizaciones.</span><span class="sxs-lookup"><span data-stu-id="3a23d-138">No wonder many organizations hesitate.</span></span>

<span data-ttu-id="3a23d-139">[Azure Migrate](https://aka.ms/azuremigrate) es un nuevo servicio que proporciona instrucciones, información y mecanismos necesarios para ayudarle a migrar a Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-139">[Azure Migrate](https://aka.ms/azuremigrate) is a new service that provides the guidance, insights, and mechanisms needed to assist you in migrating to Azure.</span></span> <span data-ttu-id="3a23d-140">Azure Migrate proporciona:</span><span class="sxs-lookup"><span data-stu-id="3a23d-140">Azure Migrate provides:</span></span>

- <span data-ttu-id="3a23d-141">Detección y evaluación de máquinas virtuales locales</span><span class="sxs-lookup"><span data-stu-id="3a23d-141">Discovery and assessment for on-premises virtual machines</span></span>

- <span data-ttu-id="3a23d-142">Asignación de dependencias integrada para la detección de alta confianza de aplicaciones de niveles múltiples</span><span class="sxs-lookup"><span data-stu-id="3a23d-142">Inbuilt dependency mapping for high-confidence discovery of multi-tier applications</span></span>

- <span data-ttu-id="3a23d-143">Ajuste del tamaño de forma inteligente a Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="3a23d-143">Intelligent right sizing to Azure virtual machines</span></span>

- <span data-ttu-id="3a23d-144">Informes de compatibilidad con directrices para corregir posibles problemas</span><span class="sxs-lookup"><span data-stu-id="3a23d-144">Compatibility reporting with guidelines for remediating potential issues</span></span>

- <span data-ttu-id="3a23d-145">Integración con el servicio Azure Database Management para la detección y migración de bases de datos</span><span class="sxs-lookup"><span data-stu-id="3a23d-145">Integration with Azure Database Management Service for database discovery and migration</span></span>

<span data-ttu-id="3a23d-146">Azure Migrate le da la seguridad de que las cargas de trabajo se pueden migrar con un impacto mínimo en el negocio y ejecutarse según lo previsto en Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-146">Azure Migrate gives you confidence that your workloads can migrate with minimal impact to the business and run as expected in Azure.</span></span> <span data-ttu-id="3a23d-147">Con las herramientas y las instrucciones adecuadas, puede lograr el máximo rendimiento de la inversión a la vez que garantiza que se cumplan las necesidades críticas de rendimiento y confiabilidad.</span><span class="sxs-lookup"><span data-stu-id="3a23d-147">With the right tools and guidance, you can achieve maximum return on investment while assuring that critical performance and reliability needs are met.</span></span>

<span data-ttu-id="3a23d-148">En la figura 2-2 se muestra la asignación de dependencias integrada para todas las conexiones de servidor y aplicación realizadas por Azure Migrate.</span><span class="sxs-lookup"><span data-stu-id="3a23d-148">Figure 2-2 shows you the built-in dependency mapping for all server and application connections performed by Azure Migrate.</span></span>

![Posicionamiento de aplicaciones listas para la infraestructura de nube](./media/image2-2.png)

> <span data-ttu-id="3a23d-150">**Figura 2-2.**</span><span class="sxs-lookup"><span data-stu-id="3a23d-150">**Figure 2-2.**</span></span> <span data-ttu-id="3a23d-151">Posicionamiento de aplicaciones listas para la infraestructura de nube</span><span class="sxs-lookup"><span data-stu-id="3a23d-151">Positioning Cloud Infrastructure-Ready applications</span></span>

## <a name="use-azure-site-recovery-to-migrate-your-existing-vms-to-azure-vms"></a><span data-ttu-id="3a23d-152">Uso de Azure Site Recovery para migrar las máquinas virtuales existentes a máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="3a23d-152">Use Azure Site Recovery to migrate your existing VMs to Azure VMs</span></span>

<span data-ttu-id="3a23d-153">Como parte de la [Azure Migrate](https://aka.ms/azuremigrate)de un extremo a otro, [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) es una herramienta que puede usar para migrar fácilmente las aplicaciones web a las máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-153">As part of the end-to-end [Azure Migrate](https://aka.ms/azuremigrate), [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) is a tool that you can use to easily migrate your web apps to VMs in Azure.</span></span> <span data-ttu-id="3a23d-154">Puede usar Site Recovery para replicar máquinas virtuales locales y servidores físicos en Azure, o para replicarlos en una ubicación local secundaria.</span><span class="sxs-lookup"><span data-stu-id="3a23d-154">You can use Site Recovery to replicate on-premises VMs and physical servers to Azure, or to replicate them to a secondary on-premises location.</span></span> <span data-ttu-id="3a23d-155">Incluso puede replicar una carga de trabajo que se ejecuta en una máquina virtual de Azure compatible, en una máquina virtual de *Hyper-V* local, en una máquina virtual de *VMware* o en un servidor físico de Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="3a23d-155">You can even replicate a workload that's running on a supported Azure VM, on an on-premises *Hyper-V* VM, on a *VMware* VM, or on a Windows or Linux physical server.</span></span> <span data-ttu-id="3a23d-156">La replicación en Azure elimina el costo y la complejidad del mantenimiento de un centro de datos secundario.</span><span class="sxs-lookup"><span data-stu-id="3a23d-156">Replication to Azure eliminates the cost and complexity of maintaining a secondary datacenter.</span></span>

<span data-ttu-id="3a23d-157">Site Recovery también se crea específicamente para entornos híbridos que se encuentran en parte de forma local y en parte en Azure.</span><span class="sxs-lookup"><span data-stu-id="3a23d-157">Site Recovery is also made specifically for hybrid environments that are partly on-premises and partly on Azure.</span></span> <span data-ttu-id="3a23d-158">Site Recovery ayuda a garantizar la continuidad empresarial manteniendo las aplicaciones que se ejecutan en máquinas virtuales y servidores físicos locales disponibles si un sitio deja de funcionar.</span><span class="sxs-lookup"><span data-stu-id="3a23d-158">Site Recovery helps ensure business continuity by keeping your apps that are running on VMs and on-premises physical servers available if a site goes down.</span></span> <span data-ttu-id="3a23d-159">Replica las cargas de trabajo que se ejecutan en máquinas virtuales y servidores físicos para que sigan estando disponibles en una ubicación secundaria si el sitio primario no está disponible.</span><span class="sxs-lookup"><span data-stu-id="3a23d-159">It replicates workloads that are running on VMs and physical servers so that they remain available in a secondary location if the primary site isn't available.</span></span> <span data-ttu-id="3a23d-160">Recupera las cargas de trabajo en el sitio principal cuando está funcionando de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3a23d-160">It recovers workloads to the primary site when it's up and running again.</span></span>

<span data-ttu-id="3a23d-161">En la figura 2-3 se muestra la ejecución de varias migraciones de máquinas virtuales mediante Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="3a23d-161">Figure 2-3 shows the execution of multiple VM migrations by using Azure Site Recovery.</span></span>

![Posicionamiento de aplicaciones listas para la infraestructura de nube](./media/image2-3.png)

> <span data-ttu-id="3a23d-163">**Figura 2-3.**</span><span class="sxs-lookup"><span data-stu-id="3a23d-163">**Figure 2-3.**</span></span> <span data-ttu-id="3a23d-164">Posicionamiento de aplicaciones listas para la infraestructura de nube</span><span class="sxs-lookup"><span data-stu-id="3a23d-164">Positioning Cloud Infrastructure-Ready applications</span></span>

### <a name="additional-resources"></a><span data-ttu-id="3a23d-165">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3a23d-165">Additional resources</span></span>

- <span data-ttu-id="3a23d-166">**Azure Migrate hoja de comentarios**</span><span class="sxs-lookup"><span data-stu-id="3a23d-166">**Azure Migrate Datasheet**</span></span>

    <https://aka.ms/azuremigration\_datasheet>

- <span data-ttu-id="3a23d-167">**Azure Migrate**</span><span class="sxs-lookup"><span data-stu-id="3a23d-167">**Azure Migrate**</span></span>

    <https://aka.ms/azuremigrate>

- <span data-ttu-id="3a23d-168">**Azure Migration Center**</span><span class="sxs-lookup"><span data-stu-id="3a23d-168">**Azure migration center**</span></span>

    <https://azure.microsoft.com/migration/>

- <span data-ttu-id="3a23d-169">**Migre a Azure con Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="3a23d-169">**Migrate to Azure with Site Recovery**</span></span>

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-to-azure>

- <span data-ttu-id="3a23d-170">**Información general del servicio Azure Site Recovery**</span><span class="sxs-lookup"><span data-stu-id="3a23d-170">**Azure Site Recovery service overview**</span></span>

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-overview>

- <span data-ttu-id="3a23d-171">**Migración de máquinas virtuales en AWS a máquinas virtuales de Azure**</span><span class="sxs-lookup"><span data-stu-id="3a23d-171">**Migrating VMs in AWS to Azure VMs**</span></span>

    <https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-aws-to-azure>

>[!div class="step-by-step"]
><span data-ttu-id="3a23d-172">[Anterior](index.md)
>[Siguiente](migrate-your-relational-databases-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3a23d-172">[Previous](index.md)
[Next](migrate-your-relational-databases-to-azure.md)</span></span>