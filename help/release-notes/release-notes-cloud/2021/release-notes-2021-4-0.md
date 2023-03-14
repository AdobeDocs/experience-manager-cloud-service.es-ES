---
title: Notas de la versión 2021.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2021.4.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 775332b5-24ce-430e-97a2-6eeb80877c64
source-git-commit: a2c844d6f72c22ed085690ff98572a52e97de40d
workflow-type: tm+mt
source-wordcount: '1535'
ht-degree: 48%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Adobe Experience Manager] as a Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2021.4.0 es el 6 de mayo de 2021.
La de la siguiente versión (2021.5.0) será el 27 de mayo de 2021.

## AEM Base as a Cloud Service{#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* [Flujo de trabajo Publicar árbol de contenido](/help/operations/replication.md#publish-content-tree-workflow) : Un nuevo modelo y paso de flujo de trabajo proporciona un mayor rendimiento al publicar jerarquías profundas de contenido.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Puntos finales de GraphQL AEM: Ahora es posible habilitar la API de GraphQL de la aplicación para configuraciones de AEM Sites individuales y crear puntos finales de GraphQL personalizados para dichas configuraciones mediante una nueva IU de la consola de GraphQL. La IU también permite administrar los extremos de GraphQL.

* Modelos de contenido, tipo de datos Fecha y hora mejorado: Ahora es posible configurar el tipo de datos Fecha y hora para permitir la creación de información solo de fecha, solo de hora o de fecha y hora.

* Modelos de contenido, tipo de datos Etiquetas mejorado: Ahora es posible configurar el tipo de datos Etiquetas para permitir la creación de etiquetas únicas o múltiples.

* Modelos de contenido, nuevo tipo de datos Marcador de pestaña: El nuevo tipo de datos Marcador de pestaña permite agrupar tipos de datos en secciones que se procesarán con pestañas en el editor de fragmentos de contenido.

### Correcciones de errores en [!DNL Sites] {#bug-fixes-sites}

* Fragmentos de contenido: al mover fragmentos de contenido o carpetas, ahora se actualizan las referencias anidadas dentro del fragmento (CQ-4320815)

* GraphQL: las consultas persistentes ahora admiten extremos definidos por el usuario específicos de las configuraciones de AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] no archiva descargas de recursos individuales en las que se haya descargado el archivo original. Esta mejora permite descargas más rápidas.

* Cuando se descarga un recurso mediante la opción linkshare, ahora puede elegir descargar o no descargar las representaciones. Anteriormente, se descargaban todas las representaciones de recursos.

* Los administradores pueden configurar [!DNL Experience Manager] para eliminar el origen de los recursos después de realizar una ingesta masiva. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al ejecutar una comprobación de estado para importar recursos de forma masiva, Experience Manager ahora proporciona más información sobre los motivos de los errores. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al importar recursos mediante la herramienta de importación masiva, los administradores ahora tienen la opción de eliminar los archivos de origen una vez completada la importación. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al editar un esquema de metadatos, un nuevo campo de selector de ruta raíz permite a los administradores realizar la selección de forma rápida y sencilla, lo que reduce el tiempo de configuración.

* Al editar un esquema de metadatos, se añade un tipo de datos que proporciona un área de texto de forma libre en el editor de metadatos. Los usuarios pueden utilizar esta área de texto para introducir texto de forma libre como metadatos de un recurso. Consulte [editor de esquemas de metadatos](/help/assets/metadata-schemas.md).

