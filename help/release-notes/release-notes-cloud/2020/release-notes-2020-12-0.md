---
title: Notas de la versión 2020.12.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2020.12.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 11%

---

# Notas de la versión para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 es el 17 de diciembre de 2020.
La de la siguiente versión (2021.1.0) es el 28 de enero de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md)**: Añada la capacidad de añadir/actualizar y eliminar variaciones de fragmentos de contenido mediante la API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* Integración con [!DNL Adobe InDesign Server] ya está disponible para [!DNL Experience Manager] as a [!DNL Cloud Service]. Proporciona automatización para procesar [!DNL Adobe InDesign] archivos usar [!DNL Adobe InDesign Server] scripts y permite a los usuarios utilizar [!DNL Assets] interfaz de usuario de templates para crear folletos o publicidades. Solo [!DNL InDesign Server] alojado por [!DNL Adobe Managed Services] es compatible con [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] se ha mejorado para rastrear y mostrar referencias de recursos cuando se utiliza un recurso en un [!DNL Experience Manager Sites] implementación mediante la funcionalidad Recursos conectados. Un nuevo [!UICONTROL Referencias] pestaña en la carpeta del recurso [!UICONTROL Propiedades] La página ahora enumera las referencias locales y remotas del recurso. Las referencias permiten a los usuarios de DAM rastrear el uso de recursos en [!DNL Sites] páginas y recursos compuestos en [!DNL Assets]. Consulte [configurar y utilizar recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] AEM Ahora se puede acceder a las funcionalidades de a través de la opción de acceso a través de la [!DNL Sites] Componentes principales basados en imágenes. Los autores pueden configurar rápidamente los componentes para utilizar Ajustes preestablecidos de imagen, Recorte inteligente y Modificadores de imagen al crear páginas web. Consulte [Versión 2.13.0 de Componentes principales](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* El [!DNL Experience Manager] La aplicación de escritorio de permite a los usuarios cargar archivos y carpetas arrastrándolos desde el Explorador de Windows o el Buscador de Mac en la interfaz de la aplicación de escritorio. Consulte [agregar recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* CIF CIF Lanzamiento del sitio de referencia de Venia de la versión 2020.12.01, que incluye la versión más reciente de componentes principales de la versión 1.6.0 de la versión de Venia. Consulte [CIF Sitio de referencia de Venia en](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obtener más información.

* CIF Lanzamiento de los componentes principales de la versión 1.6.0 de. Consulte [CIF Componentes principales](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en Adobe Experience Manager AEM () as a Cloud Service 2020.12.0 es el 10 de diciembre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Administración del autoservicio de [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) y [Nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Administración de autoservicio de [Listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* El actualizado **Entorno** La página de detalles ahora permite a los usuarios administrar nombres de dominio personalizados y Listas de permitidos IP en sus entornos.

### Correcciones de errores {#bug-fixes-cloud-manager}

* Se solucionan algunos errores en la fase de análisis del código sin proporcionar resultados.

* La tarjeta de entorno no mostraba la variable **Añadir** botón.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. AEM La versión más reciente de este plug-in incluye correcciones de errores para el Conversor de Dispatcher de y el Modernizador de repositorios, y también admite una nueva utilidad: Convertidor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html#benefits) donde puede obtener más información sobre este complemento.

* AEM Index Converter es una utilidad que se puede usar para transformar las definiciones de índice Oak personalizadas de un cliente para que sean compatibles con las definiciones de índice Oak as a Cloud Service. Consulte [Conversor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más información.

* Nueva función añadida a [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para contener todas las configuraciones de OSGi.

### Correcciones de errores {#crt-bug-fixes}

* AEM Se han realizado varias correcciones de errores en las herramientas Conversor de Dispatcher y Modernizador de repositorios de la plataforma de datos de la plataforma de distribución de recursos. Consulte [AEM Conversor de Dispatcher de](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Fecha de lanzamiento {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.1.20 es el 8 de enero de 2021.

### Novedades de [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Los usuarios ahora pueden saber si su token de acceso ha caducado pasando el puntero sobre el icono de estado en la interfaz de usuario de la herramienta de transferencia de contenido (CTT). También se les notifica en la interfaz de usuario de detalles del conjunto de migración que no pueden conectarse a su instancia de Cloud Service.

### Correcciones de errores {#ctt-bug-fixes}

* El estado de la interfaz de usuario de la herramienta de transferencia de contenido (CTT) para un conjunto de migración no persistió y cambió tras un periodo de inactividad. Esto se ha corregido.
* La opción para ver los registros se deshabilitaba si los registros no estaban disponibles. Esto se ha corregido y se ha agregado mensajería para notificar a los usuarios por qué faltan registros.
* Se muestra el estado de la interfaz de usuario de Content Transfer Tool *ERROR* cuando el usuario detuvo una ingesta. Esto se ha corregido para mostrarlo *DETENIDO* en su lugar.
