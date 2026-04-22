---
title: Configuración del cursor con AEM MCP
description: Obtenga información sobre cómo configurar Cursor para conectarse a servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: f0897898-cb1d-4af6-859c-f5a1c0ec6168
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Configuración del cursor con AEM MCP {#setup-cursor}

Siga estos pasos para conectar Cursor a los servidores MCP de AEM.

* En la configuración de MCP del cursor, cree una nueva entrada de servidor MCP con una o más URL de MCP de AEM.
* Autentique con su Adobe ID cuando se le solicite.
* Si lo desea, puede activar o desactivar las herramientas individuales haciendo clic en sus nombres. Todas las herramientas están habilitadas de forma predeterminada.
* Utilice el editor o el chat del cursor para invocar las herramientas de AEM como parte de los flujos de trabajo de desarrollo o contenido.

>[!NOTE]
>
>La interfaz de usuario Cursor está sujeta a cambios y no es definitiva. Estas instrucciones tienen fines ilustrativos.

1. Abra **Configuración del cursor** para que pueda configurar cómo se conecta el cursor a los servidores MCP.

   ![Cuadro de diálogo Configuración del cursor.](assets/cursor-1.png)

1. Abra **Herramientas y MCP** y, a continuación, elija **Agregar MCP personalizado** para iniciar una entrada de servidor MCP personalizada.

   ![Panel Herramientas y MCP con la opción de agregar un servidor MCP personalizado.](assets/cursor-2.png)

1. En el formulario personalizado del servidor MCP, escribe **Name**, tu MCP de AEM **URL** (o URL) y cualquier otro campo obligatorio y, a continuación, **Guardar**.

   ![Formulario de configuración personalizada del servidor MCP en el cursor.](assets/cursor-3.png)

1. Cuando aparezca el cuadro de diálogo de conexión, complete el inicio de sesión presionando **Connect** para que se autorice el nuevo servidor MCP.

   ![Cuadro de diálogo de conexión para el nuevo servidor MCP en Cursor.](assets/cursor-4.png)

1. En **Chat** o el editor, escriba mensajes que invoquen **AEM Tools** para que el servidor MCP configurado participe en el flujo de trabajo.

   ![Solicitando al cursor que use el nuevo servicio MCP de AEM.](assets/cursor-5.png)
