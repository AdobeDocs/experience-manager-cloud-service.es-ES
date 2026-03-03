---
title: Resumen del trabajo de desarrollo
description: Aprenda cómo el trabajo de desarrollo de AEM analiza las canalizaciones fallidas en Cloud Manager y los registros de compilación para sugerir correcciones de código y acelerar la depuración.
feature: Agentic AI, AI Assistant, AI Tools, User Roles
role: User, Admin, Architect, Developer
exl-id: 2194556f-aac2-4cdd-8f7f-00c92c8c4424
source-git-commit: a38d153194f977cf305bece1d9cae676800f52d6
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Resumen del trabajo de desarrollo {#development-job-overview}

[Como parte de Brand Experience Agent,](/help/ai-in-aem/agents/brand-experience/overview.md) el trabajo de desarrollo ayuda a los desarrolladores y administradores de AEM a crear, depurar, implementar y optimizar código de manera más eficiente.

El trabajo puede recuperar los estados de la canalización y ayudarle a solucionar problemas con los pasos de generación fallidos sugiriendo correcciones, lo que ahorra tiempo al depurar implementaciones de AEM as a Cloud Service en entornos de desarrollo, fase y producción. Examina los registros de generación y el código relacionado para recomendar una corrección que puede aplicar manualmente.

>[!VIDEO](https://video.tv.adobe.com/v/3478010?captions=spa&quality=12&learn=on)

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

>[!NOTE]
>
>La resolución de problemas de canalización se limita a las canalizaciones de pila completa (implementación y calidad de código), pero la compatibilidad con la **canalización de configuración de nivel web** ya está disponible en versión beta. Para solicitar acceso, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). Se requiere el acceso preexistente a los agentes en AEM.

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

Para acceder a este trabajo, consulte las [notas de la versión](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs) para obtener instrucciones sobre cómo inscribirse en el programa beta, asegurándose de indicar su interés en el trabajo de desarrollo. También puede enviar por correo electrónico comentarios específicos del trabajo de desarrollo a [aem-devagent@adobe.com.](mailto:aem-devagent@adobe.com)

[Siga un tutorial](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/ai/development-agent-troubleshoot-ci-cd-pipeline) para aprender a utilizar el agente de desarrollo con el fin de solucionar errores de canalización.

## Acceso al trabajo de desarrollo mediante Cloud Manager {#how-to-access-the-job}

Puede acceder al trabajo de desarrollo a través del asistente de IA que se encuentra en las interfaces de usuario, incluidas Cloud Manager o Experience Hub.

1. Para empezar, haga clic en [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) para abrir su página principal.

   ![página de inicio de Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. En el carril izquierdo, bajo el encabezado **Servicios**, haga clic en **Cloud Manager**.

   ![Se ha seleccionado la lista desplegable que muestra el ajuste preestablecido Autor de contenido](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Los widgets, las herramientas y los artefactos que se muestran dependen del perfil del usuario, los derechos y el tipo de implementación de AEM (AEM as a Cloud Service o Managed Services 6.5/6.5 LTS).

1. En el carril izquierdo, en **Programa**, haga clic en **![Icono de información general](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Información general**.

1. En la página **Resumen del programa**, en la tarjeta **Canalizaciones**, haga clic en una canalización.

   ![Canalización seleccionada](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-select.png)

1. En la página **Escaneo de código y compilación**, observe la canalización con errores.

   ![Error de canalización como se ve en la página Generar y escanear código](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-pipeline-failure.png)

1. Cerca de la esquina superior derecha de la interfaz de usuario de AEM (desde las páginas de Cloud Manager o desde la instancia de autor de los entornos de AEM), haga clic en el icono **Asistente de IA**.

   ![Icono del Asistente de IA en la barra de herramientas](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Consulte también [Asistente de IA en AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. En el cuadro de texto del panel **Ayudante de IA** cerca de la parte inferior, escriba su pregunta o mensaje, luego presione `Enter` o haga clic en ![Enviar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Por ejemplo:
   *En el programa &quot;eda-org-01-no-access&quot;, analice el error en la canalización &quot;sin acceso&quot; y solucione los problemas.*

   La solicitud genera la siguiente respuesta.

   ![Mensaje del Asistente de IA y respuesta resultante](/help/ai-in-aem/agents/brand-experience/development/assets/dev-agent-prompt-response.png)


## Permisos {#permissions}

El trabajo de desarrollo requiere la función Cloud Manager - Desarrollador o Cloud Manager - Administrador de programas.

## Ejemplos de peticiones de datos {#sample-prompts}

| Indicación | Resultado |
| --- | --- |
| *Solucionar problemas de mi canalización con errores* | Realiza un análisis de por qué ha fallado una canalización; si no está claro a qué canalización se hace referencia, se formularán preguntas adicionales al usuario. |
| *Enumerar mis canalizaciones con errores para el programa principal.* | Aunque los resultados pueden variar, este mensaje genera una tabla de canalizaciones fallidas, con una sugerencia de seguimiento para hacer referencia a una canalización específica para analizar. |
| *Analizar mi canalización con error llamada &quot;Canalización de desarrollo&quot;.* | Este mensaje resulta en un análisis de la canalización fallida con sugerencias para corregir. Si se producen varios errores, se formularán preguntas adicionales al usuario. |
| *Solucionar problemas de ejecución de canalización 1234567* | Al proporcionar un ID de ejecución de canalización exacto, se realiza un análisis de canalización. |

## Funciones fuera de ámbito {#out-of-scope-features}

La resolución de problemas de canalización funciona en el paso Generar y prueba de unidad y el paso Escaneo de código en la implementación de pila completa y las canalizaciones de calidad de código. Para otros tipos y pasos de canalización, depure los errores descargando e inspeccionando los registros.

Consulte [Registros de acceso y descarga](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.
