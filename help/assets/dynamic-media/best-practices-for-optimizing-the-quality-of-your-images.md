---
title: Práctica recomendada para optimizar la calidad de las imágenes
description: Conozca las prácticas recomendadas que le ayudan a optimizar la calidad de los recursos de imagen mediante Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management, Best Practices
role: User
exl-id: 2efc4a27-01d7-427f-9701-393497314402
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 1%

---

# Práctica recomendada para optimizar la calidad de las imágenes {#best-practices-for-optimizing-the-quality-of-your-images}

{{work-with-dynamic-media}}

La optimización de la calidad de la imagen puede ser un proceso laborioso, ya que muchos factores contribuyen a obtener resultados aceptables. El resultado es en parte subjetivo porque los individuos perciben la calidad de la imagen de manera diferente. La experimentación estructurada es clave.

Adobe Experience Manager incluye más de 100 comandos de entrega de imágenes de Dynamic Media para ajustar y optimizar imágenes y procesar resultados. Las siguientes directrices pueden ayudarle a optimizar el proceso y obtener buenos resultados rápidamente mediante algunos comandos esenciales y prácticas recomendadas.

<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Habilitar imágenes inteligentes en Dynamic Media {#bp-enable-smart-imaging}

**Imágenes inteligentes:**

* Al habilitar Imágenes inteligentes en Dynamic Media, se optimiza automáticamente el formato, el tamaño y la calidad de la imagen en función de las funciones del explorador del cliente.
¿Desea obtener más información? Vaya a [Imágenes inteligentes](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/imaging-faq).
* Mejora el rendimiento de la entrega de imágenes ajustando dinámicamente estos parámetros.
* Puede evaluar imágenes inteligentes con la herramienta de autoevaluación [Snapshot](https://snapshot.scene7.com/).

**Formatos de imagen:**

* Evite utilizar comandos explícitos `fmt=webp` o `fmt=avif` en una dirección URL a menos que sea específicamente necesario para un caso de uso.
* Smart Imaging selecciona automáticamente el mejor formato, lo que resulta en una ganancia de ancho de banda óptima.

**Comportamiento predeterminado:**

* Cuando no se especifica ningún comando de formato en la dirección URL y Smart Imaging no está habilitado, la entrega de imágenes de Dynamic Media utiliza de forma predeterminada el formato JPEG.

Al tomar decisiones informadas sobre los formatos de imagen y habilitar Imágenes inteligentes, puede afectar significativamente al rendimiento y la experiencia del usuario.


<!-- ADDED THE FOLLOWING TOPIC AS PER CQDOC-21594 -->

## Prácticas recomendadas para seleccionar la imagen de origen {#bp-select-source-image}

Consideraciones esenciales para trabajar con imágenes de origen:

* **Formato de imagen Source:**
   * El uso de formatos sin pérdidas como PNG, TIFF o PSD garantiza que la calidad de la imagen permanezca alta sin ningún artefacto de compresión.
   * Estos formatos conservan todos los datos originales, lo que los hace ideales para la edición y posterior procesamiento.
* **Tamaño de imagen de Source:**
   * Comenzar con una imagen de alta resolución proporciona más detalle y flexibilidad.
   * Cuando es necesario mostrar las imágenes en diferentes tamaños (por ejemplo, en distintos dispositivos o resoluciones de pantalla), tener una imagen de origen más grande permite un mejor escalado.
   * Para las imágenes que admiten zoom (como las fotos de productos), apunte a dimensiones de alrededor de 2000 píxeles o más en el lado más largo.
   * Los logotipos o banners que no requieran zoom se pueden cargar en el tamaño más grande necesario para el uso previsto.

Al realizar estas cuidadosas elecciones en el nivel de fuente, puede contribuir significativamente a la calidad general del contenido visual.

<!-- REMOVED TOPIC AS PER CQDOC-21594
## Best practices for image format (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG or PNG are the best choices to deliver images in good quality and with manageable size and weight.
* If no format command is supplied in the URL, Dynamic Media Image Delivery defaults to JPG for delivery.
* JPG compresses at a ratio of 10:1 and usually produces smaller image file sizes. PNG compresses at a ratio of about 2:1, except when images contain a white background. Typically though, PNG file sizes are larger than JPG files.
* JPG uses lossy compression, meaning that picture elements (pixels) are dropped during compression. PNG on the other hand uses lossless compression.
* JPG often compresses photographic images with better fidelity than synthetic images with sharp edges and contrast.
* If your images contain transparency, use PNG because JPG does not support transparency.

As a best practice for image format, start with the most common setting `&fmt=JPG`. -->

## Prácticas recomendadas para el tamaño de imagen {#best-practices-for-image-size}

La reducción dinámica del tamaño de la imagen es una de las tareas más comunes. Implica especificar el tamaño y, opcionalmente, qué modo de disminución de resolución se utiliza para reducir la escala de la imagen.

* Para cambiar el tamaño de la imagen, el método más sencillo es usar `&wid=<value>` y `&hei=<value>,`o solo `&hei=<value>`. Estos parámetros establecen automáticamente el ancho de la imagen de acuerdo con la relación de aspecto.
* `&resMode=<value>`controla el algoritmo utilizado para reducir la resolución. Comience por `&resMode=sharp2`. Este valor proporciona la mejor calidad de imagen. Aunque el uso de la disminución de resolución de `value =bilin` es más rápido, a menudo provoca el solapamiento de artefactos.

Como práctica recomendada para el tamaño de imagen, use `&wid=<value>&hei=<value>&resMode=sharp2` o `&hei=<value>&resMode=sharp2`

## Prácticas recomendadas para el enfoque de imágenes {#best-practices-for-image-sharpening}

El enfoque de imágenes es el aspecto más complejo del control de imágenes en su sitio web y donde se cometen muchos errores. Tómese el tiempo necesario para obtener más información sobre el funcionamiento del enfoque y el enmascaramiento de enfoque en Experience Manager consultando los siguientes recursos útiles:

* El documento técnico sobre prácticas recomendadas [Prácticas recomendadas para la calidad y el enfoque de imágenes de Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) también se aplica a Experience Manager.

* Vea [Usar enfoque de imagen con Experience Manager - Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

Con Experience Manager, puede enfocar las imágenes durante la ingesta, la entrega o ambas cosas. Sin embargo, normalmente es mejor enfocar las imágenes con un solo método o con el otro, pero no con ambos. Enfoque de las imágenes en el momento de la entrega, en una dirección URL, normalmente le ofrece los mejores resultados.

Existen dos métodos de enfoque de imagen que puede utilizar:

* Enfoque simple (`&op_sharpen`): al igual que el filtro de enfoque utilizado en Photoshop, el enfoque simple aplica un enfoque básico a la vista final de la imagen tras el cambio de tamaño dinámico. Sin embargo, este método no se puede configurar por el usuario. Se recomienda evitar el uso de `&op_sharpen` a menos que sea necesario.
* Máscara de enfoque (`&op_USM`): la máscara de enfoque es un filtro de enfoque estándar del sector. La práctica recomendada es enfocar las imágenes con máscara de enfoque siguiendo las directrices que se indican a continuación. El enmascaramiento de enfoque permite controlar los tres parámetros siguientes:

   * `&op_sharpen=`cantidad,radio,umbral

      * **[!UICONTROL cantidad]** (0-5, intensidad del efecto).
      * **[!UICONTROL radio]** (0-250, ancho de las &quot;líneas de enfoque&quot; dibujadas alrededor del objeto enfocado, medido en píxeles.)

     Tenga en cuenta que los parámetros radio y cantidad funcionan entre sí. La reducción del radio puede compensarse aumentando la cantidad. El radio permite un control más preciso, ya que un valor más bajo enfoca únicamente los píxeles del borde, mientras que un valor más alto enfoca una banda más ancha de píxeles.

      * **[!UICONTROL umbral]** (0-255, sensibilidad del efecto.)

     Este parámetro determina la diferencia entre los píxeles enfocados y el área circundante antes de que se consideren píxeles de borde y el filtro los enfoque. El parámetro **[!UICONTROL threshold]** ayuda a evitar áreas de enfoque excesivo con colores similares, como los tonos de piel. Por ejemplo, un valor de umbral de 12 ignora las ligeras variaciones en el brillo del tono de la piel para evitar añadir &quot;ruido&quot;, mientras que al mismo tiempo agrega contraste al borde de las áreas de alto contraste, como cuando las pestañas tocan la piel.

     Para obtener más información sobre cómo configurar estos tres parámetros, incluidas las prácticas recomendadas para su uso con el filtro, consulte los siguientes recursos:

      * El documento técnico sobre prácticas recomendadas [Prácticas recomendadas para la calidad y el enfoque de imágenes de Adobe Dynamic Media Classic](/help/assets/dynamic-media/assets/sharpening_images.pdf) también se aplica a Experience Manager.

      * Vea [Usar enfoque de imagen con Experience Manager - Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-image-sharpening-feature-video-use#dynamic-media).

      * Experience Manager también permite controlar un cuarto parámetro: monocromo (0,1). Este parámetro determina si se aplica máscara de enfoque a cada componente de color por separado utilizando el valor 0 o al brillo/intensidad de la imagen utilizando el valor 1.

Se recomienda comenzar con el parámetro radio de la máscara de enfoque. Los ajustes de radio con los que puede empezar son los siguientes:

* **[!UICONTROL Sitio web]**: 0,2-0,3 píxeles
* **[!UICONTROL Impresión fotográfica (250-300 ppp)]**: 0,3-0,5 píxeles
* **[!UICONTROL Impresión en offset (266-300 ppi)]**: 0,7-1,0 píxeles
* **[!UICONTROL Impresión en lienzo (150 ppp)]**: 1,5-2,0 píxeles

Aumente gradualmente la cantidad de 1,75 a 4. Si el enfoque sigue sin ser el deseado, aumente el radio en un punto decimal y vuelva a ejecutar la cantidad de 1,75 a 4. Repita el proceso según sea necesario.

Deje el parámetro monocromo en 0.

### Prácticas recomendadas para la compresión JPEF (`&qlt=`) {#best-practices-for-jpef-compression-qlt}

* Este parámetro controla la calidad de codificación de JPG. Un valor más alto significa una imagen de mayor calidad pero un tamaño de archivo grande; alternativamente, un valor más bajo significa una imagen de menor calidad pero un tamaño de archivo más pequeño. El rango de este parámetro es de 0 a 100.
* Para optimizar la calidad, no establezca el valor del parámetro en 100. La diferencia entre un ajuste de 90 o 95 y 100 es casi imperceptible. Y sin embargo 100 aumenta innecesariamente el tamaño del archivo de imagen. Por lo tanto, para optimizar la calidad pero evitar que los archivos de imagen sean demasiado grandes, establezca `qlt= value` en 90 o 95.
* Para optimizar para un archivo de imagen pequeño pero mantener la calidad de la imagen en un nivel aceptable, establezca `qlt= value` en 80. Los valores por debajo de 70 a 75 dan como resultado una degradación significativa de la calidad de imagen.
* Como práctica recomendada, para permanecer en el medio, establezca `qlt= value` en 85 para permanecer en el medio.
* Uso del indicador de croma en `qlt=`

   * El parámetro `qlt=` tiene una segunda configuración que le permite activar la disminución de resolución de cromaticidad de RGB con el valor `,1` o desactivar con el valor `,0`.
   * Para que sea sencillo, comience con la disminución de resolución de cromaticidad de RGB desactivada (`,0`). Esta configuración suele mejorar la calidad de imagen, especialmente en imágenes sintéticas con muchos bordes nítidos y contraste.

Como práctica recomendada para la compresión de JPG, use `&qlt=85,0`.

## Prácticas recomendadas para el tamaño de JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

El parámetro `jpegSize` es útil si desea garantizar que una imagen no supere un tamaño determinado para su entrega a dispositivos con memoria limitada.

* Este parámetro se establece en kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Define el tamaño máximo permitido para la entrega de imágenes.
* `&jpegSize=` interactúa con el parámetro de compresión de JPG `&qlt=`. Si la respuesta de JPG con el parámetro de compresión de JPG especificado (`&qlt=`) no supera el valor jpegSize, la imagen se devuelve con `&qlt=` tal como se definió. De lo contrario, `&qlt=` se reducirá gradualmente hasta que la imagen se ajuste al tamaño máximo permitido. O bien, hasta que el sistema determine que no cabe y devuelva un error.

Se recomienda configurar `&jpegSize=` y agregar el parámetro `&qlt=` si va a enviar imágenes de JPG a dispositivos con memoria limitada.

## Resumen de prácticas recomendadas {#best-practices-summary}

Como práctica recomendada, para lograr una alta calidad de imagen y un tamaño de archivo pequeño, comience con la siguiente combinación de parámetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Esta combinación de ajustes produce resultados excelentes en la mayoría de las circunstancias.

Si la imagen requiere una mayor optimización, ajuste gradualmente los parámetros de enfoque (máscara de enfoque) empezando por un radio establecido en 0,2 o 0,3. A continuación, aumente gradualmente la cantidad de 1,75 a un máximo de 4 (equivalente a 400 % en Photoshop). Compruebe que se obtiene el resultado deseado.

Si los resultados de enfoque siguen sin ser satisfactorios, aumente el radio en incrementos decimales. Para cada incremento decimal, reinicie la cantidad a 1,75 y aumente gradualmente a 4. Repita este proceso hasta que obtenga el resultado deseado. Aunque los valores anteriores son un enfoque que los estudios creativos han validado, recuerde que puede empezar con otros valores y seguir otras estrategias. Si los resultados son satisfactorios o no es una cuestión subjetiva, por lo tanto la experimentación estructurada es clave.

A medida que experimenta, las siguientes sugerencias generales son útiles para optimizar el flujo de trabajo:

* Pruebe diferentes parámetros en tiempo real directamente en una dirección URL.
* Como práctica recomendada, recuerde que puede agrupar comandos de servicio de imágenes de Dynamic Media en un ajuste preestablecido de imagen. Un ajuste preestablecido de imagen son básicamente macros de comandos de URL con nombres de ajustes preestablecidos personalizados como `$thumb_low$` y `&product_high$`. El nombre del ajuste preestablecido personalizado en una ruta URL llama a estos ajustes preestablecidos. Esta funcionalidad le ayuda a administrar comandos y configuraciones de calidad para diferentes patrones de uso de imágenes en el sitio web y acorta la longitud general de las direcciones URL.
* Experience Manager también proporciona formas más avanzadas de ajustar la calidad de la imagen, como aplicar imágenes de enfoque al ingerir. Para ajustar y optimizar los resultados de procesamiento, [los servicios de consultoría de Adobe](https://business.adobe.com/customers/consulting-services/main.html) pueden ayudarle con información y prácticas recomendadas personalizadas.
