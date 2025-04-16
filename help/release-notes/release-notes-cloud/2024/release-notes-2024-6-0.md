---
title: Notas de la versión 2024.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 4033abf4-7094-4ce4-ba93-c936062667e3
source-git-commit: 650014d0c093b9e7c1947a8fe870a5452f3083e5
workflow-type: tm+mt
source-wordcount: '1972'
ht-degree: 98%

---

# Notas de la versión 2024.6.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.6.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2022 o 2023.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.6.0) fue el 27 de junio de 2024. La siguiente versión con funcionalidades (2024.7.0) está planificada para el 25 de julio de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de junio de 2024 para ver un resumen de las funciones añadidas en la versión 2024.6.0.

>[!VIDEO](https://video.tv.adobe.com/v/3430779?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de Experience Manager Sites {#new-feature-sites}

**Servicio de datos de supervisión de uso real (RUM)** {#real-use-monitoring}

El [servicio de datos de monitorización de usuarios reales (RUM)](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) ahora está disponible de forma generalizada, lo que permite la recopilación de datos del lado del cliente para AEM as a Cloud Service. Este servicio ofrece un reflejo más preciso de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Ofrece a los clientes insights avanzados del tráfico y el rendimiento de sus páginas, lo que representa una valiosa oportunidad para comprender y mejorar el rendimiento de las páginas.

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola de fragmento de contenido.

![Examen de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a aemcs-waf-adopter@adobe.com desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de Experience Manager Assets {#new-features-assets}



**Centro de contenido**

Centro de contenido está disponible como parte de Experience Manager Assets as a Cloud Service para democratizar el acceso al contenido sobre la marca por parte de las organizaciones y sus socios comerciales. Con Centro de contenido, puede encontrar y distribuir recursos fácilmente, reutilizar y crear nuevas variaciones de la marca y acelerar la activación a escala.

![Interfaz de usuario del centro de contenido](/help/release-notes/assets/content-hub-ui.png)

**Dynamic Media con funciones de OpenAPI**

Dynamic Media con funciones de OpenAPI amplía el DAM a través de aplicaciones de Adobe y de terceros, lo que permite el acceso a recursos digitales aprobados por la marca, en cualquier canal, a través del Selector de recursos o la pila de OpenAPI. Principios clave: sin copias binarias, los recursos se optimizan y transforman en el borde para ofrecer un rendimiento rápido, entregar recursos públicos o seguros.

![Nuevo diagrama de flujo de datos de Dynamic Media](/help/assets/assets/dm-openapi-dfd.png)


### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Hay más opciones disponibles en el panel de Assets Insights**

El número de recursos por tipo y tamaño de recurso ahora está disponible en el panel de Assets Insights. Estas opciones proporcionan datos en tiempo real en el entorno de la vista Recursos. Detallan el número y el porcentaje de recursos por intervalo de tamaño y tipo de recurso.

**Actualizaciones del editor integrado de Adobe Express**

* Se ha mejorado la experiencia del usuario para guardar como un nuevo recurso en lugar de guardar como una nueva versión.

* Exportación de documentos Express de varias páginas (anteriormente solo se admitían documentos de una sola página) tanto en formato PDF como de imagen de varias páginas. Al seleccionar formatos de imagen, se guarda cada página como un recurso distinto en DAM para su distribución descendente.

* Compatibilidad para añadir metadatos en el cuadro de diálogo Guardar mientras se guarda un recurso.

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

Esta versión aporta una actualización importante al editor de reglas visuales para formularios adaptables basados en componentes básicos. Ahora puede:

* Crear reglas en el editor de reglas visuales para [anular los mensajes de éxito y error predeterminados para el envío de formularios](/help/forms/create-and-use-custom-functions.md#use-case-override-form-submission-success-and-error-handlers).

* En el Editor de reglas de formularios adaptables, se ha añadido la posibilidad de [seleccionar diferentes tipos de campos para la operación WHEN](/help/forms/rule-editor-core-components.md#allowed-multiple-fields-in-when).

* Un autor de formularios ahora puede aplicar funciones personalizadas para [preprocesar datos antes del envío](/help/forms/create-and-use-custom-functions.md#use-case-submit-altered-data-to-the-server).

* Utilice la funcionalidad [**Guardar como borrador**](/help/forms/save-core-component-based-form-as-draft.md) para guardar formularios parcialmente completados para su envío posterior. Esta funcionalidad resulta útil en situaciones en las que los usuarios tienen que interrumpir la cumplimentación de un formulario y volver a él más tarde.

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras antes que nadie y ayudar a dar forma a su desarrollo. El programa ofrece acceso a múltiples innovaciones.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Métodos mejorados de protección de bots

AEM Forms ha mejorado sus funciones de seguridad al agregar compatibilidad con dos populares soluciones de CAPTCHA: Cloudflare Turnstile y hCaptcha. Esta funcionalidad complementa la versión existente de Google reCAPTCHA, pues ofrece a los usuarios opciones adicionales. Mejora la flexibilidad para proteger sus formularios contra bots y envíos de correo no deseado.

* **Cloudflare Turnstile**: este CAPTCHA sin fricción verifica a los usuarios a través de un desafío sencillo que no requiere interacción explícita. Se integra perfectamente en sus formularios, lo que mejora la experiencia del usuario.
* **hCaptcha**: este CAPTCHA centrado en la privacidad ofrece una alternativa fácil de usar con un enfoque en la privacidad de datos. Su objetivo es encontrar un equilibrio entre la seguridad y la experiencia del usuario.
* **Google reCAPTCHA**: AEM Forms sigue siendo compatible con reCAPTCHA v2 y reCAPTCHA Enterprise, lo que ofrece una solución fiable y bien establecida.

Al ofrecer varias opciones de CAPTCHA, AEM Forms le ha permitido seleccionar la solución que mejor se adapta a sus necesidades específicas.

¿Está listo para integrar cualquiera de estas soluciones CAPTCHA con sus formularios adaptables? La documentación de Adobe proporciona instrucciones detalladas para cada uno: [Cloudflare Turnstile](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-turnstile-core-components), [hCaptcha](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/integrate-adaptive-forms-hcaptcha-core-components) y [Google reCAPTCHA](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/captcha-adaptive-forms-core-components).


### Servicio de Forms

El servicio Forms genera PDF forms interactivos para la captura de datos. También se puede utilizar para importar o exportar datos hacia y desde un formulario de PDF interactivo existente y validar los datos enviados. A continuación se muestra un desglose de sus funcionalidades:

* **Representación de formularios**: genera un formulario de PDF interactivo a partir de una plantilla creada con AEM Forms Designer y, opcionalmente, datos XML. Esta funcionalidad genera un formulario PDF rellenable que, opcionalmente, se ha rellenado previamente con datos.
* **Extracción e importación de datos**: importe datos a un formulario de PDF existente y extraiga datos de un formulario de PDF rellenado. Se admiten los formatos de datos XDP y XML y la importación a PDF forms que no sean XFA (también conocidos como AcroForms) admite además datos FDF y XFDF.
* **Validación de datos**: valide los datos enviados, en formato XDP o XML con una plantilla creada con AEM Forms Designer.

>[!IMPORTANT]
>
> Si está interesado en unirse al programa de acceso rápido de Adobe para conocer cualquier innovación pionera, solo tiene que enviar un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso. Puede solicitar acceso a todas las innovaciones o a cualquier innovación específica.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Programa para primeros usuarios de notificaciones del Centro de acciones relacionadas con el estado del contenido {#actions-center-notifications}

El [Centro de acciones](/help/operations/actions-center.md) envía notificaciones por correo electrónico cuando se producen incidentes importantes o si se observa algo en su código o configuración que aconsejan la adopción de medidas proactivas. Adobe ha introducido varios tipos nuevos de notificaciones asociadas con el estado del contenido. Esta función está disponible a través del programa para primeros usuarios. Para participar, póngase en contacto con el Servicio de atención al cliente de Adobe.

#### Las páginas contienen un gran número de nodos {#page-nodes}

Un gran número de nodos puede degradar el rendimiento del renderizado y reducir los tiempos de carga de las páginas. Reciba una notificación proactiva a través del Centro de acciones cuando se detecte un gran número de nodos en una página, así podrá realizar los pasos necesarios para reducir el número total de nodos dentro de una página.

#### Gran número de instancias de flujo de trabajo en ejecución {#running-workflows}

El rendimiento del motor de flujos de trabajo se ve afectado cuando hay un gran número de flujos de trabajo en ejecución en el entorno de creación. Recibirá una notificación proactiva a través del Centro de acciones cuando se detecte un gran número de instancias de flujo de trabajo en ejecución. Este proceso permite configurar un trabajo de depuración para terminar los flujos de trabajo en ejecución innecesarios.

#### Usuarios añadidos directamente a grupos personalizados {#users-customgroups}

Recibirá una notificación proactiva a través del Centro de acciones cuando los usuarios se añadan directamente a grupos personalizados. Este proceso le permite seguir las prácticas recomendadas de IMS añadiendo usuarios a grupos de IMS relevantes y luego incluyendo esos grupos de IMS como miembros de grupos de AEM.

#### Contenido JCR faltante {#jcr-content}

El Centro de acciones le notifica de forma proactiva cuando se detecta contenido JCR faltante. Este método permite añadir el contenido que falta y evitar el fallo de determinadas funciones de AEM Assets.

#### Flujos de trabajo completados no depurados {#workflows}

El Centro de acciones le notifica de forma proactiva cuando aún no se han depurado flujos de trabajo completados hace más de 90 días. Este método ayuda a mejorar el rendimiento del motor de flujos de trabajo al reducir el número de instancias de flujo de trabajo.

#### Recurso de sling que falta {#sling-resource}

El Centro de acciones le notifica de forma proactiva cuando se detecta un recurso de sling que falta. Este método permite añadir el recurso que falta y evitar el fallo de determinadas funciones de AEM Assets.

### Programas para primeros usuarios relacionados con la distribución de contenido {#foundation-early-adopter}

Correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**, indicando cuál de los programas para primeros usuarios que aparecen a continuación le interesa.

#### Autenticación básica en CDN (programa para primeros usuarios) {#basicauth-cdn}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como el de las partes interesadas empresariales que revisan el contenido, en lugar de servir como solución completa para los derechos de acceso de usuarios finales. La lista de nombres de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables del entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Depuración de contenido en la CDN con una clave de API de autoservicio (programa para primeros usuarios) {#purge-cdn}

Registre una clave de API de depuración de CDN en forma autoservicio y utilícela para invalidar contenido en CDN, ya sea de forma global o para uno o más recursos. [Más información](/help/implementing/dispatcher/cdn-cache-purge.md).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Creación de autoservicio de X-AEM-Edge-Key para CDN administrada por el cliente (BYOCDN) (programa para primeros usuarios) {#byocdn-keys}

Anteriormente, se necesitaba un ticket de asistencia para generar la clave X--Edge-Key necesaria para la configuración de una CDN administrada por el cliente. Este resultado ahora se puede lograr con el autoservicio a través de un archivo de configuración que se implementa mediante la canalización de configuración, lo que elimina cualquier retraso en la incorporación de un nuevo entorno. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

<!-- Email **<aemcs-cdn-config-adopter@adobe.com>** with a request to be an early adopter. -->

#### Redirecciones Del Lado Del Servidor (Programa De Usuarios Iniciales) {#server-side-redirects-early-adopter}

Configure las redirecciones del lado del servidor 301/302 en el control de código fuente e implemente en la CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Tenga en cuenta que ya hay diversas otras funciones disponibles relacionadas con la [configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluidas las transformaciones de solicitudes y respuestas, y el enrutamiento del tráfico a sitios fuera de AEM.

#### Alertas de reglas de filtro de tráfico (programa de primeros usuarios) {#traffic-filter-rules-alerts-early-adopter}

Las [Reglas de filtro de tráfico](/help/security/traffic-filter-rules-including-waf.md) recientemente publicadas, que incluyen las reglas del firewall de aplicaciones web ((Web Application Firewall, WAF) con licencia opcional, le permiten configurar qué tráfico se debe permitir o denegar.

Únase al programa para primeros usuarios para poder recibir alertas cada vez que se activen las reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantendrán informado cuando se produzcan determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

#### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el administrador de mapas de redirección de ACS Commons o una aplicación personalizada. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL superiores, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL inferiores).<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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
