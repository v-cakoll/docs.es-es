---
title: Procedimiento para emitir un bip desde un formulario Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], beep
- Windows Forms, sounds
- sounds [Windows Forms], playing
- forms [Windows Forms], sounds
- examples [Windows Forms], sounds
ms.assetid: 7ea5cded-4888-4f35-8f28-5cab1a55c973
ms.openlocfilehash: 7fecc5d5b7259b743926713f87d9303596803582
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015808"
---
# <a name="how-to-play-a-beep-from-a-windows-form"></a>Procedimiento para emitir un bip desde un formulario Windows Forms
En este ejemplo se reproduce un sonido en tiempo de ejecución.

## <a name="example"></a>Ejemplo

```vb
Public Sub OnePing()
    Beep()
End Sub
```

```csharp
public void onePing()
{
    SystemSounds.Beep.Play();
}
```

> [!NOTE]
> El sonido que se reproduce en el C# ejemplo de código <xref:System.Media.SystemSounds.Beep%2A> está determinado por la configuración de sonido del sistema. Para obtener más información, consulta <xref:System.Media.SystemSounds>.

## <a name="compiling-the-code"></a>Compilar el código
 Para C#, este ejemplo requiere una referencia al <xref:System.Media?displayProperty=nameWithType> espacio de nombres.

## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.Interaction.Beep%2A>
- <xref:System.Media.SoundPlayer>
- [Procedimientos: Reproducir un sonido del sistema desde Windows Forms](how-to-play-a-system-sound-from-a-windows-form.md)
- [Cómo: Reproducir un sonido desde Windows Forms](how-to-play-a-sound-from-a-windows-form.md)
