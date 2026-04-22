---
title: Configuración de Microsoft Copilot Studio con AEM MCP
description: Aprenda a configurar Microsoft Copilot Studio para conectarse a los servidores MCP de AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c8e96fe6-1a05-47c0-8215-0c28705e5e48
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Configuración de Microsoft Copilot Studio con AEM MCP {#setup-microsoft-copilot-studio}

Siga estos pasos para conectar Microsoft Copilot Studio a los servidores MCP de AEM.

>[!NOTE]
>
>La interfaz de usuario de Microsoft Copilot Studio está sujeta a cambios y no es definitiva. Estas instrucciones tienen fines ilustrativos.

1. En **agentes**, inicie el flujo para agregar un agente que utilizará las herramientas de MCP de AEM.

   * Cree un nuevo agente.

   ![El panel Agentes en Microsoft Copilot Studio.](assets/copilot-1.png)

1. Abra el área de herramientas de ese agente para que pueda registrar cómo llama a las capacidades externas.

   * Vaya a la sección de herramientas y haga clic en **Agregar herramienta**.

   ![Cuadro de diálogo Agregar herramienta en Microsoft Copilot Studio.](assets/copilot-2.png)

1. Decida si desea reutilizar una integración existente o definir una nueva herramienta respaldada por MCP.

   * Seleccione una herramienta existente o cree una nueva.

   ![Seleccionando protocolo de contexto de modelo como tipo de herramienta.](assets/copilot-3.png)

1. Cuando cree una nueva herramienta MCP, continúe con el paso del servidor **Protocolo de contexto de modelo**, incluido el modo de vista previa cuando aparezca.

   * Configure una nueva herramienta MCP que señale a uno o más servidores MCP de AEM **URL**.

   ![Agregando un servidor de protocolo de contexto de modelo en modo de vista previa.](assets/copilot-4.png)

1. Defina cómo el agente alcanza este punto final de MCP, incluido si el acceso es compartido o dedicado.

   * Establezca una conexión, que puede ser **compartida** o **dedicada** entre agentes.

   ![Cuadro de diálogo para crear una nueva conexión.](assets/copilot-5.png)

1. En **Agregar y configurar**, proporcione o confirme los detalles de la herramienta MCP para que el agente pueda llegar a su entorno de AEM.

   ![Panel Agregar y configurar para la herramienta MCP.](assets/copilot-6.png)

1. Complete los campos del formulario de la herramienta MCP (por ejemplo, las **URL del servidor** y las opciones relacionadas con la autenticación).

   * De forma opcional, habilite **modo de confirmación automática** o solicite la **confirmación del usuario final** para todas las interacciones con la herramienta.

   ![Formulario de configuración de la herramienta MCP.](assets/copilot-7.png)

1. Valide la conectividad con el servidor MCP; complete el inicio de sesión basado en explorador cuando Copilot Studio le redirija.

   * Inicia sesión con tu **Adobe ID** cuando se te redirija.

   ![Probando la conexión con el servidor MCP de AEM.](assets/copilot-8.png)

1. Antes de ejecutar una prueba, abre **Administrar conexiones** (o el **administrador de conexiones**) y asigna la conexión correcta a tu sesión.

   * Al probar su agente, abra primero **el administrador de conexiones** para asignar una conexión a su sesión.

   ![El panel Administrar conexiones muestra las conexiones disponibles.](assets/copilot-9.png)

1. En la experiencia de prueba, ejecute el agente con la conexión MCP de AEM.

   * Al probar su agente, presione **Reintentar** después de asignar una conexión en el **administrador de conexiones**.

   ![Probando el agente con la conexión MCP de AEM.](assets/copilot-10.png)
