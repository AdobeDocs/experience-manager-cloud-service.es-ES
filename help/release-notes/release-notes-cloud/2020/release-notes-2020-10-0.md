---
title: Notas de la versión 2020.10.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.10.0."'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 23%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 es el 28 de octubre de 2020.
La siguiente versión (2020.11.0) será el 1 de diciembre de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* **[Componentes principales 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)**: Adobe Experience Manager as a Cloud Service se beneficia de las actualizaciones automáticas de la última versión de los componentes principales. La versión 2.12.0 incluye las últimas mejoras aportadas por la comunidad. Las mejoras incluyen [un nuevo controlador de formulario de POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la capacidad de incluir CSS, JavaScript y metadatos personalizados [etiquetas mediante la configuración según el contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) y [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar la integración de la capa de datos de Adobe en los componentes personalizados. Consulte la [lista de cambios](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) en 2.12.0.

* **[Tipo de archivo del proyecto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: La base recomendada para iniciar un nuevo proyecto de Experience Manager mejoró. Ahora incluye el nuevo [Capa de datos del cliente de Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html), opción [entregar sitio en AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) y nuevas [puntos de extensión para agregar el proyecto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Carpetas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Posibilidad de crear carpetas de audiencia para organizar, buscar y seleccionar fácilmente segmentos de audiencia para utilizarlos para las capacidades de segmentación de ofertas de ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]etiquetado inteligente de vídeo con tecnología**: Al aplicar modelos de IA para analizar el contenido de vídeo de las etiquetas específicas de objetos y acciones, los usuarios de DAM pueden dedicar menos tiempo a añadir etiquetas y más tiempo utilizando la información enriquecida y expuesta. A su vez, ofrece la experiencia adecuada a los clientes. Consulte [Recursos de vídeo de etiquetas inteligentes](/help/assets/smart-tags-video-assets.md).

* **Mejoras de Brand Portal**: Las siguientes funciones nuevas y más están disponibles en [!DNL Brand Portal]. Para obtener más información, consulte [[!DNL Brand Portal] notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiencia de descarga mejorada](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para descargas rápidas y simplificadas. Los administradores pueden configurar configuraciones de descarga adicionales para ofrecer una experiencia que se adapte a las necesidades de los usuarios y las empresas.
   * La navegación con un solo clic a Archivos, [Colecciones](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) y Vínculos compartidos ahora es posible desde cualquier página.
   * Los usuarios ya pueden [seleccionar y descargar representaciones específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nueva opción de descarga de representación está disponible en el panel Representaciones de la página Detalles del recurso.
   * Un tiempo de espera de 15 minutos para sesiones de usuarios invitados garantiza una mejor experiencia a todos los usuarios simultáneos.

* **[!DNL Adobe Asset Link]versión 2.1**: Una nueva versión de [Vínculo de recurso de Adobe](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) extensión para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] está disponible. Añade compatibilidad con las últimas [!DNL Adobe Creative Cloud] aplicaciones con versión 2021, publicada en octubre de 2020.

* **[!DNL Assets]Compatibilidad con archivos WebP**: [!DNL Assets] as a Cloud Service ahora admite el formato de imagen WebP. WebP es un formato de imagen emergente creado por Google. Las imágenes en formato de archivo WebP son visualmente indistinguibles de los archivos JPG o PNG y los archivos son mucho más pequeños. El menor tamaño de archivo de los recursos mejora los tiempos de carga de página y ayuda a los creadores de contenido a ofrecer una experiencia web más rápida. Consulte cómo utilizar WebP en [crear perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Novedades de [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptable**: Ahora puede capturar y rastrear el comportamiento tanto de inicio de sesión como de no inicio de sesión (anónimo) a través de Adobe Analytics for Adaptive Forms para recopilar perspectivas del usuario final. Ayuda a los usuarios empresariales a tomar decisiones informadas sobre el contenido, el diseño y el estilo del formulario adaptable en función de las perspectivas recopiladas.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **Externalización AEM datos de flujo de trabajo para un procesamiento seguro**: Puede almacenar datos de variables de flujo de trabajo en proceso AEM que contengan elementos de datos personales confidenciales (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. Durante el procesamiento del flujo de trabajo, los datos almacenados en variables de flujo de trabajo no se guardan en AEM repositorio. Se obtiene a petición del repositorio administrado por el cliente.

### Funciones beta de [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) le ayuda a combinar una plantilla y los datos XML para generar documentos en distintos formatos. El servicio le permite generar documentos en modo sincrónico y por lotes.

Puede escribir en [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia de Venia del CIF publicado - 2020.10.2 que incluye la última versión v1.4.0 de los componentes principales del CIF. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obtener más información.

* Componentes principales de CIF v1.4.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obtener más información.

### Correcciones de errores {#bug-fixes-commerce}

* Las solicitudes de GraphQL que estaban en la consola de producto y los seleccionadores se realizaban mediante el POST HTTP. Este problema se ha solucionado para garantizar que el cliente de Apollo GraphQL respete la configuración OSGi del cliente de GraphQL para admitir solicitudes de GET si están configuradas.

* La interfaz de usuario de configuración de CIF Cloud mostraba los botones &quot;Guardar y cerrar&quot; para las configuraciones en /lib y /apps/. Sin embargo, estas interfaces son de solo lectura, por lo que la IU se ha corregido para mostrar solo el botón &quot;Cerrar&quot;.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en el Experience Manager as a Cloud Service 2020.10.0 es el 2 de octubre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* La página Entornos se ha rediseñado.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* El &quot;contenedor de compilación&quot; de Cloud Manager ahora es compatible con la compilación de proyectos mediante Java™ 8 o Java™ 11. El sistema de herramientas Maven proporciona compatibilidad con Java™ 11.

* Se aumentó el número de variables de entorno por entorno a 200.

* La tarjeta Entorno de la página Información general ahora enumera hasta tres entornos. Los usuarios pueden seleccionar **Mostrar todo** para ir a la página Environment summary y ver una tabla con una lista completa de entornos.
Consulte [Entorno de visualización](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Correcciones de errores {#bug-fixes-cloud-manager}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Los botones Cancelar y Guardar de la página Edición de canalización no de producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Al crear un programa, el nombre sugerido a veces devolvía un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y Dispatcher cuando no había ninguno presente.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo en función del título del flujo de trabajo, el modelo de flujo de trabajo, el estado, el iniciador, la ruta de carga útil y la fecha de inicio. Consulte [Buscar instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Herramienta de transferencia de contenido {#content-transfer-tool}

Obtenga más información sobre las novedades y las actualizaciones de [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versión 1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con los registros. Marcas de hora agregadas a los registros de extracción e ingesta. Mensaje añadido para indicar si los registros están vacíos.

### Correcciones de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas con nombres de archivo parcialmente similares.
