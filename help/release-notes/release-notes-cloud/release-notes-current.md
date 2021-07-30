---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 76d068de881edce2324ceb73f1a724ff0f5f585c
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 2%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] como Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de la versión actual de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.7.0) es el 29 de julio de 2021.
La siguiente versión (2021.8.0) es el 26 de agosto de 2021.

## Vídeo de la versión {#release-video}

Consulte el vídeo [Información general de la versión de julio de 2021](https://video.tv.adobe.com/v/335580) para ver un resumen de las funciones agregadas.

## Experience Manager Foundation como Cloud Service {#foundation}

### Novedades {#what-is-new-foundation}

* Configuración de Dispatcher más flexible: Los proyectos se pueden organizar más fácilmente. Por ejemplo, ahora puede incluir varios archivos de reglas de reescritura que reflejen la estructura del sitio. [Obtenga información ](/help/implementing/dispatcher/disp-overview.md#validation-debug) sobre este modo flexible, incluida cómo estructurar la configuración de Dispatcher para aprovecharla.
* La interfaz de usuario de replicación de árbol en la pestaña &quot;Distribuir&quot; del agente de replicación debe considerarse obsoleta y está planificado que se elimine después del 30 de septiembre. [Conozca ](/help/operations/replication.md#tree-activation) las estrategias de replicación alternativas.
* Se ha eliminado el paquete `org.apache.sling.datasource-1.0.4.jar` para la compatibilidad con fuentes de datos de Sling, ya que tiene una funcionalidad obsoleta y los clientes no lo utilizan.

## Documentación XML para Experience Manager as a Cloud Service {#xml-documentation}

### Novedades {#what-is-new-xml-documentation}

La documentación XML para Experience Manager como Cloud Service está disponible de forma general. Permite a los clientes Experience Manager como Cloud Service adquirir un complemento de documentación XML para importar, crear, administrar y entregar contenido técnico en varios canales, incluidos los sitios Experience Manager.

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.7.0.

### Fecha de la versión {#release-cm-july}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.7.0 es el 15 de julio de 2021.
La próxima versión está planificada para el 12 de agosto de 2021.

### Novedades {#what-is-new-cm-july}

* Los clientes ahora pueden utilizar Azul 8 y 11 JDK para sus procesos de compilación de Cloud Manager y pueden seleccionar usar uno de estos JDK para complementos Maven compatibles con las cadenas de herramientas *o* para toda la ejecución del proceso Maven.

* La dirección IP de salida saliente ahora se registrará en el archivo de registro de paso de compilación.

* Los entornos de fase y producción que ejecutan versiones antiguas de AEM ahora informarán de un estado de **Actualización disponible**.

* El número máximo de certificados SSL admitidos ha aumentado a 20 por programa.

* El número máximo de dominios que se pueden configurar ha aumentado a 500 por entorno.

* Los botones **Administrar Git** se han cambiado a **Información de Git de acceso** y el cuadro de diálogo se ha actualizado visualmente.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 28.

### Corrección de errores {#bug-fixes-cm-july}

* En algunos casos, Vista previa no era una opción disponible al enlazar una Lista de permitidos IP a un entorno.

* La navegación manual a la página de detalles de ejecución para una ejecución no existente no mostraba un error, solo una pantalla de carga interminable.

* El mensaje de error que se muestra cuando se alcanza el número máximo de certificados SSL no es útil.

* En algunas circunstancias, podría haber una discrepancia en la versión de la versión mostrada en la tarjeta de canalización de la página **Información general**.

* El asistente Agregar programa indicó incorrectamente que el nombre no se puede cambiar después de la creación.

### Problemas conocidos {#known-issues-cm-july}

Los clientes que cambien a utilizar Azul JDKs deben tener en cuenta que no todas las aplicaciones existentes se compilarán sin error en Azul JDK. Se recomienda realizar pruebas locales antes de cambiar.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones en [!DNL Assets] {#assets-features}

* La funcionalidad de automatización de contenido permite a [!DNL Experience Manager Assets] aprovechar las API [!DNL Adobe Creative Cloud] para automatizar la producción de recursos a escala. Mejora la velocidad del contenido al reducir drásticamente el tiempo necesario y las iteraciones necesarias para crear variaciones del mismo recurso. La funcionalidad no requiere programación alguna y funciona desde DAM. Consulte [generación de variaciones de recursos mediante integración de Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] incluye el visor de  [!DNL Document Cloud] PDF para previsualizar los documentos PDF de forma nativa. Esta función permite a los usuarios previsualizar archivos PDF de varias páginas sin necesidad de realizar ningún tipo de conversión o procesamiento de archivos. Esta función mejora la paridad con [!DNL Experience Manager] 6.5. Los controles disponibles en el visor incluyen zoom, navegación a páginas, controles de desacoplamiento y visualización en pantalla completa. El caso de los usuarios también permite obtener una vista previa y saltar a páginas y marcadores. Los comentarios sobre el archivo son compatibles y los comentarios y anotaciones sobre el contenido del archivo PDF se añadirán en una versión futura.

   ![Vista previa de archivos PDF en  [!DNL Experience Manager] el visor de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* La funcionalidad de descarga de Linkshare utiliza descargas asincrónicas que aumentan la velocidad de descarga. Consulte [Descargar recursos compartidos mediante el uso compartido de vínculos](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Descargar bandeja de entrada](/help/assets/assets/download-inbox.png)

* La configuración de vista se mejora para permitir a los usuarios elegir una vista predeterminada y un parámetro de ordenación predeterminado.

   ![Definir la vista predeterminada en Configuración  [!UICONTROL de vista]](/help/assets/assets/view-settings-for-defaults.png)

* Los usuarios pueden buscar y filtrar las carpetas en función de los predicados de propiedades.

   ![Filtrado de carpetas de búsqueda mediante predicados de búsqueda](/help/assets/assets/search-folders-via-predicates.png)

### Nuevas funciones disponibles en el canal de prelanzamiento [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Cuando comparte recursos digitales como un vínculo, los usuarios pueden copiar la URL en el portapapeles. La mejora permite compartir recursos de una forma más rápida y práctica.

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

La API `com.day.cq.dam.api.collection.SmartCollection` no está disponible en [!DNL Experience Manager] como [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Screens] como  [!DNL Cloud Service] {#screens}

### Corrección de errores {#bug-fixes-screens}

* La configuración del proveedor de contenido ahora se valida durante la creación o actualización.

* Todas las vistas de visualización tienen una columna de carpetas.

* Puede expandir la estructura de contenido de Screens.

* `bulk-offline-update-service` faltaban todos los permisos para algunos entornos.

* Se ha actualizado el vínculo Ayuda para que coincida con la nueva documentación de la nube de pantallas.

* No asigne listas de reproducción y no permita quitar listas de reproducción con los reproductores asignados, ahora funciona.

* El reproductor ahora vuelve a descargar los recursos cuando se borra la caché &quot;ALL&quot;.

* La programación repetida ahora funciona si la *Hora de finalización* está configurada para el día siguiente.

* `Back&Forward` ahora funciona en Screens as a Cloud Service UI.

* Antes no se podían crear etiquetas con el mismo nombre pero con diferentes áreas de nombres.

## [!DNL Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* Ahora puede utilizar el servicio de Automated forms conversion para [convertir PDF forms en francés, alemán y español](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) a formularios adaptables.
* Se ha agregado un panel independiente al editor de plantillas para mostrar los errores relacionados con los componentes de los formularios adaptables. Ayuda a consolidar todos los errores de formularios adaptables en una ubicación y a reducir el tiempo de resolución.

### Nuevas funciones disponibles en el canal de prelanzamiento [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**:  [Communication ](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html) APIShelp permite combinar plantillas XDP y datos XML para generar documentos de impresión en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones que le permitan:
   * Genere documentos rellenando archivos de plantilla con datos XML.
   * Genere formularios de salida en varios formatos, incluidas secuencias de impresión PDF no interactivas.
   * Genere archivos PDF de impresión desde un formulario XFA PDF y un formulario Adobe Acrobat.

* **Externalizador de datos de variable**: Puede guardar datos de AEM variables de flujo de trabajo en un sistema de almacenamiento externo administrado por su organización.

* **Documento de registro basado en Acrobat**: También puede  [utilizar Adobe Acrobat Form PDF (Acrobat PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html)  como plantilla para Documento de registro, además de la plantilla de formulario basada en XFA.

* **Conector** del almacén de datos de Microsoft Azure: Ahora puede  [conectar el Modelo de datos de formulario al Almacenamiento](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html) de Microsoft Azure. Permite recuperar y almacenar datos de formulario adaptables en Microsoft Azure Storage as a BLOB.

## Cloud Acceleration Manager {#cam}

### Fecha de la versión {#release-date-july-cam}

La fecha de versión de Cloud Acceleration Manager es el 15 de julio de 2021.

### Novedades {#what-is-new-cam}

Cloud Acceleration Manager es una aplicación basada en la nube diseñada para guiar a sus equipos de TI a lo largo del recorrido de transición, desde la planificación hasta la puesta en marcha del Cloud Service. Configure sus equipos para una migración correcta con prácticas recomendadas por el Adobe, sugerencias, documentación y herramientas que le ayudarán en cada fase del recorrido a AEM como Cloud Service. Obtenga más información [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Compruebe este [vídeo de demostración de Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes principales de CIF v2
   * Configuraciones simplificadas y mejoradas para URL PDP/PLP y SEO
   * Indicador visual para datos de productos clasificados en modo de creación para una mejor visibilidad de los próximos cambios
   * Nuevo componente de mapa del sitio para páginas de contenido y comercio

* Compatibilidad con la recomendación de producto [Adobe Commerce Sensei, con tecnología de Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) en AEM Tienda, con recomendaciones predefinidas o creadas sobre la marcha
