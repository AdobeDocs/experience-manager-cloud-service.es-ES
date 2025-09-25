---
title: ¿Cómo se administran  [!DNL Dynamic Media] plantillas?
description: Aprenda a crear  [!DNL Dynamic Media] plantillas con un editor de plantillas de WYSIWYG e incluya varias capas de imágenes, textos y formas para crear rápidamente titulares y prospectos y utilizarlos en aplicaciones de flujo descendente.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 97be1d044ae23859e263756116c8bac8701178b4
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 1%

---


# [!DNL Dynamic Media] plantillas{#dynamic-media-templates}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Cree plantillas personalizables en tiempo real para sus banners y folletos usando [!DNL Dynamic Media] templates, un editor de plantillas de WYSIWYG. Publique la plantilla [!DNL Dynamic Media] y utilícela en aplicaciones de flujo descendente. Una plantilla [!DNL Dynamic Media] incluye capas de imagen y texto. Agregue parámetros a las capas de imagen y texto de la plantilla y utilice [[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) para cambiar la posición y el tamaño de la capa y actualizar su contenido en tiempo real.

Algunas de las características principales incluyen:

* **[!DNL Dynamic Media]Editor de plantillas de WYSIWYG:** Cree titulares personalizables con capas de texto e imagen.
* **Parametrización de capas:** Defina pares dinámicos de clave-valor para las capas a fin de habilitar las actualizaciones en tiempo real.
* **[!DNL Dynamic Media]Compatibilidad con URL:** Use [!DNL Dynamic Media] URL para plantillas, integrando valores personalizados de aplicaciones de origen o de terceros.
* **Control de visibilidad de la capa:** Oculte o muestre de forma dinámica las capas según sea necesario.
* **Cambio de tamaño del texto inteligente:** Ajuste automáticamente el tamaño del texto para ajustar las áreas designadas.

Algunas de las ventajas clave de las plantillas de [!DNL Dynamic Media] son:

* **Optimizar 1:1 Personalization:** Adapte el contenido a las señales de clientes en tiempo real.
* **Reducir el esfuerzo manual:** Automatizar y acelerar la creación y administración de contenido.
* **Garantizar experiencias omnicanal coherentes:** Mantener la coherencia de la marca en todos los canales.
* **Reutilizar contenido de forma eficaz:** Evite el contenido de un solo uso y escale con plantillas dinámicas parametrizadas.
* **Mitigar riesgos:** Actualizar precios, descuentos y vínculos en tiempo real.
* **Mejore la participación del cliente:** Impulse experiencias interactivas y relevantes para el contexto.

>[!NOTE]
>
>Los clientes con suscripciones al SKU de seguridad mejorada no pueden usar ninguna funcionalidad de [!DNL Dynamic Media], incluidas las plantillas [!DNL Dynamic Media], en ese programa de Cloud Services.

