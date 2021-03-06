---
title: ¿Cómo se crea una plantilla de formulario adaptable?
description: Cree plantillas de formulario adaptables para definir la estructura básica y el contenido inicial con el Editor de plantillas.
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 1%

---

# Crear una plantilla de formulario adaptable {#adaptive-form-templates}

Al crear un formulario, se agregan campos y componentes para definir la estructura del formulario, el contenido y las acciones en el editor. Los campos y componentes se añaden en la variable `guideRootPanel` del contenedor de formulario. Con el Editor de plantillas, puede crear una plantilla que contenga estructura básica y contenido inicial que los autores puedan utilizar para crear formularios.

Por ejemplo, desea que todos los autores de formularios tengan ciertos cuadros de texto, botones de navegación y un botón de envío en un formulario de inscripción. Puede crear una plantilla con los componentes que los autores pueden utilizar para crear un formulario coherente con otros formularios de inscripción. Cuando los autores utilizan la plantilla para crear un formulario adaptable, el nuevo formulario hereda la estructura y los componentes especificados en la plantilla. El Editor de plantillas le permite:

* Agregue componentes de encabezado y pie de página de un formulario en la capa de estructura.
* Proporcione el contenido inicial para el formulario.
* Especifique un tema, Enviar acciones.

Puede descargar e instalar [!DNL AEM Forms] paquete de contenido de referencia de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) portal para importar temas de referencia y plantillas para su entorno.

## Uso de plantillas {#working-with-templates}

Puede acceder al editor de plantillas desde el menú Herramientas navegando hasta **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL Plantillas]**. En este caso, las plantillas están organizadas en carpetas habilitadas para plantillas editables.

Experience Manager proporciona una carpeta global para organizar las plantillas. Sin embargo, no está activada de forma predeterminada. Puede solicitar al administrador que habilite la carpeta global o que cree una carpeta para plantillas. Para obtener más información sobre cómo crear carpetas, consulte [Carpetas de plantilla](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### Crear una plantilla {#create-template}

Después de crear una carpeta, ábrala y realice los pasos siguientes para crear una plantilla:

1. Toque **[!UICONTROL Crear]** dentro de la carpeta que ha creado.
1. En la sección Elegir un tipo de plantilla , seleccione **[!UICONTROL Plantilla de formulario adaptable]** y toque **[!UICONTROL Siguiente]**.

1. En la sección Detalles de plantilla , escriba un Título de plantilla y pulse **[!UICONTROL Crear]**.
También puede proporcionar una descripción.

1. Toque **[!UICONTROL Listo]** para volver a la consola o pulse **[!UICONTROL Apertura]** para abrir la plantilla en el editor.

### IU del editor de plantillas {#template-editor-ui}

Cuando abra una plantilla para editarla, verá los siguientes componentes AEM Editor:

* **Barra de herramientas de página**
Contiene las siguientes opciones:

   * **Alternar panel lateral**: Permite mostrar u ocultar la barra lateral.
   * **Información de la página**: Permite especificar información, como el tiempo de publicación/cancelación de publicación, las miniaturas, las bibliotecas del lado del cliente, la directiva de página y la biblioteca del lado del cliente de diseño de página.

   <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Selector de modo:** Permite cambiar el modo.
Puede elegir **[!UICONTROL Estructura]** modo, **[!UICONTROL Contenido inicial]**, **[!UICONTROL Control de diseño]** en el menú contextual. El modo Estructura permite añadir y personalizar el encabezado y el pie de página. El modo de Contenido inicial permite personalizar el contenido del formulario.
   * **Vista previa:** Permite obtener una vista previa del aspecto de la plantilla al publicarla. Puede utilizar Selector de capa y Vista previa para alternar los modos de edición y vista previa.
* **Barra lateral:** Proporciona los navegadores Contenido, Propiedades, Recursos y Componentes.
* **Barra de herramientas de componentes:** Al seleccionar un componente, aparece una barra de herramientas que le permite personalizarlo.
* **Página**: Área donde se agrega contenido para crear la plantilla.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### Edición de una plantilla {#editing-a-template}

Se crea una plantilla de formulario adaptable con dos capas:

* Estructura
* Contenido inicial

El selector de capas está disponible junto a la opción Vista previa en la esquina superior derecha de la pantalla.

### Estructura {#structure}

Al seleccionar la capa de estructura en el Editor de plantillas, puede ver los contenedores de diseño encima y debajo del contenedor del formulario adaptable. Los autores pueden utilizar estos contenedores de diseño para el encabezado y el pie de página. Puede agregar, editar o personalizar el encabezado y el pie de página. Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de diseño sobre el contenedor de formulario adaptable para personalizar el encabezado de la plantilla. Arrastre y suelte el componente Pie de página del formulario adaptable en el contenedor de diseño debajo del contenedor del formulario adaptable para personalizar el pie de página de la plantilla.

![Contenedor de diseño en la capa de estructura](assets/header-layer-selector.png)

Contenedores de diseño en la capa de estructura

**A.** Contenedor de diseño para componente de encabezado **B.** Contenedor de diseño para componente de pie de página

Arrastre y suelte el componente Encabezado de formulario adaptable en el contenedor de diseño situado encima del contenedor de formulario adaptable. Después de agregar el componente, puede especificar sus propiedades que le permitan agregar un logotipo y proporcionar su título.

Del mismo modo, cuando arrastra y suelta el componente de pie de página en el contenedor de diseño debajo del contenedor de formulario adaptable, puede proporcionar la información de copyright y los detalles de la empresa.

![Encabezado y pie de página agregados en la capa Estructura](assets/header-and-footer.png)

Encabezado y pie de página agregados en la capa Estructura

#### Bloqueo/desbloqueo de componentes en la capa de estructura {#locking-unlocking-components-in-the-structure-layer}

Cuando edita la plantilla con la capa de estructura seleccionada, puede desbloquear el encabezado y el pie de página de la plantilla. Si un componente está desbloqueado en la plantilla, los autores de formularios pueden editar el componente en el formulario adaptable que utiliza la plantilla. Bloquear un componente impide que los autores de formularios lo editen en el formulario adaptable. La opción Bloquear está disponible en la barra de herramientas de componentes.

Por ejemplo, puede añadir el componente de encabezado en la plantilla. Al seleccionar el componente, puede ver una opción de bloqueo en la barra de herramientas de componentes. Normalmente, el encabezado incluye el nombre de la empresa y el logotipo, y no desea que los autores de formularios cambien el logotipo y el encabezado de una plantilla. En un formulario adaptable creado con la plantilla con el componente de encabezado bloqueado, los autores de formularios no pueden cambiar el logotipo y el nombre de la empresa.

>[!NOTE]
>
>No se recomienda bloquear o desbloquear la imagen o el logotipo en el componente del encabezado de forma individual. Puede desbloquear el componente del encabezado.

### Contenido inicial {#initial-content}

Cuando se selecciona la opción Contenido inicial , el contenedor de formulario adaptable de la plantilla se abre como un formulario adaptable para su edición. Al igual que la creación de un formulario adaptable, puede especificar la configuración inicial, como seleccionar un tema y enviar acciones.

Los autores de formularios lo utilizan como base para crear un formulario. La estructura del flujo de contenido se especifica en la capa Initial Content de la plantilla. Para cambiar a la edición del contenido inicial de la plantilla de formulario, antes de Vista previa en la barra de herramientas de la página, pulse ![lista desplegable de lienzo](assets/canvas-drop-down.png) **>** **[!UICONTROL Contenido inicial]**.


En la capa Contenido inicial , se crea la plantilla Formulario adaptable que los autores utilizan como base. La creación de una plantilla es similar a la creación de un formulario, se utilizan las opciones disponibles en la barra lateral. La barra lateral proporciona navegadores de contenido, propiedades, recursos y componentes.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Cuando selecciona Almacenar contenido o Almacenar PDF como Acción de envío, obtiene una opción para especificar la ruta de almacenamiento. Si especifica la ruta en la plantilla, todos los formularios creados a partir de ella tendrán la misma ruta. Puede especificar la ruta de almacenamiento correcta o asegurarse de que los autores de los formularios lo actualicen para evitar que los datos de todos los formularios se almacenen en la misma ubicación.

#### Creación de una plantilla de formulario adaptable con fichas y paneles {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por ejemplo, desea crear una plantilla con las siguientes pestañas:

* Información general
* Información profesional

Ha agregado un logotipo, proporcionado un título y agregado un pie de página en la capa de estructura. Bloquee el encabezado y el pie de página para impedir que los autores de formularios los editen cuando utilicen la plantilla para crear formularios.

Cambie la capa de Estructura a Contenido inicial y empiece a añadir contenido al formulario. Para crear una estructura con fichas, agregue un Panel secundario en el guideRootPanel del contenedor del formulario adaptable. Para agregar un panel:

* Puede agregar un panel tocando el botón **[!UICONTROL +]** al seleccionar la variable **[!UICONTROL Arrastre los componentes aquí]** .

* Puede arrastrar y soltar el componente del panel desde el navegador de componentes de la barra lateral.
* Puede agregar el panel secundario del `guideRootPanel` en la barra de herramientas de componentes.

Para crear las fichas Información general e Información profesional , agregue dos paneles en el panel secundario del `guideRootPanel`. Seleccione los paneles y pulse ![cmppr](assets/configure-icon.svg) para abrir las propiedades en la barra lateral. Cambie los nombres de los elementos como `general-info` y `professional-info`y títulos como Información general e Información profesional respectivamente. En la barra lateral, pulse contenido para abrir el navegador de contenido. En la ficha Objetos del formulario, seleccione `guideRootPanel`. En el editor, se selecciona guideRootPanel . Toque ![cmppr](assets/configure-icon.svg) en la barra de herramientas de componentes para abrir sus propiedades. En el campo Diseño del panel , seleccione **[!UICONTROL Pestañas arriba]** y toque **[!UICONTROL Listo]**. Se aplica la estructura de la plantilla con pestañas.

#### Adición de contenido en pestañas {#adding-content-in-tabs}

Después de agregar paneles y estructurarlos como fichas, puede agregar campos dentro de las pestañas. Al seleccionar una ficha en el editor, puede ver la variable **[!UICONTROL Arrastre los componentes aquí]** . Puede arrastrar y soltar componentes, como cuadros de texto, elementos de lista y botones. Puede arrastrar y soltar componentes desde el navegador de componentes en la barra lateral.

Cada componente tiene propiedades que mejoran la captura y manipulación de datos. Por ejemplo, puede activar la variable **[!UICONTROL Campo obligatorio]** propiedad de un componente. Los autores pueden especificar un mensaje que los clientes verán cuando omitan rellenar un campo obligatorio. Especifique el mensaje en **[!UICONTROL Mensaje de campo obligatorio]** propiedad.

En los campos plantilla de ejemplo, Nombre, Número de teléfono y Fecha de nacimiento se añaden en la pestaña Información general . En la pestaña Información profesional , Actualmente empleada, tipo de empleo, se añaden campos de cualificación educativa .

Después de agregar campos, puede agregar botones como Enviar y Restablecer.

### Activación de la plantilla {#enabling-the-template}

Al crear una plantilla, esta se agrega como borrador. Habilite la plantilla para utilizarla para crear Forms adaptable. Para habilitar una plantilla:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Plantillas]** y abra la carpeta en la que ha creado la plantilla.

1. La plantilla que ha creado se marca como borrador.
1. Seleccione la plantilla y pulse **[!UICONTROL Habilitar]** en la barra de herramientas.
Cuando cree un formulario adaptable, podrá ver la plantilla en la lista cuando se le pida que elija una plantilla.

## Importación o exportación de una plantilla {#importing-or-exporting-a-template}

Un formulario funciona con su plantilla. Cuando se descarga un formulario adaptable creado con una plantilla personalizada, la plantilla no se descarga. Al importar el formulario en otro [!DNL AEM Forms] por ejemplo, se importa sin su plantilla. Si se importa un formulario pero su plantilla no está disponible, el formulario no se procesa. Puede empaquetar la plantilla personalizada desde `/conf` nodo en `https://<server>:<port>/crx/packmgr`y portarlo en el [!DNL AEM Forms] instancia en la que desea cargar el formulario. También puede [Cree una plantilla con AEM Arquetipo e impleméntelo en la instancia de Cloud Services](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

## Creación de un formulario adaptable mediante la plantilla {#creating-an-adaptive-form-using-the-template}

Después de crear y habilitar una plantilla, esta estará disponible en el administrador de formularios al crear un formulario adaptable. Para utilizar una plantilla y crear un formulario adaptable, consulte [Creación de un formulario adaptable](creating-adaptive-form.md).

<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, in order to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. -->

## Recomendaciones {#recommendations}

* Cuando modifique las propiedades del formulario en el editor de plantillas, no utilice la propiedad BindReference .
* Si desea agregar un punto de interrupción, créelo cuando cree una plantilla de formulario adaptable.
Para obtener más información sobre los puntos de interrupción, consulte [Diseño interactivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
