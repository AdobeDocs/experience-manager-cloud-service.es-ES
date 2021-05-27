---
title: Notas de la versión 2021.4.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión 2021.4.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: aeee895e4a4b959125d08091619988d0ffa09ace
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 4%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] como Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2021.4.0 es el 6 de mayo de 2021.
La siguiente versión (2021.5.0) se publicará el 27 de mayo de 2021.

## AEM como Cloud Service Foundation{#aem-as-a-cloud-service-foundation}

### Novedades {#what-is-new-foundation}

* [Flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) : un nuevo modelo y paso de flujo de trabajo proporciona un mayor rendimiento al publicar jerarquías profundas de contenido.

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* Puntos finales de GraphQL : ahora es posible habilitar la API de GraphQL de AEM para configuraciones de AEM Sites individuales y crear puntos finales de GraphQL personalizados para esas configuraciones mediante la nueva interfaz de usuario de la consola de GraphQL. La interfaz de usuario también permite administrar los extremos de GraphQL.

* Modelos de contenido, tipo mejorado de datos de fecha y hora : ahora es posible configurar el tipo de fecha y hora para permitir la creación solo de información de fecha, hora o fecha y hora.

* Modelos de contenido, tipo de datos Etiquetas mejorado : ahora es posible configurar el tipo de datos Etiquetas para permitir la creación de etiquetas únicas o múltiples.

* Modelos de contenido, nuevo tipo de datos de marcador de posición de pestañas : el nuevo tipo de datos de marcador de posición de pestañas permite agrupar tipos de datos en secciones que se procesarán en pestañas en el editor de fragmentos de contenido.

### Correcciones de errores en [!DNL Sites] {#bug-fixes-sites}

* Fragmentos de contenido: al mover fragmentos de contenido o carpetas, ahora se actualizan las referencias anidadas dentro del fragmento (CQ-4320815)

* GraphQL: las consultas persistentes ahora admiten extremos definidos por el usuario que son específicos de las configuraciones de AEM Sites (CQ-4315928)

## [!DNL Adobe Experience Manager Assets] como  [!DNL Cloud Service] {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager] no archiva descargas de recursos individuales en las que se descarga el archivo original. Esta mejora permite descargas más rápidas.

* Cuando se descarga un recurso mediante la opción linkshare , ahora puede elegir descargar o no las representaciones. Anteriormente, se descargaban todas las representaciones de recursos.

* Los administradores pueden configurar [!DNL Experience Manager] para eliminar el origen de los recursos después de realizar una ingesta masiva de recursos. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al ejecutar una comprobación de estado para importar recursos de forma masiva, el Experience Manager ahora proporciona más información sobre los motivos de los errores. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al importar recursos mediante la herramienta de importación masiva, los administradores ahora tienen la opción de eliminar los archivos de origen una vez realizada la importación correctamente. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

* Al editar un esquema de metadatos, un nuevo campo selector de ruta raíz permite a los administradores realizar la selección de forma rápida y sencilla, lo que reduce el tiempo de configuración.

* Los metadatos de muchos recursos se pueden importar de forma masiva mediante un archivo CSV y se pueden exportar a un archivo CSV. El formato de fecha predeterminado es ahora `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`. Los usuarios pueden aprovechar un formato diferente actualizando el encabezado de la columna. Por ejemplo, agregue `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX` como encabezado de columna en el archivo CSV en lugar de la palabra `Date`.

* Al examinar los recursos en la vista Columna, un indicador visual muestra el estado aprobado o rechazado de cada recurso.

* Al examinar los recursos en la vista Columna, aparece un indicador visual para los recursos caducados.

### Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Al intentar mover varios recursos o carpetas, se registra un error en la consola y la operación de mover no se completa. La operación Mover falla si no se puede actualizar el título. (CQ-4322080)

* Un campo de metadatos puede ocultarse en función de una regla de modo que, cuando se cumple una condición predefinida, los metadatos no son obligatorios. Sin embargo, estos campos de metadatos ocultos se muestran como campos obligatorios. (CQ-4321285)

* La importación masiva de metadatos falla debido a un formato de fecha incorrecto. (CQ-4319014)

* Cuando se realiza una selección en la página Propiedades para actualizar los metadatos, la interfaz es lenta en responder cuando el esquema proporciona muchas opciones. (CQ-4318538)

* Al actualizar y guardar el valor de los metadatos en un campo de texto de una sola línea, los valores del menú desplegable se eliminan, incluso si las ediciones están desactivadas en el menú desplegable. (CQ-4317077)

* Los puntos suspensivos se pueden usar como anotaciones para revisar los recursos. Cuando se utiliza una elipse pequeña, la elipse se superpone con el número de la anotación en la versión de impresión. (CQ-4316792)

## [!DNL Adobe Experience Manager Forms] como  [!DNL Cloud Service] {#forms}

### Novedades de [!DNL Forms] {#what-is-new-forms}

* **Utilizar el método de autenticación de ID de gobierno en Adobe Sign habilitado para Adaptable Forms**

   Con la tecnología de algoritmos avanzados de aprendizaje automático, el proceso de identificación gubernamental de Adobe Sign ofrece a las empresas de todo el mundo la capacidad de garantizar una autenticación de alta calidad de la identidad de sus destinatarios. Ahora, puede utilizar el método de autenticación de identidad de ID de gobierno en Adobe Sign habilitado para Adaptive Forms.

   El ID de gobierno es un método de autenticación de identidad premium que ordena al destinatario [cargar la imagen de un documento de identidad emitido por el gobierno (licencia de conducir, ID nacional, pasaporte)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html) y luego evalúa ese documento para asegurarse de que sea auténtico.

