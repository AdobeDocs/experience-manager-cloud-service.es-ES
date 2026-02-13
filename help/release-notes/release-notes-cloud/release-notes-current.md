---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager] as a Cloud Service
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: 087c29ddd1dcfe0fc4bda7428d71a5e6157e1325
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 40%

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

La fecha de la versión de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2026.1.0) de [!DNL Cloud Service] es el viernes, 29 de enero de 2026. La próxima versión de funcionalidad (2026.2.0) está planificada para el viernes, 26 de febrero de 2026.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de enero de 2026 para ver un resumen de las funciones añadidas en la versión 2026.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3479789/?quality=12)


## Programas de AEM Beta {#aem-beta-programs}

Los programas beta de Adobe Experience Manager (AEM) son una forma para que los clientes obtengan acceso a las funciones y el código de la versión preliminar, proporcionen comentarios y guíen el futuro de AEM.

>[!IMPORTANT]
>
>Las versiones de Beta pueden contener defectos y se proporcionan &quot;TAL CUAL&quot; sin garantía de ningún tipo. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o admitir de otro modo (mediante los Servicios de soporte de Adobe o de otro modo) las versiones beta. Adobe recomienda a los clientes tener cuidado y no depender del funcionamiento o el rendimiento correctos de las versiones beta, ni de la documentación o los materiales adjuntos. Las funciones y las API de la versión beta están sujetas a cambios sin previo aviso. Por lo tanto, cualquier uso de las versiones beta es totalmente bajo el propio riesgo del cliente.

**Ventajas de participar**
El acceso anticipado a las funciones que Adobe está desarrollando permite a los clientes y socios proporcionar comentarios y dar forma al desarrollo de productos. También les ayuda a prepararse para adoptar nuevas capacidades antes de la disponibilidad general.

**Programas beta actuales**
Las siguientes secciones enumeran los programas beta y Explorer activos.

### Agentes en AEM (programa Explorer) {#agents-in-aem-beta-program}

Obtenga acceso anticipado a nuevas y potentes funciones agénticas de AEM en producción, gobernanza, optimización, descubrimiento y desarrollo. Sus comentarios definen directamente el plan de Adobe y las funciones finales. Consulte [Información general sobre agentes en AEM](/help/ai-in-aem/agents/overview.md) para obtener más información.

Este programa suele durar de 4 a 6 semanas, pero se puede adaptar para ser flexible en cuanto a su capacidad de participar activamente.

Para participar en este programa, envíe un correo electrónico a [aemagentsteam@adobe.com](mailto:aemagentsteam@adobe.com) e incluya los siguientes detalles en la medida de lo posible:

* Nombres y nombres de los miembros del equipo de Adobe ID que utilizarán agentes de forma activa.
* Enumerar los agentes específicos que usted o su equipo desearán utilizar. O simplemente decir &quot;Todos los agentes&quot;.

Adobe notificará directamente a los clientes seleccionados para la participación. La participación está sujeta a consideraciones de elegibilidad, incluidas las licencias de cliente y la capacidad limitada del programa. Aunque no todas las solicitudes se pueden satisfacer inicialmente, es posible que en futuras olas beta se consideren clientes adicionales.

### AEM Foundation (programas de Beta) {#aem-foundation-beta-programs}

