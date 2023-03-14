---
title: Notas de la versión 2020.9.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.9.0."
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 21%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] La versión 2020.9.0 as a Cloud Service es el 24 de septiembre de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* El SDK del Editor de JavaScript para la Aplicación de una sola página (SPA) [ahora es de código abierto.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* Los archivos de imagen de marca de agua son compatibles con las representaciones generadas con los microservicios de recursos. Se puede configurar como un Perfil de procesamiento y utiliza un archivo PNG como marca de agua. Consulte [marca de agua de recursos](/help/assets/watermark-assets.md).

* Mejoras en [!DNL Dynamic Media]

   * Publicación selectiva: Ahora es posible que un equipo de marketing acceda a [!DNL Dynamic Media] imágenes de recorte inteligente y representaciones dinámicas sincronizadas con [!DNL Dynamic Media] para que puedan crear material promocional, sin necesidad de publicar esos recursos en [!DNL Dynamic Media] para envío global. [!DNL Experience Manager] y [!DNL Dynamic Media] la publicación está disociada y puede producirse por separado para conseguirlo. Consulte [publicación selectiva](/help/assets/dynamic-media/selective-publishing.md).
   * Los administradores ahora pueden restablecer [!DNL Dynamic Media] Contraseña del Cloud Service que se recibe durante el aprovisionamiento. El restablecimiento se puede realizar en [!DNL Experience Manager] interfaz de usuario, sin necesidad de utilizar el [!DNL Dynamic Media Classic] aplicación de escritorio.

* Para obtener información sobre las siguientes mejoras, consulte [novedades de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=es).

   * Previsualización mejorada del PDF con la integración del Adobe Document Cloud View SDK.
   * Funcionalidad de descarga con un solo clic.
   * Nuevas configuraciones de administración para la experiencia de descarga.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Componentes principales de CIF v1.3.0. Consulte [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) para obtener más información.

* Ya está disponible la capacidad de previsualización con plantillas de producto/categoría para productos y categorías. AEM Esto permite a los usuarios/especialistas en marketing de la empresa de la comunidad de datos ver las plantillas de producto/categoría con datos reales.

* Se ha agregado la página Propiedades a productos y categorías para permitir que los usuarios comerciales puedan ver los detalles asociados con el SKU o el ID de categoría del producto.

* Función de orden agregada a la consola de producto para permitir la ordenación de productos/categorías por nombre o atributos de precio.

* Funcionalidad de búsqueda de productos agregada a la consola de producto.

### Correcciones de errores {#bug-fixes-commerce}

* Las configuraciones del Commerce Cloud no respetaban la herencia. Esto se ha corregido para garantizar que la configuración herede valores.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de [!UICONTROL Cloud Manager] La versión 2020.9.0 es el 3 de septiembre de 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido se ha vuelto a etiquetar como auditoría de experiencias.
* El proceso de generación se ha separado en tres comandos de Maven independientes.
* Si el repositorio de Git no se clona, se volverá a crear hasta tres veces.

### Correcciones de errores {#bug-fixes-cm}

* La pestaña Auditoría de contenido mostraba incorrectamente la URL base mediante el uso del dominio de autor en lugar del dominio de publicación.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.1.0.

### Novedades {#what-is-new-cra}

* El analizador de preparación para la nube (CRA) tiene una consola de estado de inicio que muestra un **Generar informe** para que el usuario haga clic en para ejecutar el CRA.

* La interfaz de usuario de CRA muestra el progreso mientras se está ejecutando. Muestra los elementos que se analizan y los resultados encontrados durante la ejecución.

* El informe CRA muestra un resumen y la cantidad de conclusiones en un formato tabular organizado por el tipo de búsqueda y el nivel de importancia. Al hacer clic en el número de esa búsqueda, se desplazará automáticamente a la ubicación de esa búsqueda en el informe.

### Correcciones de errores {#cra-bug-fixes}

* En algunos casos, el informe de CRA no se actualizaba después de forzar una actualización. Esto se ha corregido en esta versión.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión 1.1.10 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido (CTT) admite el almacén de datos del almacén de Azure Blob.

* La interfaz de usuario de CTT tiene una función de recarga automática que vuelve a cargar la página de información general cada 30 segundos.

* Botón agregado a la interfaz de usuario de CTT para recuperar *Token de acceso* fácilmente.

* Se agregó un mensaje de validación descriptivo para *URL* y *Nombre del conjunto de migración*.

## Herramientas de refactorización de código {#code-refactoring}

Siga esta sección para conocer las novedades y las actualizaciones de las herramientas de refactorización de código.

### Novedades {#what-is-new-refactoring}

* El complemento AIO-CLI admite el Modernizador de repositorio y permite a los usuarios ejecutar la herramienta mediante el complemento.

   Consulte [Recurso de Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información.

* AEM La utilidad Modernizador del repositorio se puede utilizar para reestructurar los paquetes de proyectos existentes en paquetes compatibles con la estructura de proyectos definida para el as a Cloud Service de la.

   Consulte [Recurso de Git: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obtener más información.
