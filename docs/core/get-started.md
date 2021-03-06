---
title: Introducción a .NET Core
description: Encuentre recursos para aprender a crear aplicaciones .NET Core en Windows, Linux y macOS.
author: adegeo
ms.author: adegeo
ms.date: 12/03/2019
ms.custom: vs-dotnet
ms.openlocfilehash: ddbee0764897b511cac0c4142354ba995d94a2b6
ms.sourcegitcommit: 3492dafceb5d4183b6b0d2f3bdf4a1abc4d5ed8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2020
ms.locfileid: "86416054"
---
# <a name="get-started-with-net-core"></a>Introducción a .NET Core

En este artículo se proporciona información sobre cómo comenzar con .NET Core. .NET Core se puede instalar en Windows, Linux y macOS. Puede programar en su editor de texto preferido y crear aplicaciones y bibliotecas multiplataforma.

Si no está seguro de qué es .NET Core o cómo se relaciona con otras tecnologías .NET, comience con la información general [¿Qué es .NET?](https://dotnet.microsoft.com/learn/dotnet/what-is-dotnet). En resumen, .NET Core es una implementación multiplataforma de código abierto de .NET.

## <a name="create-an-application"></a>Crear una aplicación

En primer lugar, descargue e instale el [SDK de .NET Core](https://dotnet.microsoft.com/download) en el equipo.

A continuación, abra un terminal como **PowerShell**, **Símbolo del sistema** o **bash**. Escriba los comandos `dotnet` siguientes para crear y ejecutar una aplicación C#:

```dotnetcli
dotnet new console --output sample1
dotnet run --project sample1
```

Debería ver los siguientes resultados:

```console
Hello World!
```

¡Enhorabuena! Ha creado una sencilla aplicación .NET Core. También puede usar [Visual Studio Code](./tutorials/with-visual-studio-code.md), [Visual Studio ](./tutorials/with-visual-studio.md) (solo Windows) o [Visual Studio para Mac](./tutorials/using-on-mac-vs.md) (solo macOS), para crear una aplicación .NET Core.

## <a name="tutorials"></a>Tutoriales

Para comenzar a desarrollar aplicaciones .NET Core, puede seguir estos tutoriales paso a paso:

<!-- markdownlint-disable MD025 -->

# <a name="windows"></a>[Windows](#tab/windows)

- [Creación de su primera aplicación de consola con .NET Core en Visual Studio 2019](./tutorials/with-visual-studio.md)
- [Compilación de una biblioteca de clases con .NET Standard en Visual Studio](./tutorials/library-with-visual-studio.md)
- [Introducción a .NET Core mediante la CLI de .NET Core](./tutorials/cli-create-console-app.md)

|   |   |
|---|---|
| ![icono de cámara de cine para vídeo](./media/video-icon.png "Ver un vídeo") | Vea el vídeo de Channel 9 sobre [cómo instalar y usar Visual Studio Code y .NET Core](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core/). |
| ![icono de cámara de cine para vídeo](./media/video-icon.png "Ver un vídeo") | Vea los vídeos [.NET Core 101](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oWoazjhXQzBKMrFuArxpW80) en YouTube. |

Vea el artículo [Dependencias y requisitos de .NET Core](install/dependencies.md?pivots=os-windows) para obtener una lista de las versiones de Windows admitidas.

# <a name="linux"></a>[Linux](#tab/linux)

Para comenzar a desarrollar aplicaciones .NET Core, puede seguir estos tutoriales paso a paso:

- [Introducción a .NET Core con la línea de comandos](./tutorials/cli-create-console-app.md)

|   |   |
|---|---|
| ![icono de cámara de cine para vídeo](./media/video-icon.png "Ver un vídeo") | Vea un vídeo de [introducción a Visual Studio Code mediante C# y .NET Core en Ubuntu](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu). |

Vea el artículo [Dependencias y requisitos de .NET Core](install/dependencies.md?pivots=os-linux) para obtener una lista de las distribuciones y las versiones de Linux admitidas.

# <a name="macos"></a>[macOS](#tab/macos)

Para comenzar a desarrollar aplicaciones .NET Core, puede seguir estos tutoriales paso a paso:

- [Introducción a .NET Core en macOS con Visual Studio Code](./tutorials/using-on-macos.md)
- [Introducción a .NET Core con la línea de comandos](./tutorials/cli-create-console-app.md)
- [Introducción a .NET Core en macOS con Visual Studio para Mac](./tutorials/using-on-mac-vs.md)
- [Creación de una biblioteca de .NET Standard en macOS mediante Visual Studio para Mac](tutorials/library-with-visual-studio-mac.md)

|   |   |
|---|---|
| ![icono de cámara de cine para vídeo](media/video-icon.png "Ver un vídeo") | Vea un vídeo de [introducción a Visual Studio Code mediante C# y .NET Core en macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-NET-Core-Mac). |

Vea el artículo [Dependencias y requisitos de .NET Core](install/dependencies.md?pivots=os-macos) para obtener una lista de las versiones de OS X / macOS admitidas.

---
