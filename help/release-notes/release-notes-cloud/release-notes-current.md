---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 29da5119403d47502fe4dc1d2a5c728aa0828b0e
workflow-type: tm+mt
source-wordcount: '1958'
ht-degree: 44%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de la funcionalidad actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.6.0) fue el viernes, 27 de junio de 2024. La siguiente versión con funcionalidades (2024.7.0) está planificada para el viernes, 25 de julio de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

<!--  ## Release Video {#release-video}

Have a look at the June 2024 Release Overview video for a summary of the features added in the 2024.6.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3429503?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función en Experience Manager Sites {#new-feature-sites}

**Servicio de datos de Real Use Monitoring (RUM)** {#real-use-monitoring}

El [Servicio de datos de Real Use Monitoring (RUM)](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/shwetad-patch-1/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service) ya está disponible de forma general, lo que permite la recopilación de datos del lado del cliente para AEM as a Cloud Service. Este servicio ofrece un reflejo más preciso de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Ofrece a los clientes una perspectiva avanzada del tráfico y el rendimiento de sus páginas, lo que representa una valiosa oportunidad para comprender y mejorar el rendimiento de las páginas.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola de fragmento de contenido.

![Examen de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a aemcs-waf-adopter@adobe.com desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de Experience Manager Assets {#new-features-assets}



**Content Hub**

Content Hub está disponible como parte del as a Cloud Service de Experience Manager Assets para democratizar el acceso al contenido en la marca para las organizaciones y sus socios comerciales. Con Content Hub, puede encontrar y distribuir recursos fácilmente, reutilizar y crear nuevas variaciones de marca y acelerar la activación a escala.

![Interfaz de usuario de Content Hub](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media con funciones de OpenAPI**

Dynamic Media con funciones OpenAPI amplía el DAM a través de aplicaciones de Adobe y de terceros, lo que permite el acceso a recursos digitales aprobados por la marca, en cualquier canal, a través del Selector de recursos o la pila OpenAPI. Principios clave: sin copias binarias, los recursos se optimizan y transforman en el perímetro para ofrecer un rendimiento rápido, entregar recursos públicos o seguros.

![Nuevo diagrama de flujo de datos de Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Hay más opciones disponibles en el panel de información de Assets**

El recuento de recursos por tipo y tamaño de recurso ya está disponible en el panel de información de Assets. Estas opciones ofrecen datos en tiempo real en el entorno de vista de Assets. Detallan el recuento y el porcentaje de recursos por intervalo de tamaño y tipo de recurso.

**Actualizaciones del editor de Adobes Express incrustado**

* Se ha mejorado la experiencia del usuario para guardar como un nuevo recurso en lugar de guardarla como una nueva versión.

* Exportación de documentos Express de varias páginas (anteriormente solo se admitía una página) tanto en formato de PDF de varias páginas como de imagen. Al seleccionar formatos de imagen, se guarda cada página como un recurso distinto en DAM para su distribución descendente.

* Compatibilidad para agregar metadatos en el cuadro de diálogo Guardar mientras se guarda un recurso.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Nuevas funciones en AEM Forms {#forms-new-prerelease-features}

#### Editor de reglas visuales mejorado para formularios adaptables basado en componentes principales

Esta versión supone una actualización significativa del Editor de reglas visuales para formularios adaptables basados en componentes principales. Ahora puede:

* Cree reglas en el Editor visual de reglas para [omitir los mensajes de éxito/error predeterminados para el envío del formulario](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* En el Editor de reglas de formularios adaptables, se ha añadido la posibilidad de [seleccionar diferentes tipos de campos para la operación WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autor de formularios ahora puede aplicar funciones personalizadas para [preprocesar datos antes del envío](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilice la funcionalidad [**Guardar como borrador**](/help/forms/save-core-component-based-form-as-draft.md) para guardar formularios parcialmente completados para su envío posterior. Esta funcionalidad es útil en situaciones en las que los usuarios tienen que interrumpir la cumplimentación de un formulario y volver más tarde.

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa AEM Forms Early Access ofrece una oportunidad única para que obtenga acceso exclusivo a innovaciones de vanguardia antes que nadie y le ayude a dar forma a su desarrollo. El programa ofrece acceso a múltiples innovaciones.

En estas notas de la versión se enumeran las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Métodos mejorados de protección de bots

AEM Forms ha mejorado sus funciones de seguridad al agregar compatibilidad con dos populares soluciones de CAPTCHA: Cloudflare Turnstile y hCaptcha. Esta funcionalidad complementa la versión existente de Google reCAPTCHA, ofreciendo a los usuarios opciones adicionales. Mejora la flexibilidad para proteger sus formularios de bots y envíos de correo no deseado.

* **Torniquete de Nubes**: este CAPTCHA sin fricción verifica a los usuarios a través de un desafío simple que no requiere interacción explícita. Se integra perfectamente en sus formularios, lo que mejora la experiencia del usuario.
* **hCaptcha**: este CAPTCHA centrado en la privacidad ofrece una alternativa fácil de usar con un enfoque en la privacidad de datos. Su objetivo es encontrar un equilibrio entre la seguridad y la experiencia del usuario.
* **Google reCAPTCHA**: AEM Forms sigue siendo compatible con reCAPTCHA v2 y reCAPTCHA Enterprise, lo que ofrece una solución fiable y bien establecida.

Al ofrecer varias opciones de CAPTCHA, AEM Forms le ha permitido seleccionar la solución que mejor se adapta a sus necesidades específicas.

¿Está listo para integrar cualquiera de estas soluciones CAPTCHA con su Forms adaptable? La documentación del Adobe proporciona instrucciones detalladas para cada uno de ellos: [Torniquete de Nubes](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [Chcaptcha](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components), y [Google reCAPTCHA](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servicio de Forms

El servicio Forms genera PDF forms interactivos para la captura de datos. También se puede utilizar para importar o exportar datos hacia y desde un formulario de PDF interactivo existente y validar los datos enviados. A continuación se muestra un desglose de sus funcionalidades:

* **Representación de formularios**: genera un formulario de PDF interactivo a partir de una plantilla creada con AEM Forms Designer y, opcionalmente, datos XML. Esta funcionalidad produce un formulario de PDF rellenables que, opcionalmente, se rellenan previamente con datos.
* **Extracción e importación de datos**: importe datos a un formulario de PDF existente y extraiga datos de un formulario de PDF rellenado. Se admiten los formatos de datos XDP y XML y la importación a PDF forms que no sean XFA (también conocidos como AcroForms) admite además datos FDF y XFDF.
* **Validación de datos**: valide los datos enviados, en formato XDP o XML con una plantilla creada con AEM Forms Designer.

>[!IMPORTANT]
>
> Si está interesado en unirse al Programa de Acceso Anticipado de Adobe para cualquier innovación de acceso anticipado, simplemente envíe un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso. Puede solicitar acceso a todas las innovaciones o a cualquier innovación específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programa de adopción temprana de notificaciones del Centro de acciones relacionadas con la salud de contenido {#actions-center-notifications}

[Centro de acciones](/help/operations/actions-center.md) envía notificaciones por correo electrónico cuando se producen incidentes importantes o si se observa algo sobre el código o la configuración en el que debe realizar una acción proactiva. El Adobe de ha introducido varios tipos nuevos de notificaciones asociadas con el estado del contenido. Esta función está disponible a través de un programa de usuarios pioneros. Para participar, póngase en contacto con el Servicio de atención al cliente de Adobe.

#### Las páginas contienen un gran número de nodos {#page-nodes}

Un gran número de nodos puede degradar el rendimiento de procesamiento y reducir los tiempos de carga de las páginas. Reciba una notificación proactiva a través del Centro de acciones cuando se detecte un gran número de nodos en una página, lo que le permitirá realizar los pasos necesarios para reducir el número total de nodos dentro de una página.

#### Gran número de instancias de flujo de trabajo en ejecución {#running-workflows}

El rendimiento del motor de flujo de trabajo se ve afectado cuando hay un gran número de flujos de trabajo en ejecución en el entorno de creación. Recibirá una notificación proactiva a través del Centro de acciones cuando se detecte un gran número de instancias de flujo de trabajo en ejecución. Este proceso permite configurar un trabajo de depuración para finalizar flujos de trabajo en ejecución innecesarios.

#### Usuarios añadidos directamente a grupos personalizados {#users-customgroups}

Recibirá una notificación proactiva a través del Centro de acciones cuando los usuarios se agreguen directamente a grupos personalizados. AEM Este proceso le permite seguir las prácticas recomendadas de IMS añadiendo usuarios a grupos de IMS relevantes y luego incluyendo esos grupos de IMS como miembros de grupos de.

#### Contenido JCR faltante {#jcr-content}

El Centro de acciones le notifica de forma proactiva cuando se detecta contenido JCR que falta. Este método permite añadir el contenido que falta y evitar el fallo de determinadas funciones de AEM Assets.

#### Flujos de trabajo completados no depurados {#workflows}

El Centro de acciones le notifica de forma proactiva cuando no se han purgado los flujos de trabajo completados de más de 90 días. Este método ayuda a mejorar el rendimiento del motor de flujo de trabajo al reducir el número de instancias de flujo de trabajo.

#### Falta el medio de Sling {#sling-resource}

El Centro de acciones le notifica de forma proactiva cuando se detecta un recurso Sling que falta. Este método permite añadir el recurso que falta y evitar el fallo de determinadas funciones de AEM Assets.

### Programas de adopción temprana relacionados con la entrega de contenido {#foundation-early-adopter}

Correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**, indicando cuál de los programas para primeros usuarios que aparecen a continuación le interesa.

#### Autenticación básica en CDN (programa de adopción anticipada) {#basicauth-cdn}

Protect utiliza ciertos recursos de contenido mostrando un cuadro de diálogo de autenticación básico que requiere un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como las partes interesadas de la empresa que revisan el contenido, en lugar de servir como una solución completa para los derechos de acceso del usuario final. La lista de nombre de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables de entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Purga de contenido en la CDN con una clave de API de autoservicio (programa para usuarios que adoptan por anticipado) {#purge-cdn}

Registre una clave de API de depuración de CDN en forma autoservicio y utilícela para invalidar contenido en CDN, ya sea de forma global o para uno o más recursos. [Más información](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### AEM Creación de autoservicio de la clave de X--Edge para CDN administrada por el cliente (BYOCDN) (programa de adopción anticipada) {#byocdn-keys}

Anteriormente, se necesitaba un ticket de asistencia para generar la clave X--Edge-Key necesaria para la configuración de una CDN administrada por el cliente. Este resultado ahora se puede lograr en modo de autoservicio a través de un archivo de configuración que se implementa mediante la canalización de configuración, lo que elimina cualquier retraso en la incorporación de un nuevo entorno. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecciones Del Lado Del Cliente (Programa De Usuarios Iniciales) {#client-side-redirects-early-adopter}

Configure las redirecciones del lado del cliente 301/302 en el control de código fuente e impleméntelas en la CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Tenga en cuenta que ya hay diversas otras funciones disponibles relacionadas con la [configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluidas las transformaciones de solicitudes y respuestas, y el enrutamiento del tráfico a sitios fuera de AEM.

#### Alertas de reglas de filtro de tráfico (programa de primeros usuarios) {#traffic-filter-rules-alerts-early-adopter}

Las [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) recientemente publicadas, que incluyen las reglas del firewall de aplicaciones web ((Web Application Firewall, WAF) con licencia opcional, le permiten configurar qué tráfico se debe permitir o denegar.

Únase al programa para primeros usuarios para poder recibir alertas cada vez que se activen las reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantienen informado cuando se producen determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

#### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para pioneros) {#apache-rewritemaps-early-adopter}

AEM De forma similar a la versión 6.5, Apache/dispatcher ingiere mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los carga, sin requerir la ejecución de una canalización de niveles web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el Administrador de mapas de redirección de ACS Commons o una aplicación personalizada. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL superiores, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL inferiores).<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).

## Editor universal {#universal-editor}

Puede encontrar una lista completa de las versiones de Universal Editor [aquí](/help/release-notes/universal-editor/current.md).

## Generar variaciones {#generate-variations}

Puede encontrar una lista completa de las versiones de Generar variaciones [aquí](/help/generative-ai/release-notes-generate-variations.md).

## Notas de la versión de Experience Cloud {#experience-cloud}

Puede encontrar información sobre las versiones de otras aplicaciones de Experience Cloud [aquí](https://experienceleague.adobe.com/es/docs/release-notes/experience-cloud/current).
Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).