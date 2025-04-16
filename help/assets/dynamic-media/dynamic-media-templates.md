---
title: ¿Cómo se administran  [!DNL Dynamic Media] plantillas?
description: Aprenda a crear  [!DNL Dynamic Media] plantillas mediante un editor de plantillas de WYSIWYG e incluya varias imágenes y capas de texto para crear rápidamente titulares y prospectos y utilizarlos en aplicaciones de flujo descendente.
hide: true
role: User
exl-id: 07de648e-4ae2-4524-8e05-3cf10bb6006d
source-git-commit: 6223937acc317ea57a7e91c90bac36f1b1d4be67
workflow-type: tm+mt
source-wordcount: '3029'
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

Cree plantillas personalizables en tiempo real para sus banners y folletos usando [!DNL Dynamic Media] templates, un editor de plantillas de WYSIWYG. Utilice su plantilla [!DNL Dynamic Media] en aplicaciones de flujo descendente. Una plantilla [!DNL Dynamic Media] incluye capas de imagen y texto. Agregue parámetros a las capas de imagen y texto de la plantilla y utilice [[!DNL Dynamic Media] URL](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/storage/catalog-urls-dynamic-media) para cambiar la posición y el tamaño de la capa y actualizar su contenido en tiempo real.

Algunas de las características principales incluyen:

* **[!DNL Dynamic Media]Editor de plantillas de WYSIWYG:** Cree titulares personalizables con capas de texto e imagen.
* **Parametrización de capas:** Defina pares dinámicos de clave-valor para las capas a fin de habilitar las actualizaciones en tiempo real.
* **[!DNL Dynamic Media]Soporte URL:** Utilice [!DNL Dynamic Media] URLs para plantillas, integrando valores personalizados de aplicaciones propias o de terceros.
* **Control Visibilidad capas:** ocultar dinámicamente o mostrar capas según sea necesario.
* **Cambio de tamaño del texto inteligente:** Ajuste automáticamente el tamaño del texto para ajustar las áreas designadas.

Algunas de las ventajas clave de las plantillas de [!DNL Dynamic Media] son:

* **Optimizar Personalization 1:1:** Adapte el contenido a las señales de clientes en tiempo real.
* **Reducir el esfuerzo manual:** Automatizar y acelerar la creación y administración de contenido.
* **Garantizar experiencias omnicanal coherentes:** Mantener la coherencia de la marca en todos los canales.
* **Reutilizar contenido de forma eficaz:** Evite el contenido de un solo uso y escale con plantillas dinámicas parametrizadas.
* **Mitigue los riesgos:** actualice los precios, los descuentos y los vínculos en tiempo real.
* **Mejore la participación del cliente:** Impulse experiencias interactivas y relevantes para el contexto.

>[!NOTE]
>
>Los clientes con suscripciones al SKU de seguridad mejorada no pueden usar ninguna funcionalidad de [!DNL Dynamic Media], incluidas las plantillas [!DNL Dynamic Media], en ese programa de Cloud Services.

## Antes de empezar{#prerequisites-for-dynamic-media-wysiwyg-template}

Para crear una plantilla [!DNL Dynamic Media], debe contar con:

1. Acceso a [!DNL Dynamic Media].
1. [Sincronizó las imágenes disponibles en su [!DNL AEM Assets] instancia con [!DNL Dynamic Media] para usarlas en la creación del plantilla](/help/assets/dynamic-media/config-dm.md).
1. verificado lo siguiente en el IU táctil:
   * En el **[!UICONTROL Página de configuración de Editar[!DNL Dynamic Media]]**, **[!UICONTROL [!DNL Dynamic Media]sincronizar modo]** que está configurado en **[!UICONTROL Deshabilitado de forma predeterminada]** no se aplica a todas las carpetas AEM (**[!UICONTROL la opción Sincronizar todas las contenido]** no está activada). Consulte [Configuración de Dynamic Media Cloud Service](/help/assets/dynamic-media/config-dm.md) para obtener más información.
   * **[!UICONTROL [!DNL Dynamic Media]sincronizar modo]** está configurado en **[!UICONTROL Habilitar para subcarpetas]** para la carpeta o subcarpeta de destino donde guardará la plantilla después de la creación. Consulte [Configuración de [!DNL Dynamic Media] Cloud Service](/help/assets/dynamic-media/config-dm.md) para obtener más información.

