---
title: Notas de la versión 2021.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.6.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 11%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2021.6.0 es el 28 de junio de 2021.
La siguiente versión (2021.7.0) será el 29 de julio de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general sobre la versión de junio de 2021](https://video.tv.adobe.com/v/334296) vídeo para ver un resumen de las funciones añadidas.

## XML Documentation para AEM as a cloud Service {#xml-documentation}

### Novedades {#what-is-new-xml-documentation}

* XML Documentation para AEM as a Cloud Service es ahora GA.
* Esto permitirá a los clientes existentes de AEM Cloud Service adquirir un complemento de XML Documentation para importar, crear, administrar y entregar contenido técnico en varios canales, incluidos sitios de AEM

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.6.0 y 2021.5.0.

### Fecha de la versión {#release-date-june-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.6.0 es el 10 de junio de 2021.
La próxima versión está planificada para el 15 de julio de 2021.

### Novedades {#what-is-new-junecm}

* El servicio de vista previa se implementará progresivamente en todos los programas. Se notificará al producto a los clientes cuando su programa esté habilitado para el servicio de vista previa. Consulte [Acceso al servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obtener más información.

* Las dependencias de Maven descargadas durante el paso de compilación ahora se almacenan en caché entre ejecuciones de canalización. Esta función se habilitará para los clientes en las próximas semanas.

* El nombre del programa ahora se puede editar mediante el cuadro de diálogo editar programa .

* El nombre de rama predeterminado utilizado durante la creación del proyecto y en el comando push predeterminado mediante la gestión de flujos de trabajo de Git se ha cambiado a `main`.

* Se ha actualizado la edición de la experiencia del programa en la interfaz de usuario.

* La regla de calidad `ImmutableMutableMixCheck` se ha actualizado para clasificar `/oak:index` como inmutables.

* Las reglas de calidad `CQBP-84` y `CQBP-84--dependencies` se han consolidado en una única regla. Como parte de esta consolidación, el análisis de dependencias identifica con mayor precisión los problemas en dependencias de terceros que se están implementando en el tiempo de ejecución de AEM.

* Para evitar confusiones, se han consolidado las filas de segmento Publicar AEM y Publicar Dispatcher en la página Detalles del entorno .

   ![](/help/implementing/cloud-manager/release-notes-cloud-manager/assets/aem-dispatcher.png)

* Se ha añadido una nueva regla de calidad de código para validar la estructura de `damAssetLucene` índices. Consulte [Índices Oak de DAM Asset Lucene personalizados](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obtener más información.

* La página de detalles del entorno ahora mostrará varios nombres de dominio para los servicios de publicación y vista previa (según corresponda). Consulte [Detalles del entorno](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Correcciones de errores {#bug-fixes-junecm}

* Las definiciones de nodo JCR que contenían una nueva línea después del nombre del elemento raíz no se analizaron correctamente.

* La API de repositorios de lista no filtraba los repositorios eliminados.

* Se mostraba un mensaje de error incorrecto cuando se proporcionaba un valor no válido para el paso de programación.

* En ocasiones, el usuario puede ver un verde *active* junto a una Lista de permitidos IP incluso cuando esa configuración no se haya implementado.

* Algunas secuencias de edición de programas podrían resultar en la incapacidad de crear o editar la canalización de producción.

* Algunas secuencias de edición de programas podrían dar como resultado la variable **Información general** que muestra un mensaje engañoso para volver a ejecutar la configuración del programa.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#ga-features-assets}

* La funcionalidad de automatización de contenido permite [!DNL Experience Manager Assets] aproveche el [!DNL Adobe Creative Cloud] API para automatizar la producción de recursos a escala. Mejora la velocidad del contenido al reducir drásticamente el tiempo necesario y las iteraciones necesarias para crear variaciones del mismo recurso. La funcionalidad no requiere ningún código y funciona desde DAM.
* [!DNL Adobe Asset Link] v3.0 para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]y [!DNL Adobe InDesign] y [!DNL Adobe Asset Link] v2.0 para [!DNL Adobe XD] está disponible. Proporciona:

   * Compatibilidad con [!DNL Assets Essentials].
   * Capacidad para conectarse automáticamente a [!DNL Experience Manager] como [!DNL Cloud Service] o [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nuevas funciones disponibles en la [!DNL Assets] canal de prelanzamiento {#beta-features-assets}

* La configuración de vista se mejora para permitir a los usuarios elegir una vista predeterminada y un parámetro de ordenación predeterminado.
* La funcionalidad de descarga de Linkshare utiliza descargas asincrónicas que aumentan la velocidad de descarga.
* Los usuarios pueden buscar y filtrar las carpetas en función de los predicados de propiedades.
* [!DNL Experience Manager Assets] incrusta el visualizador de PDF equipado por [!DNL Adobe Document Cloud] para obtener una vista previa de los documentos admitidos. Esta función permite a los usuarios obtener una vista previa del PDF y de otros archivos de varias páginas sin ningún procesamiento complejo. Esto mejora la paridad de características con [!DNL Experience Manager] 6.5.

### Errores corregidos en [!DNL Assets] {#bugs-fixed-assets}

* Cuando agregue un propietario a una subcarpeta, [!DNL Assets] también agrega el mismo usuario que un propietario de la carpeta principal. (CQ-4323737)
* Al agregar recursos a Colecciones, si un usuario aplica un filtro en la búsqueda Colecciones, el usuario no puede ver las Colecciones en la vista Lista. (CQ-4323181)
* Al buscar archivos y carpetas, si el usuario aplica un filtro y selecciona [!UICONTROL Archivos y carpetas], solo se muestran los archivos, pero no la carpeta. (CQ-4319543)

## [!DNL Experience Manager Sites] como [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#ga-features-sites}

* Publicar en el nivel de vista previa ahora se muestra como estado de página en la interfaz de usuario del administrador de sitios
* Publicar en el nivel de vista previa ahora muestra la URL de vista previa al final de la acción y mantiene la URL en las propiedades de la página para referencia posterior

## [!DNL Experience Manager Forms] como [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* Se ha agregado la capacidad de filtrar columnas personalizadas en AEM bandeja de entrada.
* Se ha añadido la capacidad de utilizar el editor de temas y la capa de estilo del editor de formularios adaptables para aplicar estilo al componente captcha.
* Se ha mejorado la velocidad y la precisión para detectar automáticamente secciones lógicas en los PDF forms de origen y convertirlas en los paneles de formulario adaptables correspondientes.
* Se ha añadido la acción de mover un PDF o archivo XDP de una carpeta a otra.

### Función beta de [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: Las API de comunicación le ayudan a combinar plantillas XDP y datos XML para generar documentos de impresión en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   * Genere documentos de formulario finales rellenando archivos de plantilla con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Genere PDF de impresión desde un PDF de formularios XFA y un formulario de Adobe Acrobat (AcroForm).

* **Externalizador de datos de variable**: Puede guardar datos de AEM variables de flujo de trabajo en un sistema de almacenamiento externo administrado por su organización.

Puede escribir en [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#forms-bugs-fixed}

* Cuando se valida un campo antes de enviar datos al servicio back-end mediante el Modelo de datos de formulario (FDM), las validaciones se realizan correctamente, pero el servicio Modelo de datos de formulario no invoca la validación posterior.
* Cuando se envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Este es un problema conocido en Apple iOS. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] como [!DNL Cloud Service] {#screens}

Esta sección describe las notas de la versión de AEM Screens as a Cloud Service.

### Fecha de la versión {#release-date-june-screens}

La fecha de versión de AEM Screens as a Cloud Service es el 24 de junio de 2021.

### Novedades {#what-is-new-screens-june}

>[!NOTE]
>Consulte [AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) Guía de conocimientos básicos necesarios para instalar, configurar y ejecutar correctamente Screens as a Cloud Service y enlace a la documentación técnica de conceptos detallados.

* La administración del registro masivo de dispositivos significa que el aprovisionamiento de grandes cantidades de dispositivos del reproductor es más rápido y eficiente.

* Se han mejorado las opciones de búsqueda y filtro para cada una de las vistas de inventario de Dispositivo, Pantalla y Canal.

* La instantánea de la salud del dispositivo ahorra tiempo al proporcionar un estado crítico como un vistazo.

* La página de detalles del objeto ofrece un resumen de la información más relevante para cada objeto del proyecto.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nuevos tipos de datos de referencia de productos y categorías del CIF para fragmentos de contenido (incl. compatibilidad con la interfaz de usuario del selector de productos/categorías)
* Nuevo componente principal de fragmento de contenido de comercio
* Búsqueda de comercio de texto completo compatible con AEM servidor
* Los componentes principales de comercio admiten la recopilación de datos de Adobe Commerce Sensei Recs
* Direcciones URL compatibles con SEO mejoradas para páginas de categoría
* Compatibilidad con encabezados HTTP personalizados por sitio/configuración

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de versión de la herramienta de transferencia de contenido v1.5.4 es el 28 de junio de 2021.

### Novedades {#what-is-new-ctt-latest}

* Compatibilidad con [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) paso añadido para usar con CTT. El paso de precopia se puede utilizar para acelerar significativamente las fases de extracción e ingesta de la actividad de transferencia de contenido cuando la instancia de AEM de origen está configurada para utilizar un almacén de datos de almacenamiento de blob de Amazon S3 o Azure.

* Se ha agregado protección a CTT para evitar que los usuarios detengan la ingesta y corrompa los datos una vez que hayan alcanzado el punto crítico durante la fase de ingesta.

* Los registros de extracción son más descriptivos para ayudarle a solucionar el problema.

* Se han añadido mensajes de estado de ingesta más descriptivos en la interfaz de usuario.

### Correcciones de errores {#bug-fixes-ctt-latest}

* Al detener una ingesta en la instancia de autor, la interfaz de usuario sobrescribió una ingesta finalizada anteriormente en la instancia de publicación en `STOPPED` from `FINISHED`. Esto se ha corregido.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.16 es el 30 de junio de 2021.

### Novedades {#what-is-new-bpa-latest}

* Capacidad para detectar y crear informes sobre nodos secundarios que faltan en las carpetas de `/content/dam`.

* Capacidad para detectar e informar sobre la versión de Best Practices Analyzer utilizada.

### Correcciones de errores {#bug-fixes-bpa-latest}

* Se ha corregido un error de registro relacionado con la estructura de repositorio no admitida (URS).
