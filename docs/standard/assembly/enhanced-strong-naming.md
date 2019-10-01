---
title: Nombres seguros mejorados
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies
- strong naming [.NET Framework], enhanced
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 88f9a5c848a8a46b72fb39865ffa861424107438
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972718"
---
# <a name="enhanced-strong-naming"></a><span data-ttu-id="3e6e7-102">Nombres seguros mejorados</span><span class="sxs-lookup"><span data-stu-id="3e6e7-102">Enhanced strong naming</span></span>
<span data-ttu-id="3e6e7-103">Una firma de nombre seguro es un mecanismo de identidad de .NET Framework para identificar ensamblados.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-103">A strong name signature is an identity mechanism in the .NET Framework for identifying assemblies.</span></span> <span data-ttu-id="3e6e7-104">Es una firma digital de clave pública que se suele usar para comprobar la integridad de los datos que se pasan de un remitente (firmante) a un destinatario (comprobador).</span><span class="sxs-lookup"><span data-stu-id="3e6e7-104">It is a public-key digital signature that is typically used to verify the integrity of data being passed from an originator (signer) to a recipient (verifier).</span></span> <span data-ttu-id="3e6e7-105">Esta firma se usa como identidad única para un ensamblado y garantiza que las referencias al ensamblado no son ambiguas.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-105">This signature is used as a unique identity for an assembly and ensures that references to the assembly are not ambiguous.</span></span> <span data-ttu-id="3e6e7-106">El ensamblado se firma como parte del proceso de compilación y, después, se comprueba cuando se carga.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-106">The assembly is signed as part of the build process and then verified when it is loaded.</span></span>  
  
 <span data-ttu-id="3e6e7-107">Las firmas de nombre seguro ayudan a impedir que personas malintencionadas manipulen un ensamblado y vuelvan a firmarlo con la clave del firmante original.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-107">Strong name signatures help prevent malicious parties from tampering with an assembly and then re-signing the assembly with the original signer’s key.</span></span> <span data-ttu-id="3e6e7-108">Pero las claves de nombre seguro no contienen información confiable sobre el publicador ni una jerarquía de certificados.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-108">However, strong name keys don’t contain any reliable information about the publisher, nor do they contain a certificate hierarchy.</span></span> <span data-ttu-id="3e6e7-109">Una firma de nombre seguro no garantiza la confiabilidad de la persona que ha firmado el ensamblado ni indica si dicha persona era el propietario legítimo de la clave; solo indica que el propietario de la clave ha firmado el ensamblado.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-109">A strong name signature does not guarantee the trustworthiness of the person who signed the assembly or indicate whether that person was a legitimate owner of the key; it indicates only that the owner of the key signed the assembly.</span></span> <span data-ttu-id="3e6e7-110">Por lo tanto, no se recomienda usar una firma de nombre seguro como validador de seguridad para código de terceros de confianza.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-110">Therefore, we do not recommend using a strong name signature as a security validator for trusting third-party code.</span></span> <span data-ttu-id="3e6e7-111">La manera recomendada de autenticar el código es Microsoft Authenticode.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-111">Microsoft Authenticode is the recommended way to authenticate code.</span></span>  
  
## <a name="limitations-of-conventional-strong-names"></a><span data-ttu-id="3e6e7-112">Limitaciones de los nombres seguros convencionales</span><span class="sxs-lookup"><span data-stu-id="3e6e7-112">Limitations of conventional strong names</span></span>  
 <span data-ttu-id="3e6e7-113">La tecnología de nomenclatura segura usada en las versiones anteriores a .NET Framework 4.5 tiene las limitaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e6e7-113">The strong naming technology used in versions before the .NET Framework 4.5 has the following shortcomings:</span></span>  
  
- <span data-ttu-id="3e6e7-114">Las claves se encuentran constantemente bajo ataque, y las técnicas y el hardware mejorados hacen que sea más fácil deducir una clave privada a partir de una clave pública.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-114">Keys are constantly under attack, and improved techniques and hardware make it easier to infer a private key from a public key.</span></span> <span data-ttu-id="3e6e7-115">Para protegerse contra los ataques, son necesarias claves más largas.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-115">To guard against attacks, larger keys are necessary.</span></span> <span data-ttu-id="3e6e7-116">Las versiones de .NET Framework anteriores a .NET Framework 4.5 ofrecen la posibilidad de firmar con una clave de cualquier tamaño (el tamaño predeterminado es de 1024 bits), pero si se firma un ensamblado con una clave nueva, se interrumpen todos los binarios que hacen referencia a la identidad anterior del ensamblado.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-116">.NET Framework versions before the .NET Framework 4.5 provide the ability to sign with any size key (the default size is 1024 bits), but signing an assembly with a new key breaks all binaries that reference the older identity of the assembly.</span></span> <span data-ttu-id="3e6e7-117">Por lo tanto, es muy difícil actualizar el tamaño de una clave de firma si quiere mantener la compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-117">Therefore, it is extremely difficult to upgrade the size of a signing key if you want to maintain compatibility.</span></span>  
  
