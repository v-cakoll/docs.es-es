---
title: Instrucción no válida dentro de un método o una expresión lambda de varias líneas
ms.date: 07/20/2015
f1_keywords:
- vbc30024
- bc30024
helpviewer_keywords:
- BC30024
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
ms.openlocfilehash: f3c43d640259d5e1af545e2610088aab5d70453d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396251"
---
# <a name="statement-is-not-valid-inside-a-methodmultiline-lambda"></a>La instrucción no es válida dentro de un método o una expresión lambda de varias líneas
La instrucción no es válida dentro de `Sub` un `Function` procedimiento de propiedad,, propiedad `Get` o `Set` . Algunas instrucciones se pueden colocar en el nivel de módulo o de clase. Otros, como `Option Strict` , deben estar en el nivel de espacio de nombres y preceder a todas las demás declaraciones.  
  
 **Identificador de error:** BC30024  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
- Quite la instrucción del procedimiento.  
  
## <a name="see-also"></a>Consulte también

- [Instrucción Sub](../statements/sub-statement.md)
- [Instrucción Function](../statements/function-statement.md)
- [Get (Instrucción)](../statements/get-statement.md)
- [Set (instrucción)](../statements/set-statement.md)
