---
title: Configuración de la Claude antrópica con AEM MCP
description: Aprenda a configurar Anthropic Claude para conectarse a los servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: 07a7aa5f02d7bfa992df825f3b8a19e18d569d5b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Configuración de la Claude antrópica con AEM MCP {#setup-claude}

Este artículo cubre dos formas independientes de utilizar Anthropic Claude con AEM:

- Configure manualmente uno o más servidores MCP de AEM en Claude (los servidores descritos en [Uso de MCP con AEM as a Cloud Service — Servidores MCP](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md#mcp-servers)).
- Instale Adobe Experience Manager Connector desde el mercado de conectores de Anthropic. Actualmente tiene paridad de características con Content MCP Server y mostrará un subconjunto creciente de herramientas disponibles en los servidores MCP de AEM.



## Configuración manual de los servidores MCP de AEM en Claude {#manual-configure-aems-mcp-servers-in-claude}

En esta sección se describe el método de **configuración manual**, en el que se agregan uno o más servidores MCP de AEM a Claude como conectores personalizados.

>[!NOTE]
>
>La interfaz de usuario de Claude está sujeta a cambios y no es definitiva. Estas instrucciones tienen fines ilustrativos.

1. Abra el menú de cuenta en la esquina inferior izquierda de la aplicación web Claude y elija **Configuración** para abrir el área Configuración.

   ![Menú de cuenta en Claude con la configuración seleccionada.](assets/claude-1.png)

1. En la barra lateral Configuración, seleccione **Conectores**. En la página Conectores, elija **Agregar conector personalizado** para registrar un extremo de MCP personalizado.

   ![Página de conectores en Configuración con Agregar conector personalizado.](assets/claude-2.png)

1. En el cuadro de diálogo **Agregar conector personalizado**, escriba un nombre para mostrar (por ejemplo, **Servicio MCP de contenido de AEM**) y la URL de su servidor MCP, y después elija **Agregar**. Use **Configuración avanzada** solo cuando su implementación requiera opciones adicionales.

   ![Agregar cuadro de diálogo de conector personalizado con nombre y dirección URL de MCP.](assets/claude-3.png)

1. En la lista Conectores, busca tu entrada de conector personalizada (muestra una etiqueta **CUSTOM**) y elige **Connect** para iniciar sesión y vincular el conector a tu cuenta de Claude.

   ![Lista de conectores con Connect seleccionado para el servicio MCP de contenido de AEM.](assets/claude-4.png)

1. Cuando el conector aparezca en la lista con su URL, elige **Configure** junto a **Servicio MCP de contenido de AEM** para abrir los detalles del conector y continuar con la configuración.

   ![Lista de conectores con la opción Configurar seleccionada para el servicio MCP de contenido de AEM.](assets/claude-5.png)

1. En la página **Permisos de herramientas**, revise los valores predeterminados (por ejemplo, **Necesita aprobación**) y, a continuación, establezca cada herramienta de AEM en **Permitir siempre**, **Pedir permiso** o **No permitir nunca** según la directiva de seguridad.

   ![Permisos de herramientas para el servicio MCP de contenido de AEM.](assets/claude-6.png)

1. Abra una conversación. Seleccione el menú de herramientas y modelos (icono de controles deslizantes) a la izquierda del campo de mensaje, habilite **Servicio MCP de contenido de AEM** en Conectores y, a continuación, escriba el mensaje para que Claude pueda utilizar las herramientas MCP para ese chat.

   ![Compositor de chat con el servicio MCP de contenido de AEM habilitado en el menú de herramientas.](assets/claude-7.png)

## Instale el conector de Adobe Experience Manager (mercado de conectores antrópicos) {#install-adobe-experience-manager-connector}

En esta sección se describe el **conector instalable** del mercado de conectores de Anthropic (en lugar de agregar una dirección URL de conector personalizada). Incluye un subconjunto de las herramientas disponibles en los servidores MCP de AEM.

Para instalar el **conector Adobe Experience Manager**, abra **Configuración** > **Conectores** en Claude. También puede abrir la página Conectores directamente en [https://claude.ai/settings/connectors](https://claude.ai/settings/connectors). El conector registra un servidor MCP que expone un conjunto creciente de herramientas para flujos de trabajo de AEM.

![Instalando el conector Claude de Adobe Experience Manager desde el directorio de conectores.](assets/claude-connector.png)