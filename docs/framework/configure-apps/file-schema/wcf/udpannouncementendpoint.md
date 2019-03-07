---
title: <udpAnnouncementEndpoint>
ms.date: 03/30/2017
ms.assetid: 5b3fa9c5-f372-4df9-a9d6-1e426063b721
ms.openlocfilehash: 3ffb18fbd410922df4311180ef7af5153ba5c0f5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379812"
---
# <a name="udpannouncementendpoint"></a><span data-ttu-id="207c5-101">\<udpAnnouncementEndpoint></span><span class="sxs-lookup"><span data-stu-id="207c5-101">\<udpAnnouncementEndpoint></span></span>
<span data-ttu-id="207c5-102">Este elemento de configuración define un extremo estándar usado por los servicios para enviar los mensajes del anuncio a través de un enlace de UDP.</span><span class="sxs-lookup"><span data-stu-id="207c5-102">This configuration element defines a standard endpoint that is used by services to send announcement messages over a UDP binding.</span></span> <span data-ttu-id="207c5-103">Tiene un contrato fijo y admite dos versiones de la detección.</span><span class="sxs-lookup"><span data-stu-id="207c5-103">It has a fixed contract and supports two discovery versions.</span></span> <span data-ttu-id="207c5-104">Además, tiene un enlace de UDP fijo y un valor de dirección predeterminado según se indica en las especificaciones de WS-Discovery (WS-Discovery April 2005 o WS-Discovery versión 1.1).</span><span class="sxs-lookup"><span data-stu-id="207c5-104">In addition it has a fixed UDP binding and a default address value as specified in the WS-Discovery specifications (WS-Discovery April 2005 or WS-Discovery version 1.1).</span></span> <span data-ttu-id="207c5-105">Puede especificar la dirección de multidifusión que se va a usar para enviar y recibir los mensajes del anuncio.</span><span class="sxs-lookup"><span data-stu-id="207c5-105">You can specify the multicast address to use for sending and receiving the announcement messages.</span></span>  
  
<span data-ttu-id="207c5-106">\<system.ServiceModel></span><span class="sxs-lookup"><span data-stu-id="207c5-106">\<system.ServiceModel></span></span>  
<span data-ttu-id="207c5-107">\<standardEndpoints></span><span class="sxs-lookup"><span data-stu-id="207c5-107">\<standardEndpoints></span></span>  
  
## <a name="syntax"></a><span data-ttu-id="207c5-108">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="207c5-108">Syntax</span></span>  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <announcementEndpoint>
      <standardEndpoint discoveryVersion="WSDiscovery11/WSDiscoveryApril2005"
                        maxAnnouncementDelay="Timespan"
                        multicastAddress="Uri"
                        name="String" />
    </announcementEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="207c5-109">Atributos y elementos</span><span class="sxs-lookup"><span data-stu-id="207c5-109">Attributes and Elements</span></span>  
 <span data-ttu-id="207c5-110">En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.</span><span class="sxs-lookup"><span data-stu-id="207c5-110">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="207c5-111">Atributos</span><span class="sxs-lookup"><span data-stu-id="207c5-111">Attributes</span></span>  
  
