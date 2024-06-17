---
title: Edición de imágenes
description: Edite imágenes mediante opciones que se sirven de [!DNL Adobe Express] y guarde imágenes actualizadas como versiones.
role: User
exl-id: cfc4c7b7-da8c-4902-9935-0e3d4388b975
feature: Best Practices, Interactive Images, Smart Crop, Smart Imaging
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 72%

---

# Edición de imágenes en [!DNL Assets view] {#edit-images}

[!DNL Assets view] proporciona opciones de edición fáciles de usar que se sirven de [!DNL Adobe Express]. Las acciones de edición disponibles mediante [!DNL Adobe Express] son Cambiar tamaño de imagen, Quitar fondo, Recortar imagen y Convertir JPEG en PNG o viceversa.

Después de editar una imagen, puede guardar la nueva como una nueva versión. El uso de versiones le ayuda a volver al recurso original más adelante, si es necesario. Además, las versiones solo están disponibles para los tipos de archivo PNG, lo que significa que cuando intenta eliminar el fondo de un tipo de archivo JPG, JPG se convierte automáticamente a PNG. Para editar una imagen, [abra su previsualización](navigate-assets-view.md) y haga clic en **[!UICONTROL Editar imagen]**.

>[!NOTE]
>
>Puede editar imágenes de tipos de archivo PNG y JPEG mediante [!DNL Adobe Express].

<!--The editing actions that are available are Spot healing, Crop and straighten, Resize image, and Adjust image.-->

## Edición de imágenes mediante Adobe Express {#edit-using-express}

>[!CONTEXTUALHELP]
>id="assets_express_integration"
>title="Integración de Adobe Express"
>abstract="Herramientas de edición de imágenes sencillas e intuitivas con tecnología Adobe Express disponibles directamente en AEM Assets para aumentar la reutilización de contenidos y acelerar la velocidad del contenido."

### Cambiar tamaño de imagen {#resize-image-using-express}

Cambiar el tamaño de una imagen a un tamaño específico es un caso de uso popular. [!DNL Assets view] le permite cambiar rápidamente el tamaño de la imagen para adaptarla a los tamaños de foto comunes, ya que proporciona nuevas resoluciones calculadas previamente para tamaños de foto específicos. Para cambiar el tamaño de la imagen mediante [!DNL Assets view], siga estos pasos:

1. Seleccione una imagen de su [!DNL Experience Manager] Repositorio de recursos y haga clic en **Editar**.
2. Haga clic en **[!UICONTROL Redimensionar imagen]** en las acciones rápidas disponibles en el panel izquierdo.
3. Seleccione la plataforma de medios sociales adecuada en la lista desplegable **[!UICONTROL Cambiar tamaño para]** y el tamaño de la imagen en las opciones que se muestran.
4. Escale la imagen, si es necesario, utilizando el campo **[!UICONTROL Escala de imagen]**.
5. Haga clic en **[!UICONTROL Aplicar]** para que tengan efecto los cambios.
   ![Edición de imágenes con Adobe Express](assets/adobe-express-resize-image.png)

   La imagen editada está disponible para descargar. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como uno nuevo.
   ![Guardar imagen con Adobe Express](assets/adobe-express-resize-save.png)

### Quitar fondo {#remove-background-using-express}

Puede quitar el fondo de una imagen siguiendo unos sencillos pasos, tal como se indica a continuación:

1. Seleccione una imagen de su [!DNL Experience Manager] Repositorio de recursos y haga clic en **Editar**.
2. Haga clic en **[!UICONTROL Quitar fondo]** en las acciones rápidas disponibles en el panel izquierdo. Experience Manager Assets muestra la imagen sin fondo.
3. Haga clic en **[!UICONTROL Aplicar]** para que tengan efecto los cambios.
   ![Guardar imagen con Adobe Express](assets/adobe-express-remove-background.png)

### Recortar imagen {#crop-image-using-express}

Transforme una imagen en un tamaño perfecto es fácil gracias al uso de las acciones integradas rápidas de [!DNL Adobe Express].

1. Seleccione una imagen de su [!DNL Experience Manager] Repositorio de recursos y haga clic en **Editar**.
2. Haga clic en **[!UICONTROL Recortar imagen]** en las acciones rápidas disponibles en el panel izquierdo.
3. Arrastre los identificadores de las esquinas de la imagen para crear el recorte deseado.
4. Haga clic en **[!UICONTROL Aplicar]**.
   ![Guardar imagen con Adobe Express](assets/adobe-express-crop-image.png)
