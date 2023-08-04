---
title: Personalizar vistas de propiedades de página
description: Obtenga información sobre cómo los autores ven y editan las propiedades de la página.
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# Personalizar vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-cloud/authoring/fundamentals/page-properties.md) que los usuarios pueden ver y editar. Algunos son necesarios al crear la página (vista de creación), otros se pueden ver y editar (vista de edición) en una fase posterior. Estas propiedades de página se definen y se ponen a disposición mediante el cuadro de diálogo (`cq:dialog`) del componente de página correspondiente.

El estado predeterminado de cada propiedad de página es:

* Oculto en la vista Crear (por ejemplo, **Crear página** wizard)

* Disponible en la vista de edición (por ejemplo, **Ver propiedades**)

Los campos deben configurarse específicamente si se requiere algún cambio. Esto se realiza mediante las propiedades de nodo adecuadas:

* Propiedad de página que estará disponible en la vista de creación (por ejemplo, **Crear página** asistente):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* La propiedad Page estará disponible en la vista de edición, como **Ver**/**Editar**  **Propiedades** opción:

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Consulte la [Tutorial sobre Ampliación de propiedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía para personalizar las propiedades de la página.

## Configuración de las propiedades de página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo adecuadas.

Por ejemplo, de forma predeterminada la variable [**Crear página** asistente](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) muestra los campos agrupados bajo **Más títulos y descripciones**. Para ocultarlos, configure lo siguiente:

1. Cree su componente de página en `/apps`.
1. Creación de una anulación (mediante *diff de diálogo* proporcionadas por el [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md)) para el `basic` de su componente de página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Configure las variables `path` propiedad en `basic` para señalar a la anulación de la pestaña básica (consulte el paso siguiente también). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación de `basic` - `moretitles` en la ruta correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo adecuada:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   El **Más títulos y descripciones** ya no se mostrará en la sección **Crear página** asistente.

>[!NOTE]
>
>Al configurar las propiedades de página para utilizarlas con Live Copies, consulte el documento [Ampliación del Administrador de varios sitios](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de diálogo del [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md) incluido el uso de [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). También ilustra el uso de ambos `cq:showOnCreate` y `cq:hideOnEdit`.

Puede encontrar el código de esta página en [GitHub.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
