---
title: Configuración de JetBrains con GitHub Copilot y AEM MCP
description: Aprenda a configurar el copiloto de GitHub en los IDE de JetBrains para conectarse a los servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: e153da42-51e0-49ea-8457-10bb5e77e2de
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 1%

---

# Configuración de JetBrains con GitHub Copilot y AEM MCP {#setup-jetbrains-copilot}

Siga estos pasos para conectar GitHub Copilot en un IDE de JetBrains (como IntelliJ IDEA, WebStorm o PyCharm) a los servidores MCP de AEM.

1. Abra GitHub Copilot Chat en su IDE de JetBrains haciendo clic en el icono **GitHub Copilot Chat** que se encuentra en la parte derecha del editor.

   ![El IDE de JetBrains con GitHub Copilot Chat abierto.](assets/jetbrains-copilot-1.png)

1. Haga clic en el icono **settings** del panel Chat de Copilot para abrir la configuración de MCP.

   ![Panel de chat del copiloto de GitHub con el icono de configuración resaltado.](assets/jetbrains-copilot-2.png)

1. En **Configuración**, vaya a **Herramientas > Copiloto de GitHub > Protocolo de contexto de modelo (MCP)** y haga clic en **Configurar** para abrir el archivo de configuración de `mcp.json`.

   ![Cuadro de diálogo Configuración de JetBrains que muestra la configuración del Protocolo de contexto de modelo (MCP) en el copiloto de GitHub.](assets/jetbrains-copilot-3.png)

1. Agregue una o más URL de servidor MCP de AEM al archivo `mcp.json`. Por ejemplo:

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![El archivo de configuración mcp.json con la dirección URL del servidor MCP de AEM.](assets/jetbrains-copilot-4.png)


1. Guarde el archivo. GitHub Copilot detecta la nueva configuración del servidor automáticamente y muestra una acción **Start**.

   ![Archivo mcp.json que muestra el servidor de AEM configurado con las herramientas detectadas.](assets/jetbrains-copilot-5.png)

1. Haga clic en la acción **Iniciar** y, cuando se le solicite, inicie sesión con su Adobe ID para completar el flujo de autenticación.

1. Puede revisar y administrar las herramientas detectadas si hace clic en el indicador **tools** que aparece en el panel Chat de Copilot. De forma opcional, habilite o deshabilite las herramientas individuales.


   ![El cuadro de diálogo Configurar herramientas muestra las herramientas de MCP de AEM disponibles.](assets/jetbrains-copilot-6.png)

1. Utilice GitHub Copilot Chat para invocar las herramientas de AEM como parte de los flujos de trabajo de desarrollo o contenido.
