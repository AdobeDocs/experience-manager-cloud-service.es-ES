---
title: Configuración de OpenAI ChatGPT con AEM MCP
description: Aprenda a configurar OpenAI ChatGPT para conectarse a servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Configuración de OpenAI ChatGPT con AEM MCP {#setup-chatgpt}

Siga estos pasos para conectar OpenAI ChatGPT a los servidores MCP de AEM.

* Agregue una o más URL de servidor MCP de AEM en el área donde están configuradas las conexiones o herramientas MCP.
* Almacene en déclencheur la conexión e inicie sesión con su Adobe ID cuando se le redirija.
* En un chat, consulte las herramientas de AEM configuradas en las peticiones de datos, por ejemplo:

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

>[!NOTE]
>
>La interfaz de usuario de OpenAI ChatGPT está sujeta a cambios y no es definitiva. Estas instrucciones tienen fines ilustrativos.

1. Abra **Configuración** para que pueda llegar al área donde están configuradas las herramientas o las conexiones MCP.

   ![Cuadro de diálogo Configuración de ChatGPT.](assets/chatgpt-1.png)

1. En **Aplicaciones y conectores**, abra **Configuración avanzada** para administrar el conector y las opciones relacionadas con MCP.

   ![Panel de configuración avanzada de aplicaciones y conectores en ChatGPT.](assets/chatgpt-2.png)

1. Habilite **Modo de desarrollador** en **Aplicaciones y conectores** para que pueda agregar y configurar aplicaciones o conectores personalizados.

   ![Habilitando el modo de desarrollador en la sección de aplicaciones y conectores.](assets/chatgpt-3.png)

1. Inicie **Crear nueva aplicación** (o el control equivalente) para agregar una entrada de aplicación para el servidor MCP de AEM.

   ![Cuadro de diálogo para crear una nueva aplicación en ChatGPT.](assets/chatgpt-4.png)

1. Complete el formulario **Nueva aplicación** (por ejemplo, asigne un nombre a la aplicación, introduzca la URL del servidor MCP de AEM y cualquier otro campo obligatorio) y, a continuación, **guarde**.

   ![El nuevo formulario de configuración de la aplicación en ChatGPT.](assets/chatgpt-5.png)

1. Confirme que **AEM Content MCP Service** (o su aplicación configurada) aparece en **Aplicaciones y conectores** para que ChatGPT pueda usarlo.

   ![El servicio MCP de contenido de AEM que aparece en aplicaciones y conectores.](assets/chatgpt-6.png)

1. En un chat, escriba un mensaje que indique a ChatGPT que use las **Herramientas de AEM** configuradas (por ejemplo, para consultar el contenido o los sitios de creación).

   ![Solicitando a ChatGPT que use el servicio MCP de contenido de AEM.](assets/chatgpt-7.png)