- <span data-ttu-id="3e6e7-118">La firma con nombre seguro solo admite el algoritmo SHA-1.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-118">Strong name signing supports only the SHA-1 algorithm.</span></span> <span data-ttu-id="3e6e7-119">Recientemente se ha descubierto que SHA-1 no es adecuado para las aplicaciones de hash seguro.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-119">SHA-1 has recently been found to be inadequate for secure hashing applications.</span></span> <span data-ttu-id="3e6e7-120">Por lo tanto, es necesario un algoritmo más seguro (SHA-256 o superior).</span><span class="sxs-lookup"><span data-stu-id="3e6e7-120">Therefore, a stronger algorithm (SHA-256 or greater) is necessary.</span></span> <span data-ttu-id="3e6e7-121">Es posible que SHA-1 pierda su compatibilidad con FIPS, lo que causaría problemas a los clientes que deciden usar solo algoritmos y software compatibles con FIPS.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-121">It is possible that SHA-1 will lose its FIPS-compliant standing, which would present problems for those who choose to use only FIPS-compliant software and algorithms.</span></span>  
  
## <a name="advantages-of-enhanced-strong-names"></a><span data-ttu-id="3e6e7-122">Ventajas de los nombres seguros mejorados</span><span class="sxs-lookup"><span data-stu-id="3e6e7-122">Advantages of enhanced strong names</span></span>  
 <span data-ttu-id="3e6e7-123">Las principales ventajas de los nombres seguros mejorados son la compatibilidad con los nombres seguros existentes y la capacidad de afirmar que una identidad es equivalente a otra:</span><span class="sxs-lookup"><span data-stu-id="3e6e7-123">The main advantages of enhanced strong names are compatibility with pre-existing strong names and the ability to claim that one identity is equivalent to another:</span></span>  
  
- <span data-ttu-id="3e6e7-124">Los desarrolladores que ya tengan ensamblados firmados pueden migrar sus identidades a los algoritmos SHA-2 y mantener la compatibilidad con los ensamblados que hacen referencia a identidades anteriores.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-124">Developers who have pre-existing signed assemblies can migrate their identities to the SHA-2 algorithms while maintaining compatibility with assemblies that reference the old identities.</span></span>  
  
- <span data-ttu-id="3e6e7-125">Los desarrolladores que creen ensamblados y no se vean afectados por las firmas de nombre seguro existentes pueden usar los algoritmos SHA-2, que son más seguros, y firmar los ensamblados tal como han hecho siempre.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-125">Developers who create new assemblies and are not concerned with pre-existing strong name signatures can use the more secure SHA-2 algorithms and sign the assemblies as they always have.</span></span>  
  
## <a name="use-enhanced-strong-names"></a><span data-ttu-id="3e6e7-126">Uso de nombres seguros mejorados</span><span class="sxs-lookup"><span data-stu-id="3e6e7-126">Use enhanced strong names</span></span>  
 <span data-ttu-id="3e6e7-127">Las claves de nombre seguro se componen de una clave de firma y una clave de identidad.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-127">Strong name keys consist of a signature key and an identity key.</span></span> <span data-ttu-id="3e6e7-128">El ensamblado se firma con la clave de firma y se identifica mediante la clave de identidad.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-128">The assembly is signed with the signature key and is identified by the identity key.</span></span> <span data-ttu-id="3e6e7-129">Antes de .NET Framework 4.5, estas dos claves eran idénticas.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-129">Prior to the .NET Framework 4.5, these two keys were identical.</span></span> <span data-ttu-id="3e6e7-130">A partir de .NET Framework 4.5, la clave de identidad sigue siendo la misma que en versiones anteriores de .NET Framework, pero la clave de firma se ha mejorado con un algoritmo hash más seguro.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-130">Starting with the .NET Framework 4.5, the identity key remains the same as in earlier .NET Framework versions, but the signature key is enhanced with a stronger hash algorithm.</span></span> <span data-ttu-id="3e6e7-131">Además, la clave de firma se firma con la clave de identidad para crear una contrafirma.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-131">In addition, the signature key is signed with the identity key to create a counter-signature.</span></span>  
  
 <span data-ttu-id="3e6e7-132">El atributo <xref:System.Reflection.AssemblySignatureKeyAttribute> permite que los metadatos del ensamblado usen la clave pública existente para la identidad del ensamblado, lo que permite que las referencias anteriores del ensamblado sigan funcionando.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-132">The <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute enables the assembly metadata to use the pre-existing public key for assembly identity, which allows old assembly references to continue to work.</span></span>  <span data-ttu-id="3e6e7-133">El atributo <xref:System.Reflection.AssemblySignatureKeyAttribute> usa la contrafirma para asegurarse de que el propietario de la clave de firma nueva también es el propietario de la clave de identidad anterior.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-133">The <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute uses the counter-signature to ensure that the owner of the new signature key is also the owner of the old identity key.</span></span>  
  
