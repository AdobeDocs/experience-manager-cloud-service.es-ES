---
title: Cargar recursos en el selector de recursos
description: Cargar recursos en el MFE del selector de recursos mediante la función de carga
role: Admin,User
exl-id: d6ff601c-3111-421a-9a94-cc524ce7e432
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Cargar archivos y carpetas al Selector de recursos {#upload-files-folders}

Puede cargar archivos o carpetas en el Selector de recursos desde su sistema de archivos local. Para cargar archivos mediante el sistema de archivos local, suele ser necesario utilizar una función de carga proporcionada por una aplicación de microfront-end del Selector de recursos.

## Cargar recursos desde el sistema de archivos local {#basic-upload}

Para agregar recursos al Selector de recursos, realice los siguientes pasos:

1. Si usa la vista de carril, vaya a los puntos suspensivos y haga clic en ![icono de carga](assets/upload-icon.svg) **[!UICONTROL Cargar]**. Por otro lado, haz clic en ![icono de carga](assets/upload-icon.svg) **[!UICONTROL Cargar]** en la parte superior derecha en caso de vista modal. Aparecerá la pantalla [!UICONTROL Cargar Assets].

   ![Cargar recursos al Selector de recursos](assets/upload-assets.png)

   Además, en la sección **[!UICONTROL Arrastrar archivos o carpetas aquí]**, puede arrastrar los recursos desde el sistema de archivos local o hacer clic en **[!UICONTROL Examinar]** para seleccionar manualmente los archivos o carpetas disponibles en el sistema de archivos local. Esta lista de archivos que forman parte de la carga están disponibles como una lista.

   ![Carga básica de recursos al Selector de recursos](assets/basic-upload.png)

   También puede obtener una vista previa de las imágenes seleccionadas mediante las miniaturas y hacer clic en el icono X para eliminar cualquier imagen concreta de la lista. El icono X solo se muestra cuando pasa el ratón sobre el nombre o el tamaño de la imagen. También puede hacer clic en **[!UICONTROL Quitar todo]** para eliminar todos los elementos de la lista de carga.

1. Para finalizar el proceso de carga, haz clic en **[!UICONTROL Cargar]**. Aparecerán los recursos cargados. Consulte [carga básica](/help/assets/asset-selector-customization.md#basic-upload) para ver el código que se puede configurar.

## Carga de recursos con metadatos {#upload-assets-with-metadata}

Puede añadir metadatos a los recursos mientras los carga inmediatamente en la aplicación. Los metadatos incluyen varios campos, como línea de asunto empresarial, detalles del producto, campaña, etc. Para ello, se utiliza la propiedad `metadataSchema`. Vaya a [propiedades del selector de recursos](/help/assets/asset-selector-properties.md) para obtener más información acerca de la propiedad `metadataSchema`.

Consulte [cargar con metadatos](/help/assets/asset-selector-customization.md#upload-with-metadata) para ver el fragmento de código necesario para la configuración.

![cargar recursos con metadatos](assets/upload-with-metadata.png)

1. Defina el nombre para la carga mediante el campo **[!UICONTROL Nombre de campaña]**. Puede utilizar un nombre existente o crear uno nuevo. El Selector de recursos proporciona más opciones a medida que escribe el nombre.

   Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

1. Del mismo modo, defina valores para los campos **[!UICONTROL Palabras clave]**, **[!UICONTROL Canales]**, **[!UICONTROL Periodo de tiempo]** y **[!UICONTROL Región]**. El etiquetado y la agrupación de recursos por palabras clave, canales y ubicación permite a todas las personas que utilicen el contenido aprobado de la empresa encontrar estos recursos y mantenerlos organizados.

1. Haga clic en **[!UICONTROL Cargar]** para cargar los recursos en el Selector de recursos. Aparece el cuadro de confirmación [!UICONTROL Detalles de la revisión]. Haga clic en [!UICONTROL Continuar].

1. Assets iniciar carga. Haga clic en [!UICONTROL Nueva carga] para reiniciar el procedimiento de carga. Haga clic en [!UICONTROL Listo] para completar la carga.


## Carga personalizada {#customize-upload}

El Selector de recursos le permite agregar un formulario de carga personalizado. Hay varias personalizaciones disponibles. Por ejemplo, la propiedad [hideUploadButton](/help/assets/asset-selector-properties.md) le permite ocultar el botón de carga que se muestra de forma predeterminada en la aplicación. En su lugar, puede personalizarlo para que se procese fuera de la aplicación MFE según sea necesario. Consulte [carga personalizada](/help/assets/asset-selector-customization.md#customized-upload) para ver la configuración.

![Carga personalizada](assets/customized-upload.png)

>[!MORELIKETHIS]
>
>* [Ejemplos de selector de recursos](/help/assets/asset-selector-examples.md)
>* [Integrar el Selector de recursos con varias aplicaciones](/help/assets/integrate-asset-selector.md)
>* [Propiedades del Selector de recursos](/help/assets/asset-selector-properties.md)
