---
title: Personalización de consolas
description: Obtenga información sobre las distintas opciones que proporciona AEM para personalizar las consolas de la instancia de creación.
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Personalización de consolas {#customizing-consoles}

AEM proporciona opciones para personalizar las consolas (y la [funcionalidad de creación de páginas](/help/implementing/developing/extending/page-authoring.md)) de su instancia de creación.

## Clientlibs {#clientlibs}

Clientlibs le permite ampliar la implementación predeterminada para ofrecer nuevas funcionalidades, mientras reutiliza funciones, objetos y métodos estándar. Al personalizar con clientlibs, puede crear su propia clientlib en `/apps.`. Por ejemplo, puede contener el código necesario para el componente personalizado.

Ver [Uso de bibliotecas del lado del cliente en AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Superposiciones {#overlays}

Las superposiciones se basan en definiciones de nodo y le permiten superponer la funcionalidad estándar que se encuentra en `/libs` con su propia funcionalidad personalizada en `/apps`. Al crear una superposición, no se requiere una copia 1:1 del original, ya que la [fusión de recursos Sling](/help/implementing/developing/introduction/sling-resource-merger.md) permite la herencia.

Las superposiciones se pueden utilizar de muchas maneras para ampliar las consolas de AEM. En las secciones siguientes se proporcionan varios ejemplos.

Ver también [Superposiciones para Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

>[!TIP]
>
>Si está interesado en opciones para personalizar la experiencia de creación, consulte [Personalización de la creación de páginas](/help/implementing/developing/extending/page-authoring.md).

## Personalización de la Vista Predeterminada para una Consola {#customizing-the-default-view-for-a-console}

Puede personalizar la vista predeterminada (columna, tarjeta, lista) de una consola:

* Puede reordenar las vistas superponiendo la entrada requerida en:

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * La primera entrada es la predeterminada.

   * Los nodos disponibles se correlacionan con las opciones de vista disponibles:

      * `column`
      * `card`
      * `list`

* Por ejemplo, en una superposición para una lista:

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * Defina la siguiente propiedad:

      * **Nombre**: `sling:orderBefore`
      * **Tipo**: `String`
      * **Valor**: `column`

### Agregar una nueva acción a la barra de herramientas {#add-a-new-action-to-the-toolbar}

Puede crear sus propios componentes e incluir las bibliotecas de cliente correspondientes para las acciones personalizadas.

* Por ejemplo, es posible que desee crear una acción **Promocionar a medios sociales** en:

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * A continuación, se puede conectar a un elemento de la barra de herramientas de la consola:

   * `/apps/<yourProject>/admin/ext/launches`

   * Por ejemplo, en el modo de selección:

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### Restringir una acción de barra de herramientas a un grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

Puede utilizar una condición de procesamiento personalizada para superponer la acción estándar e imponer condiciones específicas que deben cumplirse antes de que se procese.

Por ejemplo, puede que desee crear un componente para controlar las condiciones de procesamiento según un grupo:

* `/apps/myapp/components/renderconditions/group`

Para aplicar esto a la acción **Crear sitio** en la consola Sitios:

* `/libs/wcm/core/content/sites`

1. Cree la superposición:

   * `/apps/wcm/core/content/sites`

1. A continuación, añada la condición de procesamiento para la acción:

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

Con las propiedades de este nodo puede definir `groups` que tiene permiso para realizar la acción específica; por ejemplo, `administrators`

### Personalización de columnas en la vista de lista {#customizing-columns-in-list-view}

Para personalizar las columnas en la vista de lista:

1. Superponga la lista de columnas disponibles.

   * En el nodo:

     `/apps/wcm/core/content/common/availablecolumns`

1. Añada las columnas nuevas o elimine las existentes.

Si desea insertar datos adicionales, debe escribir [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con una propiedad `pageInfoProviderType`.

>[!NOTE]
>
>Esta función está optimizada para columnas de campos de texto. Para otros tipos de datos es posible superponer `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` en `/apps`.

### Filtrado de recursos {#filtering-resources}

Al utilizar una consola, un usuario debe seleccionar a menudo entre recursos como páginas, componentes o recursos. Esto puede adoptar la forma de una lista desde la que el autor debe elegir un elemento.

Para mantener la lista a un tamaño razonable y también relevante para el caso de uso, se puede implementar un filtro en forma de predicado personalizado. Consulte [Personalización de la creación de páginas](/help/implementing/developing/extending/page-authoring.md#filtering-resources) para obtener más información.
