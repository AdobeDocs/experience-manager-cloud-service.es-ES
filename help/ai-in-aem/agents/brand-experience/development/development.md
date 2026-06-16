---
title: Información general del agente de desarrollo
description: Obtenga información sobre cómo el agente de desarrollo de AEM analiza las canalizaciones con errores en Cloud Manager y los registros de compilación para sugerir correcciones de código y acelerar la depuración; también cómo recuperar información de Cloud Manager, la ayuda para errores de replicación y cómo establecer horas de inactividad y actualizar períodos libres para actualizaciones de AEM.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: 0b050b161b11b9b4cd58e575d69472d3173dfe94
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 10%

---


# Información general del agente de desarrollo {#development-agent-overview}

[Como parte de Brand Experience Agent,](/help/ai-in-aem/agents/brand-experience/overview.md) el agente de desarrollo ayuda a los desarrolladores y administradores tradicionales de AEM Java-stack a crear, depurar, implementar y optimizar código de manera más eficiente.

Admite los siguientes trabajos, a los que se puede acceder mediante la interfaz conversacional del asistente de IA.

* Trabajo de Cloud Manager: operaciones de solo lectura, incluida la lista de programas y entornos, y el estado de la canalización
* Trabajo de resolución de problemas de canalización: depurar canalizaciones con errores
* Trabajo de administración de horas tranquilas y períodos libres de actualización (disponibilidad limitada): ver, crear y editar horas silenciosas y períodos libres de actualización
* Trabajo de resolución de problemas de replicación (Beta): depure los problemas relacionados con la replicación, como las colas bloqueadas.

