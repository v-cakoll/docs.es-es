---
title: "La primera instrucción de este 'Sub New' debe ser una llamada explícita a 'MyBase.New' o a 'MyClass.New' porque el constructor '<constructorname>' de la clase base '<baseclassname>' de '<derivedclassname>' está marcado como obsoleto: '<errormessage>'"
ms.date: 07/20/2015
f1_keywords:
- vbc30920
- bc30920
helpviewer_keywords:
- BC30920
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
ms.openlocfilehash: 33dd15e3f5f5538963597f2b00f4214895e1f47a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403010"
---
# <a name="first-statement-of-this-sub-new-must-be-an-explicit-call-to-mybasenew-or-myclassnew-because-the-constructorname-in-the-base-class-baseclassname-of-derivedclassname-is-marked-obsolete-errormessage"></a>La primera instrucción de este 'Sub New' debe ser una llamada explícita a 'MyBase.New' o a 'MyClass.New' porque el constructor '\<constructorname>' de la clase base '\<baseclassname>' de '\<derivedclassname>' está marcado como obsoleto: '\<errormessage>'
Un constructor de clase no realiza una llamada de manera explícita a un constructor de clase base y el constructor de clase base se marca con el atributo <xref:System.ObsoleteAttribute> y la directiva para tratarlo como un error.  
  
 Cuando un constructor de clase derivada no llama a un constructor de clase base, Visual Basic intenta generar una llamada implícita a un constructor de clase base sin parámetros. Si no hay ningún constructor accesible en la clase base al que se pueda llamar sin argumentos, Visual Basic no puede generar una llamada implícita. En este caso, el constructor necesario se marca con el <xref:System.ObsoleteAttribute> atributo, por lo que Visual Basic no puede llamarlo.  
  
 Para marcar que cualquier elemento de programación ya no está en uso, aplíquele <xref:System.ObsoleteAttribute> . Si lo hace, puede establecer la propiedad <xref:System.ObsoleteAttribute.IsError%2A> del atributo en `True` o `False`. Si se establece en `True`, el compilador trata como un error los intentos de usar el elemento. Si se establece en `False`o se deja el valor predeterminado `False`, el compilador emite una advertencia si hay un intento de usar el elemento.  
  
 **Identificador de error:** BC30920  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1. Examine el mensaje de error indicado y tome las medidas adecuadas.  
  
2. Incluya una llamada a `MyBase.New()` o `MyClass.New()` como la primera instrucción de `Sub New` en la clase derivada.  
  
## <a name="see-also"></a>Consulte también

- [Información general de atributos](../../programming-guide/concepts/attributes/index.md)
