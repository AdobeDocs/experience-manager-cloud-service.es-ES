---
title: Notas de la versión 2020.10.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.10.0."
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 30%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 es el 28 de octubre de 2020.
La de la siguiente versión (2020.11.0) será el 1 de diciembre de 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* **[Componentes principales 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)**: Adobe Experience Manager as a Cloud Service se beneficia de las actualizaciones automáticas hasta la última versión de los componentes principales. La versión 2.12.0 incluye las mejoras más recientes aportadas por la comunidad. Las mejoras incluyen [un nuevo controlador de formularios de POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la capacidad de incluir CSS, JavaScript y metadatos personalizados [etiquetas a través de la configuración según el contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) y una [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar la integración de la capa de datos de Adobe en los componentes personalizados. Consulte la [lista de cambios](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) en 2.12.0.

* **[Arquetipo de proyecto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es)**: la base recomendada para iniciar un nuevo proyecto de Experience Manager mejoró. Ahora incluye el nuevo [Capa de datos del cliente de Adobe](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=es), opción a [entrega en AMP,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) y nuevo [puntos de extensión para agregar el proyecto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Carpetas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: capacidad para crear carpetas de audiencia para organizar, buscar y seleccionar fácilmente segmentos de audiencia que se utilizarán para las funciones de segmentación de ofertas de ContextHub.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

* **[!DNL Adobe Sensei]etiquetado inteligente de vídeo con tecnología**: Al aplicar modelos de IA para analizar el contenido de vídeo para etiquetas específicas de objetos y acciones, los usuarios de DAM pueden pasar menos tiempo agregando etiquetas y más tiempo utilizando la información expuesta y enriquecida. A su vez, ofrece la experiencia adecuada a los clientes. Consulte [Etiquetado inteligente de recursos de vídeo](/help/assets/smart-tags-video-assets.md).

* **Mejoras de Brand Portal**: Las siguientes nuevas funciones y más están disponibles en [!DNL Brand Portal]. Para obtener más información, consulte [[!DNL Brand Portal] notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiencia de descarga mejorada](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para descargas rápidas y simplificadas. Los administradores pueden configurar configuraciones de descarga adicionales para ofrecer una experiencia que se adapte a las necesidades de los usuarios y las empresas.
   * La navegación con un solo clic a Archivos, [Colecciones](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) y Vínculos compartidos ahora es posible desde cualquier página.
   * Los usuarios ya pueden [seleccionar y descargar representaciones específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nueva opción de descarga de representación está disponible en el panel Representaciones de la página Detalles del recurso.
   * Un tiempo de espera de 15 minutos para sesiones de usuarios invitados garantiza una mejor experiencia a todos los usuarios simultáneos.

* **[!DNL Adobe Asset Link]versión 2.1**: una nueva versión de [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) extensión para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], y [!DNL Adobe InDesign] está disponible. Añade compatibilidad con las últimas [!DNL Adobe Creative Cloud] aplicaciones con versión 2021, lanzadas en octubre de 2020.

* **[!DNL Assets]Compatibilidad con archivos WebP**: [!DNL Assets] as a Cloud Service ahora admite el formato de imagen WebP. WebP es un formato de imagen emergente creado por Google. Las imágenes en formato de archivo WebP no se distinguen visualmente de los archivos JPG o PNG y los archivos son mucho más pequeños. La reducción del tamaño de los archivos de los recursos mejora los tiempos de carga de página y ayuda a los creadores de contenido a ofrecer una experiencia web más rápida. Consulte cómo utilizar WebP en [crear perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## [!DNL Adobe Experience Manager Forms] as a Cloud Service {#forms-oct-2021}

### Novedades de [!DNL Forms] {#what-is-new-forms-oct-2021}

* **Analytics para Forms adaptable**: ahora puede capturar y rastrear el comportamiento del inicio de sesión y no inicio de sesión (anónimo) mediante Adobe Analytics para Forms adaptable para recopilar las perspectivas del usuario final. Ayuda a los usuarios empresariales a tomar decisiones informadas sobre el contenido, el diseño y el estilo del formulario adaptable en función de las perspectivas recopiladas.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms-oct-2021}

* **AEM Externalización de datos de flujo de trabajo de para un procesamiento seguro** AEM : puede almacenar datos de variables de flujo de trabajo de la en proceso que contengan elementos de datos personales confidenciales (SPD) en un repositorio administrado por el cliente para un procesamiento seguro. AEM Al procesar el flujo de trabajo, los datos almacenados en las variables de flujo de trabajo no se conservan en el repositorio de. Se obtiene bajo demanda del repositorio administrado por el cliente.

### Características beta de [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) le ayuda a combinar una plantilla y datos XML para generar documentos en varios formatos. El servicio le permite generar documentos en modo sincrónico y por lotes.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Lanzamiento del sitio de referencia de CIF Venia 2020.10.2, que incluye la versión más reciente de los componentes principales de CIF 1.4.0. Consulte [Sitio de referencia de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obtener más información.

* Componentes principales de CIF v1.4.0. Consulte [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obtener más información.

### Correcciones de errores {#bug-fixes-commerce}

* Las solicitudes de GraphQL que se encontraban en la consola de producto y los seleccionadores se realizaban mediante el POST HTTP. Este problema se ha corregido para garantizar que el cliente de Apollo GraphQL respete la configuración de OSGi del cliente de GraphQL para admitir solicitudes de GET si se configura.

* La interfaz de usuario de configuración de CIF Cloud muestra los botones &quot;Guardar y cerrar&quot; para las configuraciones en /lib y /apps/. Pero estas interfaces son de solo lectura, por lo que la interfaz de usuario se fija para mostrar solo el botón &quot;Cerrar&quot;.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en Experience Manager as a Cloud Service 2020.10.0 es el 2 de octubre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Se rediseñó la página Entornos.

* Cuando están en hibernación, los entornos en hibernación ahora muestran el estado discreto en Cloud Manager.

* El &quot;contenedor de compilación&quot; de Cloud Manager ahora es compatible con la compilación de proyectos mediante Java™ 8 o Java™ 11. El sistema de herramientas de Maven proporciona compatibilidad con Java™ 11.

* Se aumentó el número de variables de entorno por entorno a 200.

* La tarjeta Entorno de la página Información general ahora enumera hasta tres entornos. Los usuarios pueden seleccionar el botón **Mostrar todo** para ir a la página Resumen de entornos y ver una tabla con una lista completa de entornos.
Consulte [Entorno de visualización](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Correcciones de errores {#bug-fixes-cloud-manager}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa de zona protegida.

* Los botones Cancelar y Guardar de la página Editar la canalización que no es de producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Al crear un programa, el nombre sugerido a veces devolvía un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y Dispatcher cuando no había ninguno presente.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo basadas en el Título de flujo de trabajo, Modelo de flujo de trabajo, Estado, Iniciador, Ruta de carga útil y Fecha de inicio. Consulte [Buscar instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Herramienta de transferencia de contenido {#content-transfer-tool}

Obtenga más información sobre novedades y actualizaciones de [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang?es) Versión v1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con registros. Marcas de hora agregadas a los registros de extracción e ingesta. Se ha agregado un mensaje para indicar si los registros están vacíos.

### Correcciones de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas de acceso con nombres de archivo parcialmente similares.