Aprenda a crear una plantilla [!DNL Dynamic Media] paso a paso en este vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Antes de empezar{#prerequisites-for-dynamic-media-wysiwyg-template}

Complete los siguientes requisitos para crear una plantilla [!DNL Dynamic Media] y generar su dirección URL de envío:

1. Acceso a [!DNL Dynamic Media].
1. En la página de inicio [!DNL Assets View], tiene una carpeta en **[!UICONTROL Dynamic Media Assets]** para guardar la plantilla. [Cree una carpeta](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) en ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets &#x200B;]**&#x200B;para replicarla en&#x200B;**[!UICONTROL &#x200B; Dynamic Media Assets &#x200B;]**.
1. [Sincroniza las imágenes disponibles en tu [!DNL AEM Assets] instancia con [!DNL Dynamic Media] para usarlas para crear la plantilla](/help/assets/dynamic-media/config-dm.md).
1. Publique las imágenes que desee utilizar para crear la plantilla y generar la dirección URL de entrega de la plantilla después de crearla. La dirección URL de envío se puede utilizar en aplicaciones de flujo descendente.
1. Para usar una fuente distinta a la predeterminada [!UICONTROL Adobe Sans F2] en la capa de texto de la plantilla, [cargue y publique el archivo de fuente en AEM y Dynamic Media simultáneamente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation). [Los formatos de archivo de fuente admitidos son, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Además, asegúrese de [reprocesar](/help/assets/reprocessing-assets-view.md) las fuentes existentes para usarlas. Consulte [Fuentes](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) para obtener más información.<!--(On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**)-->
1. compruebe lo siguiente en la interfaz de usuario táctil:
   * En la página **[!UICONTROL Editar configuración de [!DNL Dynamic Media]]**, el modo de sincronización **[!UICONTROL [!DNL Dynamic Media]]** establecido en **[!UICONTROL Deshabilitado de forma predeterminada]** no se aplica a todas las carpetas de AEM (**[!UICONTROL Sincronizar todo el contenido]** está desmarcado). Consulte [Configuración de Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md) para obtener más información.
   * El modo de sincronización **[!UICONTROL [!DNL Dynamic Media]]** se ha establecido en **[!UICONTROL Habilitar para subcarpetas]** para la carpeta o subcarpeta de destino en la que guardará la plantilla después de crearla. Consulte [configurar [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md) para obtener más información.

## Crear plantilla [!DNL Dynamic Media]{#how-to-create-dynamic-media-template}

Ejecute los siguientes pasos para crear una plantilla [!DNL Dynamic Media]:

<!--
1. Navigate to your [!DNL Assets View] and [create a folder](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**. The folder tree in ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** replicates in **[!UICONTROL Dynamic Media Assets]**. Save your [!DNL Dynamic Media] template in this [!UICONTROL Dynamic Media Assets] folder.
1. Select ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]** and [upload and publish your images to [!DNL AEM] and [!DNL Dynamic Media] simultaneously](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) to use them in creating the template. Publishing images is required to generate the template's delivery URL, after creating the template. The delivery URL can be used in downstream applications.
1. [Execute these asset uploading and publishing steps](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm?lang=en#dynamic-media-publish-mode-set-to-upon-activation) to upload and publish a font file to AEM and Dynamic Media simultaneously to use it in creating the template. [!UICONTROL Adobe Sans F2] is the only default font available in the text layer. [The supported font file formats are, AFM, OTF, PFB, PFM, PhotoFont, TTC, TTF](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/upload-publish/uploading-files#supported-asset-file-formats). Ensure to [reprocess](/help/assets/reprocessing-assets-view.md) the existing fonts to use them in creating the template (On [!DNL Assets View] home page, click ![Assets](/help/assets/assets/Asset-icon.svg)**[!UICONTROL Assets]**, navigate to the font file location, select the font file one at a time and click ![Reprocess](/help/assets/assets/Refresh-docs.svg)**[!UICONTROL Reprocess]**). See [Fonts](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/support-files/fonts) to know more about fonts.
-->

1. [Crear un lienzo en blanco](#create-a-canvas)
1. [Añadir imágenes al lienzo](#add-images-to-the-canvas)
1. [Añadir capas de texto al lienzo](#add-text-to-the-canvas)
1. [Agregar formas al lienzo](#add-shapes-to-the-canvas)
1. [Edición o eliminación de una capa](#edit-or-delete-a-layer)
1. [Parametrizar capas](#parameterise-a-layer)

### Crear un lienzo en blanco{#create-a-canvas}

Siga estos pasos para crear un lienzo en blanco:

1. Vaya a [!DNL Assets View], seleccione **[!UICONTROL Dynamic Media Assets]** disponible en el panel izquierdo y vaya a la carpeta para guardar la plantilla en ella.

   ![Plantillas de Dynamic Media](/help/assets/assets/DM-Assets1.png)

1. Seleccione **[!UICONTROL Crear plantilla]**. Se muestra el cuadro de diálogo **[!UICONTROL Nueva plantilla]**.

   ![cómo crear plantillas dinámicas que se pueden personalizar en tiempo real](/help/assets/assets/new-template.png)

   >[!NOTE]
   >
   >  La plantilla se guardará en la ubicación en la que la haya creado. En la página de inicio de [!DNL Assets View], seleccione **[!UICONTROL Dynamic Media Assets]** y haga clic en **[!UICONTROL Crear plantilla]** para guardar la plantilla en la carpeta raíz de **[!UICONTROL Dynamic Media Assets]**.

1. Especifique un nombre de plantilla, defina la anchura y altura del lienzo y haga clic en **[!UICONTROL Crear]**. Se muestra un lienzo en blanco con opciones de menú en ambos lados que se utilizan para crear la plantilla. Pase el ratón sobre las opciones del menú para ver su información sobre herramientas.
   ![plantilla personalizable en tiempo real](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > El intervalo de anchura y altura permitido es de 50 a 5000.

**Opciones de menú en el panel derecho:** Utilice estas opciones para agregar las imágenes y las capas de texto necesarias al lienzo.

* ![Plantillas DM](/help/assets/assets/add-image.svg): haga clic para agregar imágenes al lienzo.
* ![plantillas personalizables](/help/assets/assets/add-text.svg): haga clic para agregar textos al lienzo.
* ![plantillas personalizables](/help/assets/assets/show-layers-list.svg): haga clic para ver la lista de todas las capas (imagen y texto) del lienzo. Cada imagen y texto añadido al lienzo se representa como una capa independiente.

**Opciones de menú en el panel izquierdo:** Utilice estas opciones para las siguientes acciones comunes del editor.

* ![Plantillas DM](/help/assets/assets/layer-selector.svg): selecciona ![Plantillas DM](/help/assets/assets/layer-selector.svg) y haz clic en una capa del lienzo para seleccionarla.
* ![plantillas compatibles con la personalización](/help/assets/assets/bring-forward.svg): haga clic en ![plantillas compatibles con la personalización](/help/assets/assets/bring-forward.svg) o use el método abreviado de teclado, **Ctrl** + **`]`** (Windows) o **Cmd** + **`]`** (Mac) para avanzar una capa seleccionada.
* ![cómo crear una plantilla que se pueda personalizar fácilmente](/help/assets/assets/send-backward.svg): haga clic en ![cómo crear una plantilla que se pueda personalizar fácilmente](/help/assets/assets/send-backward.svg) o use el método abreviado de teclado, **Ctrl** + **`[`** (Windows) o **Cmd** + **`[`** (Mac) para enviar una capa seleccionada hacia atrás.
* ![crear una plantilla que se pueda personalizar al instante](/help/assets/assets/undo.svg): haga clic en ![crear una plantilla que se pueda personalizar al instante](/help/assets/assets/undo.svg) o use el método abreviado de teclado, **Ctrl** + **Z** (Windows) o **Cmd** + **Z** (Mac) para deshacer la última acción.
* ![plantilla para crear titulares rápidamente](/help/assets/assets/redo.svg): Haz clic en ![plantilla para crear titulares rápidamente](/help/assets/assets/redo.svg) o usa el método abreviado de teclado, **Ctrl** + **Y** (Windows) o **Cmd** + **Y** (Mac) para rehacer la última acción.
* ![plantilla para crear prospectos rápidamente](/help/assets/assets/zoom-in.svg): haz clic en ![plantilla para crear prospectos rápidamente](/help/assets/assets/zoom-in.svg) o usa el método abreviado de teclado, **Ctrl** + **+** (Windows) o **Cmd** + **+** (Mac) para ampliar el lienzo.
* ![plantilla para crear titulares rápidamente](/help/assets/assets/Zoom-out.svg): haz clic en ![plantilla para crear titulares rápidamente](/help/assets/assets/Zoom-out.svg) o usa el método abreviado de teclado, **Ctrl** + **-** (Windows) o **Cmd** + **-** (Mac) para alejar el lienzo.
* Pulse **retroceso** o **eliminar** para eliminar la capa seleccionada si no se está editando ningún texto o propiedad.

Haga clic en ![plantilla para crear prospectos rápidamente](/help/assets/assets/show-layers-list.svg) y seleccione más opciones (![](/help/assets/assets/three-dots.svg)) en la capa Lienzo para editar las dimensiones de lienzo en cualquier momento mientras crea la plantilla.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> Las plantillas permiten un máximo de 20 capas, incluido el lienzo.

### Añadir imágenes al lienzo{#add-images-to-the-canvas}

Siga estos pasos para agregar imágenes al lienzo:

1. Haga clic en ![crear un titular en poco tiempo](/help/assets/assets/add-image.svg) para abrir el panel [Selector de recursos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). El panel muestra las imágenes de la instancia de AEM Assets que están sincronizadas con [!DNL Dynamic Media].
1. Examine el panel o utilice palabras clave en la barra de búsqueda para encontrar una imagen específica.
1. Arrastre y suelte una imagen en el lienzo para utilizarla. Consulte el [**[!UICONTROL Panel de propiedades]**](#reposition-resize-delete-a-layer) para cambiar el tamaño o la posición de una capa en el lienzo.
   ![crear un titular en cuestión de segundos](/help/assets/assets/add-image-to-canvas.png)
1. Habilite la opción **[!UICONTROL Radio uniforme]** y use el control deslizante **[!UICONTROL Radio de vértice]** para ajustar la redondez de las cuatro esquinas de una imagen de manera uniforme. Desactive la opción para personalizar la redondez de la esquina asignando valores de radio específicos a cada esquina.
   ![ajustar redondez de esquina de la imagen](/help/assets/assets/enable-uniform-radius-image.png)

### Añadir capas de texto al lienzo{#add-text-to-the-canvas}

Siga estos pasos para agregar capas de texto al lienzo:

1. Haga clic en ![creando nuevos titulares rápidamente](/help/assets/assets/add-text.svg) para agregar una capa de texto al lienzo y abrir el panel Propiedades.
1. Seleccione la capa y haga clic en el texto para actualizarla.
1. Seleccione **[!UICONTROL Cambio de tamaño del texto inteligente]** en el panel Propiedades para ajustar automáticamente la longitud del texto y el tamaño de la fuente para que se ajusten de forma óptima en el área designada.
   ![mejores titulares personalizables](/help/assets/assets/add-text-layer.png)

Consulte el [**[!UICONTROL Panel de propiedades]**](#reposition-resize-delete-a-layer) para cambiar la posición, el tamaño, la rotación o la eliminación de la capa. Dé formato al texto con la fuente, el tamaño, el color, el estilo y la alineación necesarios (en la capa) cambiando sus valores en los campos respectivos de la sección **[!UICONTROL Texto]** del panel. El campo **[!UICONTROL Familia de fuentes]** muestra la fuente predeterminada [!UICONTROL Adobe Sans F2], las fuentes existentes reprocesadas y las fuentes recién cargadas y publicadas. Consulte el punto 5 de la sección [Antes de comenzar](#prerequisites-for-dynamic-media-wysiwyg-template) anterior para obtener más información.

[Aplique formato a las subcadenas para aplicar estilo y controlar partes específicas del texto de forma independiente.](#apply-formatting-to-substring)

#### Dar formato a texto selectivo{#apply-formatting-to-substring}

Ejecute los siguientes pasos para dar formato a partes específicas de una cadena:

1. Seleccione uno o varios caracteres en la cadena a los que desea dar formato.
1. Aplicar formato a la selección mediante el [panel de propiedades](#properties-panel). Las siguientes opciones de formato son aplicables a las subcadenas y sus partes:
   * **Estilo de fuente**: negrita, cursiva, subrayado, subíndice y superíndice con la opción **[!UICONTROL Estilo de fuente]**.
   * **Propiedades de fuente**: cambie la familia de fuentes, el color y el tamaño mediante las opciones de panel correspondientes.
     ![format-substring](/help/assets/assets/format-substring.png)

[Cada parte de cadena con formato se muestra como una subcadena en el selector de subcadenas, disponible en el panel Parámetros. Agregue parámetros a estas partes con formato para aplicarles formato dinámico mediante la dirección URL de envío de la plantilla ](#substring-parameterisation).

### Agregar formas al lienzo {#add-shapes-to-the-canvas}

Siga estos pasos para agregar formas al lienzo:

1. Haga clic en ![crear formas](/help/assets/assets/Shapes.svg), seleccione una forma (rectángulo o círculo) para agregarla al lienzo. Use el [[!UICONTROL Panel de propiedades]](#reposition-resize-delete-a-layer) de la forma para cambiar la posición, cambiar el tamaño, girar o eliminar la capa.
1. Desplácese hasta la sección **[!UICONTROL Estilo]** del panel, defina un código hexadecimal en el campo **[!UICONTROL Color de forma]** o use el selector de color para rellenar el color de la forma seleccionada.
1. Habilite la opción **[!UICONTROL Radio uniforme]** y use el control deslizante **[!UICONTROL Radio de vértice]** para ajustar la redondez de las cuatro esquinas del rectángulo de forma uniforme. Desactive la opción para personalizar la redondez de la esquina asignando valores de radio específicos a cada esquina.
   ![ajustar redondez de esquina de las formas](/help/assets/assets/enable-uniform-radius-shape.png)
1. [Agregue el parámetro **[!UICONTROL Hide]** a la capa seleccionada](#parameterise-a-layer) para mostrar u ocultar la capa en la plantilla en tiempo real mediante la dirección URL de la plantilla.
1. Seleccione la capa a la que [desea agregarle un vínculo [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates), lo que permitirá a los usuarios hacer clic en la forma como hipervínculo en la plantilla activa.

### Edición o eliminación de una capa {#edit-or-delete-a-layer}

Siga estos pasos para editar o eliminar una capa de lienzo:

1. Haga clic en ![plantillas compatibles con las actualizaciones dinámicas](/help/assets/assets/show-layers-list.svg) y seleccione la capa en el lienzo o en la lista Capas.
1. Haga clic en **[!UICONTROL más opciones]** (![plantillas compatibles con actualizaciones en tiempo real](/help/assets/assets/three-dots.svg)) para editar o eliminar la capa.
1. Haga clic en **[!UICONTROL Eliminar]** para eliminar la capa.
1. Haga clic en **[!UICONTROL Editar]** para editar la capa con el [**[!UICONTROL Panel Propiedades]**](#reposition-resize-delete-a-layer).
   ![creación rápida de banner](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Panel Propiedades{#properties-panel}

El panel [!UICONTROL Propiedades] incluye secciones para [cambiar la posición](#reposition-resize-delete-a-layer), [cambiar el tamaño](#reposition-resize-delete-a-layer) y [rotar](#reposition-resize-delete-a-layer) una capa.  También proporciona opciones de relleno de color para [capas de forma](#add-shapes-to-the-canvas), [opciones de formato de texto](#text-formatting-options-on-properties-panel) para [capas de texto](#add-text-to-the-canvas) y una opción para [agregar un vínculo de [!UICONTROL CTA]](#add-CTA-in-dynamic-media-templates) a cualquier capa seleccionada.
Para ir al panel de propiedades de una capa, haga clic en ![creación rápida de contenido](/help/assets/assets/show-layers-list.svg) y seleccione la capa en la lista para mostrar su panel [!UICONTROL Propiedades].

![creación rápida de contenido](/help/assets/assets/properties-panel.png)

En el panel [!UICONTROL Propiedades] de una capa, seleccione otra capa del lienzo para ir a su panel [!UICONTROL Propiedades].

#### Cambiar la posición, el tamaño, la rotación o la eliminación de una capa{#reposition-resize-delete-a-layer}

Consulte estas acciones comunes de edición de capas para editar un texto o una capa de imagen:

* **Cambiar la posición de la capa:** Arrastre la capa para moverla a cualquier lugar del lienzo. Esta acción actualiza los valores X e Y en el panel de propiedades. X e Y son las coordenadas del centro de la capa en el plano del lienzo.
* **Cambiar el tamaño de la capa:** Seleccione la capa y arrastre sus controladores de borde para cambiar su tamaño. Esta acción actualiza los valores de anchura y altura en el panel de propiedades.
* **Rotar la capa:** Arrastre el controlador cuadrado colocado verticalmente sobre la capa para girarlo alrededor de su centro. Esta acción actualiza los valores de ángulo en el panel de propiedades.
* **Eliminar la capa:** Presione **Retroceso** o **eliminar** y luego haga clic en **[!UICONTROL Confirmar]** para eliminar una capa seleccionada.

#### Opciones de formato de texto{#text-formatting-options-on-properties-panel}

Dé formato al texto con la fuente, el tamaño, el color, el estilo y la alineación necesarios (dentro de la capa) cambiando sus valores en los campos respectivos de la sección **[!UICONTROL Texto]** del panel.
Asegúrese de incluir **[!UICONTROL Cambio de tamaño de texto inteligente]**. [!UICONTROL Cambio de tamaño del texto inteligente] funciona con el algoritmo [Ajuste de texto](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) para rellenar de manera óptima el texto en el área de texto y evita que el texto se desborde y minimiza el espacio adicional en la parte inferior del texto.

![creación de contenido rápidamente](/help/assets/assets/smart-text-resize.png)

### Parametrizar capas {#parameterise-a-layer}

Después de crear una plantilla con varias capas de imágenes, textos y formas, parametriza las capas seleccionadas. Cuando se parametriza una capa o su propiedad, obtiene un par clave-valor (también denominado como parámetro). Este parámetro se puede incluir en la dirección URL de la plantilla para actualizar la posición, el tamaño o el contenido de la capa en tiempo real, lo que resulta en la personalización de la plantilla en poco tiempo.

Para parametrizar una capa:

1. haga clic en ![creación instantánea de contenido](/help/assets/assets/show-layers-list.svg), seleccione una capa y haga clic en **[!UICONTROL Parámetros]**. Se muestra el panel **[!UICONTROL Parámetros]**.
1. Cambie **[!UICONTROL Include Parameter]** para asignar parámetros a una propiedad. Consulte la opción [Parámetros del panel](#parameterisation-options-or-allowed-parameters) para conocer el comportamiento de la propiedad después de la parametrización.
1. **Opcional:** Cambie el nombre del parámetro. Un nombre de parámetro tiene un nombre de capa seguido de un sufijo. Para una capa seleccionada, todas sus propiedades parametrizadas comparten el mismo nombre de capa seguido de un sufijo variable. Cambie el nombre de la capa siguiendo la convención de nomenclatura semántica, de modo que cuando incluya el parámetro en la URL, el nombre del parámetro explica por sí mismo el contenido de la capa o su propósito.
1. Haga clic en **[!UICONTROL Guardar]**.
   ![creación instantánea de contenido](/help/assets/assets/parameterise-a-layer.png)
Para cambiar entre el panel Parámetro de una capa de imagen y de texto, seleccione la capa en el lienzo y haga clic en **[!UICONTROL Parámetros]**.

#### Opción del panel Parámetros {#parameterisation-options-or-allowed-parameters}

Las propiedades parametrizadas se pueden incluir como parámetros de URL en la URL de la plantilla para editar la plantilla en tiempo real mediante la URL.

##### Parámetros de capa{#layer-parameters}

Los siguientes son parámetros de capa que se aplican tanto a las capas de imagen como a las de texto.

**[!UICONTROL X]:** Incluir para mover la capa horizontalmente a lo largo de su línea central, paralela al eje X del plano de plantilla, cambiando el valor del parámetro en la dirección URL.
**[!UICONTROL Y]:** Incluir para mover la capa verticalmente a lo largo de su línea central, paralela al eje Y del plano de la plantilla, cambiando el valor del parámetro en la dirección URL.
**[!UICONTROL Anchura]:** Incluir para ajustar el ancho de la capa cambiando el valor del parámetro en la dirección URL.
**[!UICONTROL Altura]:** Incluir para ajustar la altura de la capa cambiando el valor del parámetro en la dirección URL.
**[!UICONTROL Ocultar]:** Incluir para ocultar o mostrar la capa en la plantilla usando 0 (mostrar) y 1 (ocultar).

##### Parámetro de imagen{#image-parameter}

Incluya el parámetro **[!UICONTROL Source]** para reemplazar la imagen de la capa con una nueva imagen al cambiar la ruta de la imagen en el valor del parámetro en la dirección URL.
![parámetro de origen de imagen](/help/assets/assets/image-parameter.png)

##### Parámetros de formato de texto{#text-formatting-parameters}

Incluya los siguientes parámetros para editar el texto, su fuente, color y tamaño desde la dirección URL de envío al actualizar los valores de los parámetros en la dirección URL:

**[!UICONTROL Texto]:** Incluir para actualizar el texto de la dirección URL.
**[!UICONTROL Familia de fuentes]:** Incluir para actualizar la fuente del texto desde la dirección URL.
**[!UICONTROL Tamaño de fuente]:** Incluir para actualizar el tamaño de fuente del texto desde la dirección URL.
**[!UICONTROL Color del texto]:** Incluir para actualizar el color de fuente del texto de la dirección URL.

##### Parametrizar subcadenas{#substring-parameterisation}

En el panel **[!UICONTROL Parámetros]**, desplácese hasta la sección **[!UICONTROL Parámetros de subcadena]**. Esta sección incluye un **selector de subcadena** que muestra la cadena completa (capa de texto seleccionada) con formato coherente o sus partes con formato como subcadenas independientes. Seleccione una subcadena para [parametrizar el texto, la familia de fuentes, el tamaño de fuente y el color](#text-formatting-parameters).
Use el selector de subcadenas para [dividir subcadenas](#split-substring) para parametrizar sus partes individuales o [combinar subcadenas](#merge-substring) para aplicar parámetros uniformes.

###### Dividir subcadena{#split-substring}

Para parametrizar parte de una subcadena, tire de ella hacia fuera para convertirla en una subcadena independiente para la selección y parametrización individuales.
Ejecute los siguientes pasos para dividir una subcadena en subcadenas independientes:

1. En el selector de subcadenas, seleccione los caracteres de una subcadena para separarla.
1. Haga clic en ![dividir subcadena](/help/assets/assets/unmerge.svg) para extraerla y convertirla en una subcadena independiente dentro del **selector de subcadena**.
   ![subcadena dividida](/help/assets/assets/split-a-substring.png)
Puede seleccionar la subcadena necesaria para [parametrizar el texto, la familia de fuentes, el tamaño de fuente y el color](#text-formatting-parameters).

###### Combinar subcadena{#merge-substring}

La combinación de subcadenas elimina los parámetros individuales existentes y permite aplicar parámetros coherentes en toda la subcadena recién formada.
Ejecute los siguientes pasos para combinar dos subcadenas adyacentes y aplicar parámetros uniformes a la subcadena resultante:

1. En el selector de subcadenas, seleccione caracteres en dos subcadenas adyacentes con el mismo formato.
1. Haga clic en ![combinar subcadena](/help/assets/assets/merge.svg) para combinar las subcadenas.
   ![combinar subcadenas idénticas](/help/assets/assets/merge-two-substrings.png)
Puede aplicar parámetros uniformes a la subcadena recién formada.
   >[!NOTE]
   >
   >Solo se pueden combinar subcadenas con un formato idéntico.

### Agrupar capas para controlar su visibilidad simultáneamente{#group-layers}

Otra forma de mantener las plantillas flexibles es utilizar un nombre de parámetro único para controlar varias capas. Esta estrategia es útil para el parámetro de visibilidad (ocultar o mostrar capas), para actualizar el diseño o los gráficos de una sola plantilla.

Siga estos pasos para asignar el mismo nombre a los parámetros [!UICONTROL Hide] (![creación rápida de contenido](/help/assets/assets/Visibility-icon.svg)) de varias capas, lo que le permite ocultarlos o mostrarlos simultáneamente.

1. Vaya al [**[!UICONTROL Panel de propiedades]**](#parameterise-a-layer) de una capa.
1. Cambie el parámetro **[!UICONTROL Hide]** si no está parametrizado anteriormente.
1. **Opcional:** Cambie el nombre del parámetro **[!UICONTROL Hide]**.
1. Copie el nombre del parámetro **[!UICONTROL Hide]**.
1. Vaya al panel Parámetro de otras capas seleccionándolas en el lienzo y alterne su parámetro **[!UICONTROL Hide]** si no está parametrizado.
1. Reemplace su nombre **[!UICONTROL Hide parameter]** con el nombre copiado.
1. Haga clic en **[!UICONTROL Guardar]** para agrupar las capas.
1. Ejecute los pasos 3 y 4 en la sección [**[!UICONTROL Previsualizar y publicar]**](#preview-and-publish-template-and-copy-template-deliver-url) para ver los cambios.

## Previsualice y publique la plantilla para copiar la dirección URL de envío{#preview-and-publish-template-and-copy-template-deliver-url}

Siga estos pasos para previsualizar y publicar la plantilla y copiar la dirección URL de envío:

1. En la página de lienzo, haga clic en **[!UICONTROL Vista previa]**. También puede ir a la **[!UICONTROL vista de Assets]** **>** **[!UICONTROL Dynamic Media Assets]** **>** para buscar y seleccionar su plantilla **>** y hacer clic en **[!UICONTROL Editar plantilla]** **>** y hacer clic en **[!UICONTROL Vista previa]**. La página de vista previa muestra la plantilla, sus parámetros (capas y propiedades parametrizadas), el estado de publicación y la opción **[!UICONTROL Publish]**.
1. Seleccione parámetros del panel **[!UICONTROL Parámetros de plantilla]** para editar sus valores y actualizar instantáneamente el contenido, el tamaño, la posición o el formato de texto de la capa de plantilla correspondiente en la vista previa. Por ejemplo:
   1. Seleccione una capa de texto y edite su texto o
   1. Seleccione una capa de imagen, haga clic en ![crear contenido sobre la marcha](/help/assets/assets/add-image.svg), seleccione una imagen del selector de recursos y haga clic en **[!UICONTROL Actualizar]**.

   La plantilla se actualiza inmediatamente, mostrando el texto editado y reemplazando la imagen anterior por la nueva. Además, el valor del parámetro de imagen refleja la nueva ruta de imagen. Del mismo modo, puede cambiar el tamaño de una capa ajustando sus valores, y los cambios se aplican a la plantilla en tiempo real.
1. Seleccione el parámetro **[!UICONTROL Hide]** para [capas agrupadas](#group-layers) de la lista para mostrarlas u ocultarlas juntas en la plantilla.
1. **Opcional:** Cambie el valor del parámetro **[!UICONTROL Hide]** entre 0 y 1 y haga clic en **[!UICONTROL Refresh]** para ver los cambios. Las capas con el mismo parámetro **[!UICONTROL Hide]** se ocultan o se muestran juntas. Del mismo modo, se puede controlar la visibilidad de las capas desde la dirección URL.

   ![creando contenido sobre la marcha](/help/assets/assets/dm-templates-publish-status.png)
También puede alternar **[!UICONTROL Incluir todos los parámetros]** para editar todos los valores de parámetros mostrados y ver las actualizaciones en la vista previa de la plantilla.
   <br>
1. Para publicar la plantilla desde la página de vista previa, haz clic en **[!UICONTROL Publicar]** y confirma la publicación. Aparece un mensaje **[!UICONTROL Publicación completa]** y el estado de publicación se actualiza a **[!UICONTROL Publicado]**.

### Copiar la dirección URL de envío

Los parámetros seleccionados en la página **[!UICONTROL Vista previa]** se convierten en los parámetros de URL en la URL de la plantilla.

Asegúrese de que las imágenes de la plantilla ya se han publicado en AEM y Dynamic Media para generar la dirección URL de envío de la plantilla.

Ejecute los siguientes pasos para copiar la dirección URL de entrega de la plantilla:

1. Haga clic en **[!UICONTROL Copiar URL]**. Se muestra el cuadro de diálogo **[!UICONTROL Copiar URL]**. Seleccione y copie la dirección URL mostrada. El primer parámetro de la dirección URL comienza después del signo de interrogación **([!UICONTROL ?])** y un par clave-valor comienza con **[!UICONTROL $]** y termina con **[!UICONTROL &amp;]**. La clave y el valor están separados por un signo igual **([!UICONTROL =])**, con la clave a la izquierda y el valor a la derecha.
1. Pegue esta dirección URL en la pestaña del explorador y vea la plantilla activa. Personalice la plantilla en tiempo real actualizando el valor del parámetro requerido (valor de clave) en la dirección URL directamente, tal como se muestra en el [paso 2](#preview-and-publish-template-and-copy-template-deliver-url) de la sección **Previsualizar y publicar**.
1. Utilice esta URL para la comercialización rápida de sus productos o servicios. Puede compartir esta URL con sus clientes o integrarla en su sitio web o en cualquier aplicación de terceros descendente para mostrar el banner y realizar actualizaciones en tiempo real para reflejar las ofertas en curso.

## Realice actualizaciones en tiempo real de la plantilla desde la dirección URL{#update-the-template-from-the-url}

La edición de parámetros directamente en la dirección URL puede resultar tediosa. Para simplificar:

1. Copie la dirección URL y péguela en un bloc de notas.
1. Utilice Cmd+F (Mac) o Ctrl+F (Windows) para buscar y editar los valores de parámetro. Por ejemplo:
   * Buscar y reemplazar trazados de imagen para capas de imagen.
   * Busque las coordenadas [parametrizadas](#parameterise-a-layer) de la capa, anchura y altura, para ajustar sus valores.
   * Editar texto, fuente, color, tamaño o alineación para capas de texto.
   * Cambie los valores de visibilidad entre 0 y 1.

Pegue esta URL actualizada en el explorador para ver los cambios.

## Editar la plantilla{#edit-the-template}

Edite la plantilla siguiendo estos pasos:

1. En [!DNL Assets view], haga clic en **[!UICONTROL Dynamic Media Assets]**.
2. Navegue hasta la ubicación de la plantilla.
3. Seleccione la plantilla.
4. Haga clic en **[!UICONTROL Editar plantilla]**. El lienzo de la plantilla muestra la plantilla y la lista de todas sus capas en el panel Capas. Comience a editar la plantilla según sus necesidades.

## Añadir el vínculo de Call to action (CTA) a la capa de plantilla{#add-CTA-in-dynamic-media-templates}

Convierta cualquier imagen, texto o capa de forma de la plantilla [!DNL Dynamic Media] en un hipervínculo agregándole un vínculo de CTA que dirija a los usuarios a una página de destino.

Siga estos pasos para agregar un vínculo de CTA a una capa:

1. Vaya a la ubicación de la plantilla, seleccione la plantilla y haga clic en ![editar](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL Editar plantilla]**. La plantilla se muestra en el lienzo.
1. Seleccione la capa de plantilla y [navegue hasta su panel de propiedades](#edit-or-delete-a-layer) para agregarle un vínculo de CTA.
1. En el panel Propiedades, seleccione **[!UICONTROL Agregar CTA]**, especifique la dirección URL de destino en el campo **[!UICONTROL URL]** y haga clic en **[!UICONTROL Guardar]**.

   ![agregar CTA](/help/assets/assets/add-cta.png)

1. Haga clic en **[!UICONTROL Vista previa]** y seleccione **[!UICONTROL Publicar]** para publicar la plantilla, si no se publicó anteriormente.
1. Vaya a la carpeta donde se guardó esta plantilla, selecciónela y haga clic en ![página de detalles](/help/assets/assets/details-page-icon.svg) **[!UICONTROL Detalles]**.
1. Haga clic en **[!UICONTROL Opciones de copia]** y seleccione **[!UICONTROL Copiar código incrustado]**. Asegúrese de publicar las imágenes de la plantilla en [!DNL AEM and Dynamic Media] para copiar el código incrustado.

   ![copiar código incrustado](/help/assets/assets/copy-options1.png)

   El siguiente es un ejemplo de código incrustado:

   ```json
    <div class="adobe-dynamicmedia-template-embed-container">
    <img id="<Image ID>>" src="<Image Source>>" alt="adobe dynamicmedia template" usemap="#adobe-dynamicmedia-template-map" width="800" height="300">
    <map name="adobe-dynamicmedia-template-map">
    <area shape="rect" coords="417,-60,817,340" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    <area shape="rect" coords="6,206.57,129,231.43" href="https://business.adobe.com/products.html" alt="Layer with CTA" title="https://business.adobe.com/products.html" target="_blank">
    </map>
    </div>
   ```

1. Agregue el código incrustado copiado al archivo HTML del sitio y ejecútelo en el explorador para mostrar la plantilla.

Haga clic en el elemento CTA de la plantilla para desplazarse a la página de destino.

Vea este vídeo paso a paso para aprender a añadir un vínculo de CTA a una capa de plantilla.

>[!VIDEO](https://video.tv.adobe.com/v/3457616)

## Puntos importantes que debe tener en cuenta {#important-points-to-note}

* Después de crear una plantilla con capas de imagen parametrizadas para actualizaciones dinámicas, asegúrese de que las imágenes destinadas a actualizaciones futuras compartan las mismas dimensiones que las imágenes parametrizadas. Esto garantiza que las imágenes se ajusten perfectamente dentro de las capas sin desbordarse ni dejar espacios vacíos. Actualmente, la plantilla no admite ajustes de dimensión automáticos para ajustar las imágenes a las capas.
* No se admiten subcadenas en una capa de texto. El usuario no puede aplicar propiedades de fuente diferentes en la subcadena de una capa de texto.
* La compatibilidad con varias [!DNL Dynamic Media] empresas no está disponible actualmente con [!DNL Dynamic Media] plantillas.
* En caso de copiar o mover, el Selector de destino muestra todas las carpetas (incluidas las carpetas no sincronizadas [!DNL Dynamic Media]). Además, actualmente no muestra los recursos de plantilla [!DNL Dynamic Media] (ambas son limitaciones del selector de destino).
* Cualquier operación de actualización en una carpeta (por ejemplo, Publicar o Eliminar) desde la sección de Assets afecta a las [!DNL Dynamic Media] plantillas disponibles en esa carpeta.
* La papelera no funciona para [!DNL Dynamic Media] plantillas. Si un recurso se mueve a la papelera y luego se restaura, se restaurará en AEM pero no en [!DNL Dynamic Media]. Lo mismo es válido para [!DNL Dynamic Media] plantillas.

## Ver también

1. Explorar [[!DNL Dynamic Media] y sus capacidades](/help/assets/dynamic-media/dynamic-media.md)
1. Explorar [[!DNL Dynamic Media] con capacidades de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)