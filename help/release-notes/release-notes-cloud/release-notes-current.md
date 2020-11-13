---
title: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
description: Current Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service.
translation-type: tm+mt
source-git-commit: b67bafd9edb06a6d333e1a5bde0687994c30ea81
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 5%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service.

## Fecha de la versión {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 is October 28, 2020.
La siguiente versión (2020.11.0) será el 1 de diciembre de 2020.

## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

<!-- add when release done: * **Core Components 2.12.0**: With Core Components being on auto-update, benefit from the latest improvements contributed by the community. See list of changes since 2.11.1: Release Notes -->

* **Arquetipo de proyecto 24**: La base recomendada para el inicio de un nuevo proyecto de AEM mejoró, incluyendo ahora la nueva capa de datos del cliente de Adobe, la opción de entregar el sitio en AMP y nuevos puntos de extensión para agregar el proyecto CSS/JS.

* **Carpetas** de ContextHub: Posibilidad de crear carpetas de audiencia para organizar, buscar y seleccionar fácilmente segmentos de audiencia para utilizarlos en las funciones de objetivo de oferta de ContextHub.

## [!DNL Adobe Experience Manager Assets] como Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* **[!DNL Adobe Sensei]etiquetado** inteligente de vídeo con tecnología: Al aprovechar los modelos de AI para analizar el contenido de vídeo de etiquetas específicas de objetos y acciones, los usuarios de DAM pueden dedicar menos tiempo a añadir etiquetas y más tiempo a utilizar la información enriquecida expuesta para ofrecer la experiencia adecuada a los clientes. Consulte Recursos [de vídeo de etiquetas inteligentes](/help/assets/smart-tags-video-assets.md).

* **Mejoras** de Brand Portal: Las siguientes funciones nuevas y más están disponibles en [!DNL Brand Portal]. For details, see [[!DNL Brand Portal] release notes](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiencia](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) de descarga mejorada para descargas rápidas y simplificadas. Los administradores pueden configurar configuraciones de descarga adicionales para la oferta de una experiencia que se adapte a las necesidades de los usuarios y las empresas.
   * Ahora es posible navegar con un solo clic a Archivos, [colecciones](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/share/brand-portal-share-collection.html)y vínculos compartidos desde cualquier página.
   * Los usuarios pueden [seleccionar y descargar representaciones](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page) específicas ahora. La nueva opción de descarga de representación está disponible en el panel Representaciones de la página Detalles del recurso.
   * Un tiempo de espera de 15 minutos para sesiones de usuarios invitados garantiza una mejor experiencia a todos los usuarios simultáneos.

* **[!DNL Adobe Asset Link]versión 2.1**: Hay disponible una nueva versión de la extensión Vínculo [de recursos de](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Adobe para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] . Agrega compatibilidad con las últimas [!DNL Adobe Creative Cloud] aplicaciones con la versión 2021, publicada en octubre de 2020.

* **[!DNL Assets]Compatibilidad** con archivos WebP: [!DNL Assets] como Cloud Service ahora admite el formato de imagen WebP. WebP es un formato de imagen emergente creado por Google. Las imágenes en formato de archivo WebP no se distinguen visualmente de los archivos JPG o PNG y los archivos son mucho más pequeños. El menor tamaño de archivo de los recursos mejora los tiempos de carga de las páginas y ayuda a los creadores de contenido a ofrecer una experiencia web más rápida. Consulte [Creación de un perfil](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile)de procesamiento estándar.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia CIF Venia publicado - 2020.10.2 que incluye la última versión v1.4.0 de los componentes principales de CIF. Consulte [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obtener más detalles.

* Componentes principales de CIF v1.4.0. Consulte Componentes [principales de](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) CIF para obtener más detalles.

### Corrección de errores {#bug-fixes-commerce}

* Las solicitudes de GraphQL en la consola de producto y Pickers se realizaban a través del POST HTTP. Esto se ha solucionado para garantizar que el cliente Apollo GraphQL respete la configuración OSGi del cliente GraphQL para admitir solicitudes de GET si está configurada.

* La interfaz de usuario de configuración de CIF Cloud mostraba los botones &quot;Guardar y cerrar&quot; para las configuraciones en /lib y /apps/. Sin embargo, son de solo lectura, por lo que la IU se ha corregido para mostrar solo el botón &quot;Cerrar&quot;.


## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.11.0 es el 12 de noviembre de 2020.

### What is new in [!DNL Cloud Manager] {#what-is-new-cm}

* Ahora los usuarios pueden acceder a una nueva opción de menú Inicio de sesión **** local desde las opciones del menú entorno de las páginas de resumen de la tarjeta de **Entornos** y de los **Entornos** .
Consulte [Administración de Entornos](/help/implementing/cloud-manager/manage-environments.md##login-locally) para obtener más detalles.

* La ficha **Aprender** de Cloud Manager se ha actualizado con nuevas imágenes en la interfaz de usuario.

### Corrección de errores {#bug-fixes-cloud-manager}

* La carga de dependencias realizada antes de la ejecución de la compilación requería la descarga de un complemento de Maven.
* El vínculo del pie de página del Administrador de nubes para seleccionar un idioma ahora se desplazará a la ubicación correcta.
* A veces, durante la digitalización del código, el proceso SonarQube no se inicio. Esto se detectará automáticamente y se intentará reiniciar.
* Todas las tuberías de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo en función del título del flujo de trabajo, el modelo de flujo de trabajo, el estado, el iniciador, la ruta de carga útil y la fecha de Inicio. Consulte [Buscar instancias](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html)de flujo de trabajo.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Follow this section to learn about what is new and the updates for [Content Transfer Tool](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Release v1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con los registros. Marcas de hora agregadas a los registros de Extracción e ingesta. Mensaje agregado para indicar si los registros están vacíos.

### Corrección de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas con nombres de archivo parcialmente similares. Esto se ha solucionado.
