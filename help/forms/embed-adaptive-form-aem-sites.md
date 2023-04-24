---
title: Incrustar un formulario adaptable en una página de AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: Puede utilizar el componente Forms adaptable - Incrustar para añadir o incrustar Forms adaptable a una página de AEM Sites para rellenar y enviar un formulario sin salir de las páginas de AEM Sites.
feature: Adaptive Forms
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 2a487654c3af2d2ec3aa43481caed5e1d4fc77a2
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 66%

---

# Incrustar un formulario adaptable en una página de AEM Sites {#embed-an-adaptive-form-to-aem-sites-page}

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios integrar sin problemas Adaptive Forms en una página de AEM Sites o en una página web alojada fuera de AEM. El formulario adaptable incrustado es completamente funcional, y los usuarios pueden rellenarlo y enviarlo sin abandonar la página. Esto permite al usuario a mantenerse en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.



<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

Puede agregar un formulario adaptable en la página de AEM Sites mediante los siguientes elementos:

* **Forms adaptable: componente incrustado**
Forms adaptable: el componente Insertar permite a los autores de AEM Sites incluir un formulario adaptable existente en una página de AEM Sites, lo que mejora la reutilización de los formularios adaptables. El Forms adaptable existente se puede usar de forma independiente o incrustada en la página del sitio. Esta integración proporciona una forma cómoda para que los clientes puedan reutilizar el Forms adaptable que ya han creado.

* **El Explorador de recursos**. Todos los formularios están disponibles en la sección Recursos. Puede arrastrar y colocar el formulario como un recurso en su página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable en una página de AEM Sites que usa una plantilla editable, asegúrese de que el componente de AEM Forms está configurado como un componente permitido en la plantilla asociada.

En el caso **Forms adaptable: componente incrustado** no está visible en la variable **Panel del explorador de componentes** de AEM página sitios , realice los pasos siguientes tal como se ilustra en el vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

En caso de que la página de Sites esté usando una plantilla estática, deberá configurarla en el sistema de párrafos de la página del sitio.

## Incrustación de un formulario adaptable {#af-component}

Para incrustar un formulario adaptable utilizando la variable **[!UICONTROL Forms adaptable: incrustar]** componente:

1. Abra la página de AEM Sites en la que desee incrustar un formulario adaptable en el modo Edición.
1. En el panel Navegador de componentes , arrastre y suelte el [!UICONTROL Forms adaptable: incrustar] en la página. También puede buscar un formulario adaptable en el Explorador de recursos y arrastrarlo y colocarlo en la página de Sites. Puede agregar un nuevo formulario adaptable o incrustar un formulario adaptable existente.

   >[!NOTE]
   >
   >Varios Forms adaptables: no se admiten los componentes incrustados en una página.

1. Para crear e incrustar un nuevo formulario, pulse el icono **Crear formulario** en la barra de herramientas de componentes. Se abre una ventana para crear el formulario.

1. Pulse el componente Forms adaptable integrado - Incrustar en la página Sitios y, a continuación, pulse ![settings_icon](assets/settings_icon.png) en la barra de acciones. La variable **[!UICONTROL Editar Forms adaptable: Incrustar]** se abre.
1. En el cuadro de diálogo Editar Forms adaptable - Incrustar , especifique lo siguiente.

   **Tipo de recurso:** seleccione el tipo de recurso que desea incrustar.
   * **Ruta del recurso**: examine y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si ha colocado el formulario desde el Explorador de recursos.
   * **Después del envío**: seleccione la acción que debe activarse después del envío del formulario. Puede elegir mostrar un mensaje o una página de agradecimiento.
      * Mostrar

      * **Mensaje de agradecimiento**: escriba un mensaje con el editor de texto enriquecido para mostrarlo después del envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página de agradecimiento**: examine y seleccione la página que desea mostrar después del envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
         * **Redirigir a la página de agradecimiento**: active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento sustituye al formulario adaptable en la [!UICONTROL Forms adaptable: incrustar] sin actualizar sitios subyacentes en la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Usar el idioma de la página**: utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
   * **Definir el enfoque del formulario**: seleccione esta opción para establecer el enfoque en el primer campo del formulario adaptable.
   * **Tema**: seleccione un tema que defina el estilo de los componentes del formulario adaptable. El estilo incluye propiedades de apariencia, como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **El formulario abarca toda la anchura del marco**: Si se selecciona, el iframe no se utiliza para procesar el formulario.
   * **Altura**: especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca de cliente CSS**: especifique la ruta a una biblioteca de cliente CSS.

1. Guarde la configuración. El formulario adaptable está ahora incrustado en la página.

AEM sitio también le permite crear un formulario adaptable sobre la marcha utilizando el componente Forms adaptable - Incrustar . Siga los pasos para crear un formulario adaptable utilizando la variable **Forms adaptable: componente incrustado** en AEM página sitios:
1. Abra la página de AEM Sites en la que desee incrustar un formulario adaptable en el modo Edición.
1. En el panel del navegador de componentes, arrastre y suelte el componente Forms adaptable - Incrustar en la página.
1. Haga clic en el **Más** y se le redirige al asistente de creación de formularios.

   ![Forms adaptable: componente incrustado](/help/forms/assets/aemformcontainer.png)

1. Ahora puede incrustar un formulario adaptable en AEM páginas del sitio mediante el [!UICONTROL Componente de contenedor de AEM Forms].

## Publicación de un formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios a la hora de publicar un formulario adaptable incrustado en una página de AEM Sites:

* Si publica la página de AEM Sites por primera vez y esta incluye un formulario adaptable incrustado, publique la página de Sites y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de Sites ya publicada, publique el recurso original, y los cambios se reflejarán en la página de Sites publicada. La página de Sites publicada incluye una referencia al recurso y no requiere que vuelva a publicar la página.
* Si ha modificado la página de Sites y el formulario adaptable integrado, vuelva a publicar la página y el recurso incrustado.

## Modificación de un formulario adaptable incrustado  {#modifying-embedded-adaptive-form}

AEM página sitios mantiene una referencia al formulario adaptable en la página Adaptable Forms - Incrustar. Por lo tanto, todas las configuraciones y propiedades configuradas en el formulario adaptable original, como el tema, los estilos y la acción de envío, se mantienen en el formulario adaptable incrustado.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en Formularios adaptables en los respectivos editores y agréguelo.
* Pulse el formulario adaptable desde la página de Sites en el modo Edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abrirá en el modo Edición, en el cual puede modificarlo.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejarán automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable o la página de Sites para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas de AEM Sites:

* El encabezado y el pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Forms enviado del Portal de Forms.
* La acción de envío configurada en el formulario original se mantiene en el formulario incrustado.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en esta aplicación. Sin embargo, no está disponible en el informe de análisis de Forms.
