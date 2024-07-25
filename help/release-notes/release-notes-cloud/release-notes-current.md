---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
feature: Release Information
role: Admin
source-git-commit: e11c869c2f8cc8847869ad67a2c752e7239bd44c
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 75%

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
>Para recibir una notificación mensual por correo electrónico acerca de las actualizaciones realizadas en las notas de la versión de Experience Cloud, suscríbase a las [actualizaciones prioritarias de productos de Adobe](https://www.adobe.com/subscription/priority-product-update.html).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de la versión de funcionalidad actual de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] (2024.7.0) fue el viernes, 25 de julio de 2024. La próxima versión con funcionalidades (2024.8.0) está planificada para el viernes, 29 de agosto de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de julio de 2024 para ver un resumen de las funcionalidades añadidas en la versión 2024.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3431707?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nueva función de Experience Manager Sites {#new-feature-sites}

### Programa para primeros usuarios {#sites-early-adopter}

**Generar variaciones**

Aproveche la GenAI mediante la nueva función de AEM, [generar variaciones](/help/generative-ai/generate-variations.md), accesible ahora en Cloud Service. Generar variaciones le ayuda a generar y escalar la creación de contenido mediante el uso de IA generativa. Póngase en contacto con el equipo de cuentas de Adobe para que lo considere en el programa.

**Exploración de recursos en la consola de fragmentos de contenido**

Los autores de contenido ahora pueden examinar, ver y realizar acciones en imágenes y otros recursos sin tener que salir de la consola de fragmento de contenido.

![Examen de recursos](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

¿Quiere probar la función y compartir sus comentarios? Puede enviar un correo electrónico a aemcs-waf-adopter@adobe.com desde su ID de correo electrónico oficial para más información acerca del programa de primeros usuarios.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

**Cargar recursos mediante el Selector de recursos**

El Selector de recursos ahora permite a los autores de contenido cargar los recursos finales directamente desde el selector, ya sea arrastrando o explorando desde el sistema de archivos local. Esto permite cargar los recursos finales en DAM desde la aplicación que elija.

### Nuevas funcionalidades de la vista Recursos {#assets-view-new-features}

**Integración de Contentes credentials**

Experience Manager Assets ahora admite contentes credentials para los formatos de imagen admitidos. Proporciona información sobre el linaje del recurso y cómo se creó, incluso si se modificó con GenAI.

![Contentes credentials](/help/assets/assets/content-credentials.png)

**Vistas previas visuales del contenido de la carpeta**

Experience Manager Assets ahora muestra vistas previas visuales del contenido de la carpeta en la miniatura de la carpeta al examinar o buscar contenido, lo que mejora la capacidad de detección de los recursos disponibles en el repositorio de AEM Assets.

<!--


**Content Credentials**

Content Credentials feature in Assets view now provides detailed asset provenance data adhered to an asset. This helps to trace the enroute edits along the asset's lifecycle to prevent users from deception through deliberately tempered assets. This ensures content authenticity among users and fosters trust through transparency.

When looking at the asset details, any image with content credentials added, such as those created with GenAI, displays the manifest details in a dedicated panel. If the asset is downloaded, published, or shared, the credentials remain intact with the asset.

![check publish status1](/help/release-notes/assets/content-credentials.png)

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones en AEM Forms {#forms-new-prerelease-features}

#### Editor de reglas visuales mejorado para formularios adaptables basado en componentes principales

Los autores de formularios adaptables pueden utilizar campos de formulario repetibles en las funciones predeterminadas disponibles en el editor de reglas visuales para los componentes principales para crear una lógica empresarial compleja en los formularios, sin requerir la personalización o la asistencia del equipo de desarrollo.

### Funciones de acceso rápido de AEM Forms {#forms-new-early-access-features}

El programa para acceso rápido de AEM Forms ofrece una oportunidad única de obtener acceso exclusivo a innovaciones punteras antes que nadie y ayudar a dar forma a su desarrollo. El programa ofrece acceso a múltiples innovaciones.

En estas notas de la versión se indican las innovaciones de la versión actual. Para ver la lista completa de innovaciones disponibles en el programa para acceso rápido, consulte la [documentación del programa de acceso rápido de AEM Forms](/help/forms/early-access-ea-features.md).

#### Crear formularios adaptables mediante el Editor universal

Aproveche el Adobe Experience Manager [Universal Editor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para crear formularios adaptables mediante la creación de arrastrar y soltar WYSIWYG, tanto para experiencias de inscripción sin encabezado como con encabezado, que se entregan mediante el servicio de Edge Delivery. Los autores de formularios adaptables pueden crear e iniciar fácilmente experimentos para diversas variaciones de formularios en las páginas web y determinar las experiencias con mejor rendimiento para los usuarios finales.

>[!IMPORTANT]
>
> Si está interesado en unirse al programa de acceso rápido de Adobe para conocer cualquier innovación pionera, solo tiene que enviar un correo electrónico desde su dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso. Puede solicitar acceso a todas las innovaciones o a cualquier innovación específica.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Purga de contenido en la CDN con una clave de API de autoservicio {#purge-cdn}

La configuración de TTL con el encabezado HTTP Cache-Control es un enfoque eficaz para equilibrar el rendimiento de la entrega de contenido y la actualización de este. Sin embargo, en situaciones en las que es fundamental ofrecer inmediatamente contenido actualizado, puede resultar beneficioso depurar directamente la caché de CDN

[Aprenda](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) a configurar un token de API de purga mediante la canalización de configuración de Cloud Manager para que pueda [invocar las API de purga](/help/implementing/dispatcher/cdn-cache-purge.md), con cualquiera de estas variaciones:
* URL única
* Varias direcciones URL con una etiqueta
* Depuración de caché de CDN completa

### AEM Configuración de autoservicio de la clave X--Edge para CDN administrada por el cliente {#customermanaged-keys}

Anteriormente, se necesitaba un ticket de asistencia para generar la clave X--Edge-Key necesaria para la configuración de una CDN administrada por el cliente. Ahora se trata de un autoservicio al declarar el valor clave en un archivo de configuración que se implementa mediante la canalización de configuración, lo que elimina cualquier retraso en la incorporación de un nuevo entorno. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#CDN-HTTP-value).

### Alertas de reglas de filtro de tráfico {#traffic-filter-rules-alerts}

Reglas de filtro de tráfico, que incluyen las reglas de cortafuegos de aplicación web (WAF) con licencia opcional, le permiten configurar el tráfico que se debe bloquear.

Ahora puedes [suscribirte a las alertas](/help/security/traffic-filter-rules-including-waf.md#traffic-filter-rules-alerts) siempre que se activen tus reglas de filtro de tráfico. Las notificaciones por correo electrónico del Centro de acciones le mantendrán informado cuando se produzcan determinadas condiciones de tráfico para que pueda tomar las medidas adecuadas.

### Programas para primeros usuarios relacionados con la distribución de contenido {#foundation-early-adopter}

Correo electrónico **<aemcs-cdn-config-adopter@adobe.com>**, indicando cuál de los programas para primeros usuarios que aparecen a continuación le interesa.

#### Autenticación básica en CDN (programa para primeros usuarios) {#basicauth-cdn}

Proteja determinados recursos de contenido mostrando un cuadro de diálogo de autenticación básica que requiera un nombre de usuario y una contraseña. Esta función se dirige principalmente a casos de uso de autenticación ligera, como el de las partes interesadas empresariales que revisan el contenido, en lugar de servir como solución completa para los derechos de acceso de usuarios finales. La lista de nombres de usuario y contraseñas se administra mediante un archivo de configuración en Git que se implementa mediante la canalización de configuración, con una referencia a variables del entorno de Cloud Manager de tipo secreto. [Más información](/help/implementing/dispatcher/cdn-credentials-authentication.md#basic-auth).

#### Redirecciones del lado del cliente (programa para primeros usuarios) {#client-side-redirects-early-adopter}

Configure las redirecciones del lado del cliente 301/302 en el control de código fuente e impleméntelas en la CDN. [Más información](/help/implementing/dispatcher/cdn-configuring-traffic.md#client-side-redirectors).<!-- and join the early adopter program by emailing **<aemcs-cdn-config-adopter@adobe.com>**. --> Tenga en cuenta que ya hay diversas otras funciones disponibles relacionadas con la [configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), incluidas las transformaciones de solicitudes y respuestas, y el enrutamiento del tráfico a sitios fuera de AEM.

#### Los usuarios empresariales pueden declarar redirecciones fuera de Git (programa para primeros usuarios) {#apache-rewritemaps-early-adopter}

De forma similar a la versión AEM 6.5, Apache/Dispatcher introducirá mapas de reescritura colocados en una ubicación específica del repositorio de publicación y los cargará, sin requerir la ejecución de una canalización de niveles web. Este método permite a los usuarios empresariales declarar redirecciones mediante una hoja de cálculo o una interfaz de usuario, como el administrador de mapas de redirección de ACS Commons o una aplicación personalizada. <!-- Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information. -->

#### Edge Side Includes (ESI) para cargar contenido dinámico (programa para primeros usuarios) {#esi-early-adopter}

La CDN administrada por Adobe es ahora compatible con [Edge Side Includes (ESI)](/help/implementing/dispatcher/edge-side-includes.md), un lenguaje de marcado para el ensamblado de contenido web dinámico a nivel de Edge. Al incluir fragmentos de ESI, puede almacenar en caché la página del HTML general en la CDN con TTL superiores, mientras que con mayor frecuencia se recuperan del origen las secciones más pequeñas que requieren actualizaciones de mayor cadencia (TTL inferiores).<!--Please reach out to **<aemcs-cdn-config-adopter@adobe.com>** for more information.-->

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

## Guías de [!DNL Experience Manager] {#guides}

Puede encontrar una lista completa de las funciones nuevas y mejoradas de la última versión de Adobe Experience Manager Guides [aquí](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2406-release/whats-new-2024-06-0).

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
