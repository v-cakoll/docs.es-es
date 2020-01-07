---
ms.openlocfilehash: 4d479636f41095610eaf39f92ad0dad4863ab8b5
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2019
ms.locfileid: "74568187"
---
### <a name="typedescriptionproviderattribute-moved-to-another-assembly"></a><span data-ttu-id="a58ad-101">Se ha movido TypeDescriptionProviderAttribute a otro ensamblado</span><span class="sxs-lookup"><span data-stu-id="a58ad-101">TypeDescriptionProviderAttribute moved to another assembly</span></span>

<span data-ttu-id="a58ad-102">La clase <xref:System.ComponentModel.TypeDescriptionProviderAttribute> se ha movido.</span><span class="sxs-lookup"><span data-stu-id="a58ad-102">The <xref:System.ComponentModel.TypeDescriptionProviderAttribute> class has been moved.</span></span>

#### <a name="change-description"></a><span data-ttu-id="a58ad-103">Descripción del cambio</span><span class="sxs-lookup"><span data-stu-id="a58ad-103">Change description</span></span>

<span data-ttu-id="a58ad-104">En .NET Core 2.2 y en versiones anteriores, la clase <xref:System.ComponentModel.TypeDescriptionProviderAttribute> se encuentra en el ensamblado *System.ComponentModel.TypeConverter*.</span><span class="sxs-lookup"><span data-stu-id="a58ad-104">In .NET Core 2.2 and earlier versions, The <xref:System.ComponentModel.TypeDescriptionProviderAttribute> class is found in the *System.ComponentModel.TypeConverter* assembly.</span></span>

<span data-ttu-id="a58ad-105">A partir de .NET Core 3.0, se encuentra en el ensamblado *System.ObjectModel*.</span><span class="sxs-lookup"><span data-stu-id="a58ad-105">Starting with .NET Core 3.0, it is found in the *System.ObjectModel* assembly.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="a58ad-106">Versión introducida</span><span class="sxs-lookup"><span data-stu-id="a58ad-106">Version introduced</span></span>

<span data-ttu-id="a58ad-107">3.0</span><span class="sxs-lookup"><span data-stu-id="a58ad-107">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="a58ad-108">Acción recomendada</span><span class="sxs-lookup"><span data-stu-id="a58ad-108">Recommended action</span></span>

<span data-ttu-id="a58ad-109">Este cambio solo afecta a las aplicaciones que usan la reflexión para cargar el tipo <xref:System.ComponentModel.TypeDescriptionProviderAttribute> mediante la llamada a un método como <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType>, o una sobrecarga de <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> que supone que el tipo está en un ensamblado determinado.</span><span class="sxs-lookup"><span data-stu-id="a58ad-109">This change only affects applications that use reflection to load the <xref:System.ComponentModel.TypeDescriptionProviderAttribute> type by calling a method such as <xref:System.Reflection.Assembly.GetType%2A?displayProperty=nameWithType> or an overload of <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType> that assumes the type is in a particular assembly.</span></span> <span data-ttu-id="a58ad-110">En ese caso, el ensamblado al que se hace referencia en la llamada al método debe actualizarse para reflejar la nueva ubicación del ensamblado del tipo.</span><span class="sxs-lookup"><span data-stu-id="a58ad-110">If that is the case, the assembly referenced in the method call should be updated to reflect the type's new assembly location.</span></span>

#### <a name="category"></a><span data-ttu-id="a58ad-111">Categoría</span><span class="sxs-lookup"><span data-stu-id="a58ad-111">Category</span></span>

<span data-ttu-id="a58ad-112">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="a58ad-112">Windows Forms</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="a58ad-113">API afectadas</span><span class="sxs-lookup"><span data-stu-id="a58ad-113">Affected APIs</span></span>

- <span data-ttu-id="a58ad-114">None</span><span class="sxs-lookup"><span data-stu-id="a58ad-114">None</span></span>

<!--

### Affected APIs

- Not detectable via API analysis

-->