---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: eb633db8fe64a62661c094b88f0ce8d9950ed6d7
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 1%

---

# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas de la versión generales de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de lanzamiento {#release-date}

La fecha de la versión de la última versión 1.9.9 de [!DNL Workfront for Experience Manager enhanced connector] es 10 de abril de 2023.

## Elementos destacados de la versión {#release-highlights}

La última versión de [!DNL Workfront for Experience Manager enhanced connector] incluye las siguientes actualizaciones:

* El Experience Manager muestra un `DateTimeParseException` cuando recibe la fecha de la última modificación de Workfront durante la creación de carpetas vinculadas.

* Problemas al crear varias carpetas de proyecto vinculadas en un plazo breve.

* No se puede configurar un límite de umbral en el número de nuevos conjuntos de carpetas vinculadas al proyecto.

>[!IMPORTANT]
>
>Adobe recomienda que [actualizar a la última versión 1.9.9](../assets/update-workfront-enhanced-connector.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conocidos {#known-issues}

* Al configurar carpetas de proyecto vinculadas con AEM 6.4, el Experience Manager no guarda los valores de **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** campos. El valor de la variable **[!UICONTROL subcarpetas]** actualizaciones de campo a **[!UICONTROL undefined]** y el valor de la variable **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** actualizaciones de campo a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** en la **[!UICONTROL Más]** la lista desplegable no permite seleccionar el destino de destino dentro de Experience Manager. La variable **[!UICONTROL Enviar a]** funciona correctamente con la opción **[!UICONTROL Acciones de documento]** lista desplegable. La variable **[!UICONTROL Enviar a]** funciona correctamente para **[!UICONTROL Más]** lista desplegable así como el **[!UICONTROL Acciones de documento]** lista desplegable disponible en la nueva experiencia de Workfront.

## Versiones anteriores {#previous-releases}

### Versión de marzo de 2023 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.8, publicada el 3 de marzo de 2023, incluye las siguientes actualizaciones:

* Mejoras de rendimiento en Experience Manager al crear carpetas vinculadas a proyectos en Workfront.

* Las eliminaciones de comentarios en Workfront ahora se reflejan en Experience Manager.

* Capacidad para administrar el bloqueo de nuevos clientes en el Experience Manager as a Cloud Service de configurar el conector.


### Versión de enero de 2023 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.7, publicada el 2 de febrero de 2023, incluye las siguientes actualizaciones:

* El editor de metadatos no enumera las propiedades de los formularios personalizados de Workfront después de instalar la versión 1.9.6.

* Se muestra la consola de desarrollo `/content/dam/jcr:content/metadata/wfProjectURL not found` mensaje de error después de instalar el conector mejorado de Workfront y abrir la página principal de Assets.

### Versión de diciembre de 2022 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.6, publicada el 09 de diciembre, incluye las siguientes actualizaciones:

**Mejora**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* El conector mejorado de Workfront ahora admite la búsqueda de texto completo en recursos y carpetas.

**Corrección de errores**

* Los metadatos de la versión del documento no se sincronizan correctamente entre Workfront y el Experience Manager.
* Problemas al crear una carpeta vinculada a un Experience Manager en Workfront cuando la carpeta utiliza un esquema que no tiene definición en la configuración global.
* El formulario del editor de esquemas de metadatos deja de responder cuando se hace clic en cualquier campo debido a un tiempo de carga superior al esperado. Se ha añadido una configuración OSGi específica para formularios personalizados para resolver el problema. Los nombres de los formularios personalizados que agregue al editor de esquemas de metadatos están disponibles en los registros.

### Versión de noviembre de 2022 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.5, publicada el 11 de noviembre, incluye las siguientes actualizaciones:

* Cuando define solo un valor para un campo de varios valores en Workfront, el valor del campo no se asigna correctamente al Experience Manager.

* El Experience Manager muestra la variable `SERVER_ERROR` en el **[!UICONTROL Vincular archivos y carpetas externos]** al acceder a las carpetas de recursos debido a permisos no válidos en `/content/dam/collections`.

* Al habilitar la variable **[!UICONTROL Publicar recursos en Brand Portal]** en la página de configuración del conector mejorado de Workfront crea un evento incorrecto. El evento no se elimina incluso después de desactivar la opción.

   Para resolver el problema:

   1. Actualice a la versión 1.9.5 del conector mejorado.

   1. Desactive el **[!UICONTROL Publicar recursos en Brand Portal]** en configuración avanzada.

   1. Active la variable **[!UICONTROL Publicar recursos en Brand Portal]** .

   1. Elimine las suscripciones de eventos incorrectas.

      1. Realizar llamadas de GET a `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         Ejecute una llamada de API por cada número de página.

      1. Busque el siguiente texto para encontrar suscripciones de eventos que coincidan con la siguiente dirección URL y que no tengan un `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         Asegúrese de que el contenido entre `"objId": "",` y `"url"` coincide con la respuesta JSON. El método recomendado para ello es copiar desde cualquier suscripción de evento que tenga un `objId` y, a continuación, elimine el número.

      1. Tenga en cuenta el ID de suscripción de evento.

      1. Elimine la suscripción de evento incorrecta. Realizar una llamada Eliminar API a `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` ya que el código de respuesta significa que se han eliminado correctamente suscripciones de eventos incorrectas.
   >[!NOTE]
   >
   >Si ya ha eliminado las suscripciones de eventos incorrectas antes de ejecutar los pasos mencionados en este procedimiento, puede omitir el último paso de este procedimiento.

### Versión de octubre de 2022 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.4, publicada el 07 de octubre, incluye las siguientes actualizaciones:

* No se puede ver la pestaña Suscripciones de eventos en la página de configuración del conector mejorado debido a un gran número de eventos.

* Workfront no puede recuperar la lista de carpetas existentes en un proyecto, lo que provoca la creación de carpetas duplicadas.

### Versión de septiembre de 2022 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.3, publicada el 16 de septiembre, incluye las siguientes actualizaciones:

* No se puede cargar un archivo de más de 8 GB de tamaño.
* Problemas durante la publicación automática de recursos que se envían de Workfront a AEM.
* El campo Ruta de acceso raíz no está disponible para el campo Etiquetas mientras se edita un formulario de esquema de metadatos predeterminado.
* Problemas al agregar nuevas versiones en Workfront mediante flujos de trabajo AEM.
* Cuando se ejecuta una búsqueda AEM de recursos disponibles en Workfront, AEM muestra un mensaje de error.
* Cuando se crea un flujo de trabajo AEM para la creación de tareas a partir de un recurso y no se define un nombre de tarea principal, la tarea no se crea en Workfront.

### Versión de agosto de 2022 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.2, publicada el 3 de agosto, incluye las siguientes actualizaciones:

* La variable **[!UICONTROL Cargar documento]** el paso del flujo de trabajo no puede adjuntar un documento a Workfront.

* La variable **[!UICONTROL Cargar documento]** el paso del flujo de trabajo no puede adjuntar un documento a Tareas y problemas en Workfront. El paso de flujo de trabajo adjunta un documento a Proyectos correctamente.

### Versión de julio de 2022 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] La versión 1.9.1 incluye las siguientes actualizaciones:

* Se ha agregado compatibilidad con la autenticación entre aplicaciones de Workfront y Experience Manager mediante la clave de API de Workfront para instancias migradas a Adobe IMS.

* Cuando se vinculan archivos o carpetas externos, la aplicación Workfront muestra la variable `SERVER_ERROR` mensaje de error. El mensaje de error hace referencia a una excepción no autorizada debido a una falta de coincidencia en las claves de API.

* Cuando se ejecuta un flujo de trabajo Crear tarea para un recurso, la excepción de puntero nulo aparece en los mensajes de registro.

* Al habilitar la variable `Replace Spaces with DASH` en Configuración avanzada en Experience Manager, resulta en una creación de carpetas duplicadas en Workfront.

### Versión de junio de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Al cargar a través de una carpeta vinculada o usar la variable `Send To` acción disponible en Workfront para cargar recursos a Experience Manager as a Cloud Service, los recursos se dañan y no se pueden abrir en Adobe Photoshop.

### Versión de marzo de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Ahora puede crear carpetas vinculadas entre Adobe Workfront y AEM Assets as a Cloud Service incluso si hay varias configuraciones de carpeta vinculadas al proyecto.

* Se ha agregado compatibilidad con la paginación de suscripción de eventos.

* Se ha agregado compatibilidad con AEM 6.4.x.

* Se ha agregado compatibilidad con entornos proxy.

* Varias correcciones de errores basadas en los comentarios de socios y clientes.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)

