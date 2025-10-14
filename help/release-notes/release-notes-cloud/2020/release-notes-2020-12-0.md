---
title: Notas de la versión 2020.12.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2020.12.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
feature: Release Information
role: Admin
source-git-commit: 64344b9b2cce8d7c7f05d3e5ba94049346308a9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 9%

---

# Notas de la versión de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales del as a Cloud Service [!DNL Experience Manager].

## Fecha de lanzamiento {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] as a Cloud Service 2020.12.0 es el 17 de diciembre de 2020.
La de la siguiente versión (2021.1.0) es el 28 de enero de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md)**: agregue la capacidad de agregar/actualizar y eliminar variaciones de fragmentos de contenido mediante la API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* La integración con [!DNL Adobe InDesign Server] ya está disponible para [!DNL Experience Manager] como [!DNL Cloud Service]. Proporciona automatización para procesar [!DNL Adobe InDesign] archivos mediante scripts de [!DNL Adobe InDesign Server] y permite a los usuarios usar la interfaz de usuario de [!DNL Assets] plantillas para crear folletos o anuncios. Solo se admite [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] para [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] se ha mejorado para rastrear y mostrar referencias de recursos cuando se utiliza un recurso en una implementación remota de [!DNL Experience Manager Sites] mediante la funcionalidad Assets conectado. Ahora hay una nueva pestaña [!UICONTROL Referencias] en la página [!UICONTROL Propiedades] del recurso que enumera referencias locales y remotas del recurso. Las referencias permiten a los usuarios de DAM rastrear el uso de recursos en [!DNL Sites] páginas y en recursos compuestos en [!DNL Assets]. Consulte [configurar y utilizar Assets conectado](/help/assets/use-assets-across-connected-assets-instances.md).

* AEM Ahora se puede acceder a las capacidades de [!DNL Dynamic Media] mediante los componentes principales basados en imágenes de [!DNL Sites] de la aplicación de datos. Los autores pueden configurar rápidamente los componentes para utilizar Ajustes preestablecidos de imagen, Recorte inteligente y Modificadores de imagen al crear páginas web. Consulte [Versión de componentes principales 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* La aplicación de escritorio [!DNL Experience Manager] permite a los usuarios cargar archivos y carpetas arrastrándolos desde el Explorador de Windows o el Buscador de Mac en la interfaz de la aplicación de escritorio. Ver [agregar recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/es/docs/experience-manager-desktop-app/using/using#upload-and-add-new-assets-to-aem).

## as a Cloud Service de Adobe Experience Manager Commerce {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* CIF CIF Lanzamiento del sitio de referencia de Venia de la versión 2020.12.01, que incluye la versión más reciente de componentes principales de la versión 1.6.0 de la versión de Venia. CIF Consulte [Sitio de referencia de Venia en el que se hace referencia a Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obtener más información.

* CIF Lanzamiento de los componentes principales de la versión 1.6.0 de. CIF Consulte [Componentes principales](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en Adobe Experience Manager AEM () as a Cloud Service 2020.12.0 es el 10 de diciembre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Administración de autoservicio de [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) e [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Administración de autoservicio de [Listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La página de detalles actualizada de **Entorno** ahora permite a los usuarios administrar nombres de dominio personalizados y Listas de permitidos IP en sus entornos.

### Correcciones de errores {#bug-fixes-cloud-manager}

* Se solucionan algunos errores en la fase de análisis del código sin proporcionar resultados.

* La tarjeta de entorno no muestra de manera consistente el botón **Agregar**.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. AEM La versión más reciente de este plug-in incluye correcciones de errores para el convertidor de Dispatcher de la y el modernizador de repositorios, y también admite una nueva utilidad: Convertidor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience#benefits) para obtener más información sobre este complemento.

* Index Converter es una utilidad que se puede utilizar para transformar las definiciones de índice de Oak personalizadas de un cliente para que sean compatibles con las definiciones de índice de Oak de AEM as a Cloud Service. Consulte [Conversor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más información.

* Se ha agregado la nueva característica a [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para contener todas las configuraciones de OSGi.

### Correcciones de errores {#crt-bug-fixes}

* AEM Se han corregido varios errores en las herramientas Convertidor de Dispatcher y Modernizador de repositorios de. AEM Consulte [Conversor de Dispatcher &#x200B;](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Fecha de lanzamiento {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.1.20 es el 8 de enero de 2021.

### Novedades de [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Los usuarios ahora pueden saber si su token de acceso ha caducado pasando el puntero sobre el icono de estado en la interfaz de usuario de la herramienta de transferencia de contenido (CTT). También se les notifica en la interfaz de usuario de detalles del conjunto de migración que no pueden conectarse a su instancia de Cloud Service.

### Correcciones de errores {#ctt-bug-fixes}

* El estado de la interfaz de usuario de la herramienta de transferencia de contenido (CTT) para un conjunto de migración no persistió y cambió tras un periodo de inactividad. Este problema ya está solucionado.
* La opción para ver los registros se deshabilitaba si los registros no estaban disponibles. Este problema ahora se ha corregido y se ha añadido mensajería para notificar a los usuarios por qué faltan registros.
* El estado de la interfaz de usuario de la herramienta de transferencia de contenido *ERROR* al detener la ingesta. Este problema ahora se ha corregido para mostrar *DETENIDO*.
