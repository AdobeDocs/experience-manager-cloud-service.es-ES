---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 49d29c468a2047e3026948030c3663db0beada53
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 35%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2023 o 2024.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2026.2.0) de [!DNL Cloud Service] es el miércoles, 03 de marzo de 2026. La próxima versión de funcionalidad (2026.3.0) está planificada para el viernes, 26 de marzo de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo de información general sobre la versión de febrero de 2026 para ver un resumen de las funciones añadidas en la versión 2026.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3480399/?quality=12)


## Programas de AEM Beta {#aem-beta-programs}

Los programas beta de Adobe Experience Manager (AEM) son una forma para que los clientes obtengan acceso a las funciones y el código de la versión preliminar, proporcionen comentarios y guíen el futuro de AEM.

>[!IMPORTANT]
>
>Las versiones de Beta pueden contener defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo (mediante los Servicios de soporte de Adobe o de otro modo) las versiones beta. Adobe recomienda a los clientes tener cuidado y no depender del funcionamiento o el rendimiento correctos de las versiones beta, ni de la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Por lo tanto, cualquier uso de las versiones beta es totalmente bajo el propio riesgo del cliente.

**Ventajas de participar**
El acceso anticipado a las funciones que Adobe está desarrollando permite a los clientes y socios proporcionar comentarios y dar forma al desarrollo de productos. También les ayuda a prepararse para adoptar nuevas capacidades antes de la disponibilidad general.

**Programas beta actuales**
Las siguientes secciones enumeran los programas beta activos.

### Agentes en AEM {#agents-in-aem}

Si desea explorar las nuevas y poderosas capacidades de AEM en producción, administración, optimización, detección y desarrollo, [obtenga información sobre cómo puede obtener acceso a ellas aquí.](/help/ai-in-aem/agents/overview.md)

<!--
### Agents in AEM (Explorer program) {#agents-in-aem-beta-program}

Gain early access to powerful, new AEM agentic capabilities across production, governance, optimization, discovery, and development. Your feedback directly shapes Adobe's roadmap and final features. See [Overview of Agents in AEM](/help/ai-in-aem/agents/overview.md) to learn more.

This program typically lasts 4-6 weeks, but can be tailored to be flexible around your ability to actively participate. 

To opt in to participate in this program, email [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) and include the following details to the extent possible:

* Names and Adobe ID's of team members who will actively use agents.
* List Specific agents that you or your team will want to use. Or simply say "All Agents."

Customers selected for participation will be notified directly by Adobe. Participation is subject to eligibility considerations, including customer licensing and limited program capacity. While not all requests can be accommodated initially, additional customers may be considered in future beta waves.
-->

### AEM Foundation (programas de Beta) {#aem-foundation-beta-programs}

Ver [programas beta de AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas de Beta) {#cloud-manager-beta-programs}

Consulte [Programas beta de Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Asesor de contenido para acceder a los AEM Assets de Adobe Express**

[El Asesor de contenido ya está disponible en Adobe Express](/help/assets/native-integration-adobe-express.md), e incluye la detección inteligente de recursos para AEM Assets directamente desde la interfaz Express. El Asesor de contenido proporciona recomendaciones según el contexto basadas en contenido de lienzo e informes de campaña, admite búsquedas con tecnología de IA, habilita la compatibilidad nativa con representaciones listas para el canal sobre la marcha con tecnología de Dynamic Media y muchas otras funciones. El Asesor de contenido transforma la forma en que descubre y utiliza los recursos aprobados, lo que le ayuda a encontrar el contenido adecuado más rápido para optimizar sus flujos de trabajo creativos.

### Nuevas funciones en Dynamic Media con OpenAPI {#dynamic-media-openAPI-new-features}

**Control de acceso basado en atributos (ABAC) para Dynamic Media con OpenAPI**

El control de acceso basado en atributos (ABAC) permite a los administradores controlar el acceso a Dynamic Media con recursos OpenAPI mediante reglas impulsadas por metadatos. Los administradores pueden definir reglas para grupos de usuarios basadas en metadatos de recursos para determinar qué recursos son visibles para grupos específicos. Cuando los metadatos de un recurso coinciden con las condiciones definidas, el acceso se concede automáticamente. Esta capacidad ayuda a las organizaciones a aplicar una mejor gobernanza, lo que garantiza que los usuarios solo puedan ver y trabajar con Dynamic Media con recursos de OpenAPI relevantes para su función o permisos.

>[!NOTE]
>
>El control de acceso basado en atributos (ABAC) para Dynamic Media con OpenAPI es una función de disponibilidad limitada. Puedes habilitarlo creando un [ticket de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funciones de acceso rápido de AEM Forms {#forms-early-access-features}

**Mostrar etiquetas para el menú desplegable de selección múltiple en PDF de envío**
Los componentes desplegables de selección múltiple de Adaptive Forms ahora representan las etiquetas de visualización seleccionadas en la [PDF de envío generada](/help/forms/generate-document-of-record-core-components.md), lo que garantiza que el documento refleje con precisión lo que los usuarios ven en el formulario.

**Accesibilidad mejorada para los componentes de casilla de verificación, botón de opción y panel**
Los componentes principales de Forms adaptables presentan un marcado semántico compatible con WCAG 2.2 para [grupos de casillas de verificación (v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [grupos de botones de opción (v2)](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) y [componente Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Estos componentes aprovechan `<fieldset>` y `<legend>` elementos de HTML para establecer relaciones significativas entre las etiquetas de grupo y sus opciones, lo que permite una interpretación precisa por parte de los lectores de pantalla y otras tecnologías de asistencia.

**Compatibilidad con versiones en Forms Manager**
Forms Manager ahora [admite el control de versiones para Forms adaptable (componentes principales y componentes de base)](/help/forms/manage-form-versions-forms-manager.md), fragmentos de formulario, temáticas, plantillas XDP y recursos binarios. Cree versiones, vea el historial de versiones completo y restaure estados anteriores de los recursos de formulario directamente desde la consola Forms y documentos.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] como [!DNL Cloud Service] nuevas características de base {#foundation-new}

#### Pausar actualizaciones de mantenimiento automáticas {#pause-updates}

Días de lanzamiento, eventos en directo, picos de ventas: estos momentos no pueden fallar. [Nuestras nuevas funciones de autoservicio](/help/implementing/deploying/quiet-hours-update-free-periods.md) detienen las actualizaciones de mantenimiento automático cuando son importantes, para que sus equipos se mantengan enfocados.

* Horas de descanso: bloquea el mantenimiento automático durante las horas establecidas cada día. Ideal para horarios de trabajo, ejecuciones nocturnas o transiciones matinales.
* Período sin actualizaciones: bloquea el mantenimiento automático durante una semana completa. Utilícelo para lanzamientos, promociones o bloqueos anuales.

#### Resolución de problemas de canalización de calidad de código con el agente de desarrollo {#devagent-codequality}

Las funcionalidades de solución de problemas de canalización del agente de desarrollo ayudan a los desarrolladores a diagnosticar y resolver problemas de forma más eficaz en las implementaciones de AEM as a Cloud Service.

Anteriormente centrada en el paso **Prueba de compilación y unidad**, la solución de problemas de canalización ahora también admite el paso **Escaneo de código** en la implementación de pila completa y las canalizaciones de calidad de código.

El paso Escaneo de código evalúa el código con reglas de calidad, detecta vulnerabilidades de seguridad y genera informes de calidad detallados. Si este paso falla, puede utilizar el Asistente de IA para solicitar al Agente de desarrollo un análisis de causa raíz junto con las directrices de corrección recomendadas.

Obtenga más información sobre [Agente de desarrollo](/help/ai-in-aem/agents/brand-experience/development/development.md) y la solución de problemas de canalización.

### [!DNL Experience Manager] como [!DNL Cloud Service] avisos importantes de Foundation {#foundation-notices}

#### Degradaciones de API de Java {#java-api-deprecation}

Las API obsoletas destinadas a la eliminación del 26/2/2026 ya no deben utilizarse en el código. Para evitar bloques de implementación, elimine el uso de la API antes del 30 de marzo de 2026. Fechas importantes:

* **A partir del 26 de enero de 2026**: los correos electrónicos de notificación del Centro de acciones se envían como recordatorio para eliminar el uso de estas API.
* **26 de febrero de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **se pausarán** durante el paso **Calidad del código**. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular el problema para permitir que continúe la canalización. *Esto puede ralentizar la validación y la publicación de cambios en el código.*
* **30 de marzo de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **producirán errores** durante el paso **Calidad del código**. Las implementaciones se bloquearán hasta que se elimine el uso de API obsoleto. *Esto puede impedir que publiques actualizaciones urgentes y podría afectar a las operaciones de tu empresa.*
* **4 de mayo de 2026**: Los entornos que aún utilizan API obsoletas **no recibirán actualizaciones críticas de la versión de Adobe** y no están sujetos a los compromisos estándar del Adobe sobre rendimiento y disponibilidad. Como resultado, no recibirá nuevas funciones ni correcciones de errores, la estabilidad y el tiempo de actividad de la aplicación pueden verse afectados negativamente, y la exposición a riesgos de seguridad puede aumentar aún más.

Consulte el [artículo sobre obsolescencia](/help/release-notes/deprecated-removed-features.md#aem-apis) para obtener más detalles, pero, para mayor comodidad, estas API se enumeran a continuación:

+++ Expandir para ver las funciones obsoletas de la API de Java

* `org.apache.sling.commons.auth`
* `org.apache.felix.webconsole`
* `org.eclipse.jetty`
* `com.mongodb`
* `org.apache.abdera`
* `org.apache.felix.http.whiteboard`
* `org.apache.cocoon.xml`
* `ch.qos.logback`
* `org.slf4j.spi`
* `org.slf4j.event`
* `org.apache.log4j`
* `com.google.common`
* `com.drew`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

### Características de [!DNL Experience Manager] como [!DNL Cloud Service] pionero de la base {#foundation-early-adopter}

#### Funciones de AEM Edge (programa Beta) {#edge-functions}

Las funciones de Edge de AEM le permiten ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

#### Servidor MCP de Cloud Manager (programa Beta) {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

Los IDE modernos utilizan el Protocolo de contexto de modelo (MCP) para permitir que los modelos de lenguaje de gran tamaño (LLM) invoquen las herramientas expuestas por los servidores MCP. En lugar de integrarse directamente con especificaciones de API de bajo nivel, los desarrolladores pueden simplemente describir su intención en lenguaje natural.

Ahora disponible en versión beta, el servidor MCP de Cloud Manager le permite interactuar con las API de Cloud Manager directamente desde el IDE mediante mensajes. Los escenarios admitidos incluyen la ejecución de canalizaciones, la comprobación del estado del entorno y más.

Más información sobre [Servidores MCP de AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Para solicitar acceso al servidor beta de Cloud Manager MCP, envíe un mensaje de correo electrónico a [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com) e incluya una descripción de su caso de uso.

#### Solución de problemas de canalización de configuración de nivel web con el agente de desarrollo (programa beta) {#devagent-webtier}

Las capacidades de [solución de problemas de canalización](/help/ai-in-aem/agents/brand-experience/development/development.md) del Agente de desarrollo ayudan a los desarrolladores a diagnosticar y resolver problemas de manera eficiente en AEM como implementaciones de Cloud Service. Además de admitir canalizaciones de pila completa (implementación y calidad de código), el agente de desarrollo ahora admite la solución de problemas para la **canalización de configuración de nivel web** como parte de un programa beta.

Para solicitar acceso a la versión beta, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). Se requiere el acceso preexistente a los agentes en AEM.

#### Herramientas de IA del IDE para el desarrollo de AEM Java y Dispatcher (programa de Beta) {#ai-dev-beta}

Los equipos de pila de Java utilizan cada vez más el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar la entrega de características y mejorar la calidad del código. Únase a la versión beta para lo siguiente:

* Comparta experiencias del mundo real para ayudar a dar forma a las futuras capacidades de IA admitidas por Adobe
* Pruebe las herramientas IDE que los agentes de IA pueden utilizar para generar y depurar el código de AEM y la configuración de Dispatcher

Envíe un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) para obtener más información.

#### Herramientas de IA del IDE para la migración de AEM 6.5 a AEM Cloud Service (programa de Alpha) {#cm-ide-migration}

Acelere la migración de AEM 6.5 a AEM as a Cloud Service (pila de Java) mediante la herramienta de IA del IDE para seguir las recomendaciones del [Informe del analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) para obtener más información.

#### Autenticación de Edge para Edge Delivery Services (programa Beta) {#edge-authentication}

La autenticación de Edge le permite restringir el acceso a las páginas de Edge Delivery Services únicamente a aquellas personas que se hayan autenticado con su proveedor de identidad (IdP). Esto se logra mediante la implementación de un archivo YAML de configuración de OpenID Connect (OIDC).

Si le interesa, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso y cualquier pregunta que pueda tener.

#### Implementaciones de producción controladas para probar el código antes de aceptar tráfico en directo (programa Beta) {#canary-beta}

Valide una compilación de producción con tráfico de prueba solamente interno antes de exponerla a los usuarios finales. Realice envíos a producción, dirija solo el tráfico controlado (mediante un encabezado especial), monitorice el comportamiento y, a continuación, promocione al tráfico en directo o revierta el proceso, sin afectar a los clientes.

Implemente las versiones de código en producción, pero restrínjalas solo al tráfico de prueba interno antes de decidir si aceptar tráfico en directo en lugar de revertir el proceso.

Envíe un correo electrónico a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acceso y compartir comentarios.

#### Instantáneas para RDE (Programa Beta) {#rde-snapshot-program}

En la versión beta, los entornos de desarrollo rápido (RDE) ahora admiten una función para tomar una instantánea del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

Envíe un correo electrónico a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) si está interesado en utilizar esta función y proporcionar comentarios sobre ella.

#### Monitorización del rendimiento de las aplicaciones (APM) ampliadas (programa Alpha) {#apm-alpha}

En cuanto a la observabilidad, AEM Cloud Service admite actualmente [New Relic One](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/user-access-new-relic) proporcionado por Adobe y [Dynatrace](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/dynatrace) administrado por el cliente. Mientras exploramos la compatibilidad con opciones de APM adicionales, envíenos un correo electrónico [aemcs-apm-beta@adobe.com](mailto:aemcs-apm-beta@adobe.com) con su proveedor o tecnología preferidos, junto con casos de uso.

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Puede encontrar una lista completa de las versiones del editor universal [aquí](/help/release-notes/universal-editor/current.md).

## Generar variaciones {#generate-variations}

Puede encontrar una lista completa de las versiones de generar variaciones [aquí](/help/generative-ai/release-notes-generate-variations.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
