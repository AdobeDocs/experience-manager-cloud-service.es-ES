---
title: Información general del agente de desarrollo
description: Obtenga información sobre cómo el agente de desarrollo de AEM analiza las canalizaciones con errores en Cloud Manager y los registros de compilación para sugerir correcciones de código y acelerar la depuración.
feature: Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3648dd25c3b3b46663cc09d379aeadfd07cedfa4
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Introducción al agente de desarrollo {#development-agent-overview}

El agente de desarrollo ayuda a los desarrolladores y administradores de AEM a crear, depurar, implementar y optimizar código de forma más eficaz.

En la actualidad, el agente puede recuperar los estados de canalización y ayudarle a solucionar errores en los pasos de generación sugiriendo correcciones, lo que ahorra tiempo al depurar implementaciones de AEM as a Cloud Service en entornos de desarrollo, fase y producción. Examina los registros de generación y el código relacionado para recomendar una corrección que puede aplicar manualmente.

>[!IMPORTANT]
>
>Las respuestas generadas por IA pueden ser inexactas o engañosas. Asegúrese de volver a comprobar las correcciones y respuestas sugeridas.
>
>Consulte también [Directrices de usuario de IA generativa de Adobe Experience Cloud](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

<!-- 
## Cloud Manager Pipeline Troubleshooting  {#cloud-manager-pipeline-troubleshooting}
-->

## Acceso al agente de desarrollo a través de Cloud Manager {#how-to-access-the-agent}

Puede acceder al agente de desarrollo a través del asistente de IA que se encuentra en las interfaces de usuario, incluidas Cloud Manager o Experience Hub.

**Para tener acceso al Agente de desarrollo a través de Cloud Manager:**

1. Para empezar, haga clic en [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) para abrir su página principal.

   ![página de inicio de Adobe Experience Cloud](/help/implementing/cloud-manager/assets/experience-cloud-experiencemanager.png)

1. En el carril izquierdo, bajo el encabezado **Servicios**, haga clic en **Cloud Manager**.

   ![Se ha seleccionado la lista desplegable que muestra el ajuste preestablecido Autor de contenido](/help/implementing/cloud-manager/assets/experience-hub-role-selection.png)

   >[!IMPORTANT]
   >
   >Los widgets, las herramientas y los artefactos que se muestran dependen del perfil del usuario, los derechos y el tipo de implementación de AEM (AEM as a Cloud Service o Managed Services 6.5/6.5 LTS).

1. En el carril izquierdo, en **Programa**, haga clic en **![Icono de información general](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) Información general**.

1. En la página **Resumen del programa**, en la tarjeta **Canalizaciones**, haga clic en una canalización.

   ![Canalización seleccionada](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-select.png)

1. En la página **Escaneo de código y compilación**, observe la canalización con errores.

   ![Error de canalización como se ve en la página Generar y escanear código](/help/ai-in-aem/agents/development/assets/dev-agent-pipeline-failure.png)

1. Cerca de la esquina superior derecha de la interfaz de usuario de AEM (desde las páginas de Cloud Manager o desde la instancia de autor de los entornos de AEM), haga clic en el icono **Asistente de IA**.

   ![Icono del Asistente de IA en la barra de herramientas](/help/implementing/cloud-manager/assets/ai-assistant-icon.png)

   Consulte también [Asistente de IA en AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).

1. En el cuadro de texto del panel **Ayudante de IA** cerca de la parte inferior, escriba su pregunta o mensaje, luego presione `Enter` o haga clic en ![Enviar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   Por ejemplo:
   *En el programa &quot;eda-org-01-no-access&quot;, analice el error en la canalización &quot;sin acceso&quot; y solucione los problemas.*

   La solicitud genera la siguiente respuesta.

   ![Mensaje del Asistente de IA y respuesta resultante](/help/ai-in-aem/agents/development/assets/dev-agent-prompt-response.png)


## Permisos {#permissions}

El trabajo de solución de problemas de canalización del agente de desarrollo requiere la función Cloud Manager - Desarrollador o la función Cloud Manager - Administrador de programas.



## Ejemplos de peticiones de datos {#sample-prompts}

| Indicación | Resultado |
| --- | --- |
| *Enumerar mis canalizaciones con errores para el programa principal.* | Aunque los resultados pueden variar, este mensaje debe generar una tabla de canalizaciones fallidas, con una sugerencia de seguimiento para hacer referencia a una canalización específica para analizar. |
| *Analizar mi canalización con error llamada &quot;Canalización de desarrollo&quot;.* | Este mensaje debe resultar en un análisis de la canalización fallida con sugerencias para corregirla. |

## Funciones fuera de ámbito {#out-of-scope-features}

La resolución de problemas de la canalización funciona en el paso de compilación de la canalización de pila completa. Para otros tipos y pasos de canalización, depure los errores descargando e inspeccionando los registros.

Ver [Registros de acceso y descarga](/help/implementing/cloud-manager/manage-logs.md).

La solución de problemas de canalización no es compatible con los programas que utilizan BYOGIT (Traer su propio Git).

