---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 0c2d61f05d8a6adea1116406b18aa1245ff701d1
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 28%

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

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2026.3.0) de [!DNL Cloud Service] es el viernes, 26 de marzo de 2026. La próxima versión con funcionalidades (2026.4.0) está planificada para el viernes, 30 de abril de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the March 2026 Release Overview video for a summary of the features added in the 2026.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3480399/?quality=12)

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

### Extracción/entrada de fragmentos de contenido {#cf-checkout-in}

Para mejorar la paridad con la IU táctil de AEM, los fragmentos de contenido ahora se pueden desproteger y volver a proteger mediante la nueva IU de administración de fragmentos de contenido. La funcionalidad de desprotección no cambia, lo que bloquea de manera efectiva un fragmento de contenido desprotegido y, por lo tanto, evita que otros usuarios lo editen en el Editor de fragmentos de contenido. Los usuarios que sean propietarios de un fragmento de contenido y los administradores pueden desproteger el fragmento y volver a protegerlo. La extracción de un fragmento no afecta a los fragmentos o recursos secundarios a los que se hace referencia.

### El fragmento de contenido inicia el panel Trabajos {#cf-launches-jobs}

Los trabajos asincrónicos para inicios de fragmentos de contenido ahora se pueden ver en el panel de propiedades de la interfaz de usuario de administración de inicios de fragmentos de contenido para observar su estado: si un trabajo aún se está ejecutando, se ha completado o se ha anulado, junto con información detallada relevante sobre el trabajo.

### Actualización a RTE del Editor de fragmentos de contenido {#cf-rte-update}

El editor de texto enriquecido (RTE) del editor de fragmentos de contenido se migró de TinyMCE a TipTap. Este cambio trae consigo una serie de ventajas.

* El editor universal y el editor de fragmentos de contenido ahora utilizan la misma pila de tecnología RTE.
   * Esto significa que ambos editores ahora producen el mismo HTML.
   * Ahora, las extensiones se pueden reutilizar.
   * Ahora están disponibles las mismas funciones y métodos con ambos editores (en casos de uso sin encabezado).
   * El objetivo final es que una configuración lleve a una experiencia unificada en ambos editores.
* El editor de contenido tiene ahora un nuevo aspecto en el estilo Spectrum 2.
* Hay nueva funcionalidad disponible en el Editor de fragmentos de contenido, que incluye buscar y reemplazar y estar preparado para el asesor de contenido.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Asesor de contenido en AEM Sites**

El Asesor de contenido ya está disponible en AEM Sites e incluye la detección inteligente de recursos por parte de los AEM Assets directamente. Permite a los usuarios descubrir, examinar y reutilizar los recursos más relevantes directamente en su flujo de trabajo, lo que elimina la necesidad de cambiar de contexto.

El Asesor de contenido proporciona funciones inteligentes para recursos como sugerencias basadas en instrucciones de campaña, sugerencias contextuales, acceso a representaciones de Dynamic Media y metadatos de recursos detallados.

Próximamente: compatibilidad del Asesor de contenido con las aplicaciones B2C de Adobe Workfront y AJO, incluida la capacidad de detectar fragmentos de contenido

### Nuevas funciones de Dynamic Media {#dynamic-media-new-features}

#### Actualizaciones del Editor de plantillas de Dynamic Media {#dynamic-media-template-editor-updates}

**Mejoras en la administración de capas**

* Reordenación de capas de arrastrar y soltar: ahora las capas se pueden reordenar directamente en el panel Capas arrastrando, lo que proporciona una forma más rápida e intuitiva de organizar el orden de apilamiento de capas más allá de las acciones Traer adelante o Enviar atrás existentes.
* Copiar, pegar y duplicar: compatibilidad total para copiar, pegar y duplicar capas mediante métodos abreviados de teclado (Cmd/Ctrl+C, V, D) o el menú contextual, con compatibilidad para selecciones de varias capas.
* Botón Separar propiedades de capa: se ha añadido un botón específico Propiedades de capa para facilitar la navegación a la configuración de capa, con compatibilidad con doble clic en las capas para acceder rápidamente a ellas.

