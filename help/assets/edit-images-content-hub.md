---
title: Edición de imágenes en Content Hub mediante el Adobe Express
description: Edición de imágenes en Content Hub mediante el Adobe Express
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---

# Edición de imágenes en Content Hub {#edit-images-content-hub}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Editar imágenes en Content Hub mediante el Adobe Express](assets/edit-images-content-hub.png)

Content Hub le permite crear contenido nuevo con Adobe Express. Puede editar el contenido existente con herramientas fáciles de usar, producir variaciones de marca con plantillas y elementos de marca y crear contenido nuevo con las últimas funciones de GenAI de Adobe Firefly.

## Requisitos previos {#prereqs-edit-image-content-hub}

Derechos para acceder a Adobe Express y [usuarios de Content Hub con derechos para remezclar recursos con nuevas variaciones](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets) pueden editar imágenes con Content Hub.

>[!NOTE]
>
>Puede editar imágenes de PNG y tipos de archivo de JPG/JPEG de la mediante [!DNL Adobe Express].

## Edición de imágenes mediante [!DNL Adobe Express] {#edit-images-using-content-hub}

Para editar imágenes con Content Hub:

1. Haga clic en **[!DNL Open in Adobe Express]**, disponible en la tarjeta de recursos de la imagen que debe editar. También puede hacer clic en la imagen para abrir sus detalles y, a continuación, hacer clic en el logotipo de [!DNL Adobe Express]. A continuación, el editor incrustado para Adobe Express se carga sin salir de Content Hub.

   Puede aprovechar la funcionalidad [!DNL Adobe Express] para realizar todas las acciones relacionadas con la edición de imágenes, como [cambiar el tamaño de la imagen](https://helpx.adobe.com/express/using/resize-image.html), [quitar o cambiar el color de fondo](https://helpx.adobe.com/express/using/remove-background.html), [recortar imagen](https://helpx.adobe.com/express/using/crop-image.html), combinar la imagen con la imagen o el texto generados por IA y mucho más.

1. Realice las modificaciones y haga clic en **[!UICONTROL Guardar]** para guardar el recurso editado en cualquiera de los tipos de formato:

   * **[!UICONTROL PNG]** (se usa como formato de imagen de buena calidad)
   * JPG **** (adecuado para archivos pequeños)
   * **[!UICONTROL PDF]** (adecuado para documentos)

   ![Guardar imagen con Adobe Express](assets/adobe-express-save-as.png)

1. Especifique un nombre para el recurso en el campo **[!UICONTROL Guardar como]**.

1. Especifique el nombre de la campaña del recurso mediante el campo **[!UICONTROL Nombre de campaña]**. Puede utilizar un nombre existente o crear uno nuevo. Content Hub proporciona más opciones a medida que escribe el nombre. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

1. [Opcional] Defina valores para los campos **[!UICONTROL Palabras clave]**, **[!UICONTROL Canales]**, **[!UICONTROL Periodo de tiempo]** y **[!UICONTROL Región]**. El etiquetado y la agrupación de recursos por palabras clave, canales y ubicación permite a todas las personas que utilicen el contenido aprobado de la empresa encontrar estos recursos y mantenerlos organizados.

1. Haga clic en **[!UICONTROL Guardar como nuevo recurso]** para guardar el recurso.

Los administradores también pueden configurar los campos obligatorios y opcionales que se muestran al agregar recursos a Content Hub, como Nombre de campaña, Palabras clave, Canales, etc. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).
