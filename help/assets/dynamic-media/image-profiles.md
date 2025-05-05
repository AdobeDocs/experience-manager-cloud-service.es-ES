---
title: Perfiles de imagen de Dynamic Media
description: Obtenga información sobre cómo crear perfiles de imagen de Dynamic Media que contengan ajustes para máscara de enfoque, recorte inteligente o muestra inteligente, o ambos. A continuación, aplique el perfil a una carpeta de recursos de imagen.
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Renditions,Best Practices
role: User
exl-id: 0856f8a1-e0a9-4994-b338-14016d2d67bd
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3518'
ht-degree: 2%

---

# Perfiles de imagen de Dynamic Media {#image-profiles}

Al cargar imágenes, puede recortar automáticamente la imagen al cargar aplicando un perfil de imagen a la carpeta.

>[!IMPORTANT]
>
>Los perfiles de imagen no son aplicables a archivos PDF, GIF animado o INDD (Adobe InDesign).

## Máscara de enfoque, opción {#unsharp-mask}

Al crear un perfil de imagen, puede usar la opción **[!UICONTROL Máscara de enfoque]** para ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Puede controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora. Este efecto utiliza las mismas opciones que el filtro &quot;Máscara de enfoque&quot; de Adobe Photoshop.

>[!NOTE]
>
>La máscara de enfoque solo se aplica a representaciones de menor escala dentro del PTIFF (tiff piramidal) con una disminución de resolución superior al 50 %. La máscara de enfoque no afecta a las representaciones de mayor tamaño dentro del elemento ptiff. Mientras que las representaciones de menor tamaño, como las miniaturas, se modifican (y muestran la máscara de enfoque).

En **[!UICONTROL Máscara de enfoque]**, tiene las siguientes opciones de filtrado:

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
   <td><p>Determina el intervalo de contraste que debe omitirse cuando se aplica el filtro de máscara de enfoque. Esta opción controla la diferencia entre los píxeles enfocados y los alrededores para que se consideren píxeles de borde. Solo se enfocan los píxeles que alcanzan este umbral. Para evitar introducir ruido, experimente con valores entre 0 y 255.</p> </td>
  </tr>
 </tbody>
</table>

El enfoque se describe en [Imágenes de enfoque](/help/assets/dynamic-media/assets/sharpening_images.pdf).

## Opciones de recorte {#crop-options}

Al implementar el recorte inteligente en imágenes, Adobe recomienda la siguiente práctica recomendada y aplica el siguiente límite:

| Recurso: tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| **Imagen** - Cantidad de recortes inteligentes por imagen | 5 | 100 |

Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

<!-- CQDOC-16069 for the paragraph directly below -->

Las coordenadas de recorte inteligente dependen de la relación de aspecto. Para la configuración de recorte inteligente en un perfil de imagen, si la relación de aspecto es la misma para las dimensiones añadidas en el perfil de imagen, se envía la misma relación de aspecto a Dynamic Media. Adobe recomienda utilizar la misma área de recorte. Al hacerlo, se asegura de que no haya ningún impacto en las diferentes dimensiones utilizadas en el perfil de imagen.

Cada generación de recorte inteligente que cree requiere un procesamiento adicional. Por ejemplo, si se añaden más de cinco proporciones de aspecto de recorte inteligente, la tasa de ingesta de recursos puede ser lenta. También puede causar un aumento de la carga en los sistemas. Dado que el recorte inteligente se puede aplicar en el nivel de carpeta, Adobe recomienda utilizarlo solo para carpetas donde sea necesario.

**Directrices para definir el recorte inteligente en un perfil de imagen**
Para mantener el uso del recorte inteligente bajo control y optimizar el tiempo de procesamiento y el almacenamiento de los cultivos, Adobe recomienda las siguientes directrices y sugerencias:

