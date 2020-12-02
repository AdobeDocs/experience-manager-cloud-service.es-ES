---
title: Uso de Ocultar condiciones
description: Las condiciones de ocultación se pueden utilizar para determinar si un recurso de componente se procesa o no.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 4%

---


# Uso de Ocultar condiciones {#using-hide-conditions}

Las condiciones de ocultación se pueden utilizar para determinar si un recurso de componente se procesa o no. Un ejemplo de esto sería cuando un autor de una plantilla configura el componente principal [componente de lista](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html) en el [editor de plantillas](/help/sites-cloud/authoring/features/templates.md) y decide deshabilitar las opciones para generar la lista en base a las páginas secundarias. Al desactivar esta opción en el cuadro de diálogo de diseño, se establece una propiedad para que, cuando se procese el componente de lista, se evalúe la condición de ocultar y no se muestre la opción de mostrar páginas secundarias.

## Información general {#overview}

Los diálogos pueden llegar a ser muy complejos con numerosas opciones para el usuario, que sólo puede utilizar una fracción de las opciones disponibles. Esto puede generar experiencias de interfaz de usuario abrumadoras para los usuarios.

Al utilizar condiciones de ocultación, los administradores, desarrolladores y superusuarios pueden ocultar recursos en función de un conjunto de reglas. Esta función les permite decidir qué recursos deben mostrarse cuando un autor edita el contenido.

>[!NOTE]
>
>Ocultar un recurso basado en una expresión no reemplaza los permisos de ACL. El contenido permanece editable, pero simplemente no se muestra.

## Detalles de implementación y uso {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` es responsable de filtrar los recursos en función de la existencia y el valor de la  `granite:hide` propiedad, ubicada en el campo que se va a filtrar. La implementación de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` incluye una instancia de `FilteringResourceWrapper.`

La implementación utiliza la API de Granite [ELResolver](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) y agrega una variable personalizada `cqDesign` mediante ExpressionCustomizer.

Estos son algunos ejemplos de condiciones ocultas en un nodo de diseño ubicado en `etc/design` o como una Política de contenido.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Al definir la expresión de ocultar, tenga en cuenta:

* Para que sea válido, debe expresarse el ámbito en que se encuentra la propiedad (por ejemplo, `cqDesign.myProperty`).
* Los valores son de solo lectura.
* Las funciones (si es necesario) deben limitarse a un conjunto determinado proporcionado por el servicio.

## Ejemplo {#example}

Se pueden encontrar ejemplos de condiciones de ocultación en todo el AEM y en los [componentes principales](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) en particular. Por ejemplo, considere el [componente principal de lista](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html) tal como se implementa en el tutorial [WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[Con el editor](/help/sites-cloud/authoring/features/templates.md) de plantillas, el autor de la plantilla puede definir en el cuadro de diálogo de diseño qué opciones del componente de lista están disponibles para el autor de la página. Opciones como si se permite que la lista sea una lista estática, una lista de páginas secundarias, una lista de páginas etiquetadas, etc. se puede habilitar o deshabilitar.

Si el autor de una plantilla decide desactivar la opción de páginas secundarias, se establece una propiedad de diseño y se evalúa una condición de ocultado en relación con ella, lo que provoca que la opción no se muestre para el autor de la página.

1. De forma predeterminada, el autor de la página puede utilizar el componente principal de lista para crear una lista mediante páginas secundarias seleccionando la opción **Páginas secundarias**.

   ![Ajustes del componente lista](assets/hide-conditions-list-settings.png)

1. En el cuadro de diálogo de diseño del componente principal de lista, el autor de la plantilla puede elegir la opción **Deshabilitar elementos secundarios** para evitar que la opción de generar una lista basada en páginas secundarias se muestre al autor de la página.

   ![Cuadro de diálogo de diseño de componente de lista](assets/hide-conditions-list-design.png)

1. Se crea un nodo de directiva en `/conf/wknd/settings/wcm/policies/wknd/components/list` con una propiedad `disableChildren` establecida en `true`.

   ![Estructura de nodos de la condición de ocultar](assets/hide-conditions-node-structure.png)

1. La condición hide se define como el valor de una propiedad `granite:hide` en el nodo de propiedad de cuadro de diálogo `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Evaluación de la condición de ocultar](assets/hide-conditions-evaluation.png)

1. El valor de `disableChildren` se extrae de la configuración de diseño y la expresión `${cdDesign.disableChildren}` se evalúa como `false`, lo que significa que la opción no se procesará como parte del componente.

1. La opción **Páginas secundarias** ya no se representa para el autor de la página al usar el componente lista.

   ![Componente de lista con opción secundaria deshabilitada](assets/hide-conditions-child-disabled.png)
