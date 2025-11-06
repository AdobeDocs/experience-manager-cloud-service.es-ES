---
title: Optimización de imágenes con Dynamic Media con las funciones de OpenAPI
description: Aprenda a optimizar imágenes sobre la marcha antes de la entrega pública mediante las funciones de optimización de imágenes de Dynamic Media con las funciones de OpenAPI
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
exl-id: 7822732b-e2b9-4b35-b92b-cb7b31d84489
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---

# Optimización de imágenes con Dynamic Media con las funciones de OpenAPI{#Optimize-images-using-Dynamic-Media-with-OpenAPI-Capabilities}

[!DNL Dynamic Media with OpenAPI capabilities] ofrece capacidades de optimización de imágenes como [!DNL Smart Crop], [!DNL Image Presets] y [!DNL Smart Imaging]. Estas funciones ayudan a ofrecer imágenes de alta calidad y adaptables que se cargan rápidamente en diferentes dispositivos y redes.

## Recorte inteligente{#smart-crop-using-dynamic-media-with-openapi-capabilities}

[Recorte inteligente](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) es una capacidad de tamaño dinámico de [!DNL Dynamic Media with OpenAPI capabilities]. [!DNL Smart Crop] es una técnica de procesamiento de imágenes avanzada que utiliza el recorte según contenido con tecnología de IA para recortar imágenes de forma inteligente para varios tamaños de pantalla y, al mismo tiempo, preservar el contexto visual en las versiones recortadas. La IA analiza la imagen para identificar el punto focal o el punto de interés deseado y, a continuación, recorta automáticamente la imagen para conservar el punto focal en todas las versiones recortadas. [!DNL Smart Crop], un elemento clave del diseño interactivo, ofrece una forma rentable y eficiente en cuanto a tiempo de recortar imágenes.

