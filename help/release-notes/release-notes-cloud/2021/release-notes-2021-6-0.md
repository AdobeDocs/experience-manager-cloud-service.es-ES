---
title: Notas de la versión 2021.6.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.6.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 2c72973b-5a51-4744-bf88-50da0013ba31
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 48%

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

La fecha de lanzamiento de [!DNL Adobe Experience Manager] La versión 2021.6.0 as a Cloud Service es el 28 de junio de 2021.
La de la siguiente versión (2021.7.0) será el 29 de julio de 2021.

## Vídeo de la versión {#release-video}

Eche un vistazo a la [Información general de la versión de junio de 2021](https://video.tv.adobe.com/v/334296) para ver un resumen de las funciones añadidas.

## XML Documentation AEM para as a cloud Service {#xml-documentation}

### Novedades {#what-is-new-xml-documentation}

* XML Documentation AEM para el as a Cloud Service ahora es GA.
* Esto permitirá a los clientes existentes de AEM Cloud Service adquirir el complemento de XML Documentation AEM para importar, crear, administrar y entregar contenido técnico en varios canales, incluidos los sitios de

## Cloud Manager {#cloud-manager}

AEM Esta sección describe las notas de la versión para Cloud Manager en las versiones 2021.6.0 y 2021.5.0 de as a Cloud Service.

### Fecha de lanzamiento {#release-date-june-cm}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.6.0 es el 10 de junio de 2021.
La próxima versión está planificada para el 15 de julio de 2021.

### Novedades {#what-is-new-junecm}

* El servicio Vista previa se implementará progresivamente en todos los programas. Se notifica a los clientes en el producto cuando su programa está habilitado para el servicio Vista previa. Consulte [Acceder al servicio Vista Previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) para obtener más información.

* Las dependencias de Maven descargadas durante el paso de generación ahora se almacenan en la memoria caché entre ejecuciones de canalización. Esta característica se habilitará para los clientes en las próximas semanas.

* El nombre del programa ahora se puede editar mediante el cuadro de diálogo Editar programa.

* El nombre de rama predeterminado utilizado durante la creación del proyecto y en el comando push predeterminado mediante la administración de flujos de trabajo de Git se ha cambiado a `main`.

* Se ha actualizado Editar la experiencia del programa en la interfaz de usuario.

* La regla de calidad `ImmutableMutableMixCheck` se ha actualizado para clasificar nodos `/oak:index` como inmutables.

* Las reglas de calidad `CQBP-84` y `CQBP-84--dependencies` se han consolidado en una única regla. Como parte de esta consolidación, el análisis de dependencias identifica con mayor precisión los problemas en dependencias de terceros que se implementan en el tiempo de ejecución de AEM.

* Para evitar confusiones, se han consolidado las filas de segmento Publicar AEM y Publicar Dispatcher en la página Detalles del entorno.

  ![Entornos de Dispatcher](/help/implementing/cloud-manager/release-notes/assets/aem-dispatcher.png)

* Se ha agregado una nueva regla de calidad de código para validar la estructura de los índices `damAssetLucene`. Consulte [Índices Oak de DAM Asset Lucene personalizados](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check) para obtener más información.

* La página Detalles del entorno ahora mostrará varios nombres de dominio para los servicios Publicación y Vista previa (según corresponda). Consulte [Detalles del entorno](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.

### Correcciones de errores {#bug-fixes-junecm}

* Las definiciones de nodo JCR que contenían una nueva línea después del nombre del elemento raíz no se analizaban correctamente.

* La API Enumerar repositorios no filtraba los repositorios eliminados.

* Se mostraba un mensaje de error incorrecto cuando se proporcionaba un valor no válido para el paso de programación.

* En ocasiones, el usuario podía ver un activo *verde* junto a una lista de IP permitidas incluso cuando esa configuración no se había implementado.

* Algunas secuencias de edición de programas podrían resultar en la incapacidad para crear o editar la canalización de producción.

* Algunas secuencias de edición de programas podían dar como resultado la página **Información general** que mostraba un mensaje engañoso para volver a ejecutar la configuración del programa.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#ga-features-assets}

* La funcionalidad de automatización de contenido permite [!DNL Experience Manager Assets] use el [!DNL Adobe Creative Cloud] API para automatizar la producción de recursos a escala. Mejora la velocidad del contenido al reducir drásticamente el tiempo necesario y las iteraciones necesarias para crear variaciones del mismo recurso. La funcionalidad no requiere ningún código y funciona desde DAM.
* [!DNL Adobe Asset Link] v3.0 para [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], y [!DNL Adobe InDesign] y [!DNL Adobe Asset Link] v2.0 para [!DNL Adobe XD] se ha liberado. Proporciona lo siguiente:

   * Compatibilidad con [!DNL Assets Essentials].
   * Capacidad para conectarse automáticamente a [!DNL Experience Manager] as a [!DNL Cloud Service] o [!DNL Assets Essentials].

<!-- TBD: Checking with PMs if AAE release should be mentioned here.
-->

### Nuevas funciones disponibles en la [!DNL Assets] canal de prelanzamiento {#beta-features-assets}

* La configuración de vista se mejora para permitir que los usuarios elijan una vista predeterminada y un parámetro de ordenación predeterminado.
* La funcionalidad de descarga de Linkshare utiliza descargas asincrónicas que aumentan la velocidad de descarga.
* Los usuarios pueden buscar y filtrar las carpetas en función de los predicados de propiedades.
* [!DNL Experience Manager Assets] incrusta el Visor de PDF con tecnología [!DNL Adobe Document Cloud] para obtener una vista previa de los documentos admitidos. Esta función permite a los usuarios previsualizar el PDF y otros archivos de varias páginas sin ningún procesamiento complejo. Esto mejora la paridad de las funciones con [!DNL Experience Manager] 6.5.

### Errores corregidos en [!DNL Assets] {#bugs-fixed-assets}

* Cuando agrega un propietario a una subcarpeta, [!DNL Assets] también agrega el mismo usuario como propietario de la carpeta principal. (CQ-4323737)
* Al agregar recursos a Colecciones, si un usuario aplica un filtro en la búsqueda de Colecciones, no puede ver las Colecciones en la vista de lista. (CQ-4323181)
* Al buscar archivos y carpetas, si el usuario aplica un filtro y selecciona [!UICONTROL Archivos y carpetas], solo se muestran los archivos, pero no la carpeta. (CQ-4319543)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones de [!DNL Sites] {#ga-features-sites}

* Publicar en el nivel de vista previa ahora se muestra como estado de página en la IU del administrador de sitios
* Publicar en el nivel de vista previa ahora muestra la URL de vista previa al final de la acción y mantiene la URL en las propiedades de página para referencia posterior

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* Se ha agregado la capacidad de filtrar columnas personalizadas en la bandeja de entrada AEM.
* Se ha agregado la capacidad de utilizar el editor de temáticas y la capa de estilo del editor de formularios adaptables para aplicar estilo al componente captcha.
* Se ha mejorado la velocidad y la precisión para detectar automáticamente secciones lógicas en los PDF forms de origen y convertirlas en los paneles de formularios adaptables correspondientes.
* Se ha agregado la acción de mover un PDF o archivo XDP de una carpeta a otra.

### Característica beta de [!DNL Forms] {#what-is-new-forms-prerelease}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: las API de comunicación le ayudan a combinar plantillas XDP y datos XML para generar documentos imprimibles en varios formatos. El servicio le permite generar documentos en modo sincrónico. Las API le permiten crear aplicaciones con las que puede hacer lo siguiente:
   * Generar formularios finales al rellenar archivos de plantilla con datos XML.
   * Generar formularios de salida en varios formatos, incluidas las secuencias de impresión de PDF no interactivas.
   * Generar PDF imprimibles desde un formulario PDF de XFA y un formulario de Adobe Acrobat (AcroForm).

* **Externalizador de datos de las variables**: Puede guardar datos de las variables del flujo de trabajo de AEM en un sistema de almacenamiento externo que administre su organización.

Puede escribir a [!DNL formscsbeta@adobe.com] para inscribirse en el programa beta.

### Errores corregidos en [!DNL Forms] {#forms-bugs-fixed}

* Cuando se valida un campo antes de enviar datos al servicio back-end mediante el modelo de datos de formulario (FDM), las validaciones se realizan correctamente, pero el servicio del modelo de datos de formulario no invoca la validación posterior.
* Cuando envía un formulario que contiene un campo de carga de HTML estándar desde un dispositivo iOS de Apple, a veces, el contenido del archivo no se envía y se recibe un archivo de 0 bytes en el otro extremo. Se trata de un problema conocido de iOS de Apple. [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

Esta sección describe las notas de la versión as a Cloud Service de AEM Screens.

### Fecha de lanzamiento {#release-date-june-screens}

La fecha de lanzamiento as a Cloud Service de AEM Screens es el 24 de junio de 2021.

### Novedades {#what-is-new-screens-june}

>[!NOTE]
>Consulte [AEM Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/home.html?lang=en) Guía de conocimientos básicos necesarios para instalar, configurar y ejecutar correctamente Screens as a Cloud Service y vincular a la documentación técnica de conceptos detallados.

* La administración del registro masivo de dispositivos significa que el aprovisionamiento de grandes cantidades de reproductores es más rápido y eficiente.

* Se han mejorado las opciones de búsqueda y filtrado para cada una de las vistas de inventario de Dispositivo, Pantalla y Canal.

* La instantánea de la salud del dispositivo ahorra tiempo al proporcionar un estado crítico como un vistazo.

* La página de detalles del objeto ofrece un resumen de la información más relevante para cada objeto del proyecto.

## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Nuevos tipos de datos de referencia de productos y categorías del CIF para fragmentos de contenido (incl. soporte de la interfaz de usuario del selector de productos/categorías)
* Nuevo componente principal de fragmento de contenido de Commerce
* AEM Búsqueda de comercio de texto completo admitida en el back-end de la
* Los componentes principales de Commerce admiten la recopilación de datos de Adobe Commerce Sensei Recs
* Se han mejorado las URL compatibles con SEO para las páginas de categorías
* Compatibilidad con encabezados HTTP personalizados por sitio/configuración

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt-latest}

La fecha de lanzamiento de la herramienta de transferencia de contenido v1.5.4 es el 28 de junio de 2021.

### Novedades {#what-is-new-ctt-latest}

* Compatibilidad con un [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) Se ha añadido un paso para utilizarlo con CTT. AEM El paso previo a la copia se puede utilizar para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido cuando la instancia de origen se configura para utilizar un almacén de datos de Amazon S3 o Azure Blob Storage.

* Se ha añadido una protección a CTT para evitar que los usuarios detengan una ingesta y corrompan los datos una vez que hayan alcanzado el punto crítico durante la fase de ingesta.

* Los registros de extracción son más descriptivos para ayudar a solucionar problemas.

* Se han añadido mensajes de estado de ingesta más descriptivos en la IU.

### Correcciones de errores {#bug-fixes-ctt-latest}

* Al detener una ingesta en la instancia de autor, la interfaz de usuario sobrescribió una ingesta previamente finalizada en la instancia de publicación en `STOPPED` de `FINISHED`. Esto se ha corregido.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.16 es el 30 de junio de 2021.

### Novedades {#what-is-new-bpa-latest}

* Capacidad para detectar e informar sobre nodos secundarios que faltan en carpetas en `/content/dam`.

* Capacidad para detectar y crear informes sobre la versión de Analizador de prácticas recomendadas utilizada.

### Correcciones de errores {#bug-fixes-bpa-latest}

* Se ha corregido un error de registro relacionado con una estructura de repositorio no compatible (URS).
