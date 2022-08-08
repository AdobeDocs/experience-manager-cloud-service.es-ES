---
title: Incrustar un formulario adaptable en la página de AEM Sites
seo-title: Hwo to add an Adaptive Form to an AEM Sites page?
description: Puede utilizar el componente Contenedor de AEM Forms para añadir o incrustar Forms adaptable a una página de AEM Sites para rellenar y enviar un formulario sin salir de las páginas de AEM Sites.
feature: Adaptive Forms
source-git-commit: dac38b2a90b2a1969e5332b8a658e8f1e0e5eccb
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# Incrustar un formulario adaptable en una página de sitios AEM {#embed-an-adaptive-form-to-aem-sites-page}

## Información general {#overview}

AEM Forms permite a los desarrolladores de formularios incrustar sin problemas formularios adaptables en una página de AEM Sites o en una página web alojada fuera de AEM. El formulario adaptable integrado es completamente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario.

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

En la página AEM Sites, puede agregar un formulario adaptable mediante:

* **[Componente Contenedor de AEM Forms](/help/forms/using/embed-adaptive-form-aem-sites.md#af-component)**
AEM Forms proporciona un componente que puede agregar a las páginas del sitio. El componente Contenedor de AEM Forms permite incrustar un formulario adaptable.

* **[Navegador de recursos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos los formularios están disponibles en Assets. Puede arrastrar y soltar el formulario como un recurso en la página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable en una página de AEM Sites que use una plantilla editable, asegúrese de que el componente AEM formulario esté configurado como un componente permitido en la plantilla asociada. Para obtener más información, consulte **Política y propiedades (contenedor de diseño)** en [Creación de plantillas de página](/help/sites-authoring/templates.md).

En el caso de una página Sitios que use una plantilla estática, debe configurarla en el sistema de párrafos de la página del sitio. Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

## Incrustación de un formulario adaptable {#af-component}

Para incrustar un formulario adaptable mediante el componente Contenedor de AEM Forms:

1. Abra la página AEM sitios, en modo de edición, en la que desee incrustar un formulario adaptable.
1. En el panel Navegador de componentes , arrastre y suelte el componente Contenedor de AEM Forms en la página. También puede buscar un formulario adaptable en el explorador de Assets y arrastrarlo y colocarlo en la página Sitios . Incrusta el formulario en un contenedor de AEM Forms. Puede crear y agregar un nuevo formulario adaptable o incrustar un formulario adaptable existente.

   >[!NOTE]
   >
   >No se admiten varios componentes de contenedor de AEM Forms en una página.

1. Para crear e incrustar un nuevo formulario, en la barra de herramientas de componentes, pulse el botón **Crear formulario** icono. Se abre una ventana para crear el nuevo formulario.

1. Pulse el componente Contenedor de AEM Forms incrustado en la página Sitios y, a continuación, pulse ![settings_icon](assets/settings_icon.png) en la barra de acciones. La variable **[!UICONTROL Editar contenedor de AEM Forms]** se abre.
1. En el cuadro de diálogo Editar contenedor de AEM Forms , especifique lo siguiente.

   <!-- * **Asset Type:** Select the type of asset to embed. The options are Adaptive Form -->
   * **Ruta de recursos**: Busque y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si se ha soltado desde el explorador de Assets.
   * **Envío de anuncio** : Seleccione la acción a déclencheur en el envío del formulario. Puede elegir mostrar un mensaje de agradecimiento o una página de agradecimiento.

      * **Mensaje de agradecimiento**: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página de agradecimiento**: Busque y seleccione la página que desea mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
         * **Redirigir a la página de agradecimiento**: Active la opción para reemplazar la página que contiene el formulario adaptable incrustado por una página de agradecimiento. De lo contrario, la página de agradecimiento sustituye al formulario adaptable en el contenedor de AEM Forms, sin actualizar los sitios subyacentes de la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Usar idioma de página**: Utilice la configuración local de la página de AEM Sites en lugar de la configuración regional del formulario adaptable.
   * **Definir enfoque del formulario**: Seleccione para definir el enfoque en el primer campo del formulario adaptable.

   * **Tema**: Seleccione un tema que defina el estilo para los componentes del formulario adaptable. El estilo incluye propiedades de aspecto como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **Altura**: Especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca de cliente CSS**: Especifique la ruta a una biblioteca de cliente CSS.

1. Guarde la configuración. El formulario adaptable ahora está incrustado en la página.

## Publicar formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios para publicar un formulario adaptable incrustado en AEM página de sitios:

* Si publica la página de AEM sitios por primera vez e incluye un formulario adaptable incrustado, publique la página de sitios y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de sitio publicada, publique el recurso original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al recurso y no requiere que se vuelva a publicar la página.
* Si ha modificado la página Sitios y el formulario adaptable integrado , vuelva a publicar la página Sitios y el recurso incrustado.

## Modificación del formulario adaptable incrustado  {#modifying-embedded-adaptive-form}

AEM página sitios mantiene una referencia al formulario adaptable en el contenedor de AEM Forms. Por lo tanto, todas las configuraciones y propiedades, como el tema, los estilos y la acción de envío, configuradas en el formulario adaptable original se conservan en el formulario adaptable incrustado .

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en formularios adaptables en los editores respectivos y agréguelo.
* Pulse el formulario adaptable desde la página del sitio en modo de edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abre en modo de edición que puede modificar.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejan automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable o la página del sitio para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar formularios adaptables en páginas AEM sitios:

* El encabezado y pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Forms enviado del portal de formularios.
* La acción de envío configurada en el formulario original se conserva en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Sin embargo, puede utilizar la segmentación de experiencias en la página Sitios para presentar distintos formularios basados en perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en Adobe Analytics. Sin embargo, no está disponible en el informe de análisis de formularios.
