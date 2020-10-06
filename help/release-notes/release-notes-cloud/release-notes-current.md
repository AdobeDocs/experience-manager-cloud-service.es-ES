---
title: Notas de la versión 2020.9.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service Notas de la versión 2020.9.0.'
translation-type: tm+mt
source-git-commit: 5fb87f82c092552aa5e1c4b569399ec0bbc0da3b
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 12%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Fecha de la versión {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 is September 24, 2020.

## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* El SDK de JavaScript del Editor de una sola página (SPA) [ahora es de código abierto.](/help/implementing/developing/spa/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] como Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* Los archivos de imagen de marca de agua son compatibles con las representaciones generadas con los microservicios de recursos. Se puede configurar como un Perfil de procesamiento y utiliza un archivo PNG como marca de agua. Consulte [marca de agua de los recursos](/help/assets/watermark-assets.md).

* Mejoras en [!DNL Dynamic Media]

   * Publicación selectiva: Ahora es posible que un equipo de marketing acceda a las imágenes de recorte [!DNL Dynamic Media] inteligente y a las representaciones dinámicas sincronizadas con [!DNL Dynamic Media] fin de que puedan crear materiales promocionales, todo sin necesidad de publicar dichos recursos en [!DNL Dynamic Media] para envío global. [!DNL Experience Manager] y [!DNL Dynamic Media] la publicación está disociada y puede producirse por separado para lograrlo. Consulte Publicación [selectiva](/help/assets/dynamic-media/selective-publishing.md).
   * Los administradores ahora pueden restablecer la contraseña de [!DNL Dynamic Media] Cloud Service que se recibe al aprovisionar. El restablecimiento se puede realizar en la interfaz [!DNL Experience Manager] de usuario, sin necesidad de utilizar la aplicación de [!DNL Dynamic Media Classic] escritorio.

* Para obtener información sobre las siguientes mejoras, consulte [las novedades de Brand Portal](https://docs.adobe.com/content/help/es-ES/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Previsualización PDF mejorada con la integración del SDK de Vista de Adobe Document Cloud.
   * Funcionalidad de descarga con un solo clic.
   * Nuevas configuraciones de administración para la experiencia de descarga.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Componentes principales de CIF v1.3.0. Consulte Componentes [principales de](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) CIF para obtener más detalles.

* Ya está disponible la capacidad de previsualización con plantillas de producto/categoría para productos y categorías. Esto permite a los usuarios/especialistas en marketing de AEM negocios realizar vistas de las plantillas de producto/categoría con datos reales.

* Se agregó la página de propiedades a productos y categorías para permitir que los usuarios comerciales puedan obtener detalles de vista asociados con el SKU o ID de categoría del producto.

* Función de ordenación agregada a la consola de producto para permitir la clasificación de productos/categorías por nombre o atributos de precio.

* Funcionalidad de búsqueda de productos agregada a la consola de producto.

### Corrección de errores {#bug-fixes-commerce}

* Las configuraciones de Commerce Cloud no respetaban la herencia. Esto se ha solucionado para garantizar que la configuración hereda valores.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido se ha vuelto a etiquetar como auditoría de experiencias.
* El proceso de compilación se ha separado en tres comandos Maven independientes.
* Si el repositorio Git no se clona, se volverá a crear hasta tres veces.

### Corrección de errores {#bug-fixes-cm}

* La ficha Auditoría de contenido mostraba incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.1.0.

### Novedades {#what-is-new-cra}

* El analizador de preparación para la nube (CRA) tiene una consola de estado de inicio que muestra un botón **Generar informe** explícito en el que el usuario puede hacer clic para ejecutar el CRA.

* La interfaz de usuario de CRA muestra el progreso mientras se está ejecutando. Muestra los elementos que se analizan y los resultados encontrados durante la ejecución.

* El informe CRA muestra un resumen y el número de conclusiones en un formato de tabla organizado por el tipo de búsqueda y el nivel de importancia. Al hacer clic en el número de esa búsqueda, se desplazará automáticamente a la ubicación de esa búsqueda en el informe.

### Corrección de errores {#cra-bug-fixes}

* En algunos casos, el informe CRA no se actualizaba después de forzar una actualización. Esto se ha corregido en esta versión.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión v1.1.10 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido (CTT) admite el almacén de datos del almacén de blob de Azure.

* La interfaz de usuario de CTT tiene una función de recarga automática que vuelve a cargar la página de información general cada 30 segundos.

* Botón añadido a la interfaz de usuario de CTT para recuperar fácilmente el *Token de acceso* .

* Se agregó un mensaje de validación descriptivo para la *URL* y el nombre del conjunto *de migración*.

## Herramientas de refactorización de código {#code-refactoring}

Siga esta sección para conocer las novedades y las actualizaciones de las herramientas de refactorización de código.

### Novedades {#what-is-new-refactoring}

[Repository Modernizer](/help/move-to-cloud-service/refactoring-tools/repo-modernizer.md) es una utilidad desarrollada para reestructurar los paquetes de proyectos existentes separando contenido y código en paquetes discretos para ser compatibles con la estructura de proyectos definida para Adobe Experience Manager como Cloud Service.

* El complemento AIO-CLI admite el Modernizador de repositorio y permite a los usuarios ejecutar la herramienta mediante el complemento.

   Consulte Recurso [Git: aio-cli-plugin-aem-cloud-service-Migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) para obtener más información.

* La utilidad Modernizer del repositorio se puede utilizar para reestructurar los paquetes de proyectos existentes en paquetes compatibles con la estructura de proyectos definida para AEM como Cloud Service.

   Consulte Recurso [Git: Modernizador](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) de repositorio para obtener más detalles.

