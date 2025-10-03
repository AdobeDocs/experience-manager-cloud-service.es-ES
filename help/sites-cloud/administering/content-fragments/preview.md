---
title: Previsualización de fragmentos de contenido
description: Obtenga información sobre cómo previsualizar los fragmentos de contenido mediante una serie de métodos.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: 3781b494394405f69892686790c17ffa9c69f28b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# Previsualización de fragmentos de contenido {#previewing-content-fragments}

Los fragmentos de contenido se pueden utilizar para la entrega sin encabezado y la creación de páginas. Como los fragmentos son únicamente contenido, sin formato, revisarlos puede ser más difícil. Por lo tanto, se proporcionan varios métodos para previsualizar los fragmentos en una variedad de escenarios.

Hay varios métodos disponibles para los fragmentos de contenido, accesibles desde la consola y el editor de fragmentos de consola. La consola y el editor descritos en esta sección se han desarrollado para la entrega de contenido sin encabezado (aunque se pueden utilizar para todos los escenarios).

Puede obtener una vista previa del fragmento:

* usando el [patrón de URL de vista previa](#preview-url-pattern)

* publicando y cancelando la publicación en la [instancia de vista previa](#preview-instance)

<!--
* with a HTML template, using **[Preview]()** from the Content Fragments console
-->

Por supuesto, también puede ver su fragmento en [Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md).

>[!IMPORTANT]
>
>Se puede acceder a los fragmentos de contenido desde dos consolas: **Fragmentos de contenido** y **Assets**.
>
>También hay dos editores para crear fragmentos de contenido; aunque la funcionalidad básica es la misma, hay algunas diferencias. Ambos editores son accesibles desde ambas consolas.
>
>Esta sección trata sobre la consola **Fragmentos de contenido** y el *nuevo* editor de fragmentos de contenido. Se han desarrollado para la entrega de contenido sin encabezado (aunque se pueden utilizar en todos los casos)
>
>Para obtener más información, consulte lo siguiente:
>
>* uso de la consola **Assets** para [administrar fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md)
>* uso del editor de fragmentos de contenido [*original*](/help/assets/content-fragments/content-fragments-variations.md),
>* uso de [fragmentos de contenido para la creación de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).

## Patrón de URL de vista previa {#preview-url-pattern}

El editor de fragmentos de contenido proporciona a los autores la opción de previsualizar sus ediciones en una aplicación de front-end externa.

Para utilizar esta función, primero debe:

* Trabaje con su equipo de TI para configurar la aplicación de front-end externa que procesará el fragmento de contenido consumiendo su salida JSON.

* Cuando se configura la aplicación de front-end externa, el **Patrón de URL de vista previa predeterminado** debe definirse como una [propiedad del modelo de fragmento de contenido apropiado](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#model-properties).

La URL de vista previa debe seguir este patrón:

    `https://<preview_url>?param=${expression}`

Las expresiones disponibles son:

* `${contentFragment.path}`
* `${contentFragment.model.path}`
* `${contentFragment.model.name}`
* `${contentFragment.variation}`
* `${contentFragment.id}`

Una vez definida la dirección URL, el botón **[Vista previa](/help/sites-cloud/administering/content-fragments/authoring.md#preview-content-fragment)** está activo en la barra de herramientas superior del editor. Puede seleccionar este botón para iniciar la aplicación externa (en una pestaña independiente) para procesar el fragmento de contenido.

## Previsualizar instancia {#preview-instance}

Puede **publicar** y **cancelar la publicación** de su fragmento en el **[servicio de vista previa](/help/headless/deployment/architecture.md)** (así como en su instancia de publicación).

Puede publicar el fragmento desde el editor o desde la consola.

Consulte:

* [Publicación y vista previa de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) para obtener información detallada.

* [Cancelando la publicación de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) para obtener información detallada.

<!--
## Preview based on a HTML Template {#preview-based-on-a-html-template}

The Content Fragment console provides a **Preview** option for every fragment.

The icon can be selected to open a dialog that represents the fragment based on a HTML template. You can use the default template, or develop and load your own.
-->
