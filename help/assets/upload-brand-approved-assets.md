---
title: Cargue los recursos aprobados por la marca en  [!DNL Content Hub]
description: Obtenga información sobre cómo cargar los recursos aprobados por la marca en Content Hub
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: f1be7cfc-1803-4c17-bb58-947104aa883c
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 12%

---

# Cargar recursos aprobados de marca en Content Hub {#upload-brand-approved-assets-content-hub}

>[!CONTEXTUALHELP]
>id="upload_assets_content_hub"
>title="Cargar recursos aprobados de marca en Content Hub"
>abstract="Añada recursos aprobados a Content Hub desde el sistema de archivos local o importe recursos desde OneDrive o fuentes de datos de Dropbox. Todos los recursos se muestran en el nivel superior de Content Hub, independientemente de la estructura de carpetas, para mejorar las capacidades de búsqueda."

[Los usuarios de Content Hub con derechos para agregar recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) pueden agregarlos a Content Hub desde el sistema de archivos local o importarlos desde fuentes de datos de OneDrive o Dropbox. Todos los recursos se muestran en el nivel superior en Content Hub, independientemente de la estructura de carpetas disponible en el sistema de archivos local o en las fuentes de datos de OneDrive y Dropbox, para mejorar las funciones de búsqueda.

>[!VIDEO](https://video.tv.adobe.com/v/3445378/?captions=spa&learn=on){transcript=true}

Los recursos marcados como `Approved` en Assets as a Cloud Service están disponibles automáticamente en Content Hub. Para obtener más información, consulte [Aprobar recursos para Content Hub](/help/assets/approve-assets-content-hub.md).

Para mejorar aún más la búsqueda de recursos, Content Hub le permite:

* Defina los detalles clave relevantes para la carga de recursos, como el nombre de la campaña, las palabras clave, los canales, etc.

* Genere automáticamente más propiedades para cada recurso tras la carga correcta, como tamaño de archivo, formato, resolución y algunas otras propiedades.

* Use la inteligencia artificial proporcionada por [Adobe AI](https://business.adobe.com/ai/adobe-genai.html) para aplicar automáticamente las etiquetas relevantes a todos los recursos cargados. Estas etiquetas, que reciben el adecuado nombre de Etiquetas inteligentes, aumentan la velocidad del contenido de los proyectos al ayudarle a encontrar recursos relevantes con rapidez.

Asegúrese de cargar únicamente los recursos aprobados por su marca [en Content Hub](/help/assets/approve-assets.md).

![Cargar recursos aprobados por la marca](assets/upload-brand-approved-assets.png)

## Requisitos previos {#prerequisites-add-assets}

[Los usuarios de Content Hub con derechos para agregar recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) pueden cargar recursos a Content Hub.

## Agregar recursos a Content Hub desde el sistema de archivos local {#add-assets-local-file-system}

Para agregar recursos a Content Hub, realice los siguientes pasos:

1. Haga clic en **[!UICONTROL Agregar Assets]** para ver el cuadro de diálogo **[!UICONTROL Agregar los recursos aprobados]** que le permite crear una carga.

1. En la sección **[!UICONTROL Arrastrar archivos o carpetas aquí]**, disponible en el panel derecho, puede arrastrar los recursos desde el sistema de archivos local o hacer clic en **[!UICONTROL Examinar]** para seleccionar manualmente los archivos o carpetas disponibles en el sistema de archivos local. Esta lista de archivos que forman parte de la carga están disponibles como una lista.


   También puede obtener una vista previa de las imágenes seleccionadas mediante las miniaturas y hacer clic en el icono X para eliminar cualquier imagen concreta de la lista. El icono X solo se muestra cuando pasa el ratón sobre el nombre o el tamaño de la imagen. También puede hacer clic en **[!UICONTROL Quitar todo]** para eliminar todos los elementos de la lista de carga.

   Para finalizar el proceso de carga y habilitar el **[!UICONTROL botón Upload button]**, debe agrupar los recursos con un nombre de campaña.

   ![Cargar recursos en Content Hub](assets/upload-assets-content-hub.png)

1. Defina el nombre para la carga mediante el campo **[!UICONTROL Nombre de campaña]**. Puede utilizar un nombre existente o crear uno nuevo. Content Hub proporciona más opciones a medida que escribe el nombre. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

1. Del mismo modo, defina valores para los campos **[!UICONTROL Palabras clave]**, **[!UICONTROL Canales]**, **[!UICONTROL Periodo de tiempo]** y **[!UICONTROL Región]**. El etiquetado y la agrupación de recursos por palabras clave, canales y ubicación permite a todas las personas que utilicen el contenido aprobado de la empresa encontrar estos recursos y mantenerlos organizados.

1. Haga clic en **[!UICONTROL Cargar]** para cargar los recursos en Content Hub. Aparece el cuadro de confirmación [!UICONTROL Detalles de la revisión]. Haga clic en [!UICONTROL Continuar].

1. Assets iniciar carga. Haga clic en [!UICONTROL Nueva carga] para reiniciar el procedimiento de carga. Haga clic en [!UICONTROL Listo] para completar la carga.

Los administradores también pueden configurar los campos obligatorios y opcionales que se muestran al cargar recursos, como Nombre de campaña, Palabras clave, Canales, etc. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

## Administración de recursos cargados mediante Content Hub {#manage-assets-uploaded-using-content-hub}

[Los usuarios de Content Hub con derechos para agregar recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) pueden [agregar recursos a Content Hub](/help/assets/upload-brand-approved-assets.md) desde el sistema de archivos local o importar recursos desde fuentes de datos de OneDrive o Dropbox. Todos los recursos se muestran en el nivel superior en Content Hub, independientemente de la estructura de carpetas disponible en el sistema de archivos local o en las fuentes de datos de OneDrive y Dropbox, para mejorar las funciones de búsqueda.

La visualización de los recursos cargados mediante Content Hub depende de si ha [habilitado la opción de aprobación automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Si la opción **[!UICONTROL Aprobación automática]** está habilitada, los recursos que cargue mediante Content Hub estarán disponibles automáticamente.

* Si la opción **[!UICONTROL Aprobación automática]** está deshabilitada, los recursos que cargue mediante Content Hub no se mostrarán automáticamente. Los recursos están disponibles en la carpeta `hydrated-assets` de su entorno de Assets as a Cloud Service. Vaya a la carpeta y [edite en lotes](#bulk-approve-assets-content-hub) el estado de esos recursos a `Approved` para que se muestren en Content Hub.

![Proceso de aprobación de Content Hub](/help/assets/assets/content-hub-approval.png)

## Preguntas frecuentes {#faqs-content-hub-upload-assets}

### ¿Qué tipos de recursos puedo cargar en Content Hub y desde dónde? {#asset-types-upload-to-content-hub}

Los usuarios de Content Hub con derechos para añadir recursos pueden cargar recursos aprobados por la marca desde su sistema de archivos local. Todos los recursos cargados, independientemente de su estructura de carpetas original, se muestran en el nivel superior en Content Hub para mejorar las capacidades de búsqueda.

### ¿Cómo mejora Content Hub la búsqueda y organización de recursos? {#search-content-hub}

Content Hub mejora la búsqueda y organización de recursos al permitir que los usuarios definan detalles clave para cada carga, como el nombre de la campaña, las palabras clave, los canales, el periodo de tiempo y la región. También genera automáticamente propiedades adicionales para cada recurso (como el tamaño, el formato y la resolución del archivo) y utiliza Adobe AI para aplicar etiquetas inteligentes, lo que facilita y acelera la búsqueda de recursos relevantes.

### ¿Cómo se cargan recursos desde mi sistema de archivos local a Content Hub? {#upload-assets-content-hub}

Para cargar recursos desde el sistema de archivos local, haga clic en **Agregar Assets** para abrir el cuadro de diálogo de carga. Puede arrastrar y soltar archivos o carpetas, o bien examinar manualmente los archivos o carpetas para seleccionarlos. Debe agrupar los recursos con un nombre de campaña y se recomienda rellenar otros campos, como palabras clave, canales, periodo de tiempo y región, para mejorar la organización. Una vez que esté listo, haga clic en **Cargar**, revise los detalles y confirme que desea iniciar la carga.

### ¿Cómo funciona el proceso de aprobación de recursos en Content Hub? {#asset-approval-content-hub}

Si la opción Auto-approval está activada, los recursos cargados mediante Content Hub están disponibles automáticamente. Si está desactivado, los recursos cargados se colocan en la carpeta **hydroassets** de Assets as a Cloud Service y debe editar manualmente su estado en **Aprobado** para que se muestren en Content Hub.

### ¿Puedo configurar los campos que son obligatorios u opcionales al cargar recursos en Content Hub? {#available-fields-while-uploading-assets-to-content-hub}

Los administradores pueden utilizar la interfaz de usuario de configuración para definir los campos obligatorios u opcionales al cargar recursos en Content Hub.

### ¿Qué debo hacer si los recursos cargados no se muestran automáticamente en Content Hub? {#assets-do-not-display-in-content-hub}

Si los recursos no se muestran automáticamente, significa que la opción Aprobación automática está desactivada. Los recursos se encuentran en la carpeta **hydrated-assets** del entorno de as a Cloud Service de Assets. Debe editar en lotes su estado a **Aprobado** para que aparezcan en Content Hub.

