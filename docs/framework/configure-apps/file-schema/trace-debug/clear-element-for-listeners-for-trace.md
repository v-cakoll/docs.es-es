---
title: <clear>(Elemento <listeners> ) para<trace>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/trace/listeners/clear
helpviewer_keywords:
- clear element for <listeners> for <trace>
- <clear> element for <listeners> for <trace>
ms.assetid: b44732a8-271f-4a06-ba9e-fe3298d6f192
ms.openlocfilehash: 905dad8274fede80f4809ff3c7a014049f9df450
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2020
ms.locfileid: "79153547"
---
# <a name="clear-element-for-listeners-for-trace"></a>\<clear>(Elemento \<listeners> ) para\<trace>
Borra la colección `Listeners` de un seguimiento.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<trace>**](trace-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<listeners>**](listeners-element-for-trace.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<clear>**

## <a name="syntax"></a>Sintaxis  
  
```xml  
<clear/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### <a name="attributes"></a>Atributos  
 Ninguno.  
  
### <a name="child-elements"></a>Elementos secundarios  
 Ninguno.  
  
### <a name="parent-elements"></a>Elementos primarios  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|`configuration`|Elemento raíz de cada archivo de configuración usado por las aplicaciones de Common Language Runtime y .NET Framework.|  
|`system.diagnostics`|Especifica los agentes de escucha de seguimiento que recopilan, almacenan y enrutan mensajes, así como el nivel en el que está establecido un modificador de seguimiento.|  
|`trace`|Contiene agentes de escucha que recopilan, almacenan y enrutan los mensajes de seguimiento.|  
|`listeners`|Contiene agentes de escucha que recopilan, almacenan y enrutan mensajes. Los agentes de escucha dirigen los resultados del seguimiento a un destino adecuado.|  
  
## <a name="remarks"></a>Comentarios  
 El `<clear>` elemento quita todos los agentes de escucha de la `Listeners` colección para el seguimiento. Puede usar el `<clear>` elemento antes de usar el `<add>` elemento para estar seguro de que no hay ningún otro agente de escucha activo en la colección.  
  
 Puede borrar la `Listeners` colección mediante programación llamando al <xref:System.Diagnostics.TraceListenerCollection.Clear%2A> método en la <xref:System.Diagnostics.Trace.Listeners%2A?displayProperty=nameWithType> propiedad ( `System.Diagnostics.Trace.Listeners.Clear()` ).  
  
 Este elemento se puede usar en el archivo de configuración del equipo (Machine. config) y en el archivo de configuración de la aplicación.  
  
> [!NOTE]
> El `<clear>` elemento quita <xref:System.Diagnostics.DefaultTraceListener> de la `Listeners` colección, modificando el comportamiento de los <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> métodos, <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=nameWithType> , <xref:System.Diagnostics.Debug.Fail%2A?displayProperty=nameWithType> y <xref:System.Diagnostics.Trace.Fail%2A?displayProperty=nameWithType> . La llamada a un `Assert` `Fail` método o suele tener como resultado la presentación de un cuadro de mensaje. Sin embargo, el cuadro de mensaje no se muestra si <xref:System.Diagnostics.DefaultTraceListener> no está en la `Listeners` colección.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo usar el `<clear>` elemento antes de usar el `<add>` elemento para agregar el agente `console` de escucha a la `Listeners` colección para el seguimiento.  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <trace autoflush="false" indentsize="4">  
      <listeners>  
        <clear/>  
        <add name="console"
          type="System.Diagnostics.ConsoleTraceListener" >  
          <filter type="System.Diagnostics.EventTypeFilter"
            initializeData="Error" />  
        </add>  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>
```  
  
## <a name="see-also"></a>Consulte también

- <xref:System.Diagnostics.Trace.Listeners%2A>
- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.Debug>
- <xref:System.Diagnostics.TraceSource>
- [Esquema de la configuración de seguimiento y depuración](index.md)
- [\<remove>](remove-element-for-listeners-for-trace.md)
- [Agentes de escucha de seguimiento](../../../debug-trace-profile/trace-listeners.md)