>[!NOTE]
>
> Los desarrolladores también encontrarán útiles estas funciones impulsadas por IA:
> * [Habilidades del agente IDE](/help/ai-in-aem/local-development-with-ai-tools.md#agent-skills) para escenarios de desarrollo local como la generación de componentes de AEM.
> * [Servidores MCP locales](/help/ai-in-aem/local-development-with-ai-tools.md#aem-quickstart-mcp-server) para el desarrollo local, en particular para la depuración de problemas de AEM y Dispatcher.
> * [Servidores MCP remotos](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) para acceder a API y agentes de AEM.

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

Puede enviar por correo electrónico comentarios específicos del agente de desarrollo a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com).

## Trabajo de Cloud Manager {#cloud-manager-job}

Encuentre información acerca de sus programas y entornos de AEM, lo que incluye:
* enumerar programas y entornos
* enumerar variables de entorno
* búsqueda de los nombres de las canalizaciones y el estado de ejecución actual y los detalles de la etapa
* recuperación de vínculos a registros que se pueden descargar

### Ejemplos de peticiones de datos {#sample-cm-job-prompts}


| Indicación | Resultado |
| --- | --- |
| *Enumerar todos mis programas de AEM Cloud Service* | Muestra los programas a los que tiene acceso. |
| *Obtener detalles del programa 12345* | Recupere detalles sobre el programa. |
| *Enumerar entornos en el programa 12345* | Muestra los entornos del programa. |
| *Obtener registros para el entorno de producción* | Recupera vínculos a varios archivos de registro de AEM, Dispatcher y CDN para que se puedan descargar para la depuración u otros fines. |
| *enumerar canalizaciones para el programa 12345* | Enumerar las canalizaciones en el programa. |
| *¿Cuál es el estado de ejecución de la canalización actual?* | Responde con el estado de la canalización. |
| *Consígueme los vínculos de registro de compilación para la ejecución de la canalización 12345* | Recupera vínculos a registros de generación de canalización para una ejecución de canalización específica. |


## Trabajo de administración de horas tranquilas y períodos libres de actualización {#control-updates-job}

>[!AVAILABILITY]
>
>Esta función se encuentra en una fase de disponibilidad limitada y se implementará en las próximas semanas. Correo electrónico [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com) para acceso inmediato.

Consulte, cree y edite Horas tranquilas y Actualice periodos libres directamente a través del asistente de IA de AEM.

La principal ventaja es que se cometen menos errores de programación. A medida que realiza una solicitud, el asistente le guía a través de lo que es posible y marca los límites aplicables, como el límite de tres períodos, el espacio obligatorio de una semana entre períodos y las ventanas de exclusión de mantenimiento planificadas que no se pueden programar.

Por lo tanto, en lugar de descubrir una restricción después de una configuración fallida, los propietarios del negocio y los administradores de implementación se dirigen a una programación válida en la misma conversación. Esto protege las ventanas empresariales críticas de las actualizaciones de mantenimiento automáticas, al tiempo que reduce las idas y venidas y la configuración incorrecta.

### Ejemplos de peticiones de datos {#sample-updates-prompts}

| Indicación | Resultado |
| --- | --- |
| *¿Cuál es la programación de actualizaciones actual para el programa 12345?* | Esto genera un listado de las reglas de actualización de AEM actuales. |
| *Bloquear actualizaciones de AEM de 9 a. m. a 5 p. m. EST para el programa 12345* | Configura una regla para que las actualizaciones de AEM no se apliquen durante las horas de trabajo estándar. |
| *Quitar el bloque de actualización diaria del programa 12345* | Elimina las reglas que impiden las actualizaciones de AEM. |
| *Pausar las actualizaciones de AEM dentro de dos semanas para el programa 12345* | Crea una regla para evitar actualizaciones de AEM. |
| *Mi programa sigue actualizándose en momentos inconvenientes. ¿Qué opciones tengo?* | Responde con información sobre cómo establecer reglas para controlar la programación de actualizaciones de AEM. |



## Trabajo de resolución de problemas de canalización  {#cloud-manager-pipeline-troubleshooting}

Este trabajo puede recuperar los estados de la canalización y ayudarle a solucionar problemas con los pasos de generación fallidos mediante la sugerencia de correcciones, lo que ahorra tiempo al depurar implementaciones de AEM as a Cloud Service en entornos de desarrollo, fase y producción. Examina los registros de generación y el código relacionado para recomendar una corrección que puede aplicar manualmente.

>[!VIDEO](https://video.tv.adobe.com/v/3478010?captions=spa&quality=12&learn=on)

>[!NOTE]
>
>La resolución de problemas de canalización se limita a las canalizaciones de pila completa (implementación y calidad de código) y a la canalización de configuración de nivel web.

<!--
To access this agent, please refer to the [release notes](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) for instructions on how to enroll in the beta program, being sure to indicate your interest in the  Development Agent. You can also email development agent–specific feedback to [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com)

-->

[Siga un tutorial](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/ai/agents/development-agent-troubleshoot-ci-cd-pipeline) para aprender a utilizar el agente de desarrollo con el fin de solucionar errores de canalización.

### Acceso al agente de desarrollo a través de Cloud Manager {#how-to-access-the-agent}

Puede acceder al agente de desarrollo a través del asistente de IA que se encuentra en las interfaces de usuario, incluidas Cloud Manager o Experience Hub.

1. Para empezar y abrir la página principal, haga clic en [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home).

   ![Página principal de Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. En el carril izquierdo, bajo el encabezado **Servicios**, haga clic en **Cloud Manager**.

   ![Se ha seleccionado la lista desplegable que muestra el ajuste preestablecido Autor de contenido](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Los widgets, herramientas y artefactos que se muestran dependen del perfil de usuario, la asignación de derechos y el tipo de implementación de AEM (AEM as a Cloud Service o Managed Services 6.5/6.5 LTS).

1. En el carril izquierdo, en **Programa**, haga clic en **![Icono de información general](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Información general**.

1. En la página **Resumen del programa**, en la tarjeta **Canalizaciones**, haga clic en una canalización.

   ![Canalización seleccionada](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. En la página **Escaneo de código y compilación**, observe la canalización con errores.

   ![Error de canalización como se ve en la página Generar y escanear código](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png)

1. Cerca de la esquina superior derecha de la interfaz de usuario de AEM (desde las páginas de Cloud Manager o desde la instancia de autor de los entornos de AEM), haga clic en el icono **Asistente de IA**.

   ![Icono del Asistente de IA en la barra de herramientas](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Consulte también [Asistente de IA en AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. En el cuadro de texto del panel **Asistente de IA** cerca de la parte inferior, escriba su pregunta o solicitud, luego pulse `Enter` o haga clic en ![Icono de envío](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Por ejemplo:
   *En el programa &quot;eda-org-01-no-access&quot;, analice el error en la canalización &quot;sin acceso&quot; y solucione los problemas.*

   La solicitud genera la siguiente respuesta.

   ![Mensaje del Asistente de IA y respuesta resultante](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)

### Permisos {#permissions}

El trabajo de solución de problemas de canalización requiere la función Cloud Manager - Desarrollador o Cloud Manager - Administrador de programas.

### Ejemplos de peticiones de datos {#sample-pipeline-prompts}

| Indicación | Resultado |
| --- | --- |
| *Solucionar problemas de mi canalización con errores* | Realiza un análisis de por qué ha fallado una canalización; si no está claro a qué canalización se hace referencia, se formularán preguntas adicionales al usuario. |
| *Enumerar mis canalizaciones con errores para el programa principal.* | Aunque los resultados pueden variar, este mensaje genera una tabla de canalizaciones fallidas, con una sugerencia de seguimiento para hacer referencia a una canalización específica para analizar. |
| *Analizar mi canalización con error llamada &quot;Canalización de desarrollo&quot;.* | Este mensaje resulta en un análisis de la canalización fallida con sugerencias para corregir. Si se producen varios errores, se formularán preguntas adicionales al usuario. |
| *Solucionar problemas de ejecución de canalización 1234567* | Al proporcionar un ID de ejecución de canalización exacto, se realiza un análisis de canalización. |

### Funciones fuera de ámbito {#out-of-scope-features}

La resolución de problemas de canalización funciona en el paso Generar y prueba de unidad y el paso Escaneo de código en la implementación de pila completa y las canalizaciones de calidad de código. También admite [canalizaciones de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines).

Para otros tipos y pasos de canalización, depure los errores descargando e inspeccionando los registros. Consulte [Registros de acceso y descarga](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.



## Trabajo de resolución de problemas de replicación (Beta) {#replication-troubleshooting-job}

Depurar problemas relacionados con la replicación, como colas bloqueadas.

Envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) para obtener acceso al programa beta.
