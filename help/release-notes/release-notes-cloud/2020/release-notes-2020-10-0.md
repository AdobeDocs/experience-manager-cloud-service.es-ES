---
title: Notas de la versión 2020.10.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] notas de la versión de as a Cloud Service para 2020.10.0.'
exl-id: ac741744-5b47-47a4-b5af-e1089e92c3f0
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 26%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service 2020.10.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service 2020.10.0.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2020.10.0 es el 28 de octubre de 2020.
La siguiente versión (2020.11.0) será el 1 de diciembre de 2020.

## [!DNL Adobe Experience Manager Sites] como Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* **[Componentes principales 2.12.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)**: AEM como Cloud Service se beneficia de las actualizaciones automáticas de la última versión de los componentes principales. La versión 2.12.0 incluye las últimas mejoras aportadas por la comunidad, como [un nuevo controlador de formulario de POST;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/forms/form-container.html#post-data) la capacidad de incluir etiquetas CSS, Javascript y [de metadatos personalizadas mediante la configuración de reconocimiento de contexto;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading) y una utilidad [`DataLayerBuilder`](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/integrations.html#enabling-custom-components) para simplificar la integración de la capa de datos de Adobe en componentes personalizados. Consulte la [lista de cambios](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.12.0) en 2.12.0.

* **[Tipo de archivo del proyecto 24](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)**: La base recomendada para iniciar un nuevo proyecto de AEM ha mejorado, ya que ahora incluye la nueva capa [ de datos del cliente de ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html)Adobe, la opción de  [enviar el sitio en AMP ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html) y los nuevos puntos de  [extensión para agregar el proyecto CSS/JS.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/including-clientlibs.html#context-aware-loading)

* **[Carpetas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md#organizing-segments)**: Posibilidad de crear carpetas de audiencia para organizar, buscar y seleccionar fácilmente segmentos de audiencia para utilizarlos para las capacidades de segmentación de ofertas de ContextHub.

## [!DNL Adobe Experience Manager Assets] como Cloud Service {#assets}

* **[!DNL Adobe Sensei]etiquetado inteligente de vídeo con tecnología**: Al aprovechar los modelos de IA para analizar el contenido de vídeo para etiquetas específicas de objetos y acciones, los usuarios de DAM pueden dedicar menos tiempo a añadir etiquetas y más tiempo a utilizar la información enriquecida expuesta para ofrecer la experiencia correcta a los clientes. Consulte [Recursos de vídeo de etiquetas inteligentes](/help/assets/smart-tags-video-assets.md).

* **Mejoras** de Brand Portal: Las siguientes funciones nuevas y más están disponibles en  [!DNL Brand Portal]. Para obtener más información, consulte [[!DNL Brand Portal] notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal-release-notes.html).

   * [Experiencia de descarga mejorada ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html) para descargas rápidas y simplificadas. Los administradores pueden configurar configuraciones de descarga adicionales para ofrecer una experiencia que se adapte a las necesidades de los usuarios y las empresas.
   * La navegación con un solo clic a Archivos, [Colecciones](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/share/brand-portal-share-collection.html) y Vínculos compartidos ahora es posible desde cualquier página.
   * Los usuarios ya pueden [seleccionar y descargar representaciones específicas](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html#download-assets-from-asset-details-page). La nueva opción de descarga de representación está disponible en el panel Representaciones de la página Detalles del recurso.
   * Un tiempo de espera de 15 minutos para sesiones de usuarios invitados garantiza una mejor experiencia a todos los usuarios simultáneos.

* **[!DNL Adobe Asset Link]versión 2.1**: Hay disponible una nueva versión de  [Adobe Asset ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) Linkextension para  [!DNL Adobe Photoshop],  [!DNL Adobe Illustrator], y  [!DNL Adobe InDesign] . Agrega compatibilidad con las últimas [!DNL Adobe Creative Cloud] aplicaciones con la versión 2021, publicada en octubre de 2020.

* **[!DNL Assets]Compatibilidad con** archivos WebP:  [!DNL Assets] como Cloud Service ahora es compatible con el formato de imagen WebP. WebP es un formato de imagen emergente creado por Google. Las imágenes en formato de archivo WebP son visualmente indistinguibles de archivos JPG o PNG y los archivos son mucho más pequeños. El menor tamaño de archivo de los recursos mejora los tiempos de carga de página y ayuda a los creadores de contenido a ofrecer una experiencia web más rápida. Consulte cómo utilizar WebP en [crear perfil de procesamiento](/help/assets/asset-microservices-configure-and-use.md#create-standard-profile).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia de Venia del CIF publicado - 2020.10.2 que incluye la última versión de los componentes principales del CIF v1.4.0. Consulte el [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.2) para obtener más información.

* Componentes principales de CIF v1.4.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.4.0) para obtener más información.

### Corrección de errores {#bug-fixes-commerce}

* Las solicitudes de GraphQL en la consola de producto y los seleccionadores se realizaban mediante el POST HTTP. Esto se ha solucionado para garantizar que el cliente de Apollo GraphQL respete la configuración de OSGi del cliente de GraphQL para admitir solicitudes de GET si están configuradas.

* La interfaz de usuario de configuración de CIF Cloud mostraba los botones &quot;Guardar y cerrar&quot; para las configuraciones en /lib y /apps/. Sin embargo, son de solo lectura, por lo que la IU se ha corregido para mostrar solo el botón &quot;Cerrar&quot;.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.10.0 es el 2 de octubre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* La página Entornos se ha rediseñado.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* El contenedor de compilación de Cloud Manager ahora es compatible con la compilación de proyectos mediante Java 8 o Java 11. El sistema de herramientas Maven proporciona compatibilidad con Java 11.

* Se aumentó el número de variables de entorno por entorno a 200.

* La tarjeta Entorno de la página Información general ahora enumera hasta tres entornos. Los usuarios pueden seleccionar el botón **Mostrar todo** para ir a la página de resumen de entorno y ver una tabla con una lista completa de entornos.
Consulte [Entorno de visualización](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Corrección de errores {#bug-fixes-cloud-manager}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Los botones Cancelar y Guardar de la página Edición de canalización no de producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Algunas veces al crear un nuevo programa, el nombre sugerido era un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo en función del título del flujo de trabajo, el modelo de flujo de trabajo, el estado, el iniciador, la ruta de carga útil y la fecha de inicio. Consulte [Buscar instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la [herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) versión v1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con los registros. Marcas de hora agregadas a los registros de extracción e ingesta. Mensaje añadido para indicar si los registros están vacíos.

### Corrección de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas con nombres de archivo parcialmente similares. Esto se ha solucionado.
