---
ms.openlocfilehash: b2fcacdb02c411c4dcb12051bf0c6759faccdea2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620665"
---
### <a name="the-replace-method-in-odata-urls-is-disabled-by-default"></a>El método Replace de las direcciones URL de OData está deshabilitado de forma predeterminada

#### <a name="details"></a>Detalles

A partir de .NET Framework 4.5, el método Replace de direcciones URL de OData está deshabilitado de forma predeterminada. Cuando el método Replace de OData esté deshabilitado (ahora, de forma predeterminada), cualquier solicitud de usuario, incluidas las funciones Replace (que son poco frecuentes), generará un error.

#### <a name="suggestion"></a>Sugerencia

Si el método Replace es necesario (lo que es poco frecuente), se puede volver a habilitar mediante una opción de configuración (<xref:System.Data.Services.Configuration.DataServicesFeaturesSection.ReplaceFunction?displayProperty=fullName>). No obstante, si el método Replace está activado, puede crear vulnerabilidades de seguridad y solo debería usarse tras una revisión exhaustiva.

| NOMBRE    | Valor       |
|:--------|:------------|
| Ámbito   |Borde|
|Versión|4.5|
|Tipo|Tiempo de ejecución

#### <a name="affected-apis"></a>API afectadas

-<xref:System.Data.Services.DataService%601?displayProperty=nameWithType></li></ul>|