* **Compatibilidad para utilizar la experiencia de firma en formularios para envíos asincrónicos de formularios adaptables**

   Ahora puede utilizar la experiencia de firma en formularios para los envíos asincrónicos de formularios adaptables. También puede incrustar un formulario adaptable en una página [!DNL Experience Manager Sites] y utilizar la experiencia de firma en el formulario para los envíos de formularios adaptables.

* **Compatibilidad con el uso de una variable para especificar un archivo adjunto mientras se rellena previamente un formulario adaptable para un paso Asignar tarea**

   Al rellenar previamente un formulario adaptable para un paso Asignar tarea, ahora puede utilizar una variable de tipo de documento para seleccionar un archivo adjunto de entrada para el formulario adaptable.

* **Compatibilidad con el uso de la opción literal para establecer el valor de una variable de tipo JSON**

   Puede utilizar la opción literal para establecer el valor de una variable de tipo JSON en el paso de variable de conjunto de un flujo de trabajo AEM. La opción literal le permite especificar un JSON en forma de cadena.

* **Utilizar el entorno de desarrollo local para crear el documento de registro (DoR)**

   Puede utilizar una plantilla XDP como documento de registro en instancias de Cloud Service y AEM Forms as a Cloud Service SDK (entorno de desarrollo local). Anteriormente, la compatibilidad se limitaba a instancias de Cloud Service únicamente.

### Correcciones de errores en [!DNL Forms] {#bug-fixes-forms}

* Cuando se envía un formulario adaptable configurado para no generar un documento de registro a un flujo de trabajo AEM configurado para generar un documento de registro, no se muestra ningún mensaje de error y la tarea no se envía.

### Otras actualizaciones {#misc-2021-04-0-forms}

* Con el fin de facilitar el reconocimiento del contenido, el servicio ahora genera miniaturas en vivo para archivos XDP, PDF dinámico y de esquema.
* Añada la capacidad de mover un archivo PDF a una carpeta colocada en la interfaz de usuario de AEM Forms.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad con UID de categoría : esto desbloquea las integraciones de comercio de terceros para sistemas que utilizan Strings para id de categoría

* AEM extensión para el PWA Studio incl. integración de ejemplo

* Nuevo componente principal de navegación del CIF que amplía el componente principal de navegación de WCM

* Indicador visual para datos de catálogo clasificados en AEM tienda

* El extremo de comercio ahora se puede configurar mediante la interfaz de usuario de Cloud Manager

### Corrección de errores {#bug-fixes-commerce}

* El campo de categoría raíz no se mostraba en la pestaña de comercio de las propiedades de página de las páginas de categoría

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.4.0.

### Fecha de la versión {#release-date-cm-april}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.4.0 es el 8 de abril de 2021.
La próxima versión está planificada para el 06 de mayo de 2021.

### Novedades {#what-is-new-april}

* Actualizaciones de la interfaz de usuario de los flujos de trabajo Añadir y editar programa para que sea más intuitivo.

* Un usuario con los permisos necesarios ahora puede enviar el punto final del comercio a través de la interfaz de usuario.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o publicación. Requiere AEM versión `2021.03.5104.20210328T185548Z` o superior.

* El botón **Administrar Git** se muestra en la tarjeta Canalizaciones aunque no se hayan configurado canalizaciones.

* La versión del arquetipo de proyecto AEM utilizado por Cloud Manager se ha actualizado a la versión 27.

* Los proyectos de la consola de desarrollador de Adobe I/O creados por Cloud Manager ya no se pueden editar ni eliminar de forma involuntaria.

* Cuando un usuario agrega un nuevo entorno, se les informará de que una vez que se haya creado un entorno, no se puede mover a otra región.

* Ahora, las variables de entorno se pueden vincular a un servicio específico, ya sea de autor o publicación. Requiere AEM versión 2021.03.5104.20210328T185548Z o superior.

* Se ha aclarado el mensaje de error al iniciar una canalización cuando se eliminaba un entorno.

* Los paquetes OSGi proporcionados por los proyectos de Eclipse ahora se excluyen de la regla `CQBP-84--dependencies`.

### Corrección de errores {#bug-fixes-cm-april}

* Al editar la página Auditoría de experiencias de una canalización, una ruta de entrada que comience con una barra diagonal `( / )` ya no dará como resultado que el paso se bloquee en estado pendiente.

* Cuando se crea una nueva canalización de producción, si el usuario no agrega ninguna anulación de auditoría de contenido, la página principal predeterminada no se auditó.

* Los problemas para `CloudServiceIncompatibleWorkflowProcess` tenían la gravedad incorrecta en el archivo CSV del problema descargable.

* La comprobación `Runmode` estaba produciendo falsos positivos en nodos que no son de carpeta.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.12 es el 12 de abril de 2021.

### Corrección de errores {#bug-fixes-bpa-april}

* Se vieron filas duplicadas en el BPA registrado. Esto se ha solucionado.
* La interfaz de usuario de BPA de AEM versión 6.4.2 generaba un error de JS que desactivaba el botón Generar informe . Esto se ha solucionado

