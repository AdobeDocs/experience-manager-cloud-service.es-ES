---
title: Notas de la versión 2024.5.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.5.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 7b7a27f9-ba57-4eb2-9fcb-653b5213af04
source-git-commit: a8c74573134597e83c2720de3b2a0f75ff7896a2
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 99%

---

# Notas de la versión 2024.5.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.5.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.5.0) es el 30 de mayo de 2024. La próxima versión con funcionalidades (2024.6.0) está planificada para el 27 de junio de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de mayo de 2024 para ver un resumen de las funciones añadidas en la versión 2024.5.0:

>[!VIDEO](https://video.tv.adobe.com/v/3448065?quality=12&captions=spa)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones en Sites {#sites-new-features}

#### Configuración de la traducción de AEM {#translation-integration}

Las acciones y flujos de trabajo de traducción de contenido ahora activan eventos para permitir el seguimiento de pasos y estados de procesos relevantes desde aplicaciones externas. Se están generando los siguientes eventos. Los usuarios podrán suscribirse a eventos mediante Adobe Developer Console.

* `TRANSLATION_JOB_CREATED`
* `TRANSLATION_JOB_CONTENT_ADDITION_STARTED`
* `TRANSLATION_JOB_CONTENT_ADDITION_COMPLETED`
* `TRANSLATION_JOB_CONTENT_DELETION_STARTED`
* `TRANSLATION_JOB_CONTENT_DELETION_COMPLETED`
* `TRANSLATION_JOB_COMMITTED_FOR_TRANSLATION`
* `TRANSLATION_JOB_READY_FOR_REVIEW`
* `TRANSLATION_JOB_APPROVED`
* `TRANSLATION_JOB_COMPLETED`
* `TRANSLATION_JOB_CANCELLED`
* `TRANSLATION_JOB_ERROR`

#### Servicio de datos de monitorización de usuario real (RUM) {#real-use-monitoring}

* **[El servicio de datos de monitorización de usuario real (RUM) ahora es GA](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**, que permite la colección de datos del lado del cliente para AEM as a Cloud Service.
El servicio de monitorización de usuario real, la colección del lado del cliente, ofrece un reflejo más preciso de las interacciones, lo que garantiza una medición fiable de la participación en el sitio web. Permite a los clientes obtener perspectivas avanzadas sobre el tráfico y el rendimiento de sus páginas. Es una gran oportunidad para obtener más información sobre el rendimiento de su página y obtener perspectivas para mejorarlo.

#### Creación de AEM para Edge Delivery Services {#edge-enhancements}

Mejor estabilidad y diversas mejoras para una mejor experiencia de creación.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola de fragmento de contenido.

![Examen de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a aemcs-waf-adopter@adobe.com desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de la vista Recursos {#admin-view-new-features}

* WebM es ahora un archivo de salida compatible en el perfil de procesamiento para vídeo.
* MP4 ahora se admite en la integración nativa de AEM en Express (importación y exportación).

### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Publicación de recursos en AEM y Dynamic Media**

Experience Manager Assets ahora le permite [publicar rápidamente en Experience Manager y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md) usando la vista Recursos sin cambiar a la vista Administración. Puede publicar recursos al cargar, examinar y buscar recursos.

![comprobar estado1 de publicación](/help/assets/assets/check-publish-status1.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuevas funciones en la versión previa de AEM Forms {#forms-new-prerelease-features}

#### Editor de reglas visuales mejorado para formularios adaptables basado en componentes principales

Esta versión aporta una actualización significativa al editor de reglas visuales para formularios adaptables basados en componentes principales. Ahora puede:

* Cree reglas en el editor de reglas visuales para [anular los mensajes de éxito y error predeterminados para el envío de formularios](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* En el Editor de reglas de formularios adaptables, se ha añadido la posibilidad de [seleccionar diferentes tipos de campos para la operación WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autor de formularios ahora puede aplicar funciones personalizadas para [preprocesar datos antes del envío](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilice la funcionalidad [**Guardar como borrador**](/help/forms/save-core-component-based-form-as-draft.md) para guardar formularios parcialmente completados para su envío posterior. Esto resulta útil en situaciones en las que los usuarios tienen que interrumpir la cumplimentación de un formulario y volver a él más tarde.



### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras antes que nadie y ayudar a dar forma a su desarrollo. El programa ofrece acceso a múltiples innovaciones.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Métodos mejorados de protección de bots

AEM Forms ha mejorado sus funciones de seguridad al agregar compatibilidad con dos populares soluciones de CAPTCHA: Cloudflare Turnstile y hCaptcha. Esto se suma al reCAPTCHA de Google ya disponible, lo que proporciona a los usuarios más opciones y flexibilidad para proteger sus formularios de bots y envíos de correo no deseado.

* **Cloudflare Turnstile**: este CAPTCHA sin fricción verifica a los usuarios a través de un desafío simple que no requiere interacción explícita. Se integra perfectamente en sus formularios, lo que mejora la experiencia del usuario.
* **hCaptcha**: este CAPTCHA centrado en la privacidad ofrece una alternativa fácil de usar con un enfoque en la privacidad de datos. Su objetivo es encontrar un equilibrio entre la seguridad y la experiencia del usuario.
* **Google reCAPTCHA**: AEM Forms sigue siendo compatible con reCAPTCHA v2 y reCAPTCHA Enterprise, lo que ofrece una solución fiable y bien establecida.

Al ofrecer varias opciones de CAPTCHA, AEM Forms le ha permitido seleccionar la solución que mejor se adapta a sus necesidades específicas.

¿Está listo para integrar cualquiera de estas soluciones CAPTCHA con sus formularios adaptables? Nuestra documentación proporciona instrucciones detalladas para cada uno: [Cloudflare Turnstile](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) y [Google reCAPTCHA](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servicio de Forms

El servicio Forms genera PDF forms interactivos para la captura de datos. También se puede utilizar para importar o exportar datos hacia y desde un formulario de PDF interactivo existente y validar los datos enviados. A continuación se muestra un desglose de sus funcionalidades:

* **Representación de formularios**: genera un formulario de PDF interactivo a partir de una plantilla creada con AEM Forms Designer y, opcionalmente, datos XML. Básicamente, esto genera un formulario PDF rellenable que, opcionalmente, está rellenado previamente con datos.
* **Extracción e importación de datos**: importe datos a un formulario de PDF existente y extraiga datos de un formulario de PDF rellenado. Se admiten los formatos de datos XDP y XML y la importación a PDF forms que no sean XFA (también conocidos como AcroForms) admite además datos FDF y XFDF.
* **Validación de datos**: valide los datos enviados, en formato XDP o XML con una plantilla creada con AEM Forms Designer.

>[!IMPORTANT]
>
> Si está interesado en unirse a nuestro programa de acceso rápido para cualquier innovación pionera, solo tiene que enviar un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso. Puede solicitar acceso a todas las innovaciones o a cualquier innovación específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Las credenciales de servidor a servidor OAuth admiten integraciones de AEM con otras soluciones de Adobe {#S2S-OAuth-credentials}

Adobe Developer Console se utiliza para generar credenciales para acceder a varias API. Uno de esos tipos de credenciales, las credenciales de cuenta de servicio (JWT), han quedado obsoletas y pasan a ser credenciales de servidor a servidor de OAuth, que AEM Cloud Service ahora admite para integraciones con otras soluciones de Adobe, como Adobe Analytics y Adobe Target.

[Obtenga información sobre la obsolescencia](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md) y [aprenda a utilizar la interfaz de usuario de autor de AEM](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md) para configurar integraciones con otras soluciones de Adobe.

### Pico de tráfico predeterminado en alertas de origen {#traffic-spike-origin}

[Reciba notificaciones dinámicas](/help/security/traffic-filter-rules-including-waf.md#traffic-spike-at-origin-alert) a través del Centro de acciones cuando los patrones de tráfico en origen indican un ataque DDoS, lo que le permite investigar y configurar las reglas de filtro de tráfico.

### Nuevas funciones para los RDE {#RDE-new-features}

Los [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) permiten que los desarrolladores implementen, revisen y prueben rápidamente los cambios en la nube. Durante el mes de junio se implementarán varias funciones nuevas. También le invitamos a participar directamente con la ingeniería de Adobe en el [canal RDE Discord](https://discord.com/channels/1131492224371277874/1245304281184079872).


#### Compatibilidad con RDE para código front-end mediante temas del sitio y plantillas del sitio {#rde-frontend}

Los [RDE ahora admiten código front-end](/help/implementing/developing/introduction/rapid-development-environments.md#deploying-themes-to-rde) basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas del sitio](/help/sites-cloud/administering/site-creation/site-templates.md), para los primeros usuarios. Con los RDE, esto se hace usando una directiva de línea de comandos, en lugar de una [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). 

#### Registro mejorado para RDE {#rde-logging}

Al depurar código en un RDE, los desarrolladores pueden ahora [configurar y transmitir registros de forma más productiva](/help/implementing/developing/introduction/rapid-development-environments.md#rde-logging), utilizando la línea de comandos y sin modificar las propiedades OSGI en el control de versiones. Las funciones incluyen:

* declarar niveles de registro en un nivel por paquete o clase
* personalizar el formato de salida del registro
* transmitir varios registros en paralelo

#### Mejoras de CLI de RDE {#rde-cli-enhancements}

La interfaz de línea de comandos de RDE tiene algunas características nuevas que mejoran la experiencia del desarrollador:

* [el comando setup es interactivo](/help/implementing/developing/introduction/rapid-development-environments.md#installing-the-rde-command-line-tools-interactive), facilitando la elección entre organizaciones, programas y entornos. Ahora también es posible anular estos valores en la línea de comandos.
* [modo silencioso](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) para una salida menos detallada.
* [modo json](/help/implementing/developing/introduction/rapid-development-environments.md#global-flags) para obtener resultados útiles cuando se invoca mediante programación. 

### Nuevas notificaciones del Centro de acciones {#actions-center-notifications}

El [Centro de acciones](/help/operations/actions-center.md) envía notificaciones por correo electrónico cuando se producen incidentes importantes o si observamos algo en su código o configuración que le aconseje tomar medidas proactivas. Existen tres nuevos tipos de notificación:

* demasiadas conexiones de salida a través de una infraestructura de red avanzada
* uso de un formato de asignación de usuarios de servicio obsoleto
* un ataque DDoS potencial está en marcha

### Programa para primeros usuarios {#foundation-early-adopter}

Correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**, indicando cuál de los programas para primeros usuarios que aparecen a continuación le interesa.

#### Depuración de contenido en la CDN con una clave de API de autoservicio (programa para primeros usuarios) {#purge-cdn}

Registre una clave de API de depuración de CDN en forma autoservicio y utilícela para invalidar contenido en CDN, ya sea de forma global o para uno o más recursos. [Más información](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creación de autoservicio de X--Edge-Key para CDN administrada por el cliente (BYOCDN) (programa para primeros usuarios) {#byocdn-keys}

Anteriormente, se necesitaba un ticket de asistencia para generar la clave X--Edge-Key necesaria para la configuración de una CDN administrada por el cliente. Esto ahora se puede lograr con el autoservicio a través de un archivo de configuración que se implementa mediante la canalización de configuración, lo que elimina cualquier retraso en la incorporación de un nuevo entorno. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecciones del lado del servidor (programa de adopción temprana) {#server-side-redirects-early-adopter}

Configure las redirecciones de del lado del servidor 301/302 en el control de código fuente y implementar al CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Tenga en cuenta que ya hay diversas otras funciones disponibles relacionadas con la [configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluidas las transformaciones de solicitudes y respuestas, y el enrutamiento del tráfico a sitios fuera de AEM.

#### Alertas de reglas de filtro de tráfico (programa de primeros usuarios) {#traffic-filter-rules-alerts-early-adopter}

Las [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) recientemente publicadas, que incluyen las reglas del firewall de aplicaciones web ((Web Application Firewall, WAF) con licencia opcional, le permiten configurar qué tráfico se debe permitir o denegar.

Únase al programa para primeros usuarios para poder recibir alertas cada vez que se activen las reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantendrán informado cuando se produzcan determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

#### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Esto abre oportunidades para que un usuario empresarial declare redirecciones mediante una hoja de cálculo o una interfaz de usuario, como la que ofrece el administrador de mapas de redirección de ACS Commons o creada como parte de una aplicación de cliente. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL superiores, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL inferiores).<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## Guías de [!DNL Experience Manager] {#guides}

* **Publicación de un tema o sus elementos en un fragmento de experiencia**
Ahora, las Experience Manager Guides le permiten publicar un tema o sus elementos en un fragmento de experiencia. Un fragmento de experiencia es una unidad de contenido modular que integra tanto contenido como diseño. Los fragmentos de experiencias son fundamentales y pueden ayudarle a crear experiencias coherentes y atractivas.
* **Capacidad para pasar los metadatos de recursos del tema a la salida del PDF nativo**
Puede añadir los metadatos de recursos del tema al generar la salida del PDF nativo. Esta función le ayuda a añadir metadatos específicos para diferentes temas, como el título y el autor del tema, a los encabezados y pies de página del tema.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).
