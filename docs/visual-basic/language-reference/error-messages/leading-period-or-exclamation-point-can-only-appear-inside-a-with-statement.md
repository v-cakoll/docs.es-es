---
title: "'.' o '!' inicial sólo puede aparecer dentro de una instrucción 'With'"
ms.date: 07/20/2015
f1_keywords:
- vbc30157
- bc30157
helpviewer_keywords:
- BC30157
ms.assetid: 70daaee1-14f9-45b7-9f30-53794310b95e
ms.openlocfilehash: 149acc2baac0f45fa971a11f254d694526d140d7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397329"
---
# <a name="leading--or--can-only-appear-inside-a-with-statement"></a>'.' o '!' inicial sólo puede aparecer dentro de una instrucción 'With'
Un punto (.) o un signo de exclamación (!) que no está dentro de un `With` bloque se produce sin una expresión a la izquierda. El acceso a miembros ( `.` ) y el acceso a miembros de diccionario ( `!` ) requieren una expresión que especifique el elemento que contiene el miembro. Debe aparecer inmediatamente a la izquierda del descriptor de acceso o como destino de un `With` bloque que contiene el acceso a miembros.  
  
 **Identificador de error:** BC30157  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
1. Asegúrese de que el `With` bloque tenga el formato correcto.  
  
2. Si no hay ningún `With` bloque, agregue una expresión a la izquierda del descriptor de acceso que se evalúe como un elemento definido que contiene el miembro.  
  
## <a name="see-also"></a>Consulte también

- [Caracteres especiales en el código](../../programming-guide/program-structure/special-characters-in-code.md)
- [Instrucción With...End With](../statements/with-end-with-statement.md)
