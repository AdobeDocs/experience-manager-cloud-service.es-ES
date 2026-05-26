---
title: Fragmentos de contenido visual
description: Obtenga información sobre cómo visualizar y publicar fragmentos de contenido visual mediante plantillas de HTML.
feature: Content Fragments
role: User, Developer
source-git-commit: 9ad53c41534c552f485a2d57d3c81c270180dfaf
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 0%

---

# Fragmentos de contenido visual {#visual-content-fragments}

Los fragmentos de contenido contienen contenido estructurado que está diseñado para la salida JSON, sin diseño ni diseño. La adición de plantillas de HTML le permite crear experiencias visuales totalmente decoradas con contenido estructurado en formato HTML:

* La visualización de un fragmento de contenido ayuda a garantizar la calidad del contenido, lo que permite a las partes interesadas revisar el contenido antes de utilizarlo, sin tener que abrir el Editor de fragmentos de contenido

* El envío de un fragmento visual ayuda a la entrega omnicanal, para reutilizar experiencias modulares en varios canales, como la web, el correo electrónico o las aplicaciones móviles.

El resultado procesado de un fragmento de contenido de AEM que utiliza el diseño de una plantilla de HTML adjunta se denomina *Fragmento de contenido visual*.

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>Los fragmentos de contenido visual están actualmente en disponibilidad limitada.
>
>Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

Las plantillas de HTML contienen información de diseño, lo que permite la visualización de fragmentos de contenido. La conexión entre una plantilla y un fragmento de contenido se establece mediante la sintaxis de Handlebars para asignar etiquetas de HTML a tipos de datos (campos) definidos en el modelo de fragmento de contenido. Esta definición permite que el contenido creado en los campos respectivos del Editor de fragmentos de contenido se muestre en las ubicaciones adecuadas dentro de la plantilla.

Usted o su equipo de desarrollo pueden [crear y personalizar sus propias plantillas de HTML](/help/implementing/developing/extending/content-fragments-visualization-templates.md), luego [cargar y adjuntar una o más a los modelos de fragmentos de contenido](#upload-and-assign-your-template) para que los fragmentos correspondientes se puedan representar en experiencias, [previsualizar](#preview-your-fragment-with-a-template) y [entregar según sea necesario](#deliver-your-visual-content-fragment).

>[!NOTE]
>
>Una **plantilla genérica** siempre está disponible en AEM de forma predeterminada, asociada con cada modelo. Esta plantilla permite que los pares clave/valor del contenido estructurado se muestren en un formato limpio de estilo de tabla para admitir casos de uso de Assurance de calidad de contenido (QA).

## Crear una plantilla {#create-a-template}

Las plantillas de HTML desarrolladas mediante Handlebars le permiten previsualizar y entregar fragmentos de contenido visual en formato HTML. La sintaxis Handlebars.js define marcadores de posición para el contenido creado en los campos Fragmento de contenido.

Para obtener más información sobre cómo desarrollar sus propias plantillas, consulte [Fragmentos de contenido visual: plantillas](/help/implementing/developing/extending/content-fragments-visualization-templates.md).

## Cargar y asignar la plantilla {#upload-and-assign-your-template}

Una plantilla está asociada a un modelo de fragmento de contenido para que se pueda utilizar con cualquier fragmento de contenido creado a partir de ese modelo.

Para cargar la nueva plantilla de HTML:

1. En la consola Fragmento de contenido, abra la pestaña de **Modelos de fragmento de contenido**.
1. Vaya a la ubicación del modelo de fragmento.
1. Seleccione el icono de información (i) del modelo requerido:

   ![Consola de fragmento de contenido: icono de información](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   Se mostrará el panel derecho.
1. Desplácese hacia abajo para mostrar **Plantillas HTML**, la **Plantilla genérica** ya aparece como la predeterminada:

   ![Previsualizar fragmento con plantilla genérica de HTML](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-configure-default.png)

1. Seleccione **+** para cargar la plantilla desde un archivo HTML (`.html`). Un cuadro de diálogo le permitirá **examinar** su sistema de archivos local y seleccionar su archivo de plantilla.
1. Una vez cargadas, se muestran dos vistas de la plantilla para que las revise:

   * left: una representación de la plantilla sin contenido
   * right: el código HTML, que también se puede editar aquí antes de importar a AEM

   ![Revisar plantilla de HTML al cargar](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-upload-review.png)

1. Seleccione **Siguiente** para continuar.
1. Escriba un **nombre de plantilla** para usar en AEM.
1. Confirme con **Crear plantilla**.
1. La plantilla se creará en AEM y se enumerará en **Plantillas de HTML**, en las propiedades de los Modelos de fragmentos de contenido.
Una vez cargado, se puede usar para [previsualizar fragmentos](#preview-your-fragment-with-a-template). También puede **[descargar](#download-your-template)** o **[eliminar](#download-your-template)** la plantilla.

## Previsualización del fragmento con una plantilla {#preview-your-fragment-with-a-template}

Para obtener una vista previa del fragmento de contenido mediante una plantilla:

>[!NOTE]
>
>Como **Plantilla genérica** siempre está disponible, puede obtener una vista previa del fragmento sin cargar ninguna plantilla personalizada.

1. En la consola Fragmento de contenido vaya a la ubicación del fragmento.

1. O bien, haga lo siguiente:
   * seleccione el fragmento en la consola
   * abra el fragmento en el editor

1. Seleccione **Vista previa** en la barra de herramientas superior de:

   * la consola Fragmento de contenido
   * en el editor, donde puede seleccionar **Plantilla**

En ambos casos se abrirá una nueva ventana modal.

1. Si no hay plantillas personalizadas disponibles, AEM usará la **Plantilla genérica** para mostrar el fragmento. La **Plantilla Genérica**:

   * muestra los campos del fragmento en forma de tabla; nombre y contenido
   * muestra el contenido totalmente hidratado de fragmentos a los que se hace referencia en la misma vista

1. Si hay plantillas personalizadas disponibles, puede seleccionar la plantilla que desee usar (incluida la **Plantilla genérica**).

1. Si el fragmento de contenido está publicado, también puede ver y copiar su **URL de vista previa** y su **URL de publicación**.

Por ejemplo, obtenga una vista previa con la **plantilla genérica**:

![Previsualizar fragmento con plantilla genérica de HTML](/help/sites-cloud/administering/content-fragments/assets/cf-visual-html-template-referenced-fragment.png)

## Distribuya su fragmento de contenido visual {#deliver-your-visual-content-fragment}

El fragmento de contenido visual se puede entregar a varios destinatarios en formato HTML.

### Envío al explorador {#deliver-to-the-browser}

Copie la **URL de vista previa** o la **URL de publicación**. Acceda a esta directamente desde el explorador para ver el fragmento de contenido visual.

### Envío a Edge Delivery Services {#deliver-to-edge-delivery-services}

Puede enviar el fragmento visual en una página de servicio de Edge Delivery (EDS).

1. Vaya al proyecto EDS.
1. Agregue o acceda a un **[bloque](https://www.aem.live/developer/block-collection)** del tipo **[embed](https://sidekick-library--aem-block-collection--adobe.aem.page/tools/sidekick/library.html?plugin=blocks&path=/block-collection/embed&index=0)**.
1. Pegue la **URL de publicación** en el bloque.
1. Publique la página EDS. Se verá la representación de HTML del fragmento.

>[!NOTE]
>
>Para obtener información detallada, consulte [Integración con Edge Delivery Services (bloque incrustado)](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#integration-with-edge-services-embed-block)

### Envío a una página de AEM {#deliver-to-an-AEM-page}

Puede enviar el fragmento de contenido visual en una página de AEM mediante el componente principal: Fragmento de contenido.

Al configurar un **fragmento de contenido** [componente en su página](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page):

1. Especifique el **fragmento de contenido** requerido.
1. Seleccione **Visualización de fragmentos de contenido**.
1. Seleccione la **Plantilla de visualización** necesaria en la lista desplegable.

   ![Configurar el componente Fragmento de contenido para un fragmento visual](/help/sites-cloud/administering/content-fragments/assets/cf-visual-template-aem-page.png)

1. El fragmento visual se mostrará en la página.

>[!NOTE]
>
>Para obtener información detallada, consulte [Integración de AEM Sites con componentes principales](/help/implementing/developing/extending/content-fragments-visualization-publish-url.md#integration-aem-sites-with-core-components)

## Descargue su plantilla {#download-your-template}

Para descargar la plantilla de HTML desde AEM:

1. En la consola Fragmento de contenido, abra la pestaña de **Modelos de fragmento de contenido**.
1. Vaya a la ubicación del modelo de fragmento.
1. Seleccione el icono de información (i) del modelo requerido:

   ![Consola de fragmento de contenido: icono de información](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   Se mostrará el panel derecho.

1. Desplácese hacia abajo para mostrar **Plantillas HTML**.
1. Seleccione la elipse junto a la plantilla que desee descargar.
1. Seleccione **Descargar**.
1. Especifique el nombre y la ubicación del archivo.
1. Confirme con **Guardar**.

## Eliminar la plantilla {#delete-your-template}

Para eliminar la nueva plantilla de HTML (de AEM):

1. En la consola Fragmento de contenido, abra la pestaña de **Modelos de fragmento de contenido**.
1. Vaya a la ubicación del modelo de fragmento.
1. Seleccione el icono de información (i) del modelo requerido:

   ![Consola de fragmento de contenido: icono de información](/help/sites-cloud/administering/content-fragments/assets/cfc-information-icon.png)

   Se mostrará el panel derecho.
1. Desplácese hacia abajo para mostrar **Plantillas HTML**.
1. Seleccione la elipse junto a la plantilla que desee descargar.
1. Seleccione **Eliminar**.
1. En el siguiente cuadro de diálogo, confirme la acción con **Eliminar**.
