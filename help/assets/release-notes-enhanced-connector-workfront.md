---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 590ee3f855051e212570c624e31ca3164938122c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---

# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas de la versión generales de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de la versión {#release-date}

La fecha de la versión de la última versión 1.9.3 de [!DNL Workfront for Experience Manager enhanced connector] es 16 de septiembre de 2022.

## Elementos destacados de la versión {#release-highlights}

La última versión de [!DNL Workfront for Experience Manager enhanced connector] incluye las siguientes mejoras y correcciones de errores:

* No se puede cargar un archivo de más de 8 GB de tamaño.
* Problemas durante la publicación automática de recursos que se envían de Workfront a AEM.
* El campo Ruta de acceso raíz no está disponible para el campo Etiquetas mientras se edita un formulario de esquema de metadatos predeterminado.
* Problemas al añadir nuevas versiones en Workfront mediante flujos de trabajo AEM
* Cuando se ejecuta una búsqueda AEM de recursos disponibles en Workfront, AEM muestra un mensaje de error.
* Cuando se crea un flujo de trabajo AEM para la creación de tareas a partir de un recurso y no se define un nombre de tarea principal, la tarea no se crea en Workfront.



>[!IMPORTANT]
>
>Adobe recomienda que [actualizar a la última versión 1.9.3](../assets/update-workfront-enhanced-connector.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conocidos {#known-issues}

* Al configurar carpetas de proyecto vinculadas con AEM 6.4, el Experience Manager no guarda los valores de **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** campos. El valor de la variable **[!UICONTROL subcarpetas]** actualizaciones de campo a **[!UICONTROL undefined]** y el valor de la variable **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** actualizaciones de campo a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** en la **[!UICONTROL Más]** la lista desplegable no permite seleccionar el destino de destino dentro de Experience Manager. La variable **[!UICONTROL Enviar a]** funciona correctamente con la opción **[!UICONTROL Acciones de documento]** lista desplegable. La variable **[!UICONTROL Enviar a]** funciona correctamente para **[!UICONTROL Más]** lista desplegable así como el **[!UICONTROL Acciones de documento]** lista desplegable disponible en la nueva experiencia de Workfront.

* Workfront muestra un `SERVER_ERROR` al vincular documentos a AEM después de actualizar a la versión 8316. Para resolver el problema, asigne `rep:readProperties` a `content/dam/collections` para `wf-workfront-user` AEM grupo de usuarios.

## Versiones anteriores {#previous-releases}

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
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

