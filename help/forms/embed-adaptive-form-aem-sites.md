---
title: '¿Cómo incrustar un formulario adaptable en una página de sitios AEM? '
description: Puede incrustar Forms adaptable en páginas AEM sitios. Los usuarios pueden rellenar y enviar formularios sin salir de las páginas del sitio.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---


# Incrustar un formulario adaptable en AEM página sitios {#embed-an-adaptive-form-or-interactive-communication-in-aem-sites-page}

[!DNL AEM Forms] permite a los desarrolladores de formularios incrustar Forms adaptable sin problemas en una página de AEM Sites o en una página web alojada fuera de AEM. El formulario adaptable integrado es completamente funcional y los usuarios pueden rellenar y enviar el formulario sin salir de la página. Ayuda al usuario a permanecer en el contexto de otros elementos de la página web e interactuar simultáneamente con el formulario .

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). -->

En la página AEM Sites, puede agregar un formulario adaptable mediante:

* **[[!DNL AEM Forms] Componente contenedor](#af-component)**
   [!DNL AEM Forms] proporciona un componente que puede agregar a las páginas del sitio. La variable [!DNL AEM Forms] El componente Contenedor le permite incrustar un formulario adaptable.

* **[Navegador de recursos](/help/forms/using/embed-adaptive-form-aem-sites.md#asset-browser)**
Todos los formularios que cree estarán disponibles en Assets. Puede arrastrar y soltar el formulario como un recurso en la página.

## Requisitos previos {#prerequisites}

Para incrustar un formulario adaptable en una página de sitios AEM que utilice una plantilla editable, asegúrese de que el componente Formulario AEM esté configurado como un componente permitido en la plantilla asociada. Para obtener más información, consulte **Política y propiedades (contenedor de diseño)** en [Creación de plantillas de página](/help/sites-authoring/templates.md).

En el caso de una página Sitios que use una plantilla estática, debe configurarla en el sistema de párrafos de la página del sitio. Consulte [Configuración de componentes en el modo Diseño](/help/sites-authoring/default-components-designmode.md) para obtener más información.

## Incrustación de un formulario adaptable  {#af-component}

Incrustación de un formulario adaptable mediante [!DNL AEM Forms] Componente contenedor:

1. Abra la página AEM sitios, en modo de edición, en la que desee incrustar un formulario adaptable .
1. En el panel Navegador de componentes , arrastre y suelte el [!DNL AEM Forms] Componente de contenedor en la página.

   También puede buscar un formulario adaptable en el explorador de Assets y arrastrarlo y colocarlo en la página Sitios . Incrusta el formulario en un [!DNL AEM Forms] Contenedor.

   >[!NOTE]
   >
   >Múltiple [!DNL AEM Forms] Los componentes de contenedor de una página no son compatibles.

1. Toque las [!DNL AEM Forms] Componente contenedor en la página Sitios y, a continuación, toque ![settings_icon](assets/settings_icon.png) en la barra de acciones. La variable **[!UICONTROL Editar contenedor de AEM Forms]** se abre.
1. En la sección Editar [!DNL AEM Forms] Cuadro de diálogo Contenedor , especifique lo siguiente.

   * **Tipo de recurso:** Seleccione el tipo de recurso que desea incrustar. Las opciones son Formulario adaptable
   * **Ruta de recursos**: Busque y seleccione el formulario adaptable que desea incrustar. Se rellena automáticamente si se ha soltado desde el explorador de Assets.
   * (sólo formulario adaptable) **Envío de anuncio**: Seleccione la acción a déclencheur en el envío del formulario. Puede elegir mostrar un mensaje de agradecimiento o una página de agradecimiento.

      * **Mensaje de agradecimiento**: Escriba un mensaje con el editor de texto enriquecido para mostrarlo en el envío del formulario. Esta opción solo está disponible cuando elige mostrar un mensaje de agradecimiento.
      * **Página de agradecimiento**: Busque y seleccione la página que desea mostrar en el envío del formulario. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
      * **Actualizar página en envío**: Active esta opción para actualizar la página que contiene el formulario adaptable incrustado y mostrar la página de agradecimiento. De lo contrario, la página de agradecimiento sustituye al formulario adaptable en la [!DNL AEM Forms] sin actualizar la página. Esta opción solo está disponible cuando elige mostrar una página de agradecimiento.
   * **Tema**: Seleccione un tema que defina el estilo para los componentes del formulario adaptable . El estilo incluye propiedades de aspecto como el estilo de fuente, el color de fondo, las dimensiones y la alineación.
   * **Altura**: Especifique la altura del contenedor. Déjelo en blanco para cambiar automáticamente el tamaño del contenedor.
   * **Biblioteca de cliente CSS**: Especifique la ruta a una biblioteca de cliente CSS.


1. Guarde la configuración. El formulario adaptable ahora está incrustado en la página.

## Publicar formulario adaptable incrustado {#publishing-embedded-adaptive-form}

Consideremos los siguientes escenarios para publicar un recurso incrustado (Formulario adaptable ) en AEM página de sitios:

* Si publica la página de AEM sitios por primera vez e incluye un formulario adaptable incrustado , publique la página de sitios y el recurso incrustado.
* Si ha modificado únicamente el formulario adaptable incrustado en una página de sitio publicada, publique el recurso original y los cambios se reflejarán en la página del sitio publicada. La página del sitio publicada incluye una referencia al recurso y no requiere que se vuelva a publicar la página.
* Si ha modificado la página Sitios y el formulario adaptable integrado , vuelva a publicar la página Sitios y el recurso incrustado.

## Modificación del formulario adaptable incrustado {#modifying-embedded-adaptive-form-and-interactive-communication}

AEM página sitios mantiene una referencia al formulario adaptable en el [!DNL AEM Forms] Contenedor. Por lo tanto, todas las configuraciones y propiedades, como el tema, los estilos y la acción de envío, configuradas en el formulario adaptable original se conservan en el formulario adaptable incrustado.

Para modificar cualquier configuración o propiedad del formulario adaptable incrustado, realice una de las siguientes acciones.

* Abra el formulario original en Adaptive Forms en los editores respectivos y edítelos.
* Pulse el formulario adaptable desde la página del sitio en modo de edición y, a continuación, pulse **[!UICONTROL Editar en una nueva ventana]**. El formulario original se abre en modo de edición que puede modificar.

>[!NOTE]
>
>Los cambios realizados en el formulario adaptable original se reflejan automáticamente en el formulario incrustado. Sin embargo, vuelva a publicar el formulario adaptable o la página del sitio para reflejar los cambios en la página publicada.

## Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Tenga en cuenta los siguientes puntos al incrustar Forms adaptable en páginas AEM sitios:

* El encabezado y pie de página del formulario original no se incluyen en el formulario incrustado.
* Los borradores de usuario y los envíos de formularios incrustados son compatibles y visibles en las fichas Borradores y Forms enviado del portal de formularios.
* La acción de envío configurada en el formulario original se conserva en el formulario incrustado.
* La segmentación de experiencias y las pruebas A/B configuradas en el formulario original no funcionan en el formulario incrustado. Sin embargo, puede utilizar la segmentación de experiencias en la página Sitios para presentar distintos formularios basados en perfiles de usuario.
* Si Adobe Analytics está configurado para el formulario original, los datos de análisis del formulario incrustado se capturan en Adobe Analytics. Sin embargo, no está disponible en el informe de análisis de formularios.

