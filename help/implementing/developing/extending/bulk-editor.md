---
title: Configuración de la edición masiva de propiedades de página
description: Aprenda a configurar la edición masiva para poder editar las propiedades de varias páginas a la vez.
exl-id: 0d10c6b9-8643-479d-adc1-4066d227e83d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# Configuración de la edición masiva de propiedades de página {#configuring-bulk-editing-of-page-properties}

[La edición masiva de propiedades de página](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#from-the-sites-console-multiple-pages) le permite editar las propiedades de varias páginas a la vez.

## Consideraciones {#considerations}

Las propiedades de página no están habilitadas para la edición por lotes de forma predeterminada. Deben habilitarse explícitamente. Al definir las propiedades de página para que estén disponibles para la edición masiva, debe tener en cuenta determinadas implicaciones, como:

* Algunos campos suelen ser únicos. Debe decidir si es significativo habilitar estos campos para la edición masiva, cuando se aplica un valor.
   * Por ejemplo, los títulos de las páginas casi siempre son únicos.
* Algunos campos pueden tener varios valores, lo que requiere una representación significativa al procesar.
   * Por ejemplo, un menú desplegable de estado etiquetado **Listo para publicación**. Esto puede tener varios valores antes de la edición en lotes, como **listo**, **en revisión**, **en curso**, etc.

Debido a la posibilidad de varios valores, se recomienda habilitar únicamente los siguientes tipos de campo para la edición masiva.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Activación de un campo {#enabling-a-field}

Estos pasos utilizan `/apps/core/wcm/components/page/v1/page` del [contenido de muestra WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) como ejemplo para habilitar la edición en lotes en un campo de un entorno de desarrollo.

1. Con CRXDE, abra el componente de página.
1. Vaya al campo requerido dentro de la definición de `cq:dialog`.
1. Defina la siguiente propiedad en el nodo de campo:

   * **Nombre**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

1. Seleccione **Guardar todo** para mantener las actualizaciones.

## Limitaciones {#limitations}

La edición masiva de las propiedades de página es:

* No disponible para páginas dentro de una Live Copy.
* Solo está disponible para páginas con el mismo tipo de recurso.