* Los recursos de imagen a los que se va a aplicar un recorte inteligente deben tener un mínimo de 50 x 50 píxeles o más.
* Lo ideal es que tenga de 10 a 15 cultivos inteligentes por imagen para optimizar las relaciones de pantalla y el tiempo de procesamiento.
* Asigne un nombre a los cultivos inteligentes en función de las dimensiones de recorte, no del uso final. Al hacerlo, se ayuda a optimizar los duplicados en los que se utiliza una sola dimensión en varias páginas.
* Cree perfiles de imagen en cuanto a página/tipo de recurso para carpetas y subcarpetas específicas en lugar de un perfil de recorte inteligente común que se aplique a todas las carpetas o todos los recursos.
* Un perfil de imagen que aplique a las subcarpetas anulará un perfil de imagen que se aplique a la carpeta.
* No se permite un perfil de imagen que contenga dimensiones de recorte inteligente duplicadas.
* No se permiten perfiles de imagen con nombre duplicado que tengan definidas las opciones de recorte inteligente.

Tiene dos opciones de recorte de imagen entre las que elegir: recorte de píxeles y recorte inteligente. También puede optar por automatizar la creación de muestras de color e imagen o conservar el contenido de recorte en las resoluciones de destino.

>[!IMPORTANT]
>
>Adobe recomienda revisar los cultivos y las muestras generados para asegurarse de que sean adecuados y relevantes para su marca y valores.

