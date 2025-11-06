---
title: Personalización de las vistas de propiedades de página
description: Obtenga información sobre cómo los autores ven y editan las propiedades de la página.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# Personalización de las vistas de propiedades de página{#customizing-views-of-page-properties}

Cada página tiene un conjunto de [propiedades](/help/sites-cloud/authoring/sites-console/page-properties.md) que los usuarios pueden ver y editar. Algunos son necesarios al crear la página (vista de creación), otros se pueden ver y editar (vista de edición) en una fase posterior. Estas propiedades de página se definen y se ponen a disposición mediante el cuadro de diálogo (`cq:dialog`) del componente de página correspondiente.

El estado predeterminado de cada propiedad de página es:

* Oculto en la vista de creación (por ejemplo, **Asistente para crear página**)

* Disponible en la vista de edición (por ejemplo, **Ver propiedades**)

Los campos deben configurarse específicamente si se requiere algún cambio. Esto se realiza mediante las propiedades de nodo adecuadas:

* Propiedad de página que estará disponible en la vista de creación (por ejemplo, **Asistente para crear página**):

   * Nombre: `cq:showOnCreate`
   * Tipo: `Boolean`

* La propiedad de página estará disponible en la vista de edición, como la opción **Ver**/**Editar** **Propiedades**:

   * Nombre: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Consulte el tutorial [Ampliación de propiedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obtener una guía sobre cómo personalizar las propiedades de página.

## Configuración de las propiedades de página {#configuring-your-page-properties}

También puede configurar los campos disponibles configurando el cuadro de diálogo del componente de página y aplicando las propiedades de nodo adecuadas.

Por ejemplo, de forma predeterminada, el asistente [**Crear página**](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) muestra los campos agrupados en **Más títulos y descripción**. Para ocultarlos, configure lo siguiente:

1. Cree su componente de página en `/apps`.
1. Cree una anulación (usando *dialog diff* proporcionada por la [Fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md)) para la sección `basic` del componente de su página; por ejemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Establezca la propiedad `path` en `basic` para que apunte a la anulación de la ficha básica (vea también el paso siguiente). Por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Cree una anulación de la sección `basic` - `moretitles` en la ruta de acceso correspondiente; por ejemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique la propiedad de nodo adecuada:

   * **Nombre**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   La sección **Más títulos y descripciones** ya no se mostrará en el asistente **Crear página**.

>[!NOTE]
>
>Al configurar las propiedades de página para usarlas con Live Copies, consulte [Ampliación del Administrador de varios sitios](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) para obtener más información.

## Configuración de muestra de las propiedades de página {#sample-configuration-of-page-properties}

Este ejemplo muestra la técnica de diferencia de diálogo de la [fusión de recursos de Sling](/help/implementing/developing/introduction/sling-resource-merger.md), incluido el uso de [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). También ilustra el uso de `cq:showOnCreate` y `cq:hideOnEdit`.

Puedes encontrar el código de esta página en [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
