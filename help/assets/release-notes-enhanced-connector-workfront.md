---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: b1c5df329e45128704ae82f49673c6a755a61a73
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 84%

---

# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas generales de la versión de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de lanzamiento {#release-date}

La fecha de la última versión, 1.9.16 de [!DNL Workfront for Experience Manager enhanced connector] es el 19 de enero de 2024.

## Puntos destacados de la versión {#release-highlights}

La versión más reciente de [!DNL Workfront for Experience Manager enhanced connector] incluye las siguientes correcciones de errores:

* El [!DNL Workfront] configuración en [!DNL CRX DE] actualmente no almacena el `project ID`, que provoca errores al aplicar permisos de solo lectura. Obtenga más información sobre cómo [configuración de permisos](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#linked-folders).

* No hay documentación pública sobre cómo agregar una propiedad personalizada a la definición de índice predeterminada. Más información sobre [agregar propiedad personalizada](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#metadata-schema-mapping).

* La eliminación de las configuraciones de conexión en el conector mejorado afecta significativamente a las suscripciones de evento y otras configuraciones guardadas, lo que hace que apunten a una dirección URL antigua.

* La instalación del paquete de complementos de Forms no instala el **[!UICONTROL Alternar enrutador]**, lo que provoca el fallo del [!DNL WFEC AMS environment Toggle] función.

* Al habilitar las suscripciones a eventos en la configuración de EWC, se producen errores repetidos en las llamadas de API con `HTTP 400` error al configurar [!DNL Workfront] se ha mejorado el conector por primera vez.

* Al eliminar comentarios en recursos de carpetas vinculadas en Workfront AEM, no se encuentra la ruta de la carpeta vinculada en los recursos de carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la carpeta de la.

* AEM La compatibilidad insuficiente con los recursos de archivo grandes en la provoca un problema de tamaño de 4 bytes.

* No hay procesamiento de tiempo de solicitud para flujos críticos en la carpeta vinculada, la actualización del documento y la actualización de la nota.

>[!NOTE]
>
>AEM 6.4 ha llegado al final de la asistencia ampliada. Consulte nuestra [períodos de asistencia técnica](https://helpx.adobe.com/es/support/programs/eol-matrix.html). Busque las versiones compatibles [aquí](https://experienceleague.adobe.com/docs/?lang=es).


>[!IMPORTANT]
>
>El Adobe le recomienda [actualice a la última versión 1.9.16](/help/assets/workfront-connector-install.md) de la [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conocidos {#known-issues}

* Al configurar las carpetas vinculadas con proyectos con la versión AEM 6.4, Experience Manager no guarda los campos **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]**. El valor del campo **[!UICONTROL subcarpetas]** se actualiza a **[!UICONTROL indefinido]** y el valor del campo **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** se actualiza a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** opción disponible en el **[!UICONTROL Más]** La lista desplegable no permite seleccionar el destino de destino en Experience Manager. La opción **[!UICONTROL Enviar a]** funciona correctamente utilizando la lista desplegable **[!UICONTROL Acciones de documento]**. La opción **[!UICONTROL Enviar a]** funciona correctamente para la lista desplegable **[!UICONTROL Más]** y la lista desplegable **[!UICONTROL Acciones de documento]** disponible en la nueva experiencia de Workfront.

## Versiones anteriores {#previous-releases}

### Versión de noviembre de 2023 {#november-2023-release}

* AEM Mientras ve la lista de carpetas de, el cuadro de diálogo tarda más de un minuto en cargarse.
* Autorizado [!DNL Workfront] Los usuarios de reciben registros de errores de autenticación de forma consistente.

### Versión de octubre de 2023 {#october-2023-release}

* Cuando las suscripciones a eventos están deshabilitadas en Configuración avanzada, puede seguir seleccionando las opciones para **Suscribirse a los eventos de actualización de documentos para actualizar los metadatos de AEM Assets**, **Publicar todos los recursos del proyecto en Brand Portal al finalizar el proyecto** y **Habilitar la sincronización de comentarios**.

* Algunos de los recursos almacenados en Experience Manager no se representan correctamente al previsualizarlos en Workfront.

* Al reconfigurar la conexión de Experience Manager con Workfront, las suscripciones de eventos como la actualización de sincronización de comentarios, la eliminación o la actualización de documentos no se crean correctamente.

* Mejoras importantes de rendimiento de la API para la creación de carpetas vinculadas, actualizar, habilitar carpetas vinculadas, sincronizar comentarios, habilitar y deshabilitar, guardar la configuración avanzada en el conector.

### Versión de septiembre de 2023 {#september-2023-release}

* El conector mejorado de Experience Manager recupera todas las suscripciones de evento de Workfront mientras elimina una suscripción de evento de un proyecto, lo que provoca un impacto en el rendimiento de la aplicación.

* Cuando se envía un recurso de Workfront a Experience Manager, el tipo MIME del recurso no se establece en el atributo `dc:format` en Experience Manager.

* Los ID de proyecto de Workfront almacenados en el conector mejorado de Experience Manager incluyen duplicados.

### Versión de agosto de 2023 {#august-2023-release}

* No se pueden crear carpetas vinculadas en Experience Manager porque no hay ninguna cuenta de usuario asociada a la carpeta vinculada.

* Condiciones de carrera durante las actualizaciones de metadatos de un recurso en Experience Manager.

### Versión de junio de 2023 {#june-2023-release}

* Cuando tiene configurada la red avanzada, hay problemas al enviar contenido desde Adobe Workfront a AEM as a Cloud Service.


### Versión de mayo de 2023 {#may-2023-release}

* Workfront devuelve una respuesta HTTP 409 para suscripciones de evento duplicadas en función de una llamada REST de Experience Manager a Workfront, lo que provoca una excepción de puntero nulo.

### Versión de abril de 2023 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.9, publicada el 10 de abril de 2023, incluye las siguientes actualizaciones:

* Experience Manager muestra una excepción `DateTimeParseException` cuando recibe la fecha de la última modificación de Workfront durante la creación de la carpeta vinculada.

* Problemas al crear varias carpetas de proyecto vinculadas en un corto periodo de tiempo.

* No se puede configurar un límite de umbral en el número de nuevos conjuntos de carpetas vinculadas a proyectos.

### Versión de marzo de 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.8, publicado el 3 de marzo de 2023, incluye las siguientes actualizaciones:

* Mejoras de rendimiento en Experience Manager al crear carpetas vinculadas a proyectos en Workfront.

* Las eliminaciones de comentarios en Workfront ahora se reflejan en Experience Manager.

* Capacidad para administrar el bloqueo de nuevos clientes netos en Experience Manager as a Cloud Service para la configuración del conector.


### Versión de enero de 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] version 1.9.7, publicado el 2 de febrero de 2023, incluye las siguientes actualizaciones:

* El editor de metadatos no enumera las propiedades de los formularios personalizados de Workfront después de instalar la versión 1.9.6.

* La consola de desarrollo muestra el mensaje de error `/content/dam/jcr:content/metadata/wfProjectURL not found` después de instalar el conector mejorado de Workfront y abrir la página principal de Assets.

### Versión de diciembre de 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.6, publicado el 9 de diciembre de 2009, incluye las siguientes actualizaciones:

**Mejora**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* El conector mejorado de Workfront ahora admite la búsqueda de texto completo en recursos y carpetas.

**Corrección de errores**

* Los metadatos de la versión del documento no se sincronizan correctamente entre Workfront y Experience Manager.
* Problemas al crear una carpeta vinculada a Experience Manager en Workfront cuando la carpeta utiliza un esquema que no tiene definición en la configuración global.
* El formulario del editor de esquemas de metadatos deja de responder cuando se hace clic en cualquier campo debido a un tiempo de carga superior al esperado. Se ha añadido una configuración OSGi específica para formularios personalizados para resolver el problema. Los nombres de los formularios personalizados que añada al editor de esquemas de metadatos están disponibles en los registros.

### Versión de noviembre de 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.5, publicada el 11 de noviembre, incluye las siguientes actualizaciones:

* Cuando se define un solo valor para un campo de varios valores en Workfront, el valor del campo no se asigna correctamente a Experience Manager.

* Experience Manager muestra `SERVER_ERROR` en la pantalla **[!UICONTROL Vincular archivos y carpetas externos]** al acceder a las carpetas de recursos debido a permisos no válidos en `/content/dam/collections`.

* Al activar la opción **[!UICONTROL Publicar recursos en Brand Portal]** en la página de configuración del conector mejorado de Workfront se crea un evento incorrecto. El evento no se elimina incluso después de desactivar la opción.

  Para solucionar el problema:

   1. Actualice a la versión 1.9.5 del conector mejorado.

   1. Desactive la opción **[!UICONTROL Publicar recursos en Brand Portal]** en la configuración avanzada.

   1. Active la opción **[!UICONTROL Publicar recursos en Brand Portal]**.

   1. Elimine las suscripciones de evento erróneas.

      1. Realice llamadas GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Ejecute una llamada de API por cada número de página.

      1. Busque el siguiente texto para encontrar suscripciones de evento que coincidan con la siguiente URL y que no tengan un `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Asegúrese de que el contenido entre `"objId": "",` y `"url"` coincide con la respuesta JSON. El método recomendado para hacerlo es copiar desde cualquier suscripción de evento que tenga un `objId` y, a continuación, eliminar el número.

      1. Tenga en cuenta el ID de suscripción del evento.

      1. Elimine la suscripción de evento errónea. Realice una llamada de la API de eliminación a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` ya que el código de respuesta significa que se han eliminado correctamente las suscripciones a eventos erróneos.
  >[!NOTE]
  >
  >Si ya ha eliminado las suscripciones a eventos erróneos antes de ejecutar los pasos mencionados en este procedimiento, puede omitir el último paso de este procedimiento.

### Versión de octubre de 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.4, publicada el 7 de octubre, incluye las siguientes actualizaciones:

* No se puede ver la pestaña Suscripciones de eventos en la página de configuración del conector mejorado debido a la gran cantidad de eventos.

* Workfront no puede recuperar la lista de carpetas existentes en un proyecto, lo que provoca que se creen carpetas duplicadas.

### Versión de septiembre de 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.3, publicada el 16 de septiembre, incluye las siguientes actualizaciones:

* No se puede cargar un archivo que tenga más de 8 GB.
* Problemas durante la publicación automática de recursos enviados desde Workfront a AEM.
* El campo Ruta raíz no está disponible para el campo Etiquetas al editar un formulario de esquema de metadatos predeterminado.
* Problemas al añadir nuevas versiones en Workfront mediante flujos de trabajo de AEM.
* Cuando ejecuta una búsqueda en AEM de recursos disponibles en Workfront, AEM muestra un mensaje de error.
* Cuando se crea un flujo de trabajo en AEM para la creación de tareas a partir de un recurso y no se define un nombre de tarea principal, la tarea no se crea en Workfront.

### Versión de agosto de 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.2, publicada el 3 de agosto de 2003, incluye las siguientes actualizaciones:

* El flujo de trabajo **[!UICONTROL Cargar documento]** no consigue adjuntar un documento a Workfront.

* El flujo de trabajo **[!UICONTROL Cargar documento]** no consigue adjuntar un documento a Tareas y problemas en Workfront. El paso del flujo de trabajo adjunta correctamente un documento a los proyectos.

### Versión de julio de 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] versión 1.9.1 incluye las siguientes actualizaciones:

* Se ha añadido la autenticación entre aplicaciones de Experience Manager y Workfront mediante la clave de API de Workfront para instancias que se migran a Adobe IMS.

* Al vincular archivos o carpetas externos, la aplicación de Workfront muestra el mensaje de error `SERVER_ERROR`. El mensaje de error hace referencia a una excepción no autorizada debido a una discrepancia en las claves de API.

* Cuando se ejecuta un flujo de trabajo Crear tarea para un recurso, la excepción Puntero nulo se muestra en los mensajes de registro.

* Al activar la opción de configuración `Replace Spaces with DASH` en Configuración avanzada en Experience Manager, se produce la creación de carpetas duplicadas en Workfront.

### Versión de junio de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Al cargar mediante una carpeta vinculada o utilizar la acción `Send To` disponible en Workfront para cargar recursos en Experience Manager as a Cloud Service, los recursos se dañan y no se pueden abrir en Adobe Photoshop.

### Versión de marzo de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Ahora puede crear carpetas vinculadas entre Adobe Workfront y AEM Assets as a Cloud Service incluso si hay varias configuraciones de carpeta vinculadas a un proyecto.

* Se ha añadido compatibilidad con la paginación de suscripción de eventos.

* Se ha añadido compatibilidad con AEM 6.4.x.

* Se ha añadido compatibilidad con entornos proxy.

* Varias correcciones de errores basadas en los comentarios de socios y clientes.

>[!MORELIKETHIS]
>
>* [Integre  [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=es)