Consulte el artículo [Perfiles de imagen de Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles) para obtener información sobre cómo [crear representaciones de recorte inteligente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#creating-image-profiles) en [!DNL Admin View], [aplicarlas a carpetas](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#applying-an-image-profile-to-folders) o [editar representaciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles#editing-the-smart-crop-or-smart-swatch-of-a-single-image) ya aplicadas a una imagen o carpeta. Aprenda a crear un [!DNL Smart Crop] paso a paso en este [vídeo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

El parámetro [!DNL Smart Crop] espera que named-smartcrop-profiles existan y se hayan aplicado al recurso. Consulte [Perfiles de recorte inteligente](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=smartcrop&t=request) para obtener más información sobre el parámetro [!DNL Smart Crop] y cómo se aplican los perfiles con nombre [!DNL Smart Crop].

>[!IMPORTANT]
>
> Solo puede crear [!DNL Smart Crop] representaciones en la vista de administración.

## Ajustes preestablecidos de imagen{#image-presets-using-dynamic-media-with-openapi-capabilities}

Transforme imágenes sobre la marcha utilizando la capacidad [Ajustes preestablecidos de imagen](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=preset&t=request) en [!DNL Dynamic Media with OpenAPI capabilities]. Un [!DNL image preset] es un conjunto predefinido de reglas de tamaño y formato para una imagen de salida.

[!DNL Dynamic Media with OpenAPI capabilities] utiliza nombres de ajuste preestablecido para transformar una imagen sobre la marcha y generar su representación de forma instantánea. Cuando solicita una imagen a través de una dirección URL de entrega [!DNL Dynamic Media with OpenAPI] que incluye un parámetro preestablecido, [!DNL DM with OpenAPI] aplica las transformaciones del ajuste preestablecido, crea la representación bajo demanda y la envía al usuario.

Puede aplicar un solo ajuste preestablecido a varias imágenes a través de sus [!DNL Dynamic Media with OpenAPI] direcciones URL de entrega. Esto garantiza un formato coherente en todos los recursos sin editar manualmente cada uno.

Consulte el artículo [administración de ajustes preestablecidos de imagen](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets) para obtener información sobre [cómo crear ajustes preestablecidos de imagen en la vista de administrador](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-image-presets) y [cómo crear ajustes preestablecidos de imagen adaptables](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/managing-image-presets#creating-a-responsive-image-preset) que adaptan automáticamente los recursos para adaptarlos a diferentes tamaños de pantalla.

### Ventajas de utilizar ajustes preestablecidos de imagen{#benefits-of-image-presets}

[!DNL Image Presets] proporciona varias ventajas para administrar y entregar imágenes en [!DNL Dynamic Media with OpenAPI]. Algunas de las ventajas clave son las siguientes:

* Los ajustes preestablecidos acortan las direcciones URL de entrega de imágenes. En lugar de añadir varios modificadores de imagen para alargar la dirección URL de envío, utilice un solo ajuste preestablecido. Las URL más cortas son más fáciles de administrar y garantizan una entrega de imágenes coherente en sitios web, aplicaciones móviles, correos electrónicos y otros canales.
* Los ajustes preestablecidos de imagen crean representaciones Just-In-Time a partir de un archivo de imagen de origen. Esta capacidad de generación de representaciones bajo demanda elimina la necesidad de crear y almacenar varias representaciones estáticas del mismo archivo, lo que ahorra tiempo y almacenamiento.
* Aplique un único ajuste preestablecido a un gran conjunto de recursos a la vez, evitando ediciones manuales en cada recurso individualmente, asegurando un formato coherente y habilitando la escalabilidad.
* Al actualizar los parámetros de un ajuste preestablecido, se cambia automáticamente el formato de todas las imágenes que lo utilizan. Esto optimiza la edición al centralizar las actualizaciones de formato, lo que elimina la necesidad de volver a editar recursos individuales o código web.
* Mejora la eficacia y el rendimiento con representaciones dinámicas almacenadas en caché por la CDN, lo que da como resultado una carga más rápida y un rendimiento optimizado en todos los dispositivos y redes.

### Usar ajustes preestablecidos de imagen{#use-image-presets-using-dynamic-media-with-openapi-capabilities}

Después de crear [!DNL Image Presets], puede usarlos para los siguientes flujos de trabajo:

* [Utilice ajustes preestablecidos en la dirección URL de entrega de imágenes para crear sus representaciones sobre la marcha antes de enviarlas al usuario final](#use-presets-in-delivery-urls)
* [Uso de ajustes preestablecidos durante la creación en AEM Sites](#use-presets-during-authoring-in-aem-sites)

#### Usar ajustes preestablecidos en la URL de entrega de imágenes{#use-presets-in-delivery-urls}

Los ajustes preestablecidos hacen que las direcciones URL de envío sean más cortas y fáciles de usar.  Cada nombre de ajuste preestablecido sirve como identificador único en la dirección URL de envío. En lugar de añadir varios modificadores a la URL de entrega de un recurso, haga referencia al nombre del ajuste preestablecido para generar su representación instantáneamente. [Aprenda a aplicar ajustes preestablecidos de imagen de Dynamic Media a su imagen](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-presets).
En el siguiente ejemplo se compara una dirección URL con un ajuste preestablecido y una dirección URL sin un ajuste preestablecido.

**URL sin ajuste preestablecido (URL larga)**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?width=400&height=300&fit=crop&qualit=85&sharpen=true
```

**URL con un ajuste preestablecido (URL corta)**:

```
https://delivery-p30902-e145436-cmstg.adobeaemcloud.com/adobe/assets/urn:aaid:aem:393d5579-5be2-49a5-ac5f-8fed72bfb614/as/AdobeStock_63266433.avif?preset=thumbnail
```

La miniatura preestablecida agrupa la misma configuración de modificador de imagen.

#### Uso de ajustes preestablecidos durante la creación en AEM Sites{#use-presets-during-authoring-in-aem-sites}

Los autores pueden seleccionar [!DNL Image Presets] durante la edición de la página en la página de creación de [!DNL AEM Sites] cuando se habilita la compatibilidad con [!DNL Dynamic Media].
Siga estos pasos para utilizar los ajustes preestablecidos de imagen en la página de creación:

1. Vaya a la página de creación de Sites.
1. Ejecute los pasos de [Acceder a recursos remotos en la sección Editor de páginas de AEM](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor) para usar el panel [!DNL Asset Selector] y seleccionar un recurso.
1. En el panel [!DNL asset selector], desplácese hacia abajo hasta **[!UICONTROL Tipo de ajuste preestablecido]**, especifique `Preset=Preset Name` en el campo **[!UICONTROL Modificadores de imagen]** y haga clic en **[!UICONTROL Listo]**.
   ![ajuste preestablecido](/help/assets/assets/preset-in-asset-selector-panel.png)

## Imágenes inteligentes{#use-smart-imaging-using-dynamic-media-with-openapi-capabilities}

Cuando usa [!DNL Dynamic Media with OpenAPI capabilities] para la entrega de imágenes, las imágenes se optimizan automáticamente mediante [Imágenes inteligentes](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/). La entrega optimizada garantiza que las imágenes se carguen más rápido, tengan la máxima calidad visual y un tamaño de archivo mínimo. Esto resulta en la carga de página más rápida y una calidad visual alta y constante entre dispositivos y redes, a la vez que consume un ancho de banda mínimo, lo que hace que su sitio web sea más rápido y receptivo.

[!DNL Smart Imaging] incluye las siguientes capacidades:

* [Conversión de formato automática](#auto-format-conversion)
* [Optimización del ancho de banda de la red](#network-bandwidth-optimisation)

### Conversión de formato automática{#auto-format-conversion}

[!DNL Dynamic Media with OpenAPI] [convierte automáticamente las imágenes a formatos modernos optimizados para la web, como AVIF o WEBP](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=auto-format&t=request). La conversión depende de las capacidades del explorador y de [derechos de licencia](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate), independientemente del formato solicitado.

Los formatos AVIF y WEBP proporcionan una mejor compresión, haciendo que las imágenes sean más pequeñas y rápidas de entregar y cargar. AVIF se utiliza como formato predeterminado, ya que gestiona todas las funciones del explorador.

[!DNL Dynamic Media with OpenAPI] usa el parámetro de consulta `auto-format` para controlar el comportamiento del explorador al convertir una imagen a varios formatos para la entrega optimizada. La conversión de formato automática incluye **promoción automática** y **degradación automática**. Cuando el sistema promociona un formato optimizado para la web (AVIF o WEBP) sobre JPEG o PNG para su envío, se denomina promoción automática.

De manera predeterminada, el parámetro de consulta `auto-format` está establecido en `true`. Cuando `auto-format` está habilitado (true), el sistema ignora el formato solicitado y selecciona automáticamente un formato optimizado para la web (AVIF o WEBP) en función de las características de la imagen, las funcionalidades del explorador y [derechos de licencia](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-prime-ultimate).

Cuando `auto-format` es verdadero, el sistema entrega el formato de imagen en la siguiente secuencia:

* ***AVIF***: AVIF se entrega si el explorador lo admite y la licencia lo permite. Esto se denomina promoción automática.
* ***WEBP***: WEBP se entrega si AVIF no es compatible o no tiene licencia. Esto también es promoción automática.
* ***JPEG***: JPEG se entrega solamente cuando AVIF y WEBP no son compatibles y la imagen no tiene canal alfa (transparencia). Esto se denomina descenso automático.
* ***PNG***: PNG se entrega cuando el explorador no admite formatos modernos y la imagen tiene canal alfa (transparencia). Esto también se denomina degradación automática.

Deshabilite `auto-format` estableciendo el parámetro de consulta en `false` y, a continuación, especifique el formato requerido para que la imagen se envíe con ese formato.

### Optimización del ancho de banda de red{#network-bandwidth-optimisation}

Las imágenes se optimizan automáticamente en función de las condiciones de red del cliente para garantizar una entrega más rápida y una carga más fluida. Los parámetros [Quality](#quality-parameter) y [Max-quality](#max-quality-parameter) ajustan automáticamente la calidad controlando los niveles de compresión de la imagen, con valores que van del 1 al 100.

Vea los siguientes comportamientos clave de `quality` y `max-quality` parámetros:

* Si se especifican [!DNL quality] y [!DNL max-quality], [!DNL quality] tiene prioridad.
* Si solo se especifica [!DNL quality], la calidad se entrega independientemente del tiempo de carga en función de la velocidad de la red.
* Si solo se especifica [!DNL max-quality], la calidad de la imagen se ajusta automáticamente en función de las condiciones de la red y ofrece la mejor calidad posible hasta el valor [!DNL max-quality] especificado.
* Si no se especifica ninguno, el sistema aplica la optimización dinámica con un valor predeterminado `max-quality` de `85`.

#### Parámetro de calidad{#quality-parameter}

El parámetro quality prioriza la calidad de la imagen sobre la velocidad de carga. Corrige la calidad de la imagen de salida al valor solicitado (entre 1 y 100) e ignora las condiciones de la red. Más información sobre el [parámetro de calidad](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).

#### Parámetro de máxima calidad{#max-quality-parameter}

La calidad máxima equilibra la calidad de imagen y el tiempo de carga en función de la velocidad de red del cliente. Prioriza los tiempos de carga más rápidos al reducir la calidad de imagen en redes más lentas, al tiempo que sigue ofreciendo la máxima calidad posible (1-100) para las condiciones de red dadas. Obtenga más información acerca del [parámetro de máxima calidad](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat!in=query&path=quality&t=request).
