---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: a1b860b4d691515f7f868e4e7e1a70bac0c20cbe
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 48%

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

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2025.12.0) fue el viernes, 11 de diciembre de 2025. La próxima versión de la funcionalidad (2026.1.0) está planificada para el viernes, 29 de enero de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!-- 

## Release Video {#release-video}

Have a look at the July 2025 Release Overview video for a summary of the features added in the 2025.7.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3440923?captions=spa&quality=12)

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

### Agentes en AEM (programa Beta) {#agents-in-aem-beta-program}

Obtenga acceso anticipado a nuevas y potentes funciones agénticas de AEM en producción, gobernanza, optimización, descubrimiento y desarrollo. Sus comentarios definen directamente el plan de Adobe y las funciones finales. Consulte [Información general sobre agentes en AEM](/help/ai-in-aem/agents/overview.md) para obtener más información.

Este programa suele durar de 4 a 6 semanas, pero se puede adaptar para ser flexible en cuanto a su capacidad de participar activamente.

Para participar en este programa, envíe un correo electrónico a [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) e incluya los siguientes detalles en la medida de lo posible:

* Nombres y nombres de los miembros del equipo de Adobe ID que utilizarán agentes de forma activa.
* Enumerar los agentes específicos que usted o su equipo desearán utilizar. O simplemente decir &quot;Todos los agentes&quot;.

### AEM Foundation (programas de Beta) {#aem-foundation-beta-programs}

