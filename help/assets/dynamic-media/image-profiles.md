---
title: Perfiles de imagen de Dynamic Media
description: Obtenga información sobre cómo crear perfiles de imagen de Dynamic Media que contengan ajustes para máscara de enfoque y recorte inteligente o muestra inteligente, o ambos. A continuación, aplique el perfil a una carpeta de recursos de imagen.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3555'
ht-degree: 5%

---

# Perfiles de imagen de Dynamic Media {#image-profiles}

Al cargar imágenes, puede recortar automáticamente la imagen al cargar aplicando un perfil de imagen a la carpeta.

>[!IMPORTANT]
>
>Los perfiles de imagen no son aplicables a archivos de PDF, GIF animado o INDD (Adobe InDesign).

## Máscara de enfoque, opción {#unsharp-mask}

Al crear un perfil de imagen, puede utilizar el complemento **[!UICONTROL Máscara de enfoque]** opción para ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora. Este efecto utiliza las mismas opciones que el filtro &quot;Máscara de enfoque&quot; de Adobe Photoshop.

>[!NOTE]
>
>La máscara de enfoque solo se aplica a representaciones a escala reducida dentro del PTIFF (tiff piramidal) con una disminución de resolución superior al 50 %. Esto significa que las representaciones de mayor tamaño dentro del PTIFF no se ven afectadas por la máscara de enfoque. Mientras que las representaciones de menor tamaño, como las miniaturas, se modifican (y muestran la máscara de enfoque).

Entrada **[!UICONTROL Máscara de enfoque]**, tiene las siguientes opciones de filtrado:

<table>
 <tbody>
  <tr>
   <td><strong>Opción</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Cantidad</td>
   <td>Controla la cantidad de contraste que se aplica a los píxeles del borde. El valor predeterminado es 1,75. Para imágenes de alta resolución, puede aumentarla hasta 5. Considere la cantidad como una medida de la intensidad del filtro. El intervalo es de 0 a 5.</td>
  </tr>
  <tr>
   <td>Radio</td>
   <td>Determina el número de píxeles adyacentes a los píxeles de borde que afectarán al enfoque. Para imágenes de alta resolución, escriba de 1 a 2. Un valor bajo enfoca únicamente los píxeles de borde; un valor alto enfoca una banda más ancha de píxeles. El valor correcto depende del tamaño de la imagen. El valor predeterminado es 0,2. El intervalo es de 0 a 250.</td>
  </tr>
  <tr>
   <td>Umbral</td>
   <td><p>Determina el intervalo de contraste que debe omitirse cuando se aplica el filtro de máscara de enfoque. En otras palabras, esta opción determina la diferencia que debe existir entre los píxeles enfocados y el área adyacente para que se consideren píxeles de borde y se enfoquen. Para evitar introducir ruido, experimente con valores entre 0 y 255.</p> </td>
  </tr>
 </tbody>
</table>