Ver [programas beta de AEM Foundation](#foundation-early-adopter).

### Cloud Manager (programas de Beta) {#cloud-manager-beta-programs}

Ver [programas beta de Cloud Manager](/help/implementing/cloud-manager/release-notes/current.md).

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Servidor MCP de contenido {#content-MCP}

AEM Cloud Service ahora incluye **Servidores MCP de contenido**, lo que ofrece una forma estandarizada para que las experiencias con tecnología de IA funcionen con contenido de AEM mediante herramientas compatibles con MCP.

Los desarrolladores y usuarios avanzados que trabajan en aplicaciones de chat y plataformas de agente pueden conectar AEM a copilotos y automatizaciones personalizadas, de modo que el trabajo de contenido forme parte de flujos de trabajo empresariales integrales.

AEM proporciona dos servidores:

1. **Servidor MCP con contenido de solo lectura** - para recuperar contenido de forma segura
1. **Servidor MCP de contenido de lectura y escritura** - para realizar cambios en el contenido

Estos servidores MCP incluyen herramientas para trabajar con **Páginas**, **Fragmentos de contenido** y **Assets**, y se pueden usar desde los siguientes clientes MCP: **ChatGPT**, **Claude**, **Cursor** y **Microsoft Copilot Studio**.

Más información en [Uso de MCP con AEM Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md). Si tiene preguntas o comentarios, envíe un correo electrónico a [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Búsqueda por IA**

La búsqueda por IA presenta una experiencia de búsqueda inteligente según el contexto que va más allá de la coincidencia de palabras clave tradicional al comprender el significado y la intención detrás de las consultas del usuario. Con la tecnología de la IA y el aprendizaje automático, ofrece resultados más precisos incluso cuando las consultas se formulan de forma diferente, contienen errores ortográficos, utilizan sinónimos o se envían en diferentes idiomas, lo que ayuda a los usuarios a encontrar contenido relevante más rápido y con menos esfuerzo.

Para obtener más información, consulte Búsqueda por IA en [Assets view](/help/assets/search-assets-view.md#ai-search) y [Admin view](/help/assets/search-assets.md#ai-search).

**Versión de aplicación de escritorio 3.0.1**

[Desktop App 3.0.1 (20 de diciembre de 2025)](https://experienceleague.adobe.com/es/docs/experience-manager-desktop-app/using/release-notes) mejora la confiabilidad, el rendimiento y la estabilidad en los flujos de trabajo clave. Esta versión garantiza una nomenclatura de carpetas coherente al corregir los problemas de sincronización con AEM Author, permite un uso ininterrumpido de la aplicación durante las transferencias activas, mejora la capacidad de respuesta de la interfaz de usuario mediante el procesamiento asincrónico, optimiza las transferencias de archivos grandes con la paginación y resuelve los problemas de estabilidad, incluidos los reinicios y bloqueos del servidor de creación durante las cargas y descargas de carpetas grandes.

**Versión de Adobe Asset Link CEP 2026.01.0**

[Adobe Asset Link CEP 2026.01.0](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html?lang=es) presenta una nueva opción para volver a vincular los vínculos que faltan en InDesign que vuelve a vincular automáticamente otros recursos que faltan en la misma carpeta de AEM. La función coincide con los recursos en función del nombre de archivo, lo que reduce considerablemente el esfuerzo manual al restaurar los vínculos rotos.


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

**Mejoras en el marcador de posición de nota al pie en Forms adaptable (componentes de base)**

* Se ha agregado compatibilidad con [varias líneas con saltos de línea](/help/forms/footnotes-richtextsupport.md), lo que permite una presentación más clara y expresiva del contenido de las notas al pie.
* Las notas al pie ahora permanecen visibles de forma persistente dentro del marcador de posición de nota al pie, independientemente de la visibilidad de los paneles asociados, lo que garantiza un acceso coherente a la información crítica.
  ![Descripción de la nota al pie](/help/forms/assets/footnote-description.png){height=50%}

### Nuevas funciones de acceso anticipado de AEM Forms {#forms-new-early-access-features}

**Recuperar valores de una matriz JSON**

Se han expandido las funcionalidades personalizadas para [extraer valores de matrices JSON](/help/forms/invoke-service-enhancements-rule-editor.md#retrieve-property-values-from-a-json-array), que se reciben a través de una llamada de API y enlazarlos directamente a los campos del formulario adaptable. Ahora puede desarrollar lógica y reglas empresariales con una asignación de datos manual mínima.

**Ejecutar la IU asociada en una instancia de publicación**

Ahora puede ejecutar la [IU asociada](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md) directamente en instancias de publicación. Esto permite a los agentes acceder a la interfaz de usuario de Associate y personalizar fácilmente las comunicaciones para los clientes.

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

### [!DNL Experience Manager] como [!DNL Cloud Service] avisos importantes de Foundation {#foundation-notices}

#### Degradaciones de API de Java {#java-api-deprecation}

Las API obsoletas destinadas a la eliminación del 26/2/2026 ya no deben utilizarse en el código. Para evitar bloques de implementación, elimine el uso de la API antes del 26 de marzo de 2026. Fechas importantes:

* **A partir del 26 de enero de 2026**: los correos electrónicos de notificación del Centro de acciones se envían **semanalmente por entorno** como recordatorio para eliminar el uso de estas API.
* **26 de febrero de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **se pausarán** durante el paso **Calidad del código**. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular el problema para permitir que continúe la canalización.
* **26 de marzo de 2026**: Las canalizaciones de Cloud Manager que contienen código mediante estas API **fallarán** durante el paso de **Calidad del código**, **bloqueando implementaciones** de nuevo código hasta que se elimine el uso.
* **30 de abril de 2026**: Es posible que los entornos que aún usan estas API **ya no reciban actualizaciones críticas de la versión de Adobe**.

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

Adobe actualizó los entornos **Stage** y **Production** al tiempo de ejecución de **Java 21 de mayor rendimiento** el 14 de octubre de 2025. A partir del **9 de febrero** (despliegue gradual hasta el 11 de febrero), ni AEM Cloud Service SDK ni ningún entorno de nube funcionarán con el tiempo de ejecución de Java 11.

>[!NOTE]
>
> Para aprovechar las últimas optimizaciones de rendimiento y mejoras de idioma, se recomienda compilar con Java 17 o Java 21 (opción preferida). La compilación con Java 8 y Java 11 sigue siendo compatible por ahora, pero quedará obsoleta en una próxima versión. Se emitirá una comunicación independiente antes de la desaprobación. Consulte la sección *requisitos de tiempo de compilación* de [este artículo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).
>

#### Aplicación de la directiva de configuración de registros Java de AEM {#logconfig-policy}

Los registros de Java de AEM deben seguir un formato estándar para garantizar una monitorización fiable en todos los entornos de clientes. Ya no se admiten las configuraciones de registro personalizadas, como los cambios en el formato de los registros, archivos de salida o niveles de registro predeterminados. Los registros deben permanecer dirigidos a los archivos predeterminados y se deben conservar los niveles de registro predeterminados para el código de producto de AEM. Consulte todos los detalles en el [Artículo de registro](/help/implementing/developing/introduction/logging.md#configuration-loggers).

Ahora se ignora cualquier invalidación de registro personalizada *no admitida*. La mayoría de los clientes no se vieron afectados y Adobe se ha puesto en contacto con clientes cuya configuración actual puede verse afectada.

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

#### Funciones de AEM Edge (programa Beta) {#edge-functions}

Las funciones de AEM Edge (a las que se hace referencia en notas de versiones anteriores como *Edge Computing*) le permiten ejecutar JavaScript en el nivel de CDN, lo que acerca el procesamiento de datos al usuario final. Esto reduce la latencia y permite experiencias dinámicas y adaptables en Edge.

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

#### Instantáneas para RDE (Programa Beta) {#rde-snapshot-program}

En la versión beta, los entornos de desarrollo rápido (RDE) ahora admiten una función para tomar una instantánea del estado actual del código y el contenido, que se puede restaurar más adelante. Esto puede resultar útil al sincronizar código que puede ser necesario revertir o al cambiar entre el desarrollo de distintas características. También es posible restaurar solo el contenido mutable como punto de partida conocido para realizar pruebas.

Envíe un correo electrónico a [aemcs-rde-support@adobe.com](mailto:aemcs-rde-support@adobe.com) si está interesado en utilizar esta función y proporcionar comentarios sobre ella.

#### Herramientas de IA para IDE para el desarrollo de AEM Java y Dispatcher (programa Beta) {#ai-dev-beta}

Los equipos de pila de Java utilizan cada vez más el desarrollo asistido por IA en herramientas como Cursor, Claude Code, Visual Studio e IntelliJ para acelerar la entrega de características y mejorar la calidad del código. Únase a la versión beta para lo siguiente:

* Comparta experiencias del mundo real para ayudar a dar forma a las futuras capacidades de IA admitidas por Adobe
* Pruebe las herramientas IDE que los agentes de IA pueden utilizar para generar y depurar el código de AEM y la configuración de Dispatcher

Envíe un correo electrónico a [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com) para obtener más información.

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