Ver [programas beta de AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas de Beta) {#cloud-manager-beta-programs}

Ver [programas beta de Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Hay disponible una nueva versión del complemento Figma para la integración con AEM Assets**

* Compatibilidad con archivos de vídeo (MP4, MOV, WebM), archivos animados (GIF) y archivos vectoriales (SVG) al importar recursos del repositorio de AEM al documento de Figma.

* Compatibilidad para comprobar si hay alguna actualización de los recursos que se utilizan en el documento Figma en comparación con los recursos que existen en el repositorio de AEM y obtener la última versión de los recursos si hay alguna actualización.

* Compatibilidad con configuraciones de exportación al exportar formatos de archivo PNG (escala) y JPG (escala y calidad de imagen).

  ![Complemento Figma](/help/assets/assets/figma-v2-plugin.png)

**Detección de malware para los recursos cargados**

Los AEM Assets ahora incluyen el análisis automático de malware de los archivos cargados, lo que garantiza que los recursos sospechosos se pongan en cuarentena antes de entrar en DAM para proteger el repositorio de amenazas. Los administradores pueden configurar las opciones de análisis y las políticas de retención de cuarentena para optimizar los controles de seguridad.

**Metadatos generados por IA: actualización de idoneidad**

Los metadatos generados por IA en AEM Assets ya no requieren que el piloto de GenAI se firme para habilitarlos. La función está ahora disponible tanto para los clientes que han firmado el GenAI Rider como para los clientes que aún no han sido validados. Los clientes que se hayan excluido explícitamente del uso de GenAI seguirán teniendo la función deshabilitada. Para administrar la habilitación de características en el nivel de entorno, consulta [Deshabilitar metadatos generados por IA](/help/assets/enhance-content-discovery-with-ai-generated-metadata.md#disable-ai-generated-metadata). Este cambio se realizará para los clientes en la versión de lanzamiento 23482 o posterior.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- ### Pre-Release features in AEM Forms 

**Rule Editor Enhancements**

The Rule Editor now supports enhanced navigation and allows use of function and mathematical expressions in input parameters.

**Enhanced Navigation with Event Payload Support**
 
The `Navigate To` action in the Invoke Service handlers now supports `EVENT_PAYLOAD`, enabling form authors to configure follow-up actions based on event responses. This enhancement offers greater flexibility in designing post-submission workflows, ensuring smoother transitions and more personalized user experiences. For more information, see [Enhanced Navigation with Event Payload Support](/help/forms/invoke-service-enhancements-rule-editor.md#use-case-5-use-event-payload-in-navigate-to-action-in-invoke-service).

**Function and Mathematical Expression Support in Input Parameters**
 
Input parameters now support both function calls and mathematical expressions, enabling form authors to pass dynamically computed values directly. This enhancement streamlines rule configurations, eliminates the need for extra fields, and makes forms more adaptable to complex logic and calculation-driven scenarios. For more information, see [Function and Mathematical Expression Support in Input Parameters](/help/forms/rule-editor-core-components-user-interface.md#function-and-mathematical-expression-support-in-input-parameters). -->

### Nuevas funciones de acceso anticipado de AEM Forms {#forms-new-early-access-features}

El programa de acceso anticipado de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras y ayudar a dar forma a su desarrollo.

En estas notas de la versión se indican las innovaciones de ofrecidas en la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Mejoras en la comunicación interactiva

##### Bloqueo de plantilla

Bloquee el contenido y los elementos de diseño de las plantillas para mantener la integridad de la marca y evitar modificaciones no autorizadas. Esto garantiza la coherencia del diseño en todas las comunicaciones.

##### Compatibilidad con desbordamiento de contenido

Introducción a la opción &quot;Permitir saltos de página dentro del contenido&quot; para diseños de posición variable. Esta mejora permite una edición de varias páginas sin problemas y una mejor administración del texto para documentos complejos.

##### Edición de archivos XDP

El editor de comunicaciones interactivas ahora admite la edición XDP, incluida la integración de fragmentos. Ahora puede editar archivos XDP en un explorador en lugar de Forms Designer que solo se ejecuta en el escritorio de Microsoft Windows.

##### Numeración dinámica de páginas

Muestre automáticamente &quot;Page # of ##&quot; en las páginas maestras para una paginación clara y coherente en los documentos de varias páginas.

<!--
**Forms Optimization opportunities**

Forms Optimization uses AI to analyze your forms and suggest improvements for better performance. It highlights forms with low engagement, flags accessibility issues, and generates AI-powered variations to help increase conversion rates and compliance with WCAG standards.

>[!VIDEO](https://video.tv.adobe.com/v/3469472/) 

Key optimization opportunities include:

* Increasing visibility for forms with low views
* Improving completion rates for forms with low conversions
* Addressing accessibility compliance issues
* Streamlining navigation to enhance user experience

With Forms Optimization, you get automated, data-driven recommendations and variations, making it easier to boost engagement and ensure your forms are effective and inclusive. 
-->

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager] como [!DNL Cloud Service] nuevas características de base {#foundation-new}

#### Próximas obsolescencias de la API de Java {#java-api-deprecation}

Varias API obsoletas se marcaron para su eliminación el 31 de agosto, y por lo tanto, ya no deben utilizarse como referencia. Recibirá notificaciones del Centro de acciones si se detecta un uso de API obsoleto en el código y, después del 29 de enero, aparecerán avisos durante las compilaciones de Cloud Manager para reforzar la importancia de eliminar el uso. Consulte el [artículo sobre obsolescencia](/help/release-notes/deprecated-removed-features.md#aem-apis) para obtener más detalles, pero, para mayor comodidad, estas API se enumeran a continuación:

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
* `org.bson`
* `org.apache.jackrabbit.oak.plugins.blob`
* `org.apache.jackrabbit.oak.plugins.memory`

+++

<!--
OSGi properties:

* `org.apache.sling.commons.log.LogManager` (all properties)
* `org.apache.sling.commons.log.LogManager.factory.config` (`org.apache.sling.commons.log.file`, `org.apache.sling.commons.log.pattern`)
* 

-->

#### Desuso de tiempo de ejecución de Java 11 {#java11-runtime-deprecation}

Adobe actualizó los entornos **Stage** y **Production** al tiempo de ejecución de **Java 21 de mayor rendimiento** el 14 de octubre de 2025. A partir del **9 de febrero**, ni AEM Cloud Service SDK ni ningún entorno de nube funcionarán con el tiempo de ejecución de Java 11.

>[!NOTE]
>
> Para aprovechar las últimas optimizaciones de rendimiento y mejoras de idioma, se recomienda compilar con Java 17 o Java 21 (opción preferida). La compilación con Java 8 y Java 11 sigue siendo compatible por ahora, pero quedará obsoleta en una próxima versión. Se emitirá una comunicación independiente antes de la desaprobación. Consulte la sección *requisitos de tiempo de compilación* de [este artículo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Como se indica en las notas de la versión de abril, los registros Java de AEM deben seguir un formato estándar para garantizar una monitorización de confianza en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

A partir del **29 de enero**, se omitirán todas las invalidaciones de registro personalizadas no admitidas. Según nuestro análisis, la mayoría de los clientes no se verán afectados y Adobe se pondrá en contacto directamente con cualquier cliente cuya configuración actual pueda verse afectada.

Revise y actualice cualquier proceso descendente que dependa del comportamiento de registro personalizado. Por ejemplo:

* Si el sistema de reenvío de registros espera un formato de registro personalizado, es posible que tenga que ajustar las reglas de ingesta.
* Si anteriormente ha reducido los detalles de los registros cambiando los niveles de registro, tenga en cuenta que restablecer los niveles predeterminados podría aumentar el volumen del registro.

### Características de [!DNL Experience Manager] como [!DNL Cloud Service] pionero de la base {#foundation-early-adopter}

#### Pausar actualizaciones de mantenimiento automáticas {#pause-updates}

Días de lanzamiento, eventos en directo, picos de ventas: estos momentos no pueden fallar. [Nuestras nuevas funciones de autoservicio](/help/implementing/deploying/quiet-hours-update-free-periods.md) detienen las actualizaciones de mantenimiento automático cuando son importantes, para que sus equipos se mantengan enfocados.

* Horas de descanso: bloquea el mantenimiento automático durante las horas establecidas cada día. Ideal para horarios de trabajo, ejecuciones nocturnas o transiciones matinales.
* Período sin actualizaciones: bloquea el mantenimiento automático durante una semana completa. Utilícelo para lanzamientos, promociones o bloqueos anuales.

>[!NOTE]
>
>Disponible como función de disponibilidad limitada desde el 25 de septiembre.
>Envíe un correo electrónico a [aemcs-update-free@adobe.com](mailto:aemcs-update-free@adobe.com) para activarlo en sus programas.
>

#### Computación de Edge (programa beta)

La computación de Edge le permite ejecutar JavaScript en la capa de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

Los casos de uso comunes incluyen los siguientes:

* Personalización de contenido en función de la geolocalización, el tipo de dispositivo o los atributos del usuario
* Actuación como middleware entre la CDN y su origen
* Modificar el formato de las respuestas de API de terceros (y tal vez añadir las respuestas de varias API) antes de enviarlas al explorador
* Composición y muestra de HTML procesado por el servidor en Edge con contenido reunido de varios backend
* Exposición de un servidor MCP para LLM como ChatGPT y Claude para acceder a herramientas personalizadas

Tenemos un número limitado de oportunidades disponibles para el envío de publicaciones de AEM o para proyectos de Edge Delivery Services para sitios de producción en directo. Si está interesado en participar o desea obtener más información, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso.

#### Autenticación de Edge para Edge Delivery Services (programa Beta) {#edge-authentication}

La autenticación de Edge le permite restringir el acceso a las páginas de Edge Delivery Services únicamente a aquellas personas que se hayan autenticado con su proveedor de identidad (IdP). Esto se logra mediante la implementación de un archivo YAML de configuración de OpenID Connect (OIDC).

Si le interesa, envíe un correo electrónico a [aemcs-edgecompute-feedback@adobe.com](mailto:aemcs-edgecompute-feedback@adobe.com) con una breve descripción de su caso de uso y cualquier pregunta que pueda tener.

#### Implementaciones de producción controladas para probar el código antes de aceptar tráfico en directo (programa Beta) {#canary-beta}

Valide una compilación de producción con tráfico de prueba solamente interno antes de exponerla a los usuarios finales. Realice envíos a producción, dirija solo el tráfico controlado (mediante un encabezado especial), monitorice el comportamiento y, a continuación, promocione al tráfico en directo o revierta el proceso, sin afectar a los clientes.

Implemente las versiones de código en producción, pero restrínjalas solo al tráfico de prueba interno antes de decidir si aceptar tráfico en directo en lugar de revertir el proceso.

Envíe un correo electrónico a [aemcs-canary-deployments-beta@adobe.com](mailto:aemcs-canary-deployments-beta@adobe.com) para solicitar acceso y compartir comentarios.


#### Respuestas de IA: respuestas más inteligentes y según el contexto para AEM Sites (programa de Beta) {#ai-answers-beta}

AI Answers presenta una nueva forma en que los visitantes pueden interactuar con el contenido. Con la tecnología de recuperación de generación aumentada (RAG) , utiliza los datos administrados por AEM para ofrecer respuestas precisas y coherentes con la marca directamente dentro de sus experiencias digitales.

Nos estamos preparando para lanzar el programa Beta de respuestas de IA y ahora estamos invitando a los clientes a registrar sus intereses. Debido a que la versión beta tendrá una capacidad muy limitada, los registros tempranos recibirán una consideración prioritaria. La participación en la versión beta le permitirá explorar las respuestas de IA en su entorno de AEM Cloud Service, validar el rendimiento y la precisión y ayudar a dar forma a la experiencia futura antes de que esté disponible de forma general.

Para solicitar participación o recibir actualizaciones, comuníquese con [feedback-ai-answers@adobe.com](mailto:feedback-ai-answers@adobe.com).

#### Instantáneas para RDE (Programa Beta) {#rde-snapshot-program}

En la versión beta, los entornos de desarrollo rápido (RDE) ahora admiten una función para tomar una instantánea del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

Envíe un correo electrónico a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) si está interesado en utilizar esta función y proporcionar comentarios sobre ella.

#### Acelerar el desarrollo de AEM con IA (programa Alpha) {#ai-dev-alpha}

Los equipos de pila Java de AEM utilizan cada vez más el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar la entrega de características y mejorar la calidad del código. Estamos recopilando experiencias del mundo real para ayudar a dar forma a las futuras capacidades de IA compatibles con Adobe.

Envíe un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) para compartir lo que funciona para su equipo y lo que desea que Adobe proporcione.

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
