---
title: Configuración de OpenAI ChatGPT con AEM MCP
description: Aprenda a configurar OpenAI ChatGPT para conectarse a servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: e5eceb1e540a85aab03b7b856af36276291745f6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Configuración de OpenAI ChatGPT con AEM MCP {#setup-chatgpt}

Este artículo cubre dos formas independientes de utilizar OpenAI ChatGPT con AEM:

- Configure manualmente uno o más servidores MCP de AEM en ChatGPT (los servidores descritos en [Uso de MCP con AEM as a Cloud Service — Servidores MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md#mcp-servers)).
- Instale el complemento de Adobe Experience Manager desde el Marketplace del complemento ChatGPT. Actualmente tiene paridad de características con Content MCP Server y mostrará un subconjunto creciente de herramientas disponibles en los servidores MCP de AEM.

## Configurar manualmente los servidores MCP de AEM en ChatGPT {#manual-configure-aems-mcp-servers-in-chatgpt}

En esta sección se describe el método de **configuración manual**, en el que se agregan uno o más servidores MCP de AEM a ChatGPT como aplicaciones o conectores personalizados.

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

1. Habilite el **modo de desarrollador** en **Aplicaciones y conectores** para poder agregar y configurar un complemento personalizado.

   ![Habilitando el modo de desarrollador en la sección de aplicaciones y conectores.](assets/chatgpt-3.png)

1. Inicie **Crear nueva aplicación** (o el control equivalente) para agregar una entrada de aplicación para el servidor MCP de AEM.

   ![Cuadro de diálogo para crear una nueva aplicación en ChatGPT.](assets/chatgpt-4.png)

1. Complete el formulario **Nueva aplicación** (por ejemplo, asigne un nombre a la aplicación, introduzca la URL del servidor MCP de AEM y cualquier otro campo obligatorio) y, a continuación, **guarde**.

   ![El nuevo formulario de configuración de la aplicación en ChatGPT.](assets/chatgpt-5.png)

1. Confirme que **AEM Content MCP Service** (o su aplicación configurada) aparece en **Aplicaciones y conectores** para que ChatGPT pueda usarlo.

   ![El servicio MCP de contenido de AEM que aparece en aplicaciones y conectores.](assets/chatgpt-6.png)

1. En un chat, escriba un mensaje que indique a ChatGPT que use las **Herramientas de AEM** configuradas (por ejemplo, para consultar el contenido o los sitios de creación).

   ![Solicitando a ChatGPT que use el servicio MCP de contenido de AEM.](assets/chatgpt-7.png)

## Instalación del complemento de Adobe Experience Manager (Marketplace del complemento ChatGPT) {#install-adobe-experience-manager-plugin}

En esta sección se describe el **complemento instalable** del mercado de complementos ChatGPT (en lugar de agregar una URL de servidor MCP personalizada). Incluye un subconjunto de las herramientas disponibles en los servidores MCP de AEM.

>[!NOTE]
>
>La interfaz de usuario de OpenAI ChatGPT está sujeta a cambios y no es definitiva. Estas instrucciones tienen fines ilustrativos.

Puede acceder al complemento de Adobe Experience Manager de cualquiera de estas dos formas. Utilice el que sea más conveniente y, a continuación, continúe con los pasos de inicio de sesión siguientes.

**Opción 1: abrir la página del complemento directamente**

Vaya a [https://chatgpt.com/plugins/plugin_asdk_app_6a35d3c1258081919c084a1fd22cd02d](https://chatgpt.com/plugins/plugin_asdk_app_6a35d3c1258081919c084a1fd22cd02d) y elija **Instalar complemento**.

![Página del complemento de Adobe Experience Manager con el botón Instalar complemento.](assets/chatgpt-plugin-install.png)

**Opción 2: buscar el complemento en el mercado**

1. En **Configuración**, elige **Complementos** y al final de la lista elige **Complementos de exploración**.

   ![La página de complementos en la configuración de ChatGPT con complementos de exploración.](assets/chatgpt-plugin-1.png)

1. Busque **Adobe Experience Manager** y, a continuación, selecciónelo.

   ![Buscando el complemento de Adobe Experience Manager en el mercado de complementos.](assets/chatgpt-plugin-2.png)

**Inicia sesión y confirma**

Después de localizar o instalar el complemento con cualquiera de las opciones anteriores, complete la conexión:

1. Elija **Iniciar sesión con Adobe Experience Manager** e inicie sesión en AEM cuando se le redirija.

   ![Cuadro de diálogo Agregar Adobe Experience Manager a ChatGPT con Inicio de sesión con Adobe Experience Manager.](assets/chatgpt-plugin-3.png)

1. Confirme que el aviso verde indica que Adobe Experience Manager está conectado.

   ![El aviso verde que confirma que el complemento de Adobe Experience Manager está conectado.](assets/chatgpt-plugin-4.png)