La imagen recortada está disponible para descargar. Puede guardar el recurso editado como una nueva versión del mismo recurso o guardarlo como uno nuevo.

### Convertir JPEG a PNG {#convert-jpeg-to-png-using-express}

Puede convertir rápidamente una imagen JPEG a un formato PNG mediante Adobe Express. Siga estos pasos:

1. Seleccione una imagen de su [!DNL Experience Manager] Repositorio de recursos y haga clic en **Editar**.
2. Clic **[!UICONTROL Convertir a PNG]** de las acciones rápidas disponibles en el panel izquierdo.
   <!--![Convert to PNG with Adobe Express](/help/using/assets/adobe-express-convert-image.png)-->
3. Haga clic en **[!UICONTROL Aplicar]**.
4. Vaya a **[!UICONTROL Guardar como en la parte superior derecha]** y haga clic en **[!UICONTROL Guardar como nuevo recurso]**.

### Convertir PNG a JPEG {#convert-png-to-jpeg-using-express}

Puede convertir rápidamente una imagen PNG a un formato de JPEG mediante el Adobe Express. Ejecute los siguientes pasos:

1. Seleccione una imagen de su [!DNL Experience Manager] Repositorio de recursos y haga clic en **Editar**.
2. Clic **[!UICONTROL Convertir en JPEG]** de las acciones rápidas disponibles en el panel izquierdo.
3. Haga clic en **[!UICONTROL Aplicar]**.
4. Vaya a **[!UICONTROL Guardar como en la parte superior derecha]** y haga clic en **[!UICONTROL Guardar como nuevo recurso]**.

### Restricciones {#limitations-adobe-express}

* Resolución de imagen admitida: mínimo de 50 píxeles, máximo de 6000 píxeles por dimensión.

* Tamaño máximo de archivo admitido: 17 MB.

## Edición de imágenes mediante el editor integrado de Adobe Express {#edit-using-embedded-editor}

Las organizaciones con acceso al Adobe Express pueden utilizar herramientas integradas de edición y creación de imágenes desde el Adobe Express y el Adobe Firefly disponibles directamente en la vista de recursos para mejorar la reutilización del contenido y acelerar la velocidad de contenido. También puede utilizar elementos predefinidos para que su recurso tenga un aspecto impresionante o realizar acciones rápidas para editar la imagen con solo unos clics.

Para editar imágenes con el editor de [!DNL Adobe Express] integrado, siga estos pasos:

1. Seleccione una imagen de su repositorio de recursos de [!DNL Experience Manager].
1. Haga clic en **[!UICONTROL Abrir en Adobe Express]**.

   ![Editor de Adobe Express integrado](assets/embedded-editor.png)

   Puede aprovechar la funcionalidad de [!DNL Adobe Express] para realizar todas las acciones relacionadas con la edición de imágenes, como [redimensionar imagen](https://helpx.adobe.com/in/express/using/resize-image.html), [quitar o cambiar el color de fondo](https://helpx.adobe.com/in/express/using/remove-background.html), [recortar imagen](https://helpx.adobe.com/in/express/using/crop-image.html), y mucho más.

1. Una vez completada la edición de imágenes, puede descargar un recurso como nuevo o guardarlo como una nueva versión.

## Creación de nuevos recursos mediante Adobe Express {#create-new-embedded-editor}

[!DNL Assets view] permite crear una nueva plantilla desde cero utilizando el editor integrado de [!DNL Adobe Express]. Para crear un nuevo recurso con [!DNL Adobe Express], ejecute los pasos siguientes:

1. Vaya a **[!UICONTROL Mi espacio de trabajo]** y haga clic en **[!UICONTROL Crear]** dentro del titular del Adobe Express que se muestra en la parte superior. El lienzo blanco de [!DNL Adobe Express] se muestra dentro de la interfaz de usuario de [!DNL Assets view].
1. Cree su contenido mediante [Plantillas](https://helpx.adobe.com/in/express/using/work-with-templates.html). En caso contrario, vaya a **[!UICONTROL Sus cosas]** para modificar el contenido existente.
1. Una vez finalizada la edición, haga clic en **[!UICONTROL Guardar como nuevo recurso]**.
1. Especifique la ruta de destino del recurso creado y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>* Solo puede modificar imágenes de los tipos de formato `JPEG` y `PNG`.
>* El tamaño del recurso debe ser inferior a 17 MB.
>* Puede guardar una imagen en `PDF`, `JPEG`, o `PNG` formatos; mientras que, cuando hay varias páginas, puede guardarlas como `PDF`.

<!--
## Edit images using [!DNL Adobe Photoshop Express] {#edit-using-photoshop-express}

<!--
After editing an image, you can save the new image as a new version. Versioning helps you to revert to the original asset later, if needed. To edit an image, [open its preview](navigate-assets-view.md#preview-assets) and click **[!UICONTROL Edit Image]** ![edit icon](assets/do-not-localize/edit-icon.png) from the rail on the right.

![Options to edit an image](assets/edit-image2.png)

*Figure: The options to edit images are powered by [!DNL Adobe Photoshop Express].*
-->
<!--
### Touch up images {#spot-heal-images-using-photoshop-express}

If there are minor spots or small objects on an image, you can edit and remove the spots using the spot healing feature provided by Adobe Photoshop.

The brush samples the retouched area and makes the repaired pixels blend seamlessly into the rest of the image. Use a brush size that is only slightly larger than the spot you want to fix.

![Spot healing edit option](assets/edit-spot-healing.png)

<!-- 
TBD: See if we should give backlinks to PS docs for these concepts.
For more information about how Spot Healing works in Photoshop, see [retouching and repairing photos](https://helpx.adobe.com/photoshop/using/retouching-repairing-images.html). 
-->
<!-- 
### Crop and straighten images {#crop-straighten-images-using-photoshop-express}

Using the crop and straighten option that you can do basic cropping, rotate image, flip it horizontally or vertically, and crop it to dimensions suitable for popular social media websites.

To save your edits, click **[!UICONTROL Crop Image]**. After editing, you can save the new image as a version.

![Option to crop and straighten](assets/edit-crop-straighten.png)

Many default options let you crop your image to the best proportions that fit various social media profiles and posts.

### Resize image {#resize-image-using-photoshop-express}

You can view the common photo sizes in centimeters or inches to know the dimensions. By default, the resizing method retains the aspect ratio. To manually override the aspect ratio, click ![](assets/do-not-localize/lock-closed-icon.png).

Enter the dimensions and click **[!UICONTROL Resize Image]** to resize the image. Before you save the changes as a version, you can either undo all the changes done before saving by clicking [!UICONTROL Undo] or you can change the specific step in the editing process by clicking [!UICONTROL Revert].

![Options when resizing an image](assets/resize-image.png)

### Adjust image {#adjust-image-using-photoshop-express}

[!DNL Assets view] lets you adjust the color, tone, contrast, and more, with just a few clicks. Click **[!UICONTROL Adjust image]** in the edit window. The following options are available in the right sidebar:

* **Popular**: [!UICONTROL High Contrast & Detail], [!UICONTROL Desaturated Contrast], [!UICONTROL Aged Photo], [!UICONTROL B&W Soft], and [!UICONTROL B&W Sepia Tone].
* **Color**: [!UICONTROL Natural], [!UICONTROL Bright], [!UICONTROL High Contrast], [!UICONTROL High Contrast & Detail], [!UICONTROL Vivid], and [!UICONTROL Matte].
* **Creative**: [!UICONTROL Desaturated Contrast], [!UICONTROL Cool Light], [!UICONTROL Turquoise & Red], [!UICONTROL Soft Mist], [!UICONTROL Vintage Instant], [!UICONTROL Warm Contrast], [!UICONTROL Flat & Green], [!UICONTROL Red Lift Matte], [!UICONTROL Warm Shadows], and [!UICONTROL Aged Photo].
* **B&W**: [!UICONTROL B&W Landscape], [!UICONTROL B&W High Contrast], [!UICONTROL B&W Punch], [!UICONTROL B&W Low Contrast], [!UICONTROL B&W Flat], [!UICONTROL B&W Soft], [!UICONTROL B&W Infrared], [!UICONTROL B&W Selenium Tone], [!UICONTROL B&W Sepia Tone], and [!UICONTROL B&W Split Tone].
* **Vignetting**: [!UICONTROL None], [!UICONTROL Light], [!UICONTROL Medium], and [!UICONTROL Heavy].

![Adjust image by editing](assets/adjust-image.png)

<!--
TBD: Insert a video of the available social media options.
-->

### Siguientes pasos {#next-steps}

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/?support-solution=General#support)

>[!MORELIKETHIS]
>
>* [Acciones rápidas en el Adobe Express](https://helpx.adobe.com/in/express/using/resize-image.html)
>* [Visualización del historial de versiones de un recurso](navigate-assets-view.md)