### <a name="sign-with-sha-2-without-key-migration"></a><span data-ttu-id="3e6e7-134">Firma con SHA-2, sin migración de clave</span><span class="sxs-lookup"><span data-stu-id="3e6e7-134">Sign with SHA-2, without key migration</span></span>  
 <span data-ttu-id="3e6e7-135">Ejecute los comandos siguientes desde un símbolo del sistema para firmar un ensamblado sin migrar una firma de nombre seguro:</span><span class="sxs-lookup"><span data-stu-id="3e6e7-135">Run the following commands from a command prompt to sign an assembly without migrating a strong name signature:</span></span>  
  
1. <span data-ttu-id="3e6e7-136">Genere la nueva clave de identidad (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="3e6e7-136">Generate the new identity key (if necessary).</span></span>  
  
    ```  
    sn -k IdentityKey.snk  
    ```  
  
2. <span data-ttu-id="3e6e7-137">Extraiga la clave pública de identidad y especifique que se debe usar un algoritmo SHA-2 al firmar con esta clave.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-137">Extract the identity public key, and specify that a SHA-2 algorithm should be used when signing with this key.</span></span>  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3. <span data-ttu-id="3e6e7-138">Retrase la firma del ensamblado con el archivo de clave pública de identidad.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-138">Delay-sign the assembly with the identity public key file.</span></span>  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4. <span data-ttu-id="3e6e7-139">Vuelva a firmar el ensamblado con el par de claves de identidad completa.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-139">Re-sign the assembly with the full identity key pair.</span></span>  
  
    ```  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### <a name="sign-with-sha-2-with-key-migration"></a><span data-ttu-id="3e6e7-140">Firma con SHA-2, con migración de clave</span><span class="sxs-lookup"><span data-stu-id="3e6e7-140">Sign with SHA-2, with key migration</span></span>  
 <span data-ttu-id="3e6e7-141">Ejecute los comandos siguientes desde un símbolo del sistema para firmar un ensamblado con una firma de nombre seguro migrada.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-141">Run the following commands from a command prompt to sign an assembly with a migrated strong name signature.</span></span>  
  
1. <span data-ttu-id="3e6e7-142">Genere un par de claves de identidad y firma (si es necesario).</span><span class="sxs-lookup"><span data-stu-id="3e6e7-142">Generate an identity and signature key pair (if necessary).</span></span>  
  
    ```  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2. <span data-ttu-id="3e6e7-143">Extraiga la clave pública de firma y especifique que se debe usar un algoritmo SHA-2 al firmar con esta clave.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-143">Extract the signature public key, and specify that a SHA-2 algorithm should be used when signing with this key.</span></span>  
  
    ```  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3. <span data-ttu-id="3e6e7-144">Extraiga la clave pública de identidad, que determina el algoritmo hash que genera una contrafirma.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-144">Extract the identity public key, which determines the hash algorithm that generates a counter-signature.</span></span>  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4. <span data-ttu-id="3e6e7-145">Genere los parámetros para un atributo <xref:System.Reflection.AssemblySignatureKeyAttribute> y adjunte el atributo al ensamblado.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-145">Generate the parameters for a <xref:System.Reflection.AssemblySignatureKeyAttribute> attribute, and attach the attribute to the assembly.</span></span>  
  
    ```  
    sn -a IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  

    <span data-ttu-id="3e6e7-146">Esto genera un resultado similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-146">This produces output similar to the following.</span></span>

    ```
    Information for key migration attribute.
    (System.Reflection.AssemblySignatureKeyAttribute):
    publicKey=
    002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519
    d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936
    e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b4
    3893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a3
    4d153cdd

    counterSignature=
    e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91eb
    e1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8
    ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3
    ae5fec2c682e57b7442738
    ```

    <span data-ttu-id="3e6e7-147">Luego este resultado se puede transformar en AssemblySignatureKeyAttribute.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-147">This output can then be transformed into an AssemblySignatureKeyAttribute.</span></span>

    ```
    [assembly:System.Reflection.AssemblySignatureKeyAttribute(
    "002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b43893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a34d153cdd",
    "e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91ebe1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3ae5fec2c682e57b7442738"
    )]
    ```
  
5. <span data-ttu-id="3e6e7-148">Retrase la firma del ensamblado con la clave pública de identidad.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-148">Delay-sign the assembly with the identity public key.</span></span>  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
6. <span data-ttu-id="3e6e7-149">Firme por completo el ensamblado con el par de claves de firma.</span><span class="sxs-lookup"><span data-stu-id="3e6e7-149">Fully sign the assembly with the signature key pair.</span></span>  
  
    ```  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="3e6e7-150">Vea también</span><span class="sxs-lookup"><span data-stu-id="3e6e7-150">See also</span></span>

- [<span data-ttu-id="3e6e7-151">Creación y uso de ensamblados con nombre seguro</span><span class="sxs-lookup"><span data-stu-id="3e6e7-151">Create and use strong-named assemblies</span></span>](create-use-strong-named.md)