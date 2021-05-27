---
title: Notas de la versión 2020.12.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2020.12.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 16875180-1f23-477d-9d4d-e220998c4983
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 7%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de [!DNL Experience Manager] como Cloud Service.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2020.12.0 es el 17 de diciembre de 2020.
La siguiente versión (2021.1.0) será el 28 de enero de 2021.

## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP del fragmento de contenido: Agregue la capacidad de agregar, actualizar y eliminar variaciones de fragmento de contenido mediante la API HTTP.

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* La integración con [!DNL Adobe InDesign Server] ya está disponible para [!DNL Experience Manager] como [!DNL Cloud Service]. Proporciona automatización para procesar archivos [!DNL Adobe InDesign] mediante scripts [!DNL Adobe InDesign Server] y permite a los usuarios utilizar la interfaz de usuario [!DNL Assets] plantillas para crear folletos o anuncios. Solo se admite [!DNL InDesign Server] alojado por [!DNL Adobe Managed Services] para [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] se mejora para rastrear y mostrar referencias de recursos cuando se utiliza un recurso en una  [!DNL Experience Manager Sites] implementación remota mediante la funcionalidad Recursos conectados . Ahora, una nueva pestaña [!UICONTROL Referencias] de la página [!UICONTROL Propiedades] del recurso muestra referencias locales y remotas del recurso. Las referencias permiten a los usuarios de DAM realizar un seguimiento del uso de recursos en páginas [!DNL Sites] y en recursos compuestos en [!DNL Assets]. Consulte [configurar y utilizar recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] ahora se puede acceder a las funcionalidades a través de los componentes principales basados en  [!DNL Sites] imágenes. Los autores pueden configurar rápidamente componentes para que utilicen ajustes preestablecidos de imagen, recorte inteligente y modificadores de imagen al crear páginas web. Consulte [Versión de los componentes principales 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] la aplicación de escritorio permite a los usuarios cargar archivos y carpetas arrastrándolos desde el Explorador de Windows o el Buscador de Mac en la interfaz de la aplicación de escritorio. Consulte [agregar recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia de Venia del CIF publicado - 2020.12.01 que incluye la versión más reciente de los componentes principales del CIF v1.6.0. Consulte el [sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obtener más información.

* Componentes principales de CIF v1.6.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obtener más información.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.12.0 es el 10 de diciembre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Administración de autoservicio de [certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) y [nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Administración de autoservicio de [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La página de detalles **Entorno** actualizada ahora permite a los usuarios administrar los nombres de dominio personalizados y las Listas de permitidos IP en sus entornos.

### Corrección de errores {#bug-fixes-cloud-manager}

* Algunas ocurrencias de errores en la fase de análisis del código sin proporcionar los resultados abordados.

* La tarjeta de entorno no mostraba de forma consistente el botón **Add**.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado una nueva versión del complemento AIO-CLI. La versión más reciente de este complemento incluye correcciones de errores para el conversor AEM Dispatcher y el modernizador de repositorio, y también admite una nueva utilidad: Conversor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

* El conversor de índices es una utilidad que se puede usar para transformar las definiciones de índices OAK personalizadas de un cliente a AEM como definiciones de índices OAK compatibles con el Cloud Service. Consulte [Conversor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más información.

* Nueva función agregada al [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete separado `ui.config` para contener todas las configuraciones de OSGi.

### Corrección de errores {#crt-bug-fixes}

* Se han hecho varias correcciones de errores en las herramientas AEM Dispatcher Converter y Modernizador de repositorio. Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.1.20 es el 8 de enero de 2021.

### Novedades de [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Los usuarios ahora pueden saber si su token de acceso ha caducado al pasar el ratón por el icono de estado en la interfaz de usuario de la herramienta de transferencia de contenido (CTT). También se les notificará en la interfaz de usuario de Detalles del conjunto de migración que no pueden conectarse a su instancia de Cloud Service.

### Corrección de errores {#ctt-bug-fixes}

* El estado de la interfaz de usuario de la herramienta de transferencia de contenido (CTT) de un conjunto de migración no se mantuvo y cambió después de un período de inactividad. Esto se ha solucionado.
* La opción para ver registros estaba deshabilitada si los registros no estaban disponibles. Esto se ha solucionado y se han añadido mensajes para notificar al usuario por qué faltan los registros.
* El estado de la interfaz de usuario de la herramienta de transferencia de contenido mostraba *FAILED* cuando el usuario detenía una ingesta. Esto se ha corregido para mostrar *STOPPED* en su lugar.