| Opción | Cuándo se usa | Descripción |
| --- | --- | --- |
| **[!UICONTROL Recorte de píxeles]** | Recorte masivo de imágenes basado únicamente en dimensiones. | En la lista desplegable **[!UICONTROL Opciones de recorte]**, seleccione **[!UICONTROL Recorte de píxeles]**.<br>Para recortar desde los lados de una imagen, escriba el número de píxeles que desea recortar desde cualquier lado o cada lado de la imagen. La cantidad de imagen que se recorta depende de la configuración de ppp (píxeles por pulgada) en el archivo de imagen.<br>Un recorte de píxeles de perfil de imagen se procesa de la siguiente manera:<br>· Los valores son Superior, Inferior, Izquierda y Derecha.<br>· La parte superior izquierda se considera `0,0` y el recorte de píxeles se calcula a partir de ahí.<br>· Punto de inicio del recorte: izquierda es X y superior es Y<br>· Cálculo horizontal: tamaño de píxel horizontal de la imagen original menos izquierda y luego menos derecha.<br>· Cálculo vertical: altura de píxel vertical menos Superior y luego menos Inferior.<br>Por ejemplo, supongamos que tiene una imagen de 4000 x 3000 píxeles. Utilice valores: Superior=250, Inferior=500, Izquierda=300, Derecha=700.<br>Desde el recorte superior izquierdo (300.250) utilizando el espacio de relleno de (4000-300-700, 3000-250-500 o 3000.2250). |
| **[!UICONTROL Recorte inteligente]** | Recorte masivo de imágenes en función de su punto focal visual. | Smart Crop utiliza el poder de la inteligencia artificial en Adobe Sensei para automatizar el recorte de imágenes rápidamente de forma masiva. El recorte inteligente detecta y recorta automáticamente el punto focal de cualquier imagen para adquirir el punto de interés deseado, independientemente del tamaño de la pantalla.<br>En la lista desplegable **[!UICONTROL Opciones de recorte]**, seleccione **[!UICONTROL Recorte inteligente]** y, a continuación, a la derecha de **[!UICONTROL Recorte de imagen interactivo]**, habilite (active) la función.<br>Los tamaños predeterminados de los puntos de interrupción (**[!UICONTROL Grande]**, **[!UICONTROL Medium]**, **[!UICONTROL Pequeño]**) abarcan todos los tamaños que usan la mayoría de las imágenes en dispositivos móviles y tabletas, escritorios y banners. Si lo desea, puede editar los nombres predeterminados de Grande, Medium y Pequeño.<br>Para agregar más puntos de interrupción, seleccione **[!UICONTROL Agregar recorte]**; para eliminar un recorte, seleccione el icono Basura. |
| **[!UICONTROL Muestra de color e imagen]** | Genera una muestra de imagen para cada imagen. | **Nota**: la muestra inteligente no se admite en Dynamic Media Classic.<br>Busque y genere automáticamente muestras de alta calidad a partir de imágenes de productos que muestren color o textura.<br>En la lista desplegable **[!UICONTROL Opciones de recorte]**, seleccione **[!UICONTROL Recorte inteligente]**. A continuación, a la derecha de **[!UICONTROL Muestra de color e imagen]**, habilite (active) la característica. Escriba un valor en píxeles en los cuadros de texto **[!UICONTROL Width]** y **[!UICONTROL Height]**.<br>Aunque todos los recortes de imágenes están disponibles en el carril Representaciones, las muestras solo se utilizan mediante la función **[!UICONTROL Copiar URL]**. Utilice su propio componente de visualización para procesar la muestra en el sitio. La excepción a esta regla son los titulares de carrusel. Dynamic Media proporciona el componente de visualización para la muestra utilizada en los titulares del carrusel.<br><br>**Uso de muestras de imagen**<br> La dirección URL de las muestras de imagen es sencilla:<br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>Donde `:Swatch` se anexa a la solicitud de recurso.<br><br>**Con muestras de color**<br> Para usar muestras de color, realice una solicitud `req=userdata` con lo siguiente:<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>Por ejemplo, el siguiente es un recurso de muestra en Dynamic Media Classic:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>Y aquí está la URL `req=userdata` correspondiente del recurso de muestra:<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br>La respuesta de `req=userdata` es la siguiente:<br>`SmartCropDef=Swatch`<br>`SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br>También puede solicitar una respuesta de `req=userdata` en formato XML o JSON, como en los siguientes ejemplos de URL:<br>·`https://my.company.com</code>:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>·`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Nota**: Debe crear su propio componente WCM para solicitar un color muestra y analiza el atributo `SmartSwatchColor`, representado por un valor hexadecimal de RGB de 24 bits.<br>Consulte también [`userdata`](https://experienceleague.adobe.com/es/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata) en la Guía de referencia de visores. |
| **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** | Para mantener el contenido de recorte en la misma proporción de aspecto | Se utiliza al crear un perfil de recorte inteligente.<br>Para generar nuevo contenido de recorte (sin dejar de mantener el punto focal) para una proporción de aspecto determinada en diferentes resoluciones, anule la selección de esta opción <br>Si decide desactivar esta casilla, asegúrese de que la resolución de imagen original sea mayor que las resoluciones definidas para el perfil de recorte inteligente.<br><br>Por ejemplo, suponga que ha establecido las relaciones de aspecto en 600 x 600 (Grande), 400 x 400 (Medium) y 300 x 300 (Pequeño).<br>Cuando la opción **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** está *marcada*, verá el mismo recorte en las tres resoluciones, similar a la siguiente salida de muestra de imágenes (solo con fines ilustrativos):<br>![Opción activada](/help/assets/dynamic-media/assets/preserve-checked.png)<br><br>Cuando la opción **[!UICONTROL Conservar el contenido de recorte en las resoluciones de destino]** está *desmarcada*, el contenido de recorte es nuevo para las tres resoluciones, similar a la siguiente salida de muestra de imágenes (solo con fines ilustrativos):<br>![Opción desmarcada](/help/assets/dynamic-media/assets/preserve-unchecked.png) |

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

Consulte [Acerca de los perfiles de vídeo e imagen de Dynamic Media](/help/assets/dynamic-media/about-image-video-profiles.md).

Consulte también [Prácticas recomendadas para organizar su Assets digital con el fin de usar perfiles de procesamiento](/help/assets/organize-assets.md).

**Para crear perfiles de imagen de Dynamic Media:**

