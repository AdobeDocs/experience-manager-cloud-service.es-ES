---
title: Uso de Ocultar condiciones
description: Las condiciones de ocultado se pueden utilizar para determinar si un recurso de componente se representa o no.
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 2%

---

# Uso de Ocultar condiciones {#using-hide-conditions}

Las condiciones de ocultado se pueden utilizar para determinar si un recurso de componente se representa o no. Un ejemplo de esto sería cuando un autor de plantillas configura el componente principal [componente de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) en el [editor de plantillas](/help/sites-cloud/authoring/features/templates.md) y decide desactivar las opciones para crear la lista en función de las páginas secundarias. Al desactivar esta opción en el cuadro de diálogo de diseño, se establece una propiedad de modo que, cuando se procesa el componente de lista, se evalúe la condición de ocultado y no se muestre la opción para mostrar páginas secundarias.

## Información general {#overview}

Los diálogos pueden llegar a ser muy complejos con numerosas opciones para el usuario, que sólo puede utilizar una fracción de las opciones a su disposición. Esto puede generar experiencias de interfaz de usuario abrumadoras para los usuarios.

Al utilizar condiciones ocultas, los administradores, desarrolladores y superusuarios pueden ocultar recursos en función de un conjunto de reglas. Esta función les permite decidir qué recursos deben mostrarse cuando un autor edita el contenido.

>[!NOTE]
>
>Ocultar un recurso basado en una expresión no reemplaza los permisos ACL. El contenido permanece editable, pero simplemente no se muestra.

## Detalles de implementación y uso {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` es responsable de filtrar los recursos en función de la existencia y el valor de la variable `granite:hide` , ubicada en el campo que se va a filtrar. La aplicación de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` incluye una instancia de `FilteringResourceWrapper.`

La implementación utiliza Granite [API de ELResolver](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) y añade un `cqDesign` variable personalizada mediante ExpressionCustomizer.

Estos son algunos ejemplos de condiciones de ocultamiento en un nodo de diseño ubicado en `etc/design` o como una directiva de contenido.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Al definir la expresión de ocultación, tenga en cuenta:

* Para que sea válido, se debe expresar el ámbito en el que se encuentra la propiedad (por ejemplo, `cqDesign.myProperty`).
* Los valores son de solo lectura.
* Las funciones (si es necesario) deben limitarse a un conjunto determinado proporcionado por el servicio.

## Ejemplo {#example}

Se pueden encontrar ejemplos de condiciones de ocultamiento en AEM y en la [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) en particular. Por ejemplo, considere la [componente principal de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) tal como se implementa en la variable [Tutorial de WKND.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[Uso del editor de plantillas](/help/sites-cloud/authoring/features/templates.md), el autor de la plantilla puede definir en el cuadro de diálogo de diseño qué opciones del componente de lista están disponibles para el autor de la página. Tales opciones como si se permite que la lista sea una lista estática, una lista de páginas secundarias, una lista de páginas etiquetadas, etc. se puede activar o desactivar.

Si un autor de plantillas decide desactivar la opción de páginas secundarias, se establece una propiedad de diseño y se evalúa una condición de ocultamiento en relación con ella, lo que hace que la opción no se muestre para el autor de la página.

1. De forma predeterminada, el autor de la página puede utilizar el componente principal de la lista para crear una lista utilizando páginas secundarias seleccionando la opción **Páginas secundarias**.

   ![Configuración de componentes de lista](assets/hide-conditions-list-settings.png)

1. En el cuadro de diálogo de diseño del componente principal de la lista, el autor de la plantilla puede elegir la opción **Deshabilitar hijos** para evitar que la opción para generar una lista basada en páginas secundarias se muestre al autor de la página.

   ![Cuadro de diálogo Diseño de componente de lista](assets/hide-conditions-list-design.png)

1. Se crea un nodo de directiva en `/conf/wknd/settings/wcm/policies/wknd/components/list` con una propiedad `disableChildren` configure como `true`.

   ![Estructura del nodo de la condición de ocultación](assets/hide-conditions-node-structure.png)

1. La condición hide se define como el valor de un `granite:hide` propiedad en el nodo de propiedad dialog `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Evaluación de la condición de ocultación](assets/hide-conditions-evaluation.png)

1. El valor de `disableChildren` se extrae de la configuración de diseño y de la expresión `${cqDesign.disableChildren}` evalúa como `false`, lo que significa que la opción no se procesará como parte del componente.

1. La opción **Páginas secundarias** ya no se representa para el autor de la página al utilizar el componente de lista.

   ![Componente de lista con opción secundaria desactivada](assets/hide-conditions-child-disabled.png)
