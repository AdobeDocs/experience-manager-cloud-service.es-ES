---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 4b63c00847fa21967560a59c3bcd931433a3a73f
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 1%

---

# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas de la versión generales de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de lanzamiento {#release-date}

La fecha de la última versión, 1.9.12 de [!DNL Workfront for Experience Manager enhanced connector] es el 9 de agosto de 2023.

## Puntos destacados de la versión {#release-highlights}

La versión más reciente de [!DNL Workfront for Experience Manager enhanced connector] incluye las siguientes actualizaciones:

* No se pueden crear carpetas vinculadas en Experience Manager porque no hay ninguna cuenta de usuario asociada a la carpeta vinculada.

* Condiciones de carrera durante las actualizaciones de metadatos de un recurso en Experience Manager.


>[!NOTE]
>
>AEM La versión 6.4 de ha llegado al final de la asistencia ampliada. Para obtener más información, consulte nuestra [períodos de asistencia técnica](https://helpx.adobe.com/es/support/programs/eol-matrix.html). Buscar las versiones compatibles [aquí](https://experienceleague.adobe.com/docs/?lang=en).


>[!IMPORTANT]
>
>El Adobe le recomienda [actualice a la última versión 1.9.12](/help/assets/workfront-connector-install.md) de la [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conocidos {#known-issues}

* AEM Al configurar las carpetas vinculadas a proyectos con la versión 6.4 de, Experience Manager no guarda los valores de **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** campos. El valor de **[!UICONTROL subcarpetas]** actualizaciones de campo a **[!UICONTROL indefinido]** y el valor de **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** actualizaciones de campo a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** opción disponible en el **[!UICONTROL Más]** La lista desplegable no permite seleccionar el destino de destino en Experience Manager. El **[!UICONTROL Enviar a]** La opción funciona correctamente utilizando **[!UICONTROL Acciones de documento]** lista desplegable. El **[!UICONTROL Enviar a]** funciona correctamente para **[!UICONTROL Más]** y la lista desplegable. **[!UICONTROL Acciones de documento]** lista desplegable disponible en la nueva experiencia de Workfront.

## Versiones anteriores {#previous-releases}

### Versión de junio de 2023 {#june-2023-release}

* Cuando tiene configurada la red avanzada, hay problemas al enviar contenido desde Adobe Workfront AEM a la red as a Cloud Service de la red de la red de la red de la red de la red de la red de la red de la red de la red de la red de la red de la red de la red de.


### Versión de mayo de 2023 {#may-2023-release}

* Workfront devuelve una respuesta HTTP 409 para suscripciones de evento duplicadas en función de una llamada REST del Experience Manager a Workfront, lo que provoca una excepción de puntero nulo.

### Versión de abril de 2023 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.9 de, publicada el 10 de abril de 2023, incluye las siguientes actualizaciones:

* El Experience Manager muestra un `DateTimeParseException` excepción cuando recibe la fecha de la última modificación de Workfront durante la creación de la carpeta vinculada.

* Problemas al crear varias carpetas de proyecto vinculadas en un corto periodo de tiempo.

* No se puede configurar un límite de umbral en el número de nuevos conjuntos de carpetas vinculadas a proyectos.

### Versión de marzo de 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.8 de, publicada el 3 de marzo de 2023, incluye las siguientes actualizaciones:

* Mejoras de rendimiento en Experience Manager al crear carpetas vinculadas a proyectos en Workfront.

* Las eliminaciones de comentarios en Workfront ahora se reflejan en Experience Manager.

* Capacidad para administrar el bloqueo de nuevos clientes netos en el Experience Manager as a Cloud Service para la configuración del conector.


### Versión de enero de 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.7 de, publicada el 2 de febrero de 2023, incluye las siguientes actualizaciones:

* El editor de metadatos no enumera las propiedades de los formularios personalizados de Workfront después de instalar la versión 1.9.6.

* La consola de desarrollo muestra `/content/dam/jcr:content/metadata/wfProjectURL not found` mensaje de error después de instalar el conector mejorado de Workfront y abrir la página principal de Assets.

### Versión de diciembre de 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.6 de, lanzada el 9 de diciembre de 2009, incluye las siguientes actualizaciones:

**Mejora**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* El conector mejorado de Workfront ahora admite la búsqueda de texto completo en recursos y carpetas.

**Corrección de errores**

* Los metadatos de la versión del documento no se sincronizan correctamente entre Workfront y Experience Manager.
* Problemas al crear una carpeta vinculada al Experience Manager en Workfront cuando la carpeta utiliza un esquema que no tiene definición en la configuración global.
* El formulario del editor de esquemas de metadatos deja de responder cuando se hace clic en cualquier campo debido a un tiempo de carga superior al esperado. Se ha añadido una configuración OSGi específica para formularios personalizados para resolver el problema. Los nombres de los formularios personalizados que agregue al editor de esquemas de metadatos están disponibles en los registros.

### Versión de noviembre de 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.5 de, lanzada el 11 de noviembre de, incluye las siguientes actualizaciones:

* Cuando se define un solo valor para un campo de varios valores en Workfront, el valor del campo no se asigna correctamente al Experience Manager.

* El Experience Manager muestra `SERVER_ERROR` en el **[!UICONTROL Vincular archivos y carpetas externos]** al acceder a las carpetas de recursos debido a permisos no válidos en `/content/dam/collections`.

* Activación de la **[!UICONTROL Publicar recursos en Brand Portal]** en la página de configuración del conector mejorado de Workfront se crea un evento incorrecto. El evento no se elimina incluso después de deshabilitar la opción.

  Para resolver el problema:

   1. Actualice a la versión 1.9.5 del conector mejorado.

   1. Desactivar el **[!UICONTROL Publicar recursos en Brand Portal]** en configuración avanzada.

   1. Habilite la **[!UICONTROL Publicar recursos en Brand Portal]** opción.

   1. Elimine las suscripciones de evento incorrectas.

      1. Realizar llamadas de GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Ejecute una llamada de API por cada número de página.

      1. Busque el siguiente texto para buscar suscripciones de evento que coincidan con la siguiente URL y que no tengan un `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Asegúrese de que el contenido entre `"objId": "",` y `"url"` coincide con la respuesta JSON. El método recomendado para hacerlo es copiar desde cualquier suscripción de evento que tenga un `objId` y, a continuación, elimine el número.

      1. Tenga en cuenta el ID de suscripción de evento.

      1. Elimine la suscripción de evento incorrecta. Realizar una llamada de API de eliminación a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` ya que el código de respuesta significa la eliminación correcta de las suscripciones de evento incorrectas.
  >[!NOTE]
  >
  >Si ya ha eliminado las suscripciones a eventos incorrectas antes de ejecutar los pasos mencionados en este procedimiento, puede omitir el último paso de este procedimiento.

### Versión de octubre de 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.4, lanzada el 7 de octubre, incluye las siguientes actualizaciones:

* No se puede ver la pestaña Suscripciones de eventos en la página de configuración del conector mejorado debido a la gran cantidad de eventos.

* Workfront no puede recuperar la lista de carpetas existentes en un proyecto, lo que provoca la creación de carpetas duplicadas.

### Versión de septiembre de 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.3 de, lanzada el 16 de septiembre de, incluye las siguientes actualizaciones:

* No se puede cargar un archivo que tenga más de 8 GB.
* Problemas durante la publicación automática de recursos enviados desde Workfront AEM a los recursos de la publicación de la aplicación de forma.
* El campo Ruta raíz no está disponible para el campo Etiquetas al editar un formulario de esquema de metadatos predeterminado.
* Problemas al añadir nuevas versiones en Workfront AEM mediante flujos de trabajo de.
* AEM Cuando ejecuta una búsqueda de recursos disponibles en Workfront AEM en la que se realiza una búsqueda de la, muestra un mensaje de error.
* AEM Cuando se crea un flujo de trabajo de para la creación de tareas a partir de un recurso y no se define un nombre de tarea principal, la tarea no se crea en Workfront.

### Versión de agosto de 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.2, lanzada el 3 de agosto de 2003, incluye las siguientes actualizaciones:

* El **[!UICONTROL Cargar documento]** el paso del flujo de trabajo no puede adjuntar un documento a Workfront.

* El **[!UICONTROL Cargar documento]** Este paso del flujo de trabajo no puede adjuntar un documento a Tareas y problemas en Workfront. El paso del flujo de trabajo adjunta correctamente un documento a los proyectos.

### Versión de julio de 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.1 de incluye las siguientes actualizaciones:

* Se ha agregado compatibilidad con la autenticación entre aplicaciones de Experience Manager y Workfront mediante la clave de API de Workfront para instancias que se migran a Adobe IMS.

* Al vincular archivos o carpetas externos, la aplicación de Workfront muestra el `SERVER_ERROR` mensaje de error. El mensaje de error hace referencia a una excepción no autorizada debido a una discrepancia en las claves de API.

* Cuando se ejecuta un flujo de trabajo Crear tarea para un recurso, la excepción Puntero nulo se muestra en los mensajes de registro.

* Al activar la variable `Replace Spaces with DASH` opción de configuración en Configuración avanzada en Experience Manager, da como resultado la creación de carpetas duplicadas en Workfront.

### Versión de junio de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Cuando carga a través de una carpeta vinculada o utiliza el `Send To` acción disponible en Workfront para cargar recursos en Experience Manager as a Cloud Service, los recursos se dañan y no se pueden abrir en Adobe Photoshop.

### Lanzamiento de marzo de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Ahora puede crear carpetas vinculadas entre Adobe Workfront y AEM Assets as a Cloud Service incluso si hay varias configuraciones de carpeta vinculadas a un proyecto.

* Se ha agregado compatibilidad con la paginación de suscripción de evento.

* AEM Se ha agregado compatibilidad con la versión 6.4.x de la versión de.

* Se ha agregado compatibilidad con entornos proxy.

* Varias correcciones de errores basadas en los comentarios de socios y clientes.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
