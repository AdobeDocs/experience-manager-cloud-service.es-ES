---
title: Notas de la versión 2021.7.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2021.7.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 13%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión actual (2021.7.0) es el 29 de julio de 2021.
La siguiente versión (2021.8.0) es el 26 de agosto de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de julio de 2021](https://video.tv.adobe.com/v/335580) vídeo para ver un resumen de las funciones añadidas.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Novedades {#what-is-new-foundation}

* Configuración de Dispatcher más flexible: Los proyectos se pueden organizar más fácilmente. Por ejemplo, ahora puede incluir varios archivos de reglas de reescritura que reflejen la estructura del sitio. [Obtenga información sobre](/help/implementing/dispatcher/disp-overview.md#validation-debug) este modo flexible, que incluye cómo estructurar la configuración de Dispatcher para aprovecharla.
* La interfaz de usuario de replicación de árbol en la pestaña &quot;Distribuir&quot; del agente de replicación debe considerarse obsoleta y está planificado que se elimine después del 30 de septiembre. [Obtenga información sobre](/help/operations/replication.md#tree-activation) estrategias de replicación alternativas.
* Paquete `org.apache.sling.datasource-1.0.4.jar` se ha eliminado la compatibilidad con fuentes de datos de Sling, ya que esta funcionalidad está obsoleta y los clientes no la utilizan.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* La funcionalidad de automatización de contenido permite [!DNL Experience Manager Assets] aproveche el [!DNL Adobe Creative Cloud] API para automatizar la producción de recursos a escala. Mejora la velocidad del contenido al reducir drásticamente el tiempo necesario y las iteraciones necesarias para crear variaciones del mismo recurso. La funcionalidad no requiere programación alguna y funciona desde DAM. Consulte [generar variaciones de recursos mediante la integración de Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] incluye el [!DNL Document Cloud] Visor de PDF para obtener una vista previa nativa de los documentos PDF. Esta función permite a los usuarios obtener una vista previa de los archivos PDF de varias páginas sin necesidad de realizar ninguna conversión o procesamiento de archivos. Esta función mejora la paridad con [!DNL Experience Manager] 6.5. Los controles disponibles en el visor incluyen zoom, navegación a páginas, desacoplamiento de controles y visualización en pantalla completa. El caso de los usuarios también permite obtener una vista previa y saltar a páginas y marcadores. Los comentarios sobre el archivo en sí son compatibles y los comentarios y anotaciones sobre el contenido dentro del archivo PDF se añadirán en una versión futura.

   ![Vista previa de archivos PDF en [!DNL Experience Manager] uso del visor de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* La funcionalidad de descarga de Linkshare utiliza descargas asincrónicas que aumentan la velocidad de descarga. Consulte [Descargar recursos compartidos mediante el uso compartido de vínculos](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Descargar bandeja de entrada](/help/assets/assets/download-inbox.png)

* La configuración de vista se mejora para permitir a los usuarios elegir una vista predeterminada y un parámetro de ordenación predeterminado.

   ![Definir la vista predeterminada en [!UICONTROL Configuración de vista]](/help/assets/assets/view-settings-for-defaults.png)

* Los usuarios pueden buscar y filtrar las carpetas en función de los predicados de propiedades.

   ![Filtrado de carpetas de búsqueda mediante predicados de búsqueda](/help/assets/assets/search-folders-via-predicates.png)

### Nuevas funciones disponibles en la [!DNL Assets] canal de prelanzamiento {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Cuando comparte recursos digitales como un vínculo, los usuarios pueden copiar la URL en el portapapeles. La mejora permite compartir recursos de una forma más rápida y práctica.

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

La API `com.day.cq.dam.api.collection.SmartCollection` no está disponible en [!DNL Experience Manager] como [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* Ahora puede utilizar el servicio de Automated forms conversion para [convertir PDF forms en francés, alemán y español](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) a formularios adaptables.
* Se ha agregado un panel independiente al editor de plantillas para mostrar los errores relacionados con los componentes de los formularios adaptables. Ayuda a consolidar todos los errores de formularios adaptables en una ubicación y a reducir el tiempo de resolución.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=es) le ayuda a combinar plantillas XDP y datos XML para generar documentos de impresión en distintos formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede:
   * Generar documentos rellenando archivos de plantilla con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere archivos de PDF de impresión desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

* **Externalizador de datos de variable**: Puede guardar datos de AEM variables de flujo de trabajo en un sistema de almacenamiento externo administrado por su organización.

* **Documento de registro basado en Acrobat**: También puede [usar el PDF de formularios de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) como plantilla para Document of Record además de la plantilla de formulario basada en XFA.

* **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el Modelo de datos de formulario al almacenamiento de Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Permite recuperar y almacenar datos de formulario adaptables en Microsoft Azure Storage as a BLOB.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes principales de CIF v2
   * Configuraciones simplificadas y mejoradas para URL PDP/PLP y SEO
   * Indicador visual para datos de productos clasificados en modo de creación para una mejor visibilidad de los próximos cambios
   * Nuevo componente de mapa del sitio para páginas de contenido y comercio

* Compatibilidad con [Recomendación de producto de Adobe Commerce Sensei, con tecnología de Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) en AEM tienda utilizando recomendaciones predefinidas o creadas sobre la marcha

## [!DNL Experience Manager Screens] como [!DNL Cloud Service] {#screens}

### Corrección de errores {#bug-fixes-screens}

* La configuración del proveedor de contenido ahora se valida durante la creación o actualización.

* Todas las vistas de visualización tienen una columna de carpetas.

* Puede expandir la estructura de contenido de Screens.

* `bulk-offline-update-service` faltaban todos los permisos para algunos entornos.

* Se ha actualizado el vínculo Ayuda para que coincida con la nueva documentación de la nube de pantallas.

* No asigne listas de reproducción y no permita quitar listas de reproducción con los reproductores asignados, ahora funciona.

* El reproductor ahora vuelve a descargar los recursos cuando se borra la caché &quot;ALL&quot;.

* La programación repetida ahora funciona si la variable *Hora de finalización* está configurado para el día siguiente.

* `Back&Forward` ahora funciona en la IU as a Cloud Service de Screens.

* Antes no se podían crear etiquetas con el mismo nombre pero con diferentes áreas de nombres.

## Documentación XML para Experience Manager as a Cloud Service {#xml-documentation}

### Novedades {#what-is-new-xml-documentation}

La documentación XML para el Experience Manager as a Cloud Service está disponible de forma general. Permite a los clientes as a Cloud Service Experience Manager adquirir un complemento de documentación XML para importar, crear, administrar y entregar contenido técnico en varios canales, incluido Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.7.0.

### Fecha de la versión {#release-cm-july}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.7.0 es el 15 de julio de 2021.
La próxima versión está planificada para el 12 de agosto de 2021.

### Novedades {#what-is-new-cm-july}

* Los clientes ahora pueden utilizar Azul 8 y 11 JDK para sus procesos de construcción de Cloud Manager y pueden seleccionar utilizar uno de estos JDK para complementos Maven compatibles con las cadenas de herramientas *o* la ejecución completa del proceso Maven.

* La dirección IP de salida saliente ahora se registrará en el archivo de registro de paso de compilación.

* Los entornos de fase y producción que ejecutan versiones antiguas de AEM ahora informarán del estado de **Actualización disponible**.

* El número máximo de certificados SSL admitidos ha aumentado a 20 por programa.

* El número máximo de dominios que se pueden configurar ha aumentado a 500 por entorno.

* La variable **Administrar Git** se ha cambiado **Acceder a información de Git** y el cuadro de diálogo se ha actualizado visualmente.

* La versión del tipo de archivo del proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 28.

### Corrección de errores {#bug-fixes-cm-july}

* En algunos casos, Vista previa no era una opción disponible al enlazar una Lista de permitidos IP a un entorno.

* La navegación manual a la página de detalles de ejecución para una ejecución no existente no mostraba un error, solo una pantalla de carga interminable.

* El mensaje de error que se muestra cuando se alcanza el número máximo de certificados SSL no es útil.

* En algunas circunstancias, podría haber una discrepancia en la versión de la canalización que se muestra en la tarjeta de la canalización en la **Información general** página.

* El asistente Agregar programa indicó incorrectamente que el nombre no se puede cambiar después de la creación.

### Problemas conocidos {#known-issues-cm-july}

Los clientes que cambien a utilizar Azul JDKs deben tener en cuenta que no todas las aplicaciones existentes se compilarán sin error en Azul JDK. Se recomienda realizar pruebas locales antes de cambiar.

## Cloud Acceleration Manager {#cam}

### Fecha de la versión {#release-date-july-cam}

La fecha de versión de Cloud Acceleration Manager es el 15 de julio de 2021.

### Novedades {#what-is-new-cam}

Cloud Acceleration Manager es una aplicación basada en la nube diseñada para guiar a sus equipos de TI a lo largo del recorrido de transición, desde la planificación hasta la puesta en marcha del Cloud Service. Configure sus equipos para una migración correcta con prácticas recomendadas por el Adobe, sugerencias, documentación y herramientas que le ayudarán en cada fase del recorrido a AEM como Cloud Service. Más información [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Marque esta [Vídeo de demostración de Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