|<span data-ttu-id="207c5-112">Atributo</span><span class="sxs-lookup"><span data-stu-id="207c5-112">Attribute</span></span>|<span data-ttu-id="207c5-113">Descripción</span><span class="sxs-lookup"><span data-stu-id="207c5-113">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="207c5-114">discoveryVersion</span><span class="sxs-lookup"><span data-stu-id="207c5-114">discoveryVersion</span></span>|<span data-ttu-id="207c5-115">Cadena que especifica una de las dos versiones del protocolo WS-Discovery.</span><span class="sxs-lookup"><span data-stu-id="207c5-115">A string that specifies one of the two versions of WS-Discovery protocol.</span></span> <span data-ttu-id="207c5-116">Los valores válidos son WSDiscovery11 y WSDiscoveryApril2005.</span><span class="sxs-lookup"><span data-stu-id="207c5-116">Valid values are WSDiscovery11 and WSDiscoveryApril2005.</span></span> <span data-ttu-id="207c5-117">Este valor es del tipo <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion>.</span><span class="sxs-lookup"><span data-stu-id="207c5-117">This value is of type <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion>.</span></span>|  
|<span data-ttu-id="207c5-118">maxAnnouncementDelay</span><span class="sxs-lookup"><span data-stu-id="207c5-118">maxAnnouncementDelay</span></span>|<span data-ttu-id="207c5-119">Valor Timespan que especifica el valor máximo del tiempo que el protocolo Discovery esperará antes de enviar un mensaje de saludo.</span><span class="sxs-lookup"><span data-stu-id="207c5-119">A Timespan value that specifies the maximum value for the delay the Discovery protocol will wait before sending a Hello message.</span></span> <span data-ttu-id="207c5-120">Los mensajes esperarán un valor de tiempo aleatorio entre 0 y el valor de este atributo antes de enviarse.</span><span class="sxs-lookup"><span data-stu-id="207c5-120">The messages will wait for a random time value between 0 and the value of this attribute before being sent.</span></span> <span data-ttu-id="207c5-121">Este atributo se utiliza para establecer un retraso pequeño y aleatorio con el fin de evitar las tormentas de red cuando se pierde la conexión de una red y todos los servicios vuelven a estar en línea al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="207c5-121">This attribute is used to set a small, random delay to prevent network storms when a network goes out and all services come back online at the same time.</span></span>|  
|<span data-ttu-id="207c5-122">multicastAddress</span><span class="sxs-lookup"><span data-stu-id="207c5-122">multicastAddress</span></span>|<span data-ttu-id="207c5-123">URI que especifica una dirección de multidifusión que se va a usar para enviar y recibir los mensajes de detección.</span><span class="sxs-lookup"><span data-stu-id="207c5-123">A URI that specifies a multicast address to use for sending and receiving the discovery messages.</span></span> <span data-ttu-id="207c5-124">El valor predeterminado es la dirección de multidifusión como compatible con la especificación de protocolo.</span><span class="sxs-lookup"><span data-stu-id="207c5-124">The default value is the multicast address as conformant to the protocol specification.</span></span>|  
|<span data-ttu-id="207c5-125">name</span><span class="sxs-lookup"><span data-stu-id="207c5-125">name</span></span>|<span data-ttu-id="207c5-126">Cadena que especifica el nombre de la configuración del extremo estándar.</span><span class="sxs-lookup"><span data-stu-id="207c5-126">A String that specifies the name of the configuration of the standard endpoint.</span></span> <span data-ttu-id="207c5-127">El nombre se utiliza en el atributo `endpointConfiguration` del punto de conexión del servicio para vincular un punto de conexión estándar a su configuración.</span><span class="sxs-lookup"><span data-stu-id="207c5-127">The name is used in the `endpointConfiguration` attribute of the service endpoint to link a standard endpoint to its configuration.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="207c5-128">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="207c5-128">Child Elements</span></span>  
  
|<span data-ttu-id="207c5-129">Elemento</span><span class="sxs-lookup"><span data-stu-id="207c5-129">Element</span></span>|<span data-ttu-id="207c5-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="207c5-130">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="207c5-131">\<udpTransportSettings></span><span class="sxs-lookup"><span data-stu-id="207c5-131">\<udpTransportSettings></span></span>](udptransportsettings.md)|<span data-ttu-id="207c5-132">Colección de valores que le permite configurar el transporte UDP para el punto de conexión UDP.</span><span class="sxs-lookup"><span data-stu-id="207c5-132">A collection of settings that allow you to configure UDP transport for the UDP endpoint.</span></span>|  
  
### <a name="parent-elements"></a><span data-ttu-id="207c5-133">Elementos primarios</span><span class="sxs-lookup"><span data-stu-id="207c5-133">Parent Elements</span></span>  
  
|<span data-ttu-id="207c5-134">Elemento</span><span class="sxs-lookup"><span data-stu-id="207c5-134">Element</span></span>|<span data-ttu-id="207c5-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="207c5-135">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="207c5-136">\<standardEndpoints></span><span class="sxs-lookup"><span data-stu-id="207c5-136">\<standardEndpoints></span></span>](standardendpoints.md)|<span data-ttu-id="207c5-137">Colección de puntos de conexión estándar que son puntos de conexión predefinidos con una o más de sus propiedades (dirección, enlace, contrato) fijas.</span><span class="sxs-lookup"><span data-stu-id="207c5-137">A collection of standard endpoints that are pre-defined endpoints with one or more of their properties (address, binding, contract) fixed.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="207c5-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="207c5-138">Example</span></span>  
 <span data-ttu-id="207c5-139">En el siguiente ejemplo se muestra un cliente que escucha un anuncio a través de un transporte de multidifusión UDP con una dirección de multidifusión predeterminada y transporte de multidifusión UDP con una dirección de multidifusión especificada.</span><span class="sxs-lookup"><span data-stu-id="207c5-139">The following example demonstrates a client listening for announcement over a UDP multicast transport with default multicast address, and UDP multicast transport with specified multicast address.</span></span>  
  
```xml  
<services>
  <service name="ServiceAnnouncementListener">
    <endpoint name="udpAnnouncementEndpointStandard"
              kind="udpAnnouncementEndpoint"
              bindingConfiguration="..." />
    <endpoint name="udpAnnouncementEndpoint2"
              kind="udpAnnouncementEndpoint"
              endpointConfiguration="AnnouncementConfiguration3702"
              bindingConfiguration="..." />
    ...
  </service>
</services>
<standardEndpoints>
  <udpAnnouncementEndpoint>
    <standardEndpoint name="AnnouncementConfiguration2"
                      version="WSDiscoveryApril2005"
                      multicastAddress="soap.udp://239.255.255.250:3703"/>
  </udpAnnouncementEndpoint>
</standardEndpoints>
```  
  
## <a name="see-also"></a><span data-ttu-id="207c5-140">Vea también</span><span class="sxs-lookup"><span data-stu-id="207c5-140">See also</span></span>
- <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>