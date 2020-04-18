---
title: Colecciones y tipos de colecciones para XAML
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 2ec58026c605df31489c8aab4c4cc714dab11474
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2020
ms.locfileid: "81432585"
---
# <a name="collections-and-collection-types-for-xaml"></a><span data-ttu-id="7f0b8-102">Colecciones y tipos de colección para XAML</span><span class="sxs-lookup"><span data-stu-id="7f0b8-102">Collections and collection types for XAML</span></span>

<span data-ttu-id="7f0b8-103">En este artículo se describe cómo definir propiedades de tipos que están diseñados para admitir una colección y para admitir la sintaxis XAML para crear instancias de elementos de colección como elementos secundarios de un elemento de objeto primario o elemento de propiedad.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-103">This article describes how to define properties of types that are intended to support a collection, and to support the XAML syntax for instantiating collection items as element children of a parent object element or property element.</span></span>

## <a name="xaml-collection-concepts"></a><span data-ttu-id="7f0b8-104">Conceptos de colección XAML</span><span class="sxs-lookup"><span data-stu-id="7f0b8-104">XAML Collection Concepts</span></span>

<span data-ttu-id="7f0b8-105">Conceptualmente, cualquier relación en XAML donde hay varios elementos secundarios dentro del ámbito de un elemento de objeto XAML o un elemento de propiedad XAML debe implementarse como una colección.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-105">Conceptually, any relationship in XAML where there are multiple child items within the scope of a XAML object element or XAML property element must be implemented as a collection.</span></span> <span data-ttu-id="7f0b8-106">Esa colección debe estar asociada a una propiedad XAML determinada del tipo XAML que es el elemento primario de esa relación.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-106">That collection must be associated with a particular XAML property of the XAML type that is the parent in that relationship.</span></span> <span data-ttu-id="7f0b8-107">La propiedad debe ser una colección porque un procesador XAML espera asignar cada elemento en el marcado para que sea un elemento recién agregado de la propiedad de colección de respaldo.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-107">The property must be a collection because a XAML processor expects to assign each item in markup to be a newly added item of the backing collection property.</span></span>

<span data-ttu-id="7f0b8-108">En el nivel de lenguaje XAML, los requisitos exactos de la compatibilidad con la colección no están completamente definidos.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-108">At the XAML language level, the exact requirements of collection support are not fully defined.</span></span> <span data-ttu-id="7f0b8-109">El concepto de que una colección puede ser una lista o un diccionario (pero no ambos) se define en el nivel de lenguaje XAML, pero qué tipos de respaldo representan listas o diccionarios no está definido por el lenguaje XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-109">The concept that a collection can be either a list or a dictionary(but not both) is defined at the XAML language level, but which backing types represent either lists or dictionaries is not defined by the XAML language.</span></span>

<span data-ttu-id="7f0b8-110">En los servicios XAML de .NET, el concepto de compatibilidad con la colección XAML se define más claramente en términos de tipos de respaldo de .NET.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-110">In .NET XAML Services, the concept of XAML collection support is more clearly defined in terms of .NET backing types.</span></span> <span data-ttu-id="7f0b8-111">En concreto, la compatibilidad de XAML para colecciones se basa en varios conceptos y API de .NET que se usan para listas y diccionarios en la programación general de .NET.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-111">Specifically, the XAML support for collections is based on several .NET concepts and APIs that are used for lists and dictionaries in general .NET programming.</span></span>

1. <span data-ttu-id="7f0b8-112">La <xref:System.Collections.IList> interfaz indica una colección de listas.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-112">The <xref:System.Collections.IList> interface indicates a list collection.</span></span>

2. <span data-ttu-id="7f0b8-113">La <xref:System.Collections.IDictionary> interfaz indica una colección de diccionarios.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-113">The <xref:System.Collections.IDictionary> interface indicates a dictionary collection.</span></span>

3. <span data-ttu-id="7f0b8-114"><xref:System.Array>representa una matriz y una <xref:System.Collections.IList> matriz admite métodos.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-114"><xref:System.Array> represents an array, and an array supports <xref:System.Collections.IList> methods.</span></span>

<span data-ttu-id="7f0b8-115">En cada uno de estos conceptos de colección, `Add` un procesador XAML de Servicios XAML de .NET espera llamar al método en una instancia específica del tipo de la propiedad de colección.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-115">In each of these collection concepts, a .NET XAML Services XAML processor expects to call the `Add` method on a specific instance of the collection property's type.</span></span> <span data-ttu-id="7f0b8-116">O bien, en un escenario de serialización, un procesador XAML genera instancias de tipo XAML discretas para cada elemento que se encuentra en la lista, diccionario o matriz en función del concepto específico de cada colección de "Items".</span><span class="sxs-lookup"><span data-stu-id="7f0b8-116">Or, in a serialization scenario, a XAML processor produces discrete XAML-type instances for each item found in the list, dictionary, or array based on each collection's specific concept of "Items".</span></span> <span data-ttu-id="7f0b8-117">Estos elementos <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType>son: ; <xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>; el <xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> explícito <xref:System.Array>para .</span><span class="sxs-lookup"><span data-stu-id="7f0b8-117">These items are: <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType>; <xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>; the explicit <xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> for <xref:System.Array>.</span></span>

## <a name="generic-collections"></a><span data-ttu-id="7f0b8-118">Colecciones genéricas</span><span class="sxs-lookup"><span data-stu-id="7f0b8-118">Generic Collections</span></span>

<span data-ttu-id="7f0b8-119">Las colecciones genéricas pueden ser útiles para la programación general de .NET y también se pueden usar para las propiedades de la colección XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-119">Generic collections can be useful for general .NET programming, and can also be used for XAML collection properties.</span></span> <span data-ttu-id="7f0b8-120">Sin embargo, <xref:System.Collections.Generic.IList%601> las <xref:System.Collections.Generic.IDictionary%602> interfaces genéricas y no se identifican por los <xref:System.Collections.IList> <xref:System.Collections.IDictionary>procesadores XAML de servicios XAML de .NET como equivalentes a los no genéricos o .</span><span class="sxs-lookup"><span data-stu-id="7f0b8-120">However, the generic interfaces <xref:System.Collections.Generic.IList%601> and <xref:System.Collections.Generic.IDictionary%602> are not identified by .NET XAML Services XAML processors as being equivalent to the non-generic <xref:System.Collections.IList> or <xref:System.Collections.IDictionary>.</span></span> <span data-ttu-id="7f0b8-121">En lugar de implementar las interfaces, un enfoque recomendado para <xref:System.Collections.Generic.List%601> <xref:System.Collections.Generic.Dictionary%602>los tipos de propiedad de colección genérica es derivar de las clases o .</span><span class="sxs-lookup"><span data-stu-id="7f0b8-121">Rather than implementing the interfaces, a recommended approach for generic collection property types is to derive from the classes <xref:System.Collections.Generic.List%601> or <xref:System.Collections.Generic.Dictionary%602>.</span></span> <span data-ttu-id="7f0b8-122">Estas clases implementan las interfaces no genéricas y, por lo tanto, incluyen la compatibilidad esperada para las colecciones XAML en la implementación base.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-122">These classes implement the non-generic interfaces and thus include the expected support for XAML collections in the base implementation.</span></span>

## <a name="read-only-collections-and-initialization-logic"></a><span data-ttu-id="7f0b8-123">Colecciones de solo lectura y lógica de inicialización</span><span class="sxs-lookup"><span data-stu-id="7f0b8-123">Read-Only Collections and Initialization Logic</span></span>

<span data-ttu-id="7f0b8-124">En la programación de .NET, es un patrón de diseño común para hacer cualquier propiedad que contiene un valor de una colección como una colección de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-124">In .NET programming, it is a common design pattern to make any property that holds a value of a collection as a read-only collection.</span></span> <span data-ttu-id="7f0b8-125">Este patrón permite que la instancia propietaria de la propiedad collection controle mejor lo que sucede con la colección.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-125">This pattern permits the instance that owns the collection property to better control what happens to the collection..</span></span> <span data-ttu-id="7f0b8-126">En concreto, el patrón evita la sustitución accidental de toda la colección preexistente estableciendo la propiedad.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-126">Specifically, the pattern prevents accidental replacement of the entire pre-existing collection by setting the property.</span></span> <span data-ttu-id="7f0b8-127">En este patrón, cualquier acceso a la colección por los llamadores debe realizarse en su lugar <xref:System.Collections.IList>llamando a métodos o propiedades según lo admitido por el tipo de colección o las interfaces de colección relevantes como .</span><span class="sxs-lookup"><span data-stu-id="7f0b8-127">In this pattern, any access to the collection by callers should instead be made by calling methods or properties as supported by the collection type and/or the relevant collection interfaces such as <xref:System.Collections.IList>.</span></span>

<span data-ttu-id="7f0b8-128">El uso de este patrón implica que cualquier clase que expone una propiedad de colección de solo lectura debe inicializar primero esa propiedad para contener una colección vacía.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-128">Using this pattern implies that any class that exposes a read-only collection property must first initialize that property to hold an empty collection.</span></span> <span data-ttu-id="7f0b8-129">Normalmente, la inicialización se realiza como parte del comportamiento de construcción de la clase.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-129">Typically the initialization is performed as part of the construction behavior for the class.</span></span> <span data-ttu-id="7f0b8-130">Para ser útil para XAML, es importante que el constructor sin parámetros siempre haga referencia a esta lógica, porque XAML suele llamar al constructor sin parámetros antes de procesar las propiedades (propiedades de colección o de otro modo).</span><span class="sxs-lookup"><span data-stu-id="7f0b8-130">To be useful for XAML, it is important that such logic is always referenced by the parameterless constructor, because XAML generally calls the parameterless constructor prior to processing the properties (collection properties or otherwise).</span></span>

## <a name="xaml-type-system-support-and-collections"></a><span data-ttu-id="7f0b8-131">Compatibilidad y cobros del sistema de tipos XAML</span><span class="sxs-lookup"><span data-stu-id="7f0b8-131">XAML Type System Support and Collections</span></span>

<span data-ttu-id="7f0b8-132">Más allá de la mecánica básica de análisis de XAML y rellenar o serializar propiedades de colección, el sistema de tipos XAML tal como se implementa en Servicios XAML de .NET incluye varias características de diseño que pertenecen a colecciones en XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-132">Beyond the basic mechanics of parsing XAML and populating or serializing collection properties, the XAML type system as implemented in .NET XAML Services includes several design features that pertain to collections in XAML.</span></span>

1. <span data-ttu-id="7f0b8-133"><xref:System.Xaml.XamlType.IsCollection%2A>devuelve true si el tipo XAML está respaldado por un tipo que proporciona compatibilidad con la colección XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-133"><xref:System.Xaml.XamlType.IsCollection%2A> returns true if the XAML type is backed by a type that provides XAML collection support.</span></span>

2. <span data-ttu-id="7f0b8-134"><xref:System.Xaml.XamlType.IsDictionary%2A>y <xref:System.Xaml.XamlType.IsArray%2A> puede identificar aún más qué modo de colección admite el tipo XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-134"><xref:System.Xaml.XamlType.IsDictionary%2A> and <xref:System.Xaml.XamlType.IsArray%2A> can further identify which collection mode the XAML type supports.</span></span> <span data-ttu-id="7f0b8-135">Para los procesadores XAML personalizados que se basan en los <xref:System.Xaml.XamlWriter> servicios XAML de .NET y el sistema de tipos XAML, pero no en las implementaciones existentes, es posible que sea necesario saber qué modo de colección se usa para saber qué método invocar para el procesamiento de la colección.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-135">For custom XAML processors that are based on .NET XAML Services and the XAML type system but not based on existing <xref:System.Xaml.XamlWriter> implementations, knowing which collection mode is used might be necessary in order to know which method to invoke for collection processing.</span></span>

3. <span data-ttu-id="7f0b8-136">Cada uno de los valores de propiedad <xref:System.Xaml.XamlType.LookupCollectionKind%2A> anteriores está potencialmente influenciado por invalidaciones de un tipo XAML.</span><span class="sxs-lookup"><span data-stu-id="7f0b8-136">Each of the previous property values is potentially influenced by overrides of <xref:System.Xaml.XamlType.LookupCollectionKind%2A> on a XAML type.</span></span>