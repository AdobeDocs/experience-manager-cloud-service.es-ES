---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 95e2216ee79433783da384134243f3688ff7797d
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 30%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] versión de característica actual (2026.4.0) es el 30 de abril de 2026. La próxima versión de la funcionalidad (2026.5.0) está planificada para el 28 de mayo de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 
## Release Video {#release-video}

Have a look at the April 2026 Release Overview video for a summary of the features added in the 2026.4.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3483060/?quality=12)
-->

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

Ver [programas beta de Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Integración de traducción de AI {#ai-translation-integration}

Los usuarios de AEM ahora pueden aprovechar los modelos de idiomas grandes (LLM) para la traducción de contenido, lo que ofrece calidad de traducción humana a velocidad de traducción automática. Al igual que los servicios de traducción tradicionales de terceros, Azure OpenAI puede configurarse como proveedor de traducción en AEM, con compatibilidad con LLM adicionales planificados para futuras versiones. Los clientes utilizan sus propias licencias LLM para esta capacidad. Además, las guías de estilo de traducción corporativa se pueden cargar en AEM, lo que permite extraer reglas de traducción para garantizar la coherencia de marca y estilo. Consulte [Configuración de la integración de traducción de IA](/help/sites-cloud/administering/translation/ai-translation-integration.md) para obtener más información.

### Editor de fragmentos de contenido {#cf-editor}

El nuevo Editor de fragmentos de contenido ahora le permite previsualizar la representación JSON de un fragmento de contenido. Esto ayuda a validar la estructura de contenido independientemente del procesamiento y restaura la paridad con el editor de fragmentos de contenido anterior en la interfaz de usuario táctil de AEM para esta capacidad.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Asesor de contenido ya disponible para aplicaciones de Adobe Workfront y que no son de Adobe**

El Asesor de contenido ya está disponible para aplicaciones de Adobe Workfront y que no sean de Adobe (terceros), lo que amplía la detección inteligente de recursos y la reutilización de contenido más allá de Adobe Express y AEM Sites. Esta versión ofrece toda la experiencia del Asesor de contenido, incluida la búsqueda basada en IA, las recomendaciones según el contexto, la detección basada en instrucciones de campaña, el acceso a representaciones de Dynamic Media, la detección de fragmentos de contenido, los filtros y los metadatos de recursos a flujos de trabajo de Adobe Workfront y aplicaciones externas.

Ahora puede detectar, evaluar y reutilizar recursos aprobados de AEM Assets directamente en sus aplicaciones preferidas, lo que permite un uso coherente de los recursos, una mayor eficacia y una creación de contenido optimizada en las aplicaciones de Adobe y que no sean de Adobe.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms

* **Anular la configuración de nube de reCAPTCHA con OSGi** 
Los ID de proyecto empresarial, las claves de sitio y los secretos de reCAPTCHA que mantenga con sus archivos de origen pueden resolverse en valores diferentes en cada entorno de Cloud Service después de [agregar la anulación e implementación de la configuración según el contexto mediante Cloud Manager](/help/forms/captcha-adaptive-forms.md#override-recaptcha-osgi).

* **Autenticación basada en certificados** 
Los Forms adaptables que se envían a una lista de SharePoint de Microsoft ahora admiten la [autenticación basada en certificados](/help/forms/connect-forms-to-sharepoint-list.md#certificate-based-authentication) junto con la autenticación de URL de OAuth. Para el inicio de sesión basado en certificados, registre un alias de certificado y detalles del inquilino en AEM y Microsoft Azure.

* **Mejoras en el editor de reglas**

   * El editor de reglas de Forms adaptable ahora admite la gramática simplificada para las reglas de [Evento de envío y Evento de Déclencheur para los déclencheur listos para usar (OOTB) y para los eventos personalizados](/help/forms/rule-editor-enhancements-use-cases.md#simplified-grammar-for-ootb-and-custom-events), de modo que los autores no se limitan únicamente a la gramática en los déclencheur personalizados.
   * Cuando las reglas de Forms adaptable basadas en componentes principales ahora incluyen el componente [Archivo adjunto junto con otras condiciones que utilizan la lógica AND u OR](/help/forms/rule-editor-enhancements-use-cases.md#combined-when-conditions-with-the-file-attachment-component), de modo que la regla ejecuta sus acciones solo cuando el estado del archivo adjunto y las demás comprobaciones se evalúan según lo previsto.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] como [!DNL Cloud Service] nuevas características de base {#foundation-new}

#### Herramientas de IA del IDE para AEM Java y desarrollo de Dispatcher {#ai-dev}

Los equipos de pila de Java utilizan cada vez más el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar la entrega de características y mejorar la calidad del código.

Los agentes de codificación pueden utilizar las herramientas IDE para generar y depurar el código AEM y la configuración de Dispatcher. Como ejemplo, el tutorial de vídeo siguiente muestra la creación de un componente de AEM mediante las habilidades de agente.

Obtenga más información sobre [Desarrollo local con herramientas de IA](/help/ai-in-aem/local-development-with-ai-tools.md) y no dude en enviar un correo electrónico a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) con preguntas o comentarios.


>[!VIDEO](https://video.tv.adobe.com/v/3484978/?learn=on&enablevpops)

#### Servidor MCP de Experience Governance {#gov-mcp-server}

### Nuevas funciones en AEM Forms {#forms-new-features}

**Compatibilidad con versiones en Forms Manager**
Forms Manager ahora [admite el control de versiones para Forms adaptable (componentes principales y componentes de base)](/help/forms/manage-form-versions-forms-manager.md), fragmentos de formulario, temáticas, plantillas XDP y recursos binarios. Cree versiones, vea el historial de versiones completo y restaure estados anteriores de los recursos de formulario directamente desde la consola Forms y documentos.

### Funciones de acceso rápido de AEM Forms {#forms-early-access-features}

Experience Governance MCP Server ya está disponible de forma general (GA). Se integra con las herramientas para desarrolladores de IA y bots de chat que admiten el Protocolo de contexto de modelo (MCP), lo que le permite salvaguardar la integridad y el cumplimiento de la marca mediante indicadores de lenguaje natural en su bot de chat o IDE. Puede evaluar el contenido (texto, imágenes, páginas) con reglas de gobernanza de marca y recuperar las configuraciones de marca y las comprobaciones de gobernanza disponibles.

Obtenga más información acerca de [AEM MCP Servers](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md) y el [Agente de control](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview).


>[!VIDEO](https://video.tv.adobe.com/v/3486258/?learn=on&enablevpops)

#### Conector de Claude {#aem-claude-connector}

Los usuarios de Claude pueden examinar el [mercado de conectores](https://claude.ai/settings/connectors) de Anthropic para instalar con un solo clic el [conector Adobe Experience Manager](/help/ai-in-aem/mcp-support/setup-claude.md#aem-claude-connector). Este servidor MCP expone un conjunto cada vez más amplio de herramientas para interactuar con AEM, incluida la edición de contenido mediante mensajes.

#### AEM OIDC en Publicar nuevas funciones {#aem-oidc-on-publish-new-features}

* Corrección: Los parámetros de consulta de la solicitud original se pierden tras la autenticación
* Redirección personalizada después de la autenticación en la [documentación de autenticación de OIDC](/help/security/open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier.md#custom-redirect-after-authentication)

#### Compatibilidad del servicio de correo con la API de Microsoft Graph {#mail-service-graph-api}

El servicio de correo de AEM ahora es compatible con Microsoft® Outlook (a través de Microsoft 365) mediante la API de Microsoft Graph. Esto resulta especialmente útil para las organizaciones que no permiten SMTP, que ya es compatible con el servicio de correo. La autenticación se realiza mediante OAuth 2.0. [Aprenda a configurar](/help/security/oauth2-support-for-mail-service.md#microsoft-graph-api).

#### Los registros de CDN se pueden reenviar a la lógica de sumo {#sumo-cdn-logforwarding}

La [función de reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md#sumologic) ahora admite el envío de registros de CDN a la lógica de sumo. Anteriormente, el reenvío de registros a Sumo Logic se limitaba a registros de AEM.

### [!DNL Experience Manager] como [!DNL Cloud Service] avisos importantes de Foundation {#foundation-notices}

#### Errores enriquecidos de autenticación IMS {#ims-auth-rich-errors}

Para solucionar problemas de integraciones de IMS, `imsauth` ha agregado compatibilidad con *errores enriquecidos*.

En lugar de devolver únicamente un código de estado HTTP, estos errores proporcionan un contexto adicional para ayudar a diagnosticar y resolver los problemas que pueden bloquear la autenticación y el acceso.

#### Degradaciones de API de Java {#java-api-deprecation}

Es fundamental eliminar el uso de API obsoletas.

Desde el **14 de abril**, las canalizaciones de Cloud Manager que contienen código mediante API cuyo objetivo es la eliminación el 26/2/2026 **fallan durante el paso Calidad del código**. Las implementaciones se bloquearán hasta que se elimine el uso de API obsoleto. *Esto puede impedir que publique actualizaciones con plazos específicos y podría afectar a las operaciones de su empresa.*

A partir del **11 de junio de 2026**, los entornos que sigan usando estas API obsoletas **no recibirán actualizaciones críticas de la versión de Adobe** y no estarán sujetos a los compromisos estándar de Adobe en cuanto a rendimiento y disponibilidad. Como resultado, no recibirá nuevas funciones ni correcciones de errores, la estabilidad y el tiempo de actividad de la aplicación podrían verse afectados negativamente y la exposición al riesgo de seguridad podría aumentar aún más.

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

### Características de [!DNL Experience Manager] como [!DNL Cloud Service] pionero de la base {#foundation-early-adopter}

#### Funciones de AEM Edge (programa Beta) {#edge-functions}

[Funciones de Edge de AEM](/help/implementing/developing/introduction/edge-functions.md) le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exponer un servidor MCP para asistentes de IA como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

#### Solución de problemas de canalización de configuración de nivel web (programa Beta) {#devagent-webtier}

Las funcionalidades de [solución de problemas de canalización](/help/ai-in-aem/agents/brand-experience/development/development.md) del agente de desarrollo ayudan a los desarrolladores a diagnosticar y resolver problemas de forma eficaz en las implementaciones de AEM as a Cloud Service. Además de admitir canalizaciones de pila completa (implementación y calidad de código), el agente de desarrollo ahora admite la solución de problemas para la **canalización de configuración de nivel web** como parte de un programa beta.

Para solicitar acceso a la versión beta, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). Se requiere el acceso preexistente a los agentes en AEM.

#### Resolución de problemas de replicación de IA (programa Alpha) {#replication-ai-troubleshooting-alpha}

Con el Asistente de IA en AEM Author y otras interfaces, puede solucionar problemas relacionados con la replicación, como colas bloqueadas. Para unirse al programa Alpha, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com) en el que describa su interés.

#### Herramientas de IA del IDE para la migración de AEM 6.5 a AEM Cloud Service (programa de Beta) {#cm-ide-migration}

Acelere la migración de AEM 6.5 a AEM as a Cloud Service (pila de Java) mediante la herramienta de IA del IDE para seguir las recomendaciones del [Informe del analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Envíe un correo electrónico a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) para obtener más información y solicitar acceso a la función.

#### Autenticación de Edge para Edge Delivery Services (programa Beta) {#edge-authentication}

La autenticación de Edge le permite restringir el acceso a las páginas de Edge Delivery Services únicamente a aquellas personas que se hayan autenticado con su proveedor de identidad (IdP). Esto se logra mediante la implementación de un archivo YAML de configuración de OpenID Connect (OIDC).

Si le interesa, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso y cualquier pregunta que pueda tener.

#### Implementaciones de producción controladas para probar el código antes de aceptar tráfico en directo (programa Beta) {#canary-beta}

Valide una compilación de producción con tráfico de prueba solamente interno antes de exponerla a los usuarios finales. Realice envíos a producción, dirija solo el tráfico controlado (mediante un encabezado especial), monitorice el comportamiento y, a continuación, promocione al tráfico en directo o revierta el proceso, sin afectar a los clientes.

Envíe un correo electrónico a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acceso y compartir comentarios.

#### Instantáneas para RDE (Programa Beta) {#rde-snapshot-program}

En la versión beta, los entornos de desarrollo rápido (RDE) ahora admiten una característica [para tomar una instantánea](/help/implementing/developing/introduction/rapid-development-environments.md#snapshots) del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

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