* Los metadatos de muchos recursos se pueden importar de forma masiva mediante un archivo CSV y se pueden exportar a un CSV también. El formato de fecha predeterminado es ahora `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Los usuarios pueden aprovechar un formato diferente actualizando el encabezado de la columna. Por ejemplo, añada `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` como encabezado de columna en el archivo CSV en lugar de la palabra `Date`.

* Al examinar los recursos en la vista Columna, un indicador visual muestra el estado aprobado o rechazado de cada uno.

* Al examinar los recursos en la vista Columna, aparece un indicador visual para los caducados.

### Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Al intentar mover varios recursos o carpetas, se registra un error en la consola y la operación de movimiento no se completa. La operación de mover falla si el título no se puede actualizar. (CQ-4322080)

* Un campo de metadatos se puede ocultar en función de una regla como que, cuando se cumple una condición predefinida, los metadatos no sean obligatorios. Sin embargo, estos campos de metadatos ocultos se muestran como campos obligatorios. (CQ-4321285)

* La importación masiva de metadatos falla debido a un formato de fecha incorrecto. (CQ-4319014)

* Cuando se realiza una selección en la página Propiedades para actualizar los metadatos, la interfaz tarda en responder cuando el esquema proporciona muchas opciones. (CQ-4318538)

* Al actualizar y guardar el valor de los metadatos en un campo de texto de una sola línea, los valores del menú desplegable se eliminan, incluso si las ediciones están desactivadas en el menú desplegable. (CQ-4317077)

* Puede utilizar puntos suspensivos como anotación para revisar los recursos. Cuando se utiliza una elipse pequeña, la elipse se superpone con el número de la anotación en la versión de impresión. (CQ-4316792)

* La opción Publicación rápida no se muestra cuando se selecciona un recurso de los resultados de búsqueda después de buscarlo. (CQ-4317748)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Utilizar el método de autenticación de Id. de gobierno en los formularios adaptables habilitados para Adobe Sign**

   Con la tecnología de algoritmos avanzados de aprendizaje automático, el proceso de Id. de gobierno de Adobe Sign ofrece a las empresas de todo el mundo la capacidad de garantizar una autenticación de alta calidad de la identidad de sus destinatarios. Ahora puede utilizar el método de autenticación de identidad de Id. de gobierno en los formularios adaptativos habilitados para Adobe Sign.

   La Id. de gobierno es un método de autenticación de identidad premium que indica al destinatario cómo [cargar la imagen de un documento de identidad emitido por el gobierno (licencia de conducir, identificación nacional, pasaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html) y luego evalúa ese documento para asegurarse de que es auténtico.

* **Compatibilidad para utilizar la experiencia de firma en formularios para envíos asincrónicos de formularios adaptables**

   Ahora puede utilizar la experiencia de firma en formularios para los envíos asincrónicos de formularios adaptables. También puede incrustar un formulario adaptable en una página [!DNL Experience Manager Sites] y utilizar la experiencia de firma en formularios para los envíos de formularios adaptables.

* **Compatibilidad para utilizar una variable para especificar un archivo adjunto mientras se rellena previamente un formulario adaptable para un paso Asignar tarea**

   Al rellenar previamente un formulario adaptable para un paso Asignar tarea, ahora puede utilizar una variable del tipo de documento para seleccionar un archivo adjunto de entrada para el formulario adaptable.

* **Compatibilidad con el uso de la opción literal para establecer el valor de una variable de tipo JSON**

   Puede utilizar la opción literal para establecer el valor de una variable del tipo JSON en el paso establecer variable de un flujo de trabajo de AEM. La opción literal le permite especificar un JSON en forma de cadena.

* **Utilizar el entorno de desarrollo local para crear el documento de registro (DoR)**

   Puede utilizar un XDP como plantilla del documento de registro en instancias de Cloud Service y el SDK (entorno de desarrollo local) de AEM Forms as a Cloud Service. Anteriormente, la compatibilidad se limitaba únicamente a instancias de Cloud Service.

### Correcciones de errores en [!DNL Forms] {#bug-fixes-forms}

* Cuando se envía un formulario adaptable configurado para no generar un documento de registro a un flujo de trabajo de AEM configurado para generar un documento de registro, no se muestra ningún mensaje de error y la tarea no se envía.

### Otras actualizaciones {#misc-2021-04-0-forms}

* Para facilitar el reconocimiento del contenido, el servicio ahora genera miniaturas en directo para los archivos XDP, PDF dinámico y Esquema.
* Añada la capacidad de mover un archivo de PDF a una carpeta colocada en la interfaz de usuario de AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad con UID de categoría: esto desbloquea las integraciones de comercio de terceros para sistemas que utilizan cadenas para ID de categoría

* AEM Extensión para PWA Studio incl. integración de ejemplo

* Nuevo componente principal de navegación del CIF que amplía el componente principal de navegación de WCM

* AEM Indicador visual para datos de catálogo clasificados en tienda de

* El extremo de comercio ahora se puede configurar mediante la interfaz de usuario de Cloud Manager

### Correcciones de errores {#bug-fixes-commerce}

* El campo de categoría raíz no se mostraba en la pestaña de comercio de las propiedades de página de las páginas de categoría

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.4.0.

### Fecha de lanzamiento {#release-date-cm-april}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.4.0 es el 8 de abril de 2021.
La próxima versión está planificada para el 6 de mayo de 2021.

### Novedades {#what-is-new-april}

* Actualizaciones de la interfaz de usuario de los flujos de trabajo Agregar y editar programa para que sea más intuitivo.

* Un usuario con los permisos necesarios ahora puede enviar el punto final de Commerce a través de la interfaz de usuario.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o de publicación. Requiere la versión de AEM `2021.03.5104.20210328T185548Z` o superior.

* El botón **Administrar Git** se muestra en la tarjeta Canalizaciones aunque estas no se hayan configurado.

* La versión del arquetipo de proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 27.

* Los proyectos de la consola de desarrollador de Adobe I/O creados por Cloud Manager ya no se pueden editar ni eliminar de manera involuntaria.

* Cuando un usuario agrega un entorno nuevo, se les informará de que una vez que se haya creado un entorno, no se podrá mover a otra región.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o de publicación. Requiere la versión de AEM 2021.03.5104.20210328T185548Z o superior.

* Se ha aclarado el mensaje de error al iniciar una canalización cuando se eliminaba un entorno.

* Los paquetes OSGi proporcionados por los proyectos de Eclipse ahora se excluyen de la regla `CQBP-84--dependencies`.

### Correcciones de errores {#bug-fixes-cm-april}

* Al editar la página Auditoría de experiencias de una canalización, una ruta de entrada que comience con una barra diagonal `( / )` ya no hará que el paso se quede atascado en estado “pendiente”.

* Cuando se crea una canalización de producción nueva, si el usuario no agrega ninguna anulación de la auditoría de contenido, la página principal predeterminada no se auditaba.

* Problemas para `CloudServiceIncompatibleWorkflowProcess` tenía la gravedad incorrecta en el archivo del problema CSV descargable.

* La comprobación de `Runmode` producía falsos positivos en nodos que no son de carpeta.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.12 es el 12 de abril de 2021.

### Correcciones de errores {#bug-fixes-bpa-april}

* Se han visto filas duplicadas en el informe de BPA. Esto se ha corregido.
* AEM La interfaz de usuario de BPA en la versión 6.4.2 de la generaba un error de JS que deshabilitaba el botón Generar informe. Esto se ha corregido.
