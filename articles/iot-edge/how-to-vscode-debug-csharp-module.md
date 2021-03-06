---
title: "Uso de Visual Studio Code para depurar un módulo de C# con Azure IoT Edge | Microsoft Docs"
description: "Depuración de un módulo de C# con Azure IoT Edge en VS Code"
services: iot-edge
keywords: 
author: shizn
manager: timlt
ms.author: xshi
ms.date: 12/06/2017
ms.topic: article
ms.service: iot-edge
ms.openlocfilehash: 01d321dce439e153b494dfd0de52c100dab78f39
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2017
---
# <a name="use-visual-studio-code-to-debug-c-module-with-azure-iot-edge"></a>Uso de Visual Studio Code para depurar un módulo de C# con Azure IoT Edge
En este artículo se proporcionan instrucciones detalladas para usar [Visual Studio Code](https://code.visualstudio.com/) como la herramienta de desarrollo principal para depurar los módulos de IoT Edge.

## <a name="prerequisites"></a>requisitos previos
En este tutorial se asume que utiliza un equipo o una máquina virtual con Windows o Linux como el equipo de desarrollo. El dispositivo de IoT Edge podría ser otro dispositivo físico o se puede simular el dispositivo de IoT Edge en el equipo de desarrollo.

Asegúrese de haber completado los siguientes tutoriales antes de empezar con esta guía.
- [Uso de Visual Studio Code para desarrollar un módulo de C# con Azure IoT Edge](how-to-vscode-develop-csharp-module.md)

Una vez completado el tutorial anterior, debe tener listos los siguientes elementos:
- Un registro de Docker local que se ejecuta en el equipo de desarrollo. Se recomienda usar un registro de Docker local para fines de prototipo y pruebas.
- El archivo `Program.cs` con el código más reciente del módulo de filtro.
- Un archivo `deployment.json` actualizado para el módulo de sensor y el módulo de filtro.
- Una versión en tiempo de ejecución de Edge que se ejecute en el equipo de desarrollo.

## <a name="build-your-iot-edge-module-for-debugging-purpose"></a>Creación de un módulo de IoT Edge para fines de depuración
1. Para iniciar la depuración, debe usar el archivo **dockerfile.debug** para recompilar la imagen de Docker e implementar de nuevo la solución Edge. En el explorador de VS Code, haga clic en la carpeta Docker para abrirla. Después, haga clic en la carpeta `linux-x64`, haga clic con el botón derecho en el archivo **Dockerfile.debug** y luego haga clic en **Build IoT Edge module Docker image** (Generar imagen de Docker del módulo de IoT Edge).
3. En la ventana **Seleccionar carpeta**, vaya a `./bin/Debug/netcoreapp2.0/publish` o especifíquelo. Haga clic en **Seleccionar carpeta como EXE_DIR**.
4. En el cuadro de texto emergente de la parte superior de la ventana de VS Code, escriba el nombre de la imagen. Por ejemplo: `<your container registry address>/filtermodule:latest`. Si va a realizar la implementación en el registro local, debe ser `localhost:5000/filtermodule:latest`.
5. Inserte la imagen en el repositorio de Docker. Use el comando **Edge: Push IoT Edge module Docker image** (Edge: insertar la imagen de Docker del módulo de IoT Edge) y escriba la dirección URL de la imagen en el cuadro de texto emergente de la parte superior de la ventana de VS Code. Use la misma dirección URL de la imagen utilizada en el paso anterior.
6. Puede reutilizar `deployment.json` para la reimplementación. En la paleta de comandos, escriba y seleccione **Edge: Restart Edge** (Edge: reiniciar Edge) para obtener el módulo de filtro que se ejecuta con la versión de depuración.

## <a name="start-debugging-in-vs-code"></a>Inicio de la depuración en VS Code
1. Vaya a la ventana de depuración de VS Code. Presione **F5** y seleccione **IoT Edge (.Net Core)**.
2. En `launch.json`, vaya a la sección **Debug IoT Edge Custom Module (.NET Core)** y rellene `<container_name>` en `pipeArgs`. Debe ser `filtermodule` en este tutorial.
3. Vaya a Program.cs. Agregue un punto de interrupción en `method static async Task<MessageResponse> FilterModule(Message message, object userContext)`.
4. Vuelva a presionar **F5**. Después, seleccione el proceso al que desea agregarlo. En este tutorial, el nombre del proceso debe ser `FilterModule.dll`.
5. En la ventana de depuración de VS Code, puede ver las variables en el panel izquierdo. 

> [!NOTE]
> En el ejemplo anterior se muestra cómo depurar módulos de IoT Edge en .Net Core en contenedores. Se basa en la versión de depuración de `Dockerfile.debug`, que incluye VSDBG (el depurador de línea de comandos de .NET Core) en la imagen de contenedor al realizar la compilación. Se recomienda utilizar directamente o personalizar `Dockerfile` sin VSDBG para módulos de IoT Edge listos para entornos de producción cuando termine de depurar los módulos de C#.

## <a name="next-steps"></a>pasos siguientes

En este tutorial, ha creado un módulo de IoT Edge y lo ha implementado para fines de depuración, y ha empezado a depurarlo en VS Code. Puede continuar con cualquiera de los siguientes tutoriales para obtener información sobre otros escenarios al desarrollar Azure IoT Edge en VS Code. 

> [!div class="nextstepaction"]
> [Desarrollo e implementación de un módulo de C# en VS Code](how-to-vscode-develop-csharp-module.md)
