---
title: Notas de la versión 2024.1.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2024.1.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 89%

---

# Notas de la versión 2024.1.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2024.1.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de la versión de versiones anteriores, como 2021 o 2022.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como versión de funcionalidad actual (2024.1.0) de [!DNL Cloud Service] es el viernes, 25 de enero de 2024. La próxima versión con funcionalidades (2024.3.0) está planificada para el 11 de abril de 2024.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de enero de 2024 para ver un resumen de las funciones añadidas en la versión 2024.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager en AEM Sites {#sites-extension-manager}

**Explore el nuevo [Extension Manager en AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** para personalizar la configuración de AEM mediante la configuración de extensiones de IU.

![Extension Manager en AEM Sites](/help/assets/sites/extension-manager/homepage.png)

El Extension Manager de AEM Sites permite a los desarrolladores y profesionales acceder, administrar y personalizar las [extensiones de la IU](https://developer.adobe.com/uix/docs/) creadas con el [Generador de aplicaciones de Adobe](https://developer.adobe.com/app-builder/) para mejorar la funcionalidad de AEM Sites.
Con Extension Manager, puede:

* Habilitar o deshabilitar las extensiones por instancia;
* Configurar los parámetros de extensión;
* Previsualizar extensiones y generar un vínculo de vista previa compartible;
* Descubrir las funciones de extensibilidad de la IU mediante demostraciones interactivas;
* Acceder a las funciones experimentales de Adobe mediante extensiones de origen.

Estamos buscando activamente comentarios y nuevos casos de uso para las extensiones de IU.  Si desea conectarse, envíe un correo electrónico a `uix@adobe.com`.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Funciones de versión preliminar de vista de administrador {#admin-view-prerelease}

**Previsualizar representaciones para todos los tipos de vídeo admitidos**

Experience Manager Assets ahora genera de forma predeterminada representaciones de previsualización de todos los tipos de vídeo admitidos sin requerir una configuración de perfil de procesamiento

### Vista de recursos {#assets-view-features}

**Lista de bloqueados de etiquetas inteligentes**

Ahora, Assets Essentials permite definir una lista de bloqueados compuesta por palabras que no deben añadirse como etiquetas inteligentes a los recursos cuando se cargan en el repositorio. Esta posibilidad le ayuda a mantener el cumplimiento de la marca y reduce el esfuerzo por moderar las etiquetas inteligentes.

![Lista de bloqueados de etiquetas inteligentes](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### Programa para primeros usuarios {#forms-early-adopter}

* **[Envío de un formulario adaptable a un escenario de Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**: Forms as a Cloud Service ofrece opciones listas para usar para conectar fácilmente un formulario adaptable con Adobe Workfront.  Esto simplifica el proceso de envío de un formulario adaptable a un escenario de Adobe Workfront, permitiéndole activar un escenario de Workfront Fusion al enviar un formulario adaptable.

* **[Compatibilidad con idiomas de derecha a izquierda](/help/forms/supporting-new-language-localization-core-components.md)**: los formularios adaptables creados en los componentes principales ahora se pueden presentar en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu.  Más de 2000 millones de personas en todo el mundo hablan los idiomas RTL.  El uso de un formulario en idioma RTL le permite ampliar el alcance de sus formularios adaptables para adaptarse a estos diversos públicos y seleccionar en los mercados RTL. En ciertas regiones, también es un mandato legal proporcionar formularios en el idioma local.  Al adaptarse a los idiomas locales, no solo abre las puertas a un público más amplio, sino que también garantiza el cumplimiento de las leyes y regulaciones relevantes.

  ![Compatibilidad con idiomas de derecha a izquierda](/help/forms/assets/right-to-left-language-support.png)

* **[Proteja sus documentos con las API de DocAssurance (parte de las API de comunicación)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: las API de DocAssurance le permiten proteger la información confidencial mediante la firma y el cifrado de los documentos. Mediante el cifrado, el contenido de un documento se transforma en un formato ilegible, lo que garantiza que solo los usuarios autorizados puedan obtener acceso. Esta capa de protección fortificada no solo protege los datos valiosos de miradas no autorizadas, sino que también proporciona tranquilidad. Las API de firma permiten a su organización proteger la seguridad y la privacidad de los documentos PDF de Adobe que distribuye y recibe. Este servicio utiliza firmas digitales y certificación para garantizar que solo los destinatarios previstos puedan modificar los documentos.

  Puede escribir a `aem-forms-early-adopter-program@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta posibilidad.

* **[Puede aprovechar el Servicio de telemetría operativa](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)** para habilitar la recopilación en el lado del cliente para AEM as a Cloud Service.
El servicio de telemetría operativa ofrece una reflexión más precisa de las interacciones del usuario, lo que garantiza una medida fiable de la participación en el sitio web. Es una gran oportunidad para obtener perspectivas avanzadas sobre el rendimiento de su página. Es beneficioso para los clientes que utilizan CDN administrada por Adobe o CDN no administrada por Adobe. Además, para los clientes que utilizan una CDN no administrada por Adobe, ahora se pueden habilitar los informes de tráfico automatizados para ellos, lo que elimina la necesidad de compartir cualquier informe de tráfico con Adobe.

  Si está interesado en probar esta nueva característica y compartir sus comentarios, envíe un mensaje de correo electrónico a `aemcs-rum-adopter@adobe.com`, junto con su nombre de dominio para cada uno de los entornos para los que desea habilitar la telemetría operativa desde su dirección de correo electrónico asociada a su Adobe ID. A continuación, el equipo de productos de Adobe activará el Servicio de telemetría operativa.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Compatibilidad con Dynatrace {#dynatrace}

Los clientes de Dynatrace pueden monitorizar su uso de AEM. [Lea cómo](/help/implementing/cloud-manager/dynatrace.md) para solicitar conectividad con su entorno de Dynatrace para monitorizar el rendimiento de las aplicaciones. Tenga en cuenta que New Relic APM, que está disponible para todos los clientes, dejará de recopilar datos si Dynatrace está habilitado.

### Compatibilidad con RDE para código front-end mediante temas del sitio y plantillas del sitio: Programa para primeros usuarios {#rde-frontend-early-adopter}

Los [Entornos de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) admiten ahora código front-end basado en [temas del sitio](/help/sites-cloud/administering/site-creation/site-themes.md) y [plantillas del sitio](/help/sites-cloud/administering/site-creation/site-templates.md), para los primeros usuarios. Con los RDE, esto se hace usando una directiva de línea de comandos, en lugar de una [canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md). Póngase en contacto con **aemcs-rde-support@adobe.com** para probarlo y proporcionar comentarios.

### Programa de adopción temprana de asignación de dominios {#cdn-config-early-adopter}

Además de las recientemente lanzadas [Reglas de filtrado de tráfico](/help/security/traffic-filter-rules-including-waf.md), que incluyen las reglas del firewall de aplicaciones web (Web Application Firewall, WAF) con licencia opcional, existe la posibilidad de utilizar la canalización de configuración para declarar e implementar [otros tipos de configuración de CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md). Únase al programa de usuarios que lo adoptaron por correo electrónico **`aemcs-cdn-config-adopter@adobe.com`** para obtener acceso a:

* Redirecciones del lado del cliente 301/302
* solicitudes de proxy en el perímetro a orígenes arbitrarios
* transformaciones de URL
* configuración o modificación de encabezados de solicitud o respuesta
* páginas de error personalizadas cuando la CDN no puede llegar a AEM

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí](/help/implementing/cloud-manager/release-notes/current.md).

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
