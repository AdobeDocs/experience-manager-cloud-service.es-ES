---
title: Previsualización de fragmentos de contenido
description: Obtenga información sobre cómo previsualizar los fragmentos de contenido mediante una serie de métodos.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
badgeSaas: label="AEM Sites" type="Positive" tooltip="(Se aplica a AEM Sites)."
exl-id: 40c02806-76a2-43ed-982c-0410c2125a36
source-git-commit: 5413e173ac159015f224845e238779c5dc997ee5
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# Previsualización de fragmentos de contenido {#previewing-content-fragments}

Los fragmentos de contenido se pueden utilizar para la entrega sin encabezado y la creación de páginas. Como los fragmentos son únicamente contenido, sin formato, revisarlos puede ser más difícil. Por lo tanto, se proporcionan varios métodos para previsualizar los fragmentos en una variedad de escenarios.

Hay varios métodos disponibles para los fragmentos de contenido, accesibles desde la consola y el editor de fragmentos de consola. La consola y el editor descritos en esta sección se han desarrollado para la entrega de contenido sin encabezado (aunque se pueden utilizar para todos los escenarios).

Puede obtener una vista previa del fragmento:

* publicando y cancelando la publicación en la [instancia de vista previa](#preview-instance)

* en una [aplicación externa](#preview-url-pattern), utilizando el [patrón de URL de vista previa](#preview-url-pattern)

* con una [plantilla de visualización (HTML)](#preview-with-visualization-html-templates)

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

## Previsualizar instancia {#preview-instance}

Puede **publicar** y **cancelar la publicación** de su fragmento en el **[servicio de vista previa](/help/headless/deployment/architecture.md)** (así como en su instancia de publicación).

Puede publicar el fragmento desde el editor o desde la consola.

Consulte:

* [Publicación y vista previa de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment) para obtener información detallada.

* [Cancelando la publicación de un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#unpublishing-a-fragment) para obtener información detallada.

## Vista previa en una aplicación externa {#preview-in-an-external-application}

El editor de fragmentos de contenido proporciona a los autores la opción de previsualizar sus ediciones en una aplicación de front-end externa.

### Patrón de URL de vista previa {#preview-url-pattern}

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

### Vista previa en la aplicación externa {#preview-in-the-external-application}

Puede obtener una vista previa de un fragmento de contenido en una aplicación externa:

>[!NOTE]
>
>[Patrón de URL de vista previa](#preview-url-pattern) debe estar configurado para esta opción.

1. En la consola Fragmento de contenido vaya a la ubicación del fragmento.
1. Abra el fragmento en el editor
1. Seleccione **Vista previa** en la barra de herramientas superior.
1. Seleccione **Aplicación** para abrir el fragmento en la aplicación externa; por ejemplo, el [Editor universal](/help/implementing/universal-editor/introduction.md).

## Vista previa con plantillas de visualización (HTML) {#preview-with-visualization-html-templates}

<!-- CQDOC-23232 - remove when GA -->

>[!NOTE]
>
>Los fragmentos de contenido visual están actualmente en disponibilidad limitada.
>
>Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [experience-production-agent@adobe.com](mailto:experience-production-agent@adobe.com).

AEM le permite obtener una vista previa del fragmento de contenido mediante un diseño visual basado en una plantilla de HTML.

Consulte [Fragmentos de contenido visual](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md) para obtener detalles sobre cómo [obtener una vista previa del fragmento con plantillas](/help/sites-cloud/administering/content-fragments/visual-content-fragments.md#preview-your-template-with-a-template).

>[!NOTE]
>
>Consulte [Fragmentos de contenido visual: plantillas](/help/implementing/developing/extending/content-fragments-visualization-templates.md) para obtener más información sobre cómo crear, personalizar y cargar sus propias plantillas de HTML.

