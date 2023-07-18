---
title: Incrustar un formulario adaptable en una página de AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: 'Puede utilizar el componente de Formularios adaptables: incrustar para añadir o incrustar formularios adaptables en una página de AEM Sites para rellenar y enviar un formulario sin tener que abandonar la página.'
feature: Adaptive Forms
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: b6dcb6308d1f4af7a002671f797db766e5cfe9b5
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 99%

---

# Incrustar un formulario adaptable en una página de AEM Sites {#embed-an-adaptive-form-to-aem-sites-page}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | Este artículo |


## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar sin problemas formularios adaptables en una página de AEM Sites o en una página web hospedada fuera de AEM. El formulario adaptable incrustado es completamente funcional, y los usuarios pueden rellenarlo y enviarlo sin abandonar la página. Esto permite al usuario a mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.



<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Puede agregar un formulario adaptable en la página de AEM Sites mediante los siguientes elementos:

* Componente **Formularios adaptables: incrustar**
El componente de Formularios adaptables: incrustar permite a los autores de AEM Sites incluir un formulario adaptable existente en una página de AEM Sites, lo que mejora la reutilización de los formularios adaptables. Los formularios adaptables existentes se pueden usar de forma independiente o incrustada en la página del sitio. Esta integración proporciona una forma cómoda para que los clientes puedan reutilizar los formularios adaptables que ya han creado.

* **El Explorador de recursos**. Todos los formularios están disponibles en la sección Recursos. Puede arrastrar y colocar el formulario como un recurso en su página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable en una página de AEM Sites que usa una plantilla editable, asegúrese de que el componente de AEM Forms está configurado como un componente permitido en la plantilla asociada.

En el caso de que el componente de **Formularios adaptables: incrustar** no sea visible en el **Panel del explorador de componentes** de páginas de AEM Sites, siga los pasos siguientes tal como se muestra en el vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

En caso de que la página de Sites esté usando una plantilla estática, deberá configurarla en el sistema de párrafos de la página del sitio.

## Incrustación de un formulario adaptable {#af-component}

Para incrustar un formulario adaptable utilizando el componente **[!UICONTROL Formularios adaptables: incrustar]**:

1. Abra la página de AEM Sites en la que desee incrustar un formulario adaptable en el modo Edición.
1. En el panel Explorador de componentes, arrastre y coloque el componente [!UICONTROL Formularios adaptables: incrustar] en la página. También puede buscar un formulario adaptable en el explorador de recursos y arrastrarlo y colocarlo en la página de Sites. Puede crear un nuevo formulario adaptable o incrustar un formulario adaptable existente.

   >[!NOTE]
   >
   >No se admiten varios componentes de Formularios adaptables: incrustar en una misma página.

1. Para crear e incrustar un nuevo formulario, pulse el icono **Crear formulario** en la barra de herramientas de componentes. Se abre una ventana para crear el formulario.

1. Pulse en el componente de Formularios adaptables: incrustar en la página de Sites y, a continuación, pulse ![settings_icon](assets/settings_icon.png) en la barra de acciones. Se abrirá el cuadro de diálogo de **[!UICONTROL Editar formularios adaptables: incrustar]**.
1. En el cuadro de diálogo Editar formularios adaptables: incrustar, especifique lo siguiente.

   **Tipo de recurso:** seleccione el tipo de recurso que desea incrustar.
   * **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
   * **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
      * Mostrar

      * **Mensaje de agradecimiento**: escriba un mensaje con el editor de texto enriquecido para mostrarlo después del envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página de agradecimiento**: examine y seleccione la página que desea mostrar después del envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
         * **Redirigir a la página de agradecimiento**: active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento reemplaza al formulario adaptable en el componente de [!UICONTROL Formularios adaptables: incrustar] sin actualizar la página de Sites subyacente. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
   * **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable.
   * **Tema**: seleccione un tema que defina el estilo de los componentes del formulario adaptable. El estilo incluye propiedades de apariencia, como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **El formulario abarca la anchura completa del marco**: si se activa, iframe no se utiliza para procesar el formulario.
   * **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

AEM Sites también permite crear un formulario adaptable sobre la marcha utilizando el componente de Formularios adaptables: incrustar. Siga los pasos para crear un formulario adaptable mediante el **Componente de Formularios adaptables: incrustar** en la página de AEM Sites:
1. Abra la página de AEM Sites en la que desee incrustar un formulario adaptable en el modo Edición.
1. Desde el panel del explorador de componentes, arrastre y suelte el componente de Formularios adaptables: incrustar en la página.
1. Haga clic en el icono **Más** y se le redirigirá al asistente de creación de formularios.

   Componente ![Formularios adaptables: incrustar](/help/forms/assets/aemformcontainer.png)

1. Ahora puede incrustar un formulario adaptable en páginas del sitio de AEM mediante el [!UICONTROL Componente de contenedor de AEM Forms].

## Publicación de un formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios a la hora de publicar un formulario adaptable incrustado en una página de AEM Sites:

* Si publica la página de AEM Sites por primera vez y esta incluye un formulario adaptable incrustado, publique la página de Sites y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de Sites ya publicada, publique el recurso original, y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada incluye una referencia al recurso y no requiere que vuelva a publicar la página.
* Si ha modificado la página de Sites y el formulario adaptable integrado, vuelva a publicar la página y el recurso incrustado.

## Modificación de un formulario adaptable incrustado  {#modifying-embedded-adaptive-form}

La página de AEM Sites mantiene una referencia al formulario adaptable en el componente de Formularios adaptables: incrustar. Por lo tanto, todas las configuraciones y propiedades configuradas en el formulario adaptable original, como el tema, los estilos y la acción de envío, se mantienen en el formulario adaptable incrustado.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en Formularios adaptables en los respectivos editores y agréguelo.
* Pulse el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo Edición, en el cual puede modificarlo.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejarán automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable o la página de Sites para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de AEM Sites:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de los usuarios y los envíos de formularios incrustados son compatibles y visibles en las pestañas Borradores y Formularios enviados del portal de Formularios.
* La acción de envío configurada en el formulario original se mantiene en el formulario incrustado.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en esta aplicación. Sin embargo, no está disponible en el informe de análisis de Forms.