## Crear [!DNL Dynamic Media] plantilla de WYSIWYG{#how-to-create-dynamic-media-wysiwyg-template}

Ejecute los siguientes pasos para crear una plantilla [!DNL Dynamic Media]:

1. Vaya a [!DNL Assets View] y [cree una carpeta](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/add-delete-assets-view) en **[!UICONTROL Assets]**. El árbol de carpetas de **[!UICONTROL Assets]** se replica en **[!UICONTROL Dynamic Media Assets]**. Utilice esta carpeta [!UICONTROL Dynamic Media Assets] para guardar la plantilla [!DNL Dynamic Media] más adelante.
1. Seleccione **[!UICONTROL Assets]** y [cargue y publique sus imágenes en [!DNL AEM] y [!DNL Dynamic Media] simultáneamente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/publish-assets-to-aem-and-dm#dynamic-media-publish-mode-set-to-upon-activation) para usarlas para crear la plantilla.
1. [Crear un lienzo en blanco](#create-a-canvas)
1. [Añadir imágenes al lienzo](#add-images-to-the-canvas)
1. [Añadir capas de texto al lienzo](#add-text-to-the-canvas)
1. [Edición o eliminación de una capa](#edit-or-delete-a-layer)
1. [Parametrizar capas](#parameterise-a-layer)

### Crear un lienzo en blanco{#create-a-canvas}

Siga estos pasos para crear un lienzo vacío:

1. Desplácese hasta [!DNL Assets View] Dynamic Media Assets ]**disponibles en el panel izquierdo y selecciónela**[!UICONTROL .

   ![Plantillas de Dynamic Media](/help/assets/assets/DM-Assets1.png)

1. Seleccione **[!UICONTROL Crear plantilla]** en este Página o navegue hasta la carpeta de Assets ]**de Dynamic Media**[!UICONTROL  y seleccione **[!UICONTROL Crear plantilla]**. El plantilla se guarda en la ubicación donde se crea, ya sea en la carpeta raíz, como **[!UICONTROL Dynamic Media Assets]** , o en una carpeta dentro de la raíz. Después de seleccionar **[!UICONTROL Crear plantilla]** , aparece el **[!UICONTROL cuadro de diálogo Plantilla]** Nuevo.
   ![Cómo crear plantillas dinámicas que se pueden personalizar en tiempo real](/help/assets/assets/new-template.png)

1. Especifique un nombre plantilla, defina el ancho y la altura del lienzo y haga clic en **[!UICONTROL Crear]**. Se muestra un lienzo en blanco con opciones de menú en ambos lados que se utilizarán para crear el plantilla. Pase el ratón por encima de las opciones de menú para ver su información sobre herramientas.
   ![plantilla personalizable en tiempo real](/help/assets/assets/blank-canvas-page.png)

   >[!NOTE]
   >
   > El rango permitido de anchura y altura es de 50 a 5000.

**Opciones de menú en el panel derecho:** Utilice estas opciones para agregar las imágenes y capas de texto necesarias al lienzo.

* ![Plantillas DM](/help/assets/assets/add-image.svg): haga clic para agregar imágenes al lienzo.
* ![plantillas personalizables](/help/assets/assets/add-text.svg): haga clic para agregar textos al lienzo.
* ![plantillas personalizables](/help/assets/assets/show-layers-list.svg): haga clic para ver la lista de todas las capas (imagen y texto) del lienzo. Cada imagen y texto añadido al lienzo se representa como una capa independiente.

**Opciones de menú en el panel izquierdo:** Utilice estas opciones para acciones comunes del editor como se menciona a continuación.

* ![Plantillas DM](/help/assets/assets/layer-selector.svg): seleccione una capa.
* ![plantillas que admiten personalización](/help/assets/assets/bring-forward.svg): haga clic para avanzar una capa seleccionada o presione **Ctrl** + **]** (Windows) o **Cmd** + **]** (Mac).
* ![cómo crear una plantilla que se pueda personalizar fácilmente](/help/assets/assets/send-backward.svg): haga clic para enviar una capa seleccionada hacia atrás o presione **Ctrl** + **[** (Windows) o **Cmd** + **[** (Mac).
* ![crear una plantilla que se pueda personalizar al instante](/help/assets/assets/undo.svg): haz clic para deshacer la última acción o presiona **Ctrl** + **Z** (Windows) o **Cmd** + **Z** (Mac).
* ![plantilla para crear titulares rápidamente](/help/assets/assets/redo.svg): haz clic para rehacer la última acción o presiona **Ctrl** + **Y** (Windows) o **Cmd** + **Y** (Mac).
* ![plantilla crear folletos rápidamente](/help/assets/assets/zoom-in.svg): Haga clic para acercar el lienzo o presione **Ctrl** + **+** (Windows) o Cmd + **+** (Mac).
* ![plantilla crear banners rápidamente](/help/assets/assets/Zoom-out.svg): Haga clic para alejar el lienzo o presione **Ctrl** + **-** (Windows) o **Cmd** + **-** (Mac).
* Pulse **Retroceso** o **Eliminar** para eliminar la capa seleccionada si no se está editando ningún texto o Propiedad.

Haga clic en ![plantilla para crear prospectos rápidamente](/help/assets/assets/show-layers-list.svg) **>** más opciones (![](/help/assets/assets/three-dots.svg)) en la capa Lienzo para editar las dimensiones de lienzo en cualquier momento mientras crea la plantilla.
![](/help/assets/assets/edit-canvas1.png)

>[!NOTE]
>
> Las plantillas permiten un máximo de 20 capas, incluido el lienzo.

### Añadir imágenes al lienzo{#add-images-to-the-canvas}

Siga estos pasos para agregar imágenes al lienzo:

1. Haga clic en ![crear un titular en poco tiempo](/help/assets/assets/add-image.svg) para mostrar el panel [Selector de recursos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector). El panel muestra las imágenes de la instancia de AEM Assets que están sincronizadas con [!DNL Dynamic Media].
1. Examine el panel o utilice palabras clave en la barra de búsqueda para encontrar una imagen específica.
1. Arrastre y suelte una imagen en el lienzo para utilizarla. Consulte el panel]**](#reposition-resize-delete-a-layer) Propiedades para cambiar el tamaño o la [**[!UICONTROL posición de una capa en el lienzo.
   ![crear un banner en segundos](/help/assets/assets/add-image-to-canvas.png)

### Añadir capas de texto al lienzo{#add-text-to-the-canvas}

Siga estos pasos para agregar capas de texto al lienzo:

1. Haga clic en ![creando nuevos titulares rápidamente](/help/assets/assets/add-text.svg) para agregar una capa de texto al lienzo y abrir el panel Propiedades.
1. Seleccione la capa y haga clic en el texto para actualizarla.
1. Seleccione **[!UICONTROL Cambio de tamaño del texto inteligente]** en el panel Propiedades para ajustar automáticamente la longitud del texto y el tamaño de la fuente para que se ajusten de forma óptima en el área designada.
   ![mejores titulares personalizables](/help/assets/assets/add-text-layer.png)

Consulte el panel]**](#reposition-resize-delete-a-layer) Propiedades para cambiar la [**[!UICONTROL posición, el tamaño, la rotación o la eliminación de la capa. Dé formato al texto con la fuente, el tamaño, el color, el estilo y la alineación necesarios (en la capa) cambiando sus valores en los campos respectivos de la sección **[!UICONTROL Texto]** del panel.

>[!NOTE]
>
> Para usar una fuente distinta a la familia de fuentes predeterminada Adobe Sans F2, debe cargar y publicar el archivo de fuente en [!AEM Assets] y [!DNL Dynamic Media]. Si tiene fuentes antiguas en su instancia, asegúrese de [volver a procesar](/help/assets/reprocessing-assets-view.md) para verlas en el editor de plantillas.

### Edición o eliminación de una capa {#edit-or-delete-a-layer}

Siga estos pasos para editar o eliminar una capa de lienzo:

1. Haga clic en ![las plantillas compatibles con actualizaciones dinámicas](/help/assets/assets/show-layers-list.svg) y seleccione la capa en el lienzo o en el lista Capas.
1. Haga clic en **[!UICONTROL más opciones]** (![plantillas compatibles con actualizaciones](/help/assets/assets/three-dots.svg) en tiempo real) para editar o eliminar la capa.
1. Haga clic en **[!UICONTROL Eliminar]** para eliminar la capa.
1. Haga clic en **[!UICONTROL Editar]** para editar la capa mediante el [**[!UICONTROL panel Propiedades]**](#reposition-resize-delete-a-layer).
   ![Creación rápida banner](/help/assets/assets/dm-templates/edit-delete-layer.png)

### Panel Propiedades{#properties-panel}

Para navegar al panel de propiedades de una capa:

1. Haga clic en ![creación](/help/assets/assets/show-layers-list.svg) rápida contenido.
1. Seleccione la capa en la lista.

Este panel muestra la posición del punto central de la capa en el plano del lienzo (valores X e Y) y las dimensiones de la capa (ancho y alto) junto con las opciones de formato de texto.

![Creación rápida contenido](/help/assets/assets/properties-panel.png)

En el panel de propiedades de una capa, seleccione otra capa en el lienzo para navegar hasta su panel de propiedades.


#### Cambiar la posición, el tamaño, la rotación o la eliminación de una capa{#reposition-resize-delete-a-layer}

Consulte estas acciones comunes de edición de capas para editar un texto o una capa de imagen:

* **Cambiar la posición de la capa:** Arrastre la capa para moverla a cualquier lugar del lienzo. Esta acción actualiza los valores X e Y en el panel de propiedades.
* **Cambiar el tamaño de la capa:** Seleccione la capa y arrastre sus controladores de borde para cambiar su tamaño. Esta acción actualiza los valores de anchura y altura en el panel de propiedades.
* **Rotar la capa:** Arrastre el tirador cuadrado colocado verticalmente sobre la capa para girarlo alrededor de su centro. Esta acción actualiza los valores de ángulo en el panel de propiedades.
* **Eliminar la capa:** presione **Retroceso** o **Eliminar** y, a continuación, haga clic en **[!UICONTROL Confirmar]** para eliminar la capa seleccionada.

#### Opciones de formato de texto{#text-formatting-options-on-properties-panel}

Dé formato al texto con los fuente, tamaño, color, estilo y alineación necesarios (dentro de la capa) cambiando sus valores en los campos respectivos en la **[!UICONTROL sección Texto]** en el panel.
Asegúrese de incluir **[!UICONTROL Smart Text Resize]**. [!UICONTROL Smart Text Resize] funciona en [el algoritmo Copyfitting](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/text-formatting/r-copy-fitting) para rellenar de manera óptima el texto en el área de texto y evita el desbordamiento del texto y minimiza el espacio adicional en la parte inferior del texto.

![creación de contenido rápidamente](/help/assets/assets/smart-text-resize.png)

### Parametrizar capas {#parameterise-a-layer}

Después de crear una plantilla con varias capas de imágenes y textos, parametrice las capas seleccionadas. Cuando una capa o su Propiedad se parametriza, obtiene un par clave-valor (también llamado parámetro). Este parámetro se puede incluir en la URL de plantilla para actualizar la posición, el tamaño o la contenido de la capa en tiempo real, lo que resulta en una personalización plantilla en poco tiempo.

Para parametrizar una capa:

1. haga clic en ![creación instantánea de contenido](/help/assets/assets/show-layers-list.svg), seleccione una capa y haga clic en **[!UICONTROL Parámetros]**. Se muestra el panel **[!UICONTROL Parámetros]**.
1. Cambie **[!UICONTROL Include Parameter]** para asignar parámetros a una propiedad. Consulte la opción [Parámetros del panel](#parameterisation-options-or-allowed-parameters) para conocer el comportamiento de la propiedad después de la parametrización.
1. **Opcional:** Cambie el nombre del parámetro. Un nombre de parámetro tiene un nombre de capa seguido de un sufijo. Para una capa seleccionada, todas sus propiedades parametrizadas comparten el mismo nombre de capa seguido de un sufijo variable. Cambie el nombre de la capa siguiendo la convención de nomenclatura semántica, de modo que cuando incluya el parámetro en la URL, el nombre del parámetro explica por sí mismo el contenido de la capa o su propósito.
1. Haga clic en **[!UICONTROL Guardar]**.
   ![creación instantánea de contenido](/help/assets/assets/parameterise-a-layer.png)
Para cambiar entre el panel Parámetro de una capa de imagen y de texto, seleccione la capa en el lienzo y haga clic en **[!UICONTROL Parámetros]**.

#### Opción del panel Parámetros {#parameterisation-options-or-allowed-parameters}

Las propiedades parametrizadas se pueden incluir como parámetros de URL en la URL de la plantilla para editar la plantilla en tiempo real mediante la URL.

**Parámetros de imagen:**

**[!UICONTROL X]:** Incluya para mover la capa horizontalmente a lo largo de su línea central, paralela al eje X del plano plantilla, cambiando el valor del parámetro en el URL.
**[!UICONTROL Y]:** Incluya para mover la capa verticalmente a lo largo de su línea central, paralela al eje Y del plano plantilla, cambiando el valor del parámetro en el URL.
**[!UICONTROL Anchura]:** Incluir para ajustar el ancho de la capa cambiando el valor del parámetro en la URL.
**[!UICONTROL Altura]:** Incluir para ajustar la altura de la capa cambiando el valor del parámetro en la URL.
**[!UICONTROL Ocultar]:** incluya para ocultar o mostrar la capa en el plantilla utilizando 0 (mostrar) y 1 (ocultar).
**[!UICONTROL Source]:** Incluir para reemplazar la imagen de la capa con una nueva imagen cambiando la ruta de la imagen en el valor del parámetro en la dirección URL.

**Parámetros de formato de texto:**

Incluya los siguientes parámetros para editar el texto, su fuente, color y tamaño desde la URL al actualizar los valores de los parámetros en la URL.

**[!UICONTROL Texto]:** Incluir para actualizar el texto de la dirección URL.
**[!UICONTROL Familia de fuentes]:** Incluir para actualizar la fuente del texto desde la dirección URL.
**[!UICONTROL Tamaño de fuente]:** Incluir para actualizar el tamaño de fuente del texto desde la dirección URL.
**[!UICONTROL Color del texto]:** Incluir para actualizar el color de fuente del texto de la dirección URL.

### Agrupar capas para controlar su visibilidad simultáneamente{#group-layers}

Otra forma de mantener sus plantillas flexibles es utilizando un solo nombre de parámetro para controlar múltiples capas. Esta estrategia es útil para el parámetro de visibilidad (ocultar o mostrar capas), para actualizar el diseño o los gráficos de una sola plantilla.

Siga estos pasos para asignar el mismo nombre a los parámetros de ocultar (![creación rápida contenido](/help/assets/assets/Visibility-icon.svg)) de varias capas, lo que le permite ocultar o mostrarlos simultáneamente.

1. Vaya al [**[!UICONTROL Panel de propiedades]**](#parameterise-a-layer) de una capa.
1. Cambie el parámetro **[!UICONTROL Hide]** si no está parametrizado anteriormente.
1. **Opcional:** Cambie el nombre del parámetro **[!UICONTROL Hide]**.
1. Copie el nombre del parámetro **[!UICONTROL Hide]**.
1. Vaya al panel Parámetro de otras capas seleccionándolas en el lienzo y alterne su parámetro **[!UICONTROL Hide]** si no está parametrizado.
1. Reemplace su nombre **[!UICONTROL Hide parameter]** con el nombre copiado.
1. Haga clic en **[!UICONTROL Guardar]** para agrupar las capas.
1. Ejecute el paso 3 y luego el 4 en la sección [**[!UICONTROL Previsualizar y publicar]**](#preview-and-publish-template-and-copy-template-deliver-url) para ver los cambios.

## Previsualice y publique la plantilla para copiar la dirección URL de envío{#preview-and-publish-template-and-copy-template-deliver-url}

Siga estos pasos para previsualizar y publicar la plantilla y copiar la dirección URL de envío:

1. En la página de lienzo, haga clic en **[!UICONTROL Vista previa]**. También puede ir a la **[!UICONTROL vista de Assets]** **>** **[!UICONTROL Dynamic Media Assets]** **>** para buscar y seleccionar su plantilla **>** y hacer clic en **[!UICONTROL Editar plantilla]** **>** y hacer clic en **[!UICONTROL Vista previa]**. La página de vista previa muestra la plantilla, sus parámetros (capas y propiedades parametrizadas), el estado de publicación y la opción **[!UICONTROL Publish]**.
1. Seleccione parámetros en el panel Parámetros ]**de**[!UICONTROL  plantilla para editar sus valores y actualizar instantáneamente la contenido, el tamaño, la posición o el formato de texto de la capa de plantilla correspondiente en el previsualización. Por ejemplo:
   1. Seleccione una capa de texto y edite su texto o
   1. Seleccione una capa de imagen, haga clic en ![la creación de contenido sobre la marcha](/help/assets/assets/add-image.svg), seleccione una imagen del selector recurso y haga clic en **[!UICONTROL Actualizar]**.

   El plantilla se actualiza inmediatamente, mostrando el texto editado y reemplazando la imagen anterior por la nueva. Además, el valor del parámetro de imagen refleja la nueva ruta de imagen. Del mismo modo, puede cambiar el tamaño de una capa ajustando sus valores, y los cambios se aplican al plantilla en tiempo real.
1. Seleccione el **[!UICONTROL parámetro Ocultar]** para [las capas](#group-layers) agrupadas desde la lista para mostrarlas o ocultar juntas en el plantilla.
1. **Opcional:** Cambie el **[!UICONTROL valor del parámetro Ocultar entre]** 0 y 1 y haga clic en **[!UICONTROL Actualizar]** para ver los cambios. Las capas con el mismo **[!UICONTROL parámetro Ocultar]** se ocultan o se muestran juntas. Del mismo modo, puede controlar la visibilidad de las capas desde la URL.

   ![Creación de contenido sobre la marcha](/help/assets/assets/dm-templates-publish-status.png)
También puede alternar **[!UICONTROL Incluir todos los parámetros]** para editar todos los valores de parámetro mostrados y ver las actualizaciones en el previsualización plantilla.
   <br>
1. Para publicar el plantilla en el Página previsualización, haga clic en **[!UICONTROL Publish]**  y confirme a publicar. Se muestra el mensaje Publicación completa y el estado de publicación se actualiza a Publicado.

>[!NOTE]
>
>La publicación de la plantilla requiere que las imágenes de la plantilla se publiquen primero.

### Copiar la dirección URL de envío

Los parámetros seleccionados en la página **[!UICONTROL Vista previa]** se convierten en los parámetros de URL en la URL de la plantilla.

Para copiar la URL de la plantilla publicada que se muestra en la vista previa:

1. Haga clic en **[!UICONTROL Copiar URL]**. Aparecerá el **[!UICONTROL cuadro de diálogo Copiar URL]** . Seleccione y copie el URL mostrado. El primer parámetro del URL comienza después de un signo **de interrogación ([!UICONTROL ?])** y un par clave-valor empieza por **[!UICONTROL $]** y termina por **[!UICONTROL &amp;]**. La clave y el valor están separados por un signo **igual ([!UICONTROL =]),** con la clave a la izquierda y el valor a la derecha.
1. Pegar este URL en su explorador pestaña y vea su plantilla en vivo. Personalice el plantilla en tiempo real actualizando el valor del parámetro requerido (valor de la clave) en el URL directamente, como se muestra en [el paso 2](#preview-and-publish-template-and-copy-template-deliver-url) de **Vista previa y Publish** sección.
1. Utilice este URL para obtener una rápida comercialización de sus productos o servicios. Puede compartir este URL con sus clientes o integrarlo en su sitio web o en cualquier aplicación de terceros posteriores para mostrar el banner y realizar actualizaciones en tiempo real para reflejar las ofertas en curso.

Aprenda a crear una plantilla [!DNL Dynamic Media] paso a paso en este vídeo.
>[!VIDEO](https://video.tv.adobe.com/v/3443281)

## Realizar actualizaciones en tiempo real al plantilla desde la URL{#update-the-template-from-the-url}

Editar parámetros directamente en la URL puede ser tedioso. Para simplificar:

1. Copie el URL y péguelo en un bloc de notas.
1. Utilice Cmd + F (Mac) o Ctrl + F (Windows) para buscar y editar los valores de los parámetros. Por ejemplo:
   * Buscar y reemplazar trazados de imagen para capas de imagen.
   * Busque las coordenadas [parametrizadas](#parameterise-a-layer) de la capa, anchura y altura, para ajustar sus valores.
   * Editar texto, fuente, color, tamaño o alineación para capas de texto.
   * Cambie los valores de visibilidad entre 0 y 1.

Pegue esta URL actualizada en el explorador para ver los cambios.

## Editar la plantilla{#edit-the-template}

Edite la plantilla siguiendo estos pasos:

1. En [!DNL Assets view], haga clic en **[!UICONTROL Dynamic Media Assets]**.
2. Navegue hasta la ubicación de la plantilla.
3. Seleccione el plantilla.
4. Haga clic en **[!UICONTROL Editar plantilla]**. El lienzo de plantilla muestra la plantilla y la lista de todas sus capas en el panel Capas. Comience a editar la plantilla según sus necesidades.

## Añadir el vínculo de la llamada a la acción (CTA) a la capa de plantilla{#add-CTA-in-dynamic-media-templates}

Convierta cualquier imagen o capa de texto de la plantilla [!DNL Dynamic Media] en un hipervínculo agregándole un vínculo de CTA que dirija a los usuarios a una página de destino. Siga estos pasos para agregar un vínculo de CTA a una capa:

1. Vaya a la ubicación de la plantilla, seleccione la plantilla y haga clic en ![editar](/help/assets/assets/edit-pen-icon.svg) **[!UICONTROL Editar plantilla]**. La plantilla se muestra en el lienzo.
1. Seleccione la capa de plantilla y [navegue hasta su panel de propiedades](#edit-or-delete-a-layer) para agregarle un vínculo de CTA.
1. En el panel de propiedades, seleccione **[!UICONTROL añadir llamada a acción]**, especifique el URL de destino en el **[!UICONTROL campo URL]** y haga clic en **[!UICONTROL Guardar]**.

   ![añadir llamada a la acción](/help/assets/assets/add-cta.png)

1. Haga clic en **[!UICONTROL Vista previa]** para obtener una vista previa de la plantilla y ver sus parámetros definidos.
1. Haga clic en **[!UICONTROL Publicar]** y seleccione **[!UICONTROL Sí]** para publicar la plantilla, si no se publicó anteriormente.
1. Vaya a la carpeta donde se guardó esta plantilla, selecciónela y haga clic en ![página de detalles](/help/assets/assets/details-page-icon.svg) **[!UICONTROL Detalles]**.
1. Haga clic en **[!UICONTROL Opciones de copia]** y seleccione **[!UICONTROL Copiar código incrustado]**.

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
* Actualmente la compatibilidad de varias [!DNL Dynamic Media] empresas no está disponible con [!DNL Dynamic Media] plantillas.
* En caso de copiar o mover, el Selector de destino muestra todas las carpetas (incluidas las carpetas no[!DNL Dynamic Media] sincronizadas). Además, actualmente, no muestra el [!DNL Dynamic Media] activos de plantilla (ambas son limitaciones de selector de destino).
* Cualquier operación de actualización en una carpeta (por ejemplo, Publish o Eliminar) desde Assets sección afecta a las [!DNL Dynamic Media] plantillas disponibles dentro de esa carpeta.
* La papelera no funciona con [!DNL Dynamic Media] las plantillas. Si un recurso se mueve a la papelera y luego se restaura, el recurso se restaura en AEM pero no en [!DNL Dynamic Media]. Lo mismo puede decirse de [!DNL Dynamic Media] las plantillas.

## Véase también

1. Explore [[!DNL Dynamic Media] y sus capacidades](/help/assets/dynamic-media/dynamic-media.md)
1. Explore [[!DNL Dynamic Media] con las capacidades de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md)
