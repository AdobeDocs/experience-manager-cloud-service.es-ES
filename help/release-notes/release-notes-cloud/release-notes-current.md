---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: 1ac061dfc9773a1de0b1d5f8c427f8d770ca73fa
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 5%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las Notas de revisión generales para [!DNL Experience Manager] como Cloud Service.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2020.12.0 es el 17 de diciembre de 2020.
La siguiente versión (2021.1.0) será el 28 de enero de 2021.

## [!DNL Adobe Experience Manager Sites] como Cloud Service  {#sites}

* **[Content Fragment HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md)**: Añada la capacidad de agregar/actualizar y eliminar variaciones de fragmento de contenido mediante la API HTTP.

## [!DNL Adobe Experience Manager Assets] como un  [!DNL Cloud Service] {#assets}

* La integración con [!DNL Adobe InDesign Server] ya está disponible para [!DNL Experience Manager] como [!DNL Cloud Service]. Proporciona automatización para procesar [!DNL Adobe InDesign] archivos mediante [!DNL Adobe InDesign Server] secuencias de comandos y permite a los usuarios utilizar la interfaz de usuario de plantillas [!DNL Assets] para crear folletos o publicidades. Sólo [!DNL InDesign Server] hospedado por [!DNL Adobe Managed Services] se admite para [!DNL Experience Manager as a Cloud Service]. <!-- TBD: Add link to article. -->

* [!DNL Experience Manager] se mejora para realizar el seguimiento y mostrar referencias de recursos cuando se utiliza un recurso en una  [!DNL Experience Manager Sites] implementación remota mediante la funcionalidad Recursos conectados. Una nueva ficha [!UICONTROL Referencias] de la página [!UICONTROL Propiedades] del recurso ahora lista referencias locales y remotas del recurso. Las referencias permiten a los usuarios de DAM rastrear el uso de recursos en [!DNL Sites] páginas y en activos compuestos en [!DNL Assets]. Consulte [configurar y utilizar recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).

* [!DNL Dynamic Media] ahora se puede acceder a las funciones mediante los componentes principales basados en  [!DNL Sites] imágenes. Los autores pueden configurar rápidamente componentes para utilizar ajustes preestablecidos de imagen, recorte inteligente y modificadores de imagen al crear páginas web. Consulte [Versión de Componentes principales 2.13.0](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.13.0).

* [!DNL Experience Manager] la aplicación de escritorio permite a los usuarios cargar archivos y carpetas arrastrándolos desde el Explorador de Windows o el Buscador de Mac en la interfaz de la aplicación de escritorio. Consulte [adición de recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia de CIF Venia publicado - 2020.12.01 que incluye la versión más reciente de componentes principales de CIF v1.6.0. Consulte [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.12.01) para obtener más detalles.

* Componentes principales de CIF v1.6.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.6.0) para obtener más detalles.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2021.1.0 es el 14 de enero de 2021.

### Corrección de errores {#bug-fixes-cloud-manager}

* En ocasiones, la instancia de Producción de recursos puede mostrar el estado de Brand Portal en la página de detalles **Entornos** como *Pendiente* sin permitir al usuario realizar ninguna acción.

* Al activar una deshibernación desde Cloud Manager, a veces se mostraba un mensaje de error incluso cuando la deshibernación se iniciaba correctamente.

* Se han abordado casos raros de fallo en la creación o eliminación de entornos.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades en [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. La versión más reciente de este complemento incluye correcciones de errores para AEM Dispatcher Converter y el Modernizer de Repositorio y también admite una nueva utilidad: Convertidor de índices. Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

* Index Converter es una utilidad que se puede utilizar para transformar las definiciones de índice OAK personalizadas de un cliente para AEM como definiciones de índice OAK compatibles con el Cloud Service. Consulte [Convertidor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más detalles.

* Se agregó una nueva función al [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para contener todas las configuraciones de OSGi.

### Corrección de errores {#crt-bug-fixes}

* Se han realizado varias correcciones de errores en las herramientas AEM Dispatcher Converter y el Modernizador de repositorio. Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Repositorio de repositorios](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## Herramientas de Transición de nube {#code-transition-tools}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.2.20 es el 1 de febrero de 2021.

### Novedades en [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido. Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los elementos secundarios.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.