1. Seleccione el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Para agregar un perfil de imagen, seleccione **[!UICONTROL Crear]**.
1. Introduzca un nombre de perfil y valores para máscara de enfoque, recorte o muestra, o ambos.

   >[!TIP]
   >
   >Utilice un nombre de perfil específico para el propósito deseado. Por ejemplo, supongamos que desea crear un perfil que genere solo muestras. Es decir, el recorte inteligente está desactivado (desactivado) y la muestra de color e imagen activada (activada). En estos casos, puede utilizar el nombre de perfil &quot;Muestra inteligente&quot;.

   Consulte también [Opciones de recorte y muestra inteligente](#crop-options) y [Máscara de enfoque](#unsharp-mask).

   ![recorte](assets/crop.png)

1. Seleccione **[!UICONTROL Guardar]**. El perfil creado aparece en la lista de perfiles disponibles.

## Editar o eliminar perfiles de imagen de Dynamic Media {#editing-or-deleting-image-profiles}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea editar o eliminar. Para editarlo, seleccione **[!UICONTROL Editar perfil de procesamiento de imagen]**. Para quitarlo, seleccione **[!UICONTROL Eliminar perfil de procesamiento de imagen]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Si está editando, guarde los cambios. Si está eliminando, confirme que desea eliminar el perfil.

## Aplicar un perfil de imagen de Dynamic Media a las carpetas {#applying-an-image-profile-to-folders}

Cuando se asigna un perfil de imagen a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. Como tal, solo puede asignar un perfil de imagen a una carpeta. Tenga en cuenta la estructura de carpetas de donde carga, almacena, utiliza y archiva los recursos.

Si ha asignado un perfil de imagen diferente a una carpeta, el nuevo perfil anulará el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta más adelante.

Las carpetas con un perfil asignado muestran el nombre del perfil en la tarjeta.

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Puede aplicar perfiles de imagen a carpetas específicas o globalmente a todos los recursos.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de imagen existente cambiado a posteriori. Vea [Volver a procesar recursos en una carpeta después de haber editado su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

### Aplicar perfiles de imagen de Dynamic Media a carpetas específicas {#applying-image-profiles-to-specific-folders}

Puede aplicar un perfil de imagen a una carpeta desde el menú **[!UICONTROL Herramientas]** o, si está en la carpeta, desde **[!UICONTROL Propiedades]**.

Las carpetas con un perfil asignado muestran el nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente cambiado a posteriori. Vea [Volver a procesar recursos en una carpeta después de haber editado su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

#### Aplicación de perfiles de imagen de Dynamic Media a carpetas desde la interfaz de usuario Perfiles {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea aplicar a una o varias carpetas.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Seleccione **[!UICONTROL Aplicar perfil de procesamiento a las carpetas]** y seleccione la carpeta o carpetas que desee usar para recibir los recursos cargados recientemente. A continuación, seleccione **[!UICONTROL Aplicar]**. Las carpetas con un perfil asignado muestran el nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicar perfiles de imagen de Dynamic Media a carpetas desde Propiedades {#applying-image-profiles-to-folders-from-properties}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Assets]**.
1. Vaya a una *carpeta* (no a un recurso) a la que desee aplicar un perfil de imagen.
1. Según la vista en la que se encuentre, siga uno de estos procedimientos:
   * En la vista de tarjeta, pase el puntero sobre la carpeta y, a continuación, seleccione la marca de verificación para seleccionarla.
   * En Vista de columna o Vista de lista, active la casilla a la izquierda del nombre de la carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione la ficha **[!UICONTROL Procesamiento de Dynamic Media]**.
1. En **[!UICONTROL Perfil de imagen]**, en la lista desplegable **[!UICONTROL Nombre de perfil]**, seleccione el perfil que desee aplicar.
1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**. Las carpetas con un perfil asignado muestran el nombre del perfil directamente debajo del nombre de la carpeta.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Aplicar un perfil de imagen de Dynamic Media globalmente {#applying-an-image-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicar uno globalmente. Cualquier contenido cargado en Experience Manager Assets en cualquier carpeta tiene el perfil seleccionado aplicado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente cambiado a posteriori. Vea [Volver a procesar recursos en una carpeta después de haber editado su perfil de procesamiento](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

**Para aplicar un perfil de imagen de Dynamic Media globalmente:**

1. Realice una de las siguientes acciones:

   * Vaya a `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`, aplique el perfil adecuado y seleccione **[!UICONTROL Guardar]**.

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * Vaya a CRXDE Lite hasta el siguiente nodo: `/content/dam/jcr:content`.

     Agregue la propiedad `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` y seleccione **[!UICONTROL Guardar todo]**.

     ![configurar_perfiles_de_imagen](assets/configure_image_profiles.png)

## Editar el recorte inteligente o la muestra inteligente de una sola imagen {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>Adobe recomienda revisar los cultivos inteligentes y las muestras inteligentes que se generen para asegurarse de que sean adecuados y relevantes para su marca y valores.

Para restringir el punto focal de una imagen, puede ajustar manualmente la alineación o cambiar el tamaño de la ventana de recorte inteligente.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

>[!IMPORTANT]
>
>Al ajustar manualmente la ventana de recorte inteligente de un recurso, se guardan los cambios. Estas ediciones permanecen intactas incluso si vuelve a procesar el recurso más adelante. Sin embargo, si edita la anchura, la altura o ambas opciones en el área **[!UICONTROL Recorte de imagen adaptable]** del perfil de imagen, ese recurso estará sujeto a reprocesamiento.
>Consulte [Volver a procesar recursos de Dynamic Media en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Vuelva a ejecutar el recorte inteligente para generar los recortes adicionales de nuevo, si es necesario.

Ver también [Editar el recorte inteligente o la muestra inteligente de varias imágenes](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Para editar el recorte inteligente o la muestra inteligente de una sola imagen:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Assets]** y, a continuación, a la carpeta que tenga aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.
1. Para abrir su contenido, seleccione la carpeta.
1. Seleccione la imagen cuyo recorte inteligente o muestra inteligente desee ajustar.
1. En la barra de herramientas, seleccione **[!UICONTROL Recorte inteligente]**.

   >[!TIP]
   >
   >Utilice la tecla de acceso directo `s` para editar los recortes inteligentes o las muestras inteligentes.

1. Realice una de las siguientes acciones:

   * Cerca de la esquina superior derecha de la página, arrastre la barra deslizante hacia la izquierda o hacia la derecha para aumentar o disminuir la visualización de la imagen, respectivamente.
   * En la imagen, arrastre un controlador de esquina para ajustar el tamaño del área visible del recorte o muestra.
   * En la imagen, arrastre el cuadro o la muestra a una nueva ubicación. Solo puede editar muestras de imagen; las muestras de color son estáticas.
   * Cerca de la esquina superior derecha de la imagen, seleccione **[!UICONTROL Revertir]** para deshacer todas las ediciones y restaurar el recorte o muestra original.
   * Utilice las teclas de flecha del teclado para recortar el tamaño del fotograma, cambiar la posición de la imagen o ambas cosas.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Editar el recorte inteligente o la muestra inteligente de varias imágenes {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>Adobe recomienda revisar los cultivos inteligentes y las muestras inteligentes que se generen para asegurarse de que sean adecuados y relevantes para su marca y valores.

Después de aplicar un perfil de imagen (que contiene un recorte inteligente) a una carpeta, se les aplica un recorte a todas las imágenes de dicha carpeta. Si es necesario, puede ajustar manualmente la alineación o cambiar el tamaño de la ventana de recorte inteligente en varias imágenes para ajustar aún más sus puntos focales.

Después de editar un recorte inteligente y guardarlo, el cambio se propaga dondequiera que utilice el recorte para las imágenes específicas.

>[!IMPORTANT]
>
>Al ajustar manualmente la ventana de recorte inteligente de varios recursos, se guardan los cambios. Estas ediciones permanecen intactas incluso si vuelve a procesar los recursos más adelante. Sin embargo, si edita la anchura, la altura o ambas opciones en el área **[!UICONTROL Recorte de imagen adaptable]** del perfil de imagen, esos recursos se someterán a reprocesamiento.
>Consulte [Volver a procesar recursos de Dynamic Media en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

Vuelva a ejecutar el recorte inteligente para generar los recortes adicionales de nuevo, si es necesario.

**Para editar el recorte inteligente o la muestra inteligente de varias imágenes:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Assets]** y, a continuación, a una carpeta que tenga aplicado un recorte inteligente o un perfil de imagen de muestra inteligente.
1. En la carpeta, seleccione el icono **[!UICONTROL Más acciones]** (...) y luego seleccione **[!UICONTROL Recorte inteligente]**.

1. En la página **[!UICONTROL Editar recortes inteligentes]**, realice una de las siguientes acciones:

   * Ajuste el tamaño de visualización de las imágenes en la página.

     A la derecha de la lista desplegable de nombre del punto de interrupción, arrastre la barra deslizante a la izquierda o a la derecha para cambiar el tamaño de la visualización de la imagen visible.

     ![edit_smart_crop-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Filtre la lista de imágenes visibles en función de los nombres de los puntos de interrupción. En el ejemplo siguiente, las imágenes se filtran con el nombre de punto de interrupción &quot;Medium&quot;.

     Cerca de la esquina superior derecha de la página, en la lista desplegable, seleccione un nombre de punto de interrupción para filtrar por las imágenes que ve. (Consulte la imagen anterior).

     ![edit_smart_crop-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Cambie el tamaño del cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, en la imagen, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible del recorte.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, en la imagen, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible del recorte. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el controlador de esquina del cuadro de recorte. Ajuste el tamaño del área visible de la muestra.

     ![Cambiando el tamaño del recorte inteligente de una imagen](assets/edit_smart_crops-resize.png).

   * Mueva el cuadro de recorte inteligente. Realice una de las siguientes acciones:

      * Si la imagen solo tiene un recorte inteligente o una muestra inteligente, en la imagen, arrastre el cuadro de recorte a una nueva ubicación.
      * Si la imagen tiene un recorte inteligente y una muestra inteligente, en la imagen, arrastre el cuadro de recorte inteligente a una nueva ubicación. O bien, seleccione la muestra inteligente debajo de la imagen (las muestras de color son estáticas) y, a continuación, arrastre el cuadro de recorte de muestra inteligente a una nueva ubicación.

     ![edit_smart_crop-move](assets/edit_smart_crops-move.png)

   * Deshacer todas las ediciones y restaurar el recorte inteligente o la muestra inteligente original (solo se aplica a la sesión de edición actual).

     Seleccione **[!UICONTROL Revertir]** sobre la imagen.

     ![edit_smart_crop-revert](assets/edit_smart_crops-revert.png)

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]** y, a continuación, **[!UICONTROL Cerrar]** para volver a la carpeta de recursos.

## Eliminación de un perfil de imagen de las carpetas {#removing-an-image-profile-from-folders}

Cuando se quita un perfil de imagen de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanecerá intacto.

Puede quitar un perfil de imagen de una carpeta desde el menú **[!UICONTROL Herramientas]** o, si se encuentra en la carpeta, desde **[!UICONTROL Propiedades]**.

### Eliminación de perfiles de imagen de Dynamic Media de carpetas mediante la interfaz de usuario Perfiles {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de imagen]**.
1. Seleccione el perfil de imagen que desea eliminar de una o varias carpetas.
1. Seleccione **[!UICONTROL Quitar perfil de procesamiento de las carpetas]**, seleccione la carpeta o carpetas que desee usar para quitar el perfil y seleccione **[!UICONTROL Quitar]**.

   Puede confirmar que el perfil de imagen ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de imagen de Dynamic Media de carpetas mediante Propiedades {#removing-image-profiles-from-folders-via-properties}

1. Seleccione el logotipo de Experience Manager, vaya a **[!UICONTROL Assets]** y luego a la carpeta de la que desee quitar un perfil de imagen.
1. En la carpeta, active la marca de verificación para seleccionarla y, a continuación, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione la ficha **[!UICONTROL Perfiles de imagen]**.
1. En la lista desplegable **[!UICONTROL Nombre de perfil]**, selecciona **[!UICONTROL Ninguno]**, luego selecciona **[!UICONTROL Guardar y cerrar]**.

   Las carpetas con un perfil asignado muestran el nombre del perfil directamente debajo del nombre de la carpeta.