**Características de formato de texto**

* Control de interlineado: el nuevo regulador de interlineado permite un control preciso del alto de la línea en las capas de texto, con compatibilidad total de extremo a extremo, incluidas las operaciones deshacer/rehacer y guardar/cargar plantillas.
* Formato de todas las mayúsculas: las capas de texto ahora admiten la opción Formato de todas las mayúsculas en la barra de herramientas Estilo de fuente junto con Negrita, Cursiva y Subrayado.
* Opciones de alineación vertical: se han agregado controles de alineación vertical para las capas de texto, lo que permite colocar el texto con mayor precisión en los cuadros de texto.

**Controles de tamaño y Dimension**

* Desbloqueo de relación de aspecto: los usuarios ahora pueden desbloquear la relación de aspecto al ajustar las propiedades de tamaño, lo que permite ajustes independientes de anchura y altura para un tamaño de capa más flexible.
* Configuración de líneas de ajuste de texto: se ha agregado compatibilidad con los ajustes `copyfitlines` y `copyfitmaxlines` en las propiedades de ajuste de texto, lo que proporciona un control más preciso sobre el comportamiento de ajuste de texto.

**Polaco visual**

* Iconos actualizados para capas de Timer y Shape con iconos refinados del sistema de diseño Spectrum 2 (S2).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Funciones de acceso rápido de AEM Forms {#forms-early-access-features}

**Mostrar etiquetas para el menú desplegable de selección múltiple en PDF de envío**
Los componentes desplegables de selección múltiple de Adaptive Forms ahora representan las etiquetas de visualización seleccionadas en la [PDF de envío generada](/help/forms/generate-document-of-record-core-components.md), lo que garantiza que el documento refleje con precisión lo que los usuarios ven en el formulario.

**Accesibilidad mejorada para los componentes de casilla de verificación, botón de opción y panel**
Los componentes principales de Forms adaptables presentan un marcado semántico compatible con WCAG 2.2 para [grupos de casillas de verificación (v2)](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group), [grupos de botones de opción (v2)](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button) y [componente Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Estos componentes aprovechan `<fieldset>` y `<legend>` elementos de HTML para establecer relaciones significativas entre las etiquetas de grupo y sus opciones, lo que permite una interpretación precisa por parte de los lectores de pantalla y otras tecnologías de asistencia.

**Compatibilidad con versiones en Forms Manager**
Forms Manager ahora [admite el control de versiones para Forms adaptable (componentes principales y componentes de base)](/help/forms/manage-form-versions-forms-manager.md), fragmentos de formulario, temáticas, plantillas XDP y recursos binarios. Cree versiones, vea el historial de versiones completo y restaure estados anteriores de los recursos de formulario directamente desde la consola Forms y documentos.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] como [!DNL Cloud Service] nuevas características de base {#foundation-new}

#### Administración simplificada de índices {#simplified-index-management}

[Administración simplificada de índices](https://oak-indexing.github.io/oakTools/simplified.html) proporciona una forma más sencilla de definir índices personalizados y personalizar índices listos para usar (OOTB) mediante un archivo JSON, sin copiar definiciones completas ni administrar versiones manualmente. Las personalizaciones se combinan con el índice OOTB más reciente y se crea una nueva versión de índice cuando es necesario.

#### Servidor MCP de Cloud Manager {#cm-mcp-server}

>[!VIDEO](https://video.tv.adobe.com/v/3480340/?quality=12)

Los IDE modernos utilizan el Protocolo de contexto de modelo (MCP) para permitir que los modelos de lenguaje de gran tamaño (LLM) invoquen las herramientas expuestas por los servidores MCP. En lugar de integrarse directamente con especificaciones de API de bajo nivel, los desarrolladores pueden simplemente describir su intención en lenguaje natural.

El servidor MCP de Cloud Manager le permite interactuar con las API de Cloud Manager directamente desde el IDE mediante mensajes. Los escenarios admitidos incluyen la ejecución de canalizaciones, la comprobación del estado del entorno y más.

Más información sobre [Servidores MCP de AEM](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

### [!DNL Experience Manager] como [!DNL Cloud Service] avisos importantes de Foundation {#foundation-notices}

#### Degradaciones de API de Java {#java-api-deprecation}

Las API obsoletas destinadas a la eliminación del 26/2/2026 ya no deben utilizarse en el código. Para evitar bloqueos de implementación, elimine el uso de la API antes del **30 de marzo de 2026**. Fechas importantes:

* **A partir del 26 de enero de 2026**: los correos electrónicos de notificación del Centro de acciones se envían como recordatorio para eliminar el uso de estas API.
* **26 de febrero de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **se pausarán** durante el paso **Calidad del código**. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular el problema para permitir que continúe la canalización. *Esto puede ralentizar la validación y la publicación de cambios en el código.*
* **30 de marzo de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **producirán errores** durante el paso **Calidad del código**. Las implementaciones se bloquearán hasta que se elimine el uso de API obsoleto. *Esto puede impedir que publique actualizaciones con plazos específicos y podría afectar a las operaciones de su empresa.*
* **4 de mayo de 2026**: Los entornos que aún utilicen API obsoletas **no recibirán actualizaciones críticas de la versión de Adobe** y no estarán sujetos a los compromisos estándar de Adobe en cuanto a rendimiento y disponibilidad. Como resultado, no recibirá nuevas funciones ni correcciones de errores, la estabilidad y el tiempo de actividad de la aplicación podrían verse afectados negativamente y la exposición al riesgo de seguridad podría aumentar aún más.

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

#### Herramientas de IA del IDE para el desarrollo de AEM Java y Dispatcher (programa público de Beta) {#ai-dev-beta}

Los equipos de pila de Java utilizan cada vez más el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar la entrega de características y mejorar la calidad del código.

Participe en la versión beta pública (no es necesario registrarse) para probar las herramientas IDE que los agentes de codificación pueden utilizar para generar y depurar el código AEM y la configuración de Dispatcher.

Obtenga más información en la documentación beta de [Desarrollo local con herramientas de IA](/help/ai-in-aem/local-development-with-ai-tools.md) y envíe un correo electrónico a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) con preguntas o comentarios.

#### Funciones de AEM Edge (programa Beta) {#edge-functions}

Las funciones de Edge de AEM le permiten ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

#### Solución de problemas de canalización de configuración de nivel web con el agente de desarrollo (programa Beta) {#devagent-webtier}

Las funcionalidades de [solución de problemas de canalización](/help/ai-in-aem/agents/brand-experience/development/development.md) del agente de desarrollo ayudan a los desarrolladores a diagnosticar y resolver problemas de forma eficaz en las implementaciones de AEM as a Cloud Service. Además de admitir canalizaciones de pila completa (implementación y calidad de código), el agente de desarrollo ahora admite la solución de problemas para la **canalización de configuración de nivel web** como parte de un programa beta.

Para solicitar acceso a la versión beta, envíe un correo electrónico a [aem-devagent@adobe.com](mailto:aem-devagent@adobe.com). Se requiere el acceso preexistente a los agentes en AEM.

#### Herramientas de IA del IDE para la migración de AEM 6.5 a AEM Cloud Service (programa de Alpha) {#cm-ide-migration}

Acelere la migración de AEM 6.5 a AEM as a Cloud Service (pila de Java) mediante la herramienta de IA del IDE para seguir las recomendaciones del [Informe del analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

Envíe un correo electrónico a [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com) para obtener más información.

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
