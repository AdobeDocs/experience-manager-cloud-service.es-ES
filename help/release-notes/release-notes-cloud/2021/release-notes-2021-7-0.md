---
title: Notas de la versión 2021.7.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.7.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 50%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versión actual (2021.7.0) es el 29 de julio de 2021.
La de la siguiente versión (2021.8.0) es el 26 de agosto de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general de la versión de julio de 2021](https://video.tv.adobe.com/v/335580) para ver un resumen de las funciones añadidas.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Novedades {#what-is-new-foundation}

* Configuración de Dispatcher más flexible: los proyectos se pueden organizar más fácilmente. Por ejemplo, ahora puede incluir varios archivos de reglas de reescritura que reflejen la estructura del sitio. [Más información](/help/implementing/dispatcher/disp-overview.md#validation-debug) este modo flexible incluye información sobre cómo estructurar la configuración de dispatcher para que pueda aprovecharla.
* La IU de replicación de árbol en la pestaña Distribuir del agente de replicación debe considerarse obsoleta y se planea eliminarla después del 30 de septiembre. [Más información](/help/operations/replication.md#tree-activation) estrategias de replicación alternativas.
* Paquete `org.apache.sling.datasource-1.0.4.jar` para la compatibilidad con fuentes de datos Sling se ha eliminado, ya que su funcionalidad está obsoleta y los clientes no la utilizan.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* La funcionalidad de automatización de contenido permite [!DNL Experience Manager Assets] use el [!DNL Adobe Creative Cloud] API para automatizar la producción de recursos a escala. Mejora la velocidad del contenido al reducir drásticamente el tiempo necesario y las iteraciones necesarias para crear variaciones del mismo recurso. La funcionalidad no requiere programación alguna y funciona desde DAM. Consulte [generación de variaciones de recursos mediante la integración de Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] incluye el [!DNL Document Cloud] Visor de PDF para previsualizar documentos de PDF de forma nativa. Esta función permite a los usuarios previsualizar archivos de PDF de varias páginas sin ningún tipo de conversión o procesamiento de archivos. Esta función mejora la paridad con [!DNL Experience Manager] 6.5. Los controles disponibles en el visor incluyen zoom, navegación a páginas, controles de desacoplamiento y visualización en pantalla completa. Los casos de usuario también previsualizan y saltan a páginas y marcadores. Se admiten comentarios en el propio archivo. Los comentarios y anotaciones sobre el contenido del archivo del PDF se añadirán en una versión futura.

  ![Previsualización de archivos de PDF en [!DNL Experience Manager] uso del Visor de PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* La funcionalidad de descarga de Linkshare utiliza descargas asincrónicas que aumentan la velocidad de descarga. Consulte [Descargar recursos compartidos mediante el uso compartido de vínculos](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Descargar bandeja de entrada](/help/assets/assets/download-inbox.png)

* La configuración de vista se mejora para permitir que los usuarios elijan una vista predeterminada y un parámetro de ordenación predeterminado.

  ![Establecer vista predeterminada en [!UICONTROL Configuración de vista]](/help/assets/assets/view-settings-for-defaults.png)

* Los usuarios pueden buscar y filtrar las carpetas en función de los predicados de propiedades.

  ![Filtrado de carpetas de búsqueda mediante predicados de búsqueda](/help/assets/assets/search-folders-via-predicates.png)

### Nuevas funciones disponibles en la [!DNL Assets] canal de prelanzamiento {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Al compartir recursos digitales como vínculo, los usuarios pueden copiar la URL en el portapapeles. La mejora permite compartir recursos de una manera más rápida y práctica.

### Errores corregidos en [!DNL Assets] {#assets-bugs-fixed}

La API `com.day.cq.dam.api.collection.SmartCollection` no está disponible en [!DNL Experience Manager] as a [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* Ahora puede utilizar el servicio Automated Forms Conversion para [convertir formularios PDF en francés, alemán y español](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=es#language-specific-meta-model) a formularios adaptables.
* Se ha agregado un panel independiente al editor de plantillas para mostrar los errores relacionados con los componentes de los formularios adaptables. Ayuda a consolidar todos los errores de formularios adaptables en una ubicación y a reducir el tiempo de resolución.

### Nuevas funciones disponibles en el canal de prelanzamiento de [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las [API de comunicación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   * Generar documentos rellenando archivos de plantilla con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere archivos de PDF imprimibles desde un PDF de formularios XFA y un formulario de Adobe Acrobat.

* **Externalizador de datos de las variables**: Puede guardar datos de las variables del flujo de trabajo de AEM en un sistema de almacenamiento externo que administre su organización.

* **Documento de registro basado en Acrobat**: También puede [usar el formulario PDF de Adobe Acrobat (PDF de Acrobat)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=es) como plantilla para el documento de registro además de la plantilla de formulario basada en XFA.

* **Conector del almacén de datos de Microsoft Azure**: Ahora puede [conectar el modelo de datos de formulario al almacenamiento de Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html?lang=es). Permite recuperar y almacenar datos de formulario adaptables en el almacenamiento de Microsoft Azure como un BLOB.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Componentes principales del CIF v2
   * Configuraciones simplificadas y mejoradas para URL de PDP/PLP y SEO
   * Indicador visual para datos de productos clasificados en el modo de creación para una mejor visibilidad de los próximos cambios
   * Nuevo componente de mapa del sitio para páginas de contenido y comercio

* Compatibilidad con [Adobe Commerce Sensei Product Recommendations, con tecnología de Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) AEM en el frente de la tienda de datos con recomendaciones predefinidas o creadas sobre la marcha

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Correcciones de errores {#bug-fixes-screens}

* La configuración del proveedor de contenido ahora se valida durante la creación o actualización.

* Todas las vistas de visualización tienen una columna de carpetas.

* Puede expandir Estructura de contenido de Screens.

* `bulk-offline-update-service` faltaban todos los permisos para algunos entornos.

* Se ha actualizado el vínculo de Ayuda para que coincida con la nueva documentación de Screens Cloud.

* Cancele la asignación de listas de reproducción y no permita la eliminación de listas de reproducción con reproductores asignados. Ahora funciona.

* El Reproductor ahora vuelve a descargar los recursos cuando se borra &quot;ALL&quot; Cache.

* La Programación repetida ahora funciona si la variable *Hora de finalización* está configurado para el día siguiente.

* `Back&Forward` ahora funciona en la IU as a Cloud Service de Screens.

* Antes no se podían crear etiquetas con el mismo nombre pero con áreas de nombres diferentes.

## XML Documentation para Experience Manager as a Cloud Service {#xml-documentation}

### Novedades {#what-is-new-xml-documentation}

XML Documentation para Experience Manager as a Cloud Service suele estar disponible. Permite a los clientes as a Cloud Service de Experience Manager adquirir el complemento de XML Documentation para importar, crear, administrar y ofrecer contenido técnico en varios canales, incluido Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.7.0.

### Fecha de lanzamiento {#release-cm-july}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.7.0 es el 15 de julio de 2021.
La próxima versión está planificada para el 12 de agosto de 2021.

### Novedades {#what-is-new-cm-july}

* Los clientes ahora pueden utilizar Azul 8 y 11 JDK para sus procesos de generación de Cloud Manager y pueden seleccionar utilizar uno de estos JDK para complementos de Maven compatibles con las cadenas de herramientas *o* realizar la ejecución completa del proceso de Maven.

* La dirección IP de salida ahora se registrará en el archivo de registro del paso de generación.

* Los entornos de fase y producción que ejecutan versiones antiguas de AEM ahora informarán que hay una **Actualización disponible**.

* El número máximo de certificados SSL admitidos ha aumentado a 20 por programa.

* El número máximo de dominios que se pueden configurar ha aumentado a 500 por entorno.

* El botón **Administrar Git** se ha cambiado a **Acceder a la información de Git** y el cuadro de diálogo se ha actualizado visualmente.

* La versión del arquetipo del proyecto AEM que utiliza Cloud Manager se ha actualizado a la versión 28.

### Correcciones de errores {#bug-fixes-cm-july}

* En algunos casos, la Vista previa no estaba disponible al enlazar una Lista de IP permitidas a un entorno.

* La navegación manual a la página de detalles de la ejecución para una ejecución no existente no mostraba error, solo una pantalla de carga interminable.

* El mensaje de error que se muestra cuando se alcanza el número máximo de certificados SSL no era útil.

* En algunas circunstancias, podría haber una discrepancia en la versión de la canalización que se muestra en la tarjeta Canalización en la página **Información general**.

* El asistente Agregar programa indicaba incorrectamente que el nombre no se podía cambiar después de la creación.

### Problemas conocidos {#known-issues-cm-july}

Los clientes que cambien a Azul JDKs deben tener en cuenta que no todas las aplicaciones existentes se compilarán sin errores en Azul JDK. Se recomienda realizar pruebas locales antes de cambiar.

## Cloud Acceleration Manager {#cam}

### Fecha de lanzamiento {#release-date-july-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 15 de julio de 2021.

### Novedades {#what-is-new-cam}

Cloud Acceleration Manager es una aplicación basada en la nube diseñada para guiar a sus equipos de TI a lo largo del recorrido de transición, desde la planificación hasta la puesta en marcha de Cloud Service. Configure sus equipos para una migración correcta con prácticas recomendadas por Adobe, sugerencias, documentación y herramientas que le ayudarán en cada fase del recorrido a AEM as Cloud Service. Más información [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Marque esto [Vídeo de demostración de Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