El enfoque se describe en [Enfoque de imágenes](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opciones de recorte {#crop-options}

Al implementar el recorte inteligente en imágenes, Adobe recomienda la siguiente práctica recomendada y aplica el siguiente límite:

| Recurso: tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| **Imagen** - Número de recortes inteligentes por imagen | 5 | 100 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

Las coordenadas de recorte inteligente dependen de la relación de aspecto. Para la configuración de Recorte inteligente en un perfil de imagen, si la proporción de aspecto es la misma para las dimensiones añadidas en el perfil de imagen, se envía la misma proporción de aspecto a Dynamic Media. El Adobe recomienda utilizar la misma área de recorte. Al hacerlo, se asegura de que no haya ningún impacto en las diferentes dimensiones utilizadas en el perfil de imagen.

Cada generación de recorte inteligente que cree requiere un procesamiento adicional. Por ejemplo, si se añaden más de cinco proporciones de aspecto de recorte inteligente, la tasa de ingesta de recursos puede ser lenta. También puede causar un aumento de la carga en los sistemas. Como puede aplicar el recorte inteligente en el nivel de carpeta, Adobe recomienda utilizarlo en las carpetas *solamente* donde sea necesario.

**Directrices para definir el recorte inteligente en un perfil de imagen**
Para mantener bajo control el uso del recorte inteligente y optimizar el tiempo de procesamiento y el almacenamiento de los cultivos, Adobe recomienda las siguientes directrices y sugerencias:

* Los recursos de imagen a los que se va a aplicar un recorte inteligente deben tener un mínimo de 50 x 50 píxeles o más.
* Lo ideal es que tenga de 10 a 15 cultivos inteligentes por imagen para optimizar las relaciones de pantalla y el tiempo de procesamiento.
* Asigne un nombre a los cultivos inteligentes en función de las dimensiones de recorte, no del uso final. Al hacerlo, se ayuda a optimizar los duplicados en los que se utiliza una sola dimensión en varias páginas.
* Cree perfiles de imagen en cuanto a página/tipo de recurso para carpetas y subcarpetas específicas en lugar de un perfil de recorte inteligente común que se aplique a todas las carpetas o todos los recursos.
* Un perfil de imagen que aplique a las subcarpetas anulará un perfil de imagen que se aplique a la carpeta.
* No se permite un perfil de imagen que contenga dimensiones de recorte inteligente duplicadas.
* No se permiten perfiles de imagen con nombre duplicado que tengan definidas las opciones de recorte inteligente.

Hay dos opciones de recorte de imagen entre las que elegir: Recorte de píxeles y Recorte inteligente. También puede optar por automatizar la creación de muestras de color e imagen o conservar el contenido de recorte en las resoluciones de destino.

>[!IMPORTANT]
>
>El Adobe recomienda revisar los cultivos y las muestras que se hayan generado para asegurarse de que sean adecuados y relevantes para la marca y los valores.

| Opción | Cuándo se usa | Descripción |
| --- | --- | --- |
| **[!UICONTROL Recorte de píxeles]** | Recorte masivo de imágenes basado únicamente en dimensiones. | Desde el **[!UICONTROL Opciones de recorte]** , seleccione la opción **[!UICONTROL Recorte de píxeles]**.<br>Para recortar desde los lados de una imagen, escriba el número de píxeles que desea recortar desde cualquier lado o cada lado de la imagen. La cantidad de imagen que se recorta depende de la configuración de ppp (píxeles por pulgada) en el archivo de imagen.<br>Un recorte de píxeles del perfil de imagen se procesa de la siguiente manera:<br>· Los valores son Superior, Inferior, Izquierda y Derecha.<br>· Se considera la parte superior izquierda `0,0` y el recorte de píxeles se calcula a partir de ahí.<br>· Punto de inicio del recorte: a la izquierda es X y arriba es Y<br>· Cálculo horizontal: tamaño de píxel horizontal de la imagen original menos Izquierda y luego menos Derecha.<br>· Cálculo vertical: altura de píxel vertical menos Superior y luego menos Inferior.<br>Por ejemplo, supongamos que tiene una imagen de 4000 x 3000 píxeles. Utilice valores: Superior=250, Inferior=500, Izquierda=300, Derecha=700.<br>Desde el recorte superior izquierdo (300 250) utilizando el espacio de relleno de (4000-300-700, 3000-250-500 o 3000 2250). |
| **[!UICONTROL Recorte inteligente]** | Recorte masivo de imágenes en función de su punto focal visual. | Smart Crop utiliza el poder de la inteligencia artificial en Adobe Sensei para automatizar rápidamente el recorte masivo de imágenes. El recorte inteligente detecta y recorta automáticamente el punto focal de cualquier imagen para adquirir el punto de interés deseado, independientemente del tamaño de la pantalla.<br>Desde el **[!UICONTROL Opciones de recorte]** , seleccione la opción **[!UICONTROL Recorte inteligente]**, luego a la derecha de **[!UICONTROL Recorte de imagen interactivo]**, habilite (active) la función.<br>Los tamaños de punto de interrupción predeterminados (**[!UICONTROL Grande]**, **[!UICONTROL Mediana]**, **[!UICONTROL Pequeño]**) cubren la gama completa de tamaños que la mayoría de las imágenes se utilizan en dispositivos móviles y tabletas, equipos de escritorio y banners. Si lo desea, puede editar los nombres predeterminados de Grande, Mediano y Pequeño.<br>Para añadir más puntos de interrupción, seleccione **[!UICONTROL Añadir recorte]**; para eliminar un recorte, seleccione el icono Basura. |
| **[!UICONTROL Muestra de color e imagen]** | Bulk genera una muestra de imagen para cada imagen. | **Nota**: la muestra inteligente no es compatible con Dynamic Media Classic.<br>Busque y genere automáticamente muestras de alta calidad a partir de imágenes de productos que muestren color o textura.<br>Desde el **[!UICONTROL Opciones de recorte]** , seleccione la opción **[!UICONTROL Recorte inteligente]**. A la derecha de **[!UICONTROL Muestra de color e imagen]**, habilite (active) la función. Introduzca un valor de píxel en **[!UICONTROL Ancho]** y **[!UICONTROL Altura]** cuadros de texto.<br>Aunque todos los recortes de imagen están disponibles en el carril Representaciones, las muestras solo se utilizan a través del **[!UICONTROL Copiar URL]** función. Utilice su propio componente de visualización para procesar la muestra en el sitio. La excepción a esta regla son los titulares de carrusel. Dynamic Media proporciona el componente de visualización para la muestra utilizada en los titulares del carrusel.<br><br>**Uso de muestras de imagen**<br> La URL de las muestras de imagen es sencilla:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Donde `:Swatch` se adjunta a la solicitud de recurso.<br><br>**Uso de muestras de color**<br> Para utilizar muestras de color, debe crear un `req=userdata` con lo siguiente:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por ejemplo, a continuación se muestra un recurso de muestra en Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Y aquí está la muestra del recurso correspondiente `req=userdata` URL:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>El `req=userdata` La respuesta es la siguiente:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>También puede solicitar una `req=userdata` respuesta en formato XML o JSON, como en los siguientes ejemplos de URL:<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota**: debe crear su propio componente WCM para solicitar una muestra de color y analizar el `SmartSwatchColor` , representado por un valor hexadecimal de RGB de 24 bits.<br>Consulte también [`userdata`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html) en la Guía de referencia de visores. |
| **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** | Para mantener el contenido de recorte en la misma proporción de aspecto | Se utiliza al crear un perfil de recorte inteligente.<br>Para generar nuevo contenido de recorte (sin dejar de mantener el punto focal) para una proporción de aspecto determinada en diferentes resoluciones, desactive esta opción <br>Si decide desactivar esta casilla, asegúrese de que la resolución de imagen original sea mayor que las resoluciones definidas para el perfil de recorte inteligente.<br><br>Por ejemplo, supongamos que ha establecido las relaciones de aspecto en 600 x 600 (Grande), 400 x 400 (Mediano) y 300 x 300 (Pequeño).<br>Cuándo **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** La opción es *comprobado*, verá el mismo recorte en las tres resoluciones, similar a la siguiente salida de muestra de imágenes (solo con fines ilustrativos):<br>![Opción activada](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Cuándo **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** La opción es *desenfrenado*, el contenido de recorte es nuevo para las tres resoluciones, similar a la siguiente salida de muestra de imágenes (solo para fines ilustrativos):<br>![Opción sin marcar](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

### Formatos de archivo de imagen compatibles con el recorte inteligente y las muestras de color

La resolución máxima admitida del tamaño del archivo de entrada es de 16 K.

>[!NOTE]
>
>La resolución de 16K es una resolución de pantalla con aproximadamente 16 000 píxeles horizontalmente. La resolución de 16K más discutida es 15360 × 8640, que duplica el recuento de píxeles de 8K UHD en cada dimensión, para un total de cuatro veces más píxeles. Esta resolución tiene 132,7 megapíxeles, 16 veces más píxeles que la resolución 4K y 64 veces más píxeles que la resolución 1080p.

| Formato de imagen | Extensión de archivo sin distinción de mayúsculas y minúsculas | Tipo MIME | Espacio de color de entrada compatible | Tamaño máximo de archivo de entrada admitido | ¿Formato de imagen admitido? |
| --- | --- | --- | --- | --- | --- |
| BMP | `.bmp` | image/bmp | sRGB | 4 GB | Sí |
| CMYK | | | | | Sí |
| EPS | | | | | No |
| GIF | `.gif` | image/gif | sRGB | 15 GB | Sí; se utiliza el primer fotograma del GIF animado para la representación. No se puede configurar ni cambiar el primer fotograma. |
| JPEG | `.jpg` y `.jpeg` | image/jpeg | sRGB | 15 GB | Sí |
| PNG | `.png` | image/png | sRGB | 15 GB | Sí |
| PSD | `.psd` | image/vnd.adobe.photoshop | sRGB<br>CMYK | 2 GB | Sí |
| SVG | | | | | No |
| TIFF | `.tif` y `.tiff` | image/tiff | sRGB<br>CMYK | 4 GB | Sí |
| WebP/WebP animado | | | | | No |

## Creación de perfiles de imagen de Dynamic Media {#creating-image-profiles}

Para definir parámetros de procesamiento avanzados para otros tipos de recursos, consulte [Configuración del procesamiento de recursos](config-dm.md#configuring-asset-processing).

Consulte [Acerca de los perfiles de imagen y de vídeo de Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Consulte también [Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de procesamiento](/help/assets/organize-assets.md).

**Para crear perfiles de imagen de Dynamic Media:**

1. Seleccione el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Para añadir un perfil de imagen, seleccione **[!UICONTROL Crear]**.
1. Introduzca un nombre de perfil y valores para máscara de enfoque, recorte o muestra, o ambos.

   Sugerencia: Utilice un nombre de perfil específico para el propósito deseado. Por ejemplo, supongamos que desea crear un perfil que genere solo muestras. Es decir, el recorte inteligente está desactivado (desactivado) y la muestra de color e imagen activada (activado). En estos casos, se puede utilizar el nombre de perfil &quot;Muestras inteligentes&quot;.

   Consulte también [Opciones de recorte y muestra inteligente](#crop-options) y [Máscara de enfoque](#unsharp-mask).

   ![recorte](assets/crop.png)

1. Seleccionar **[!UICONTROL Guardar]**. El perfil creado aparece en la lista de perfiles disponibles.

## Editar o eliminar perfiles de imagen de Dynamic Media {#editing-or-deleting-image-profiles}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea editar o eliminar. Para editarlo, seleccione **[!UICONTROL Editar perfil de procesamiento de imagen]**. Para eliminarlo, seleccione **[!UICONTROL Eliminar perfil de procesamiento de imagen]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Si está editando, guarde los cambios. Si está eliminando, confirme que desea eliminar el perfil.

## Aplicar un perfil de imagen de Dynamic Media a las carpetas {#applying-an-image-profile-to-folders}

Cuando se asigna un perfil de imagen a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Como tal, solo puede asignar un perfil de imagen a una carpeta. Tenga en cuenta la estructura de carpetas de donde carga, almacena, utiliza y archiva los recursos.

Si ha asignado un perfil de imagen diferente a una carpeta, el nuevo perfil anulará el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario con el nombre del perfil que aparece en la tarjeta.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puede aplicar perfiles de imagen a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen existente cambiado a posteriori. Consulte [Vuelva a procesar los recursos de una carpeta después de editar su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Aplicar perfiles de imagen de Dynamic Media a carpetas específicas {#applying-image-profiles-to-specific-folders}

Puede aplicar un perfil de imagen a una carpeta desde el **[!UICONTROL Herramientas]** o si se encuentra en la carpeta, en **[!UICONTROL Propiedades]**.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente cambiado a posteriori. Consulte [Vuelva a procesar los recursos de una carpeta después de editar su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas desde la interfaz de usuario Perfiles {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea aplicar a una o varias carpetas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleccionar **[!UICONTROL Aplicar perfil de procesamiento a las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para recibir los recursos cargados recientemente y seleccione **[!UICONTROL Aplicar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicar perfiles de imagen de Dynamic Media a carpetas desde Propiedades {#applying-image-profiles-to-folders-from-properties}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]**.
1. Vaya a *carpeta* (no es un recurso) al que desea aplicar un perfil de imagen.
1. Según la vista en la que se encuentre, siga uno de estos procedimientos:
   * En la vista de tarjeta, pase el puntero sobre la carpeta y, a continuación, seleccione la marca de verificación para seleccionarla.
   * En Vista de columna o Vista de lista, active la casilla a la izquierda del nombre de la carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione el **[!UICONTROL Procesamiento de Dynamic Media]** pestaña.
1. En **[!UICONTROL Perfil de imagen]**, desde el **[!UICONTROL Nombre de perfil]** , seleccione el perfil que desee aplicar.
1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar un perfil de imagen de Dynamic Media globalmente {#applying-an-image-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicar uno globalmente. Cualquier contenido cargado en Experience Manager Assets en cualquier carpeta tiene el perfil seleccionado aplicado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente cambiado a posteriori. Consulte [Vuelva a procesar los recursos de una carpeta después de editar su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Para aplicar un perfil de imagen de Dynamic Media globalmente:**

1. Realice una de las siguientes acciones:

   * Vaya a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` y aplique el perfil adecuado y seleccione **[!UICONTROL Guardar]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * Vaya al CRXDE Lite en el siguiente nodo: `/content/dam/jcr:content`.

     Añadir la propiedad `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` y seleccione **[!UICONTROL Guardar todo]**.

     ![configure_image_profiles](assets/configure_image_profiles.png)

## Editar el recorte inteligente o la muestra inteligente de una sola imagen {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>El Adobe recomienda revisar los cultivos inteligentes y las muestras inteligentes que se hayan generado para asegurarse de que sean adecuados y relevantes para su marca y valores.

Puede realinear o cambiar manualmente el tamaño de la ventana de recorte inteligente de una imagen para restringir aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

>[!IMPORTANT]
>
>Cuando se realinea o se cambia el tamaño manualmente de la ventana de recorte inteligente de un recurso, dicha edición se mantiene y conserva, incluso si posteriormente se decide reprocesar el recurso. Sin embargo, si edita la anchura, la altura o ambas opciones en la **[!UICONTROL Recorte de imagen interactivo]** del perfil de imagen y, a continuación, ese recurso está sujeto a reprocesamiento.
>Consulte [Volver a procesar los recursos de Dynamic Media en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Puede volver a ejecutar el recorte inteligente para generar los recortes adicionales de nuevo, si es necesario.

Consulte también [Editar el recorte inteligente o la muestra inteligente de varias imágenes](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar el recorte inteligente o la muestra inteligente de una sola imagen:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]**, luego a la carpeta que tenga aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.
1. Para abrir su contenido, seleccione la carpeta.
1. Seleccione la imagen cuyo recorte inteligente o muestra inteligente desee ajustar.
1. En la barra de herramientas, seleccione **[!UICONTROL Recorte inteligente]**.

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior derecha de la página, arrastre la barra deslizante hacia la izquierda o hacia la derecha para aumentar o disminuir la visualización de la imagen, respectivamente.
   * En la imagen, arrastre un controlador de esquina para ajustar el tamaño del área visible del recorte o muestra.
   * En la imagen, arrastre el cuadro o la muestra a una nueva ubicación. Solo puede editar muestras de imagen; las muestras de color son estáticas.
   * Sobre la imagen, seleccione  **[!UICONTROL Revertir]** para deshacer todas las ediciones y restaurar el recorte o la muestra original.
   * Utilice las teclas de flecha del teclado para recortar el tamaño del fotograma, cambiar la posición de la imagen o ambas cosas.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**, luego seleccione **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Editar el recorte inteligente o la muestra inteligente de varias imágenes {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>El Adobe recomienda revisar los cultivos inteligentes y las muestras inteligentes que se hayan generado para asegurarse de que sean adecuados y relevantes para su marca y valores.

Después de aplicar un perfil de imagen (que contiene Recorte inteligente) a una carpeta, se les aplica un recorte a todas las imágenes de dicha carpeta. Si lo desea, puede *manualmente* realinee o cambie el tamaño de la ventana de recorte inteligente en varias imágenes para restringir aún más su punto focal.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

>[!IMPORTANT]
>
>Cuando se realinea o se cambia el tamaño manualmente de la ventana de recorte inteligente de varios recursos, dichas ediciones se mantienen y conservan, incluso si posteriormente se decide reprocesar dichos recursos. Sin embargo, si edita la anchura, la altura o ambas opciones en el área **[!UICONTROL Recorte de imagen adaptable]** del perfil de imagen, esos recursos se someterán a reprocesamiento.
>Consulte [Volver a procesar los recursos de Dynamic Media en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Puede volver a ejecutar el recorte inteligente para generar los recortes adicionales de nuevo, si es necesario.

**Para editar el recorte inteligente o la muestra inteligente de varias imágenes:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]**, luego a una carpeta que tenga aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.
1. En la carpeta, seleccione la **[!UICONTROL Más acciones]** (...) y seleccione **[!UICONTROL Recorte inteligente]**.

1. En el **[!UICONTROL Editar recortes inteligentes]** , realice una de las siguientes acciones:

   * Ajuste el tamaño de visualización de las imágenes en la página.

     A la derecha de la lista desplegable de nombre del punto de interrupción, arrastre la barra deslizante a la izquierda o a la derecha para cambiar el tamaño de la visualización de la imagen visible.

     ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre la lista de imágenes visibles en función de los nombres de los puntos de interrupción. En el ejemplo siguiente, las imágenes se filtran con el nombre de punto de interrupción &quot;Medium&quot;.

     Cerca de la esquina superior derecha de la página, en la lista desplegable, seleccione un nombre de punto de interrupción para filtrar por las imágenes que ve. (Consulte la imagen anterior).

     ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Cambie el tamaño del cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, en la imagen, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible del recorte.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, en la imagen, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible del recorte. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible de la muestra.

     ![Cambio del tamaño del recorte inteligente de una imagen](assets/edit_smart_crops-resize.png).

   * Mueva el cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, en la imagen, arrastre el cuadro de recorte a una nueva ubicación.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, en la imagen, arrastre el cuadro de recorte inteligente a una nueva ubicación. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el cuadro de recorte de muestra inteligente a una nueva ubicación.

     ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Deshacer todas las ediciones y restaurar el recorte inteligente o la muestra inteligente original (solo se aplica a la sesión de edición actual).

     Seleccionar **[!UICONTROL Revertir]** encima de la imagen.

     ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**, luego seleccione **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Eliminación de un perfil de imagen de las carpetas {#removing-an-image-profile-from-folders}

Cuando se quita un perfil de imagen de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanecerá intacto.

Puede quitar un perfil de imagen de una carpeta desde el **[!UICONTROL Herramientas]** o si se encuentra en la carpeta, en **[!UICONTROL Propiedades]**.

### Eliminación de perfiles de imagen de Dynamic Media de carpetas mediante la interfaz de usuario Perfiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea eliminar de una o varias carpetas.
1. Seleccionar **[!UICONTROL Quitar perfil de procesamiento de las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para quitar el perfil y seleccione **[!UICONTROL Eliminar]**.

   Puede confirmar que el perfil de imagen ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de imagen de Dynamic Media de carpetas mediante Propiedades {#removing-image-profiles-from-folders-via-properties}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]** y luego a la carpeta de la que desea quitar un perfil de imagen.
1. En la carpeta, seleccione la marca de verificación para seleccionarla y, a continuación, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione el **[!UICONTROL Perfiles de imagen]** pestaña.
1. Desde el **[!UICONTROL Nombre de perfil]** , seleccione la opción **[!UICONTROL Ninguno]**, luego seleccione **[!UICONTROL Guardar y cerrar]**.

   Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.
