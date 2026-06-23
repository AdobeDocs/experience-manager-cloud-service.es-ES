---
title: Mover un componente a la página maestra
description: Aprenda a mover un componente de una página de diseño a la página maestra para que aparezca de forma coherente en todas las páginas de una comunicación interactiva.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: move-component-to-master-page-ic-editor
source-git-commit: 38a10bc5caaa1615188d2e6623b9d432bd4c3d69
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 2%

---


# Mover un componente a la página maestra

La página maestra de una comunicación interactiva define elementos que se repiten en todas las páginas, encabezados, pies de página, marcas de agua, números de página y cualquier otro contenido que deba aparecer de forma coherente en todo el documento. Por el contrario, los componentes que se encuentran en páginas de diseño individuales solo aparecen en esas páginas específicas.

Si diseña un componente en una página normal y posteriormente decide que pertenece a cada página, puede moverlo directamente a la página maestra desde el lienzo sin tener que eliminarlo y volver a crearlo. El componente se coloca en la misma posición visual que ocupaba en la página de diseño.

| Quién | Ventaja |
|-----|---------|
| **Autor (diseñador de comunicaciones interactivas)** | Promocione un componente a cada página en una acción en lugar de duplicarlo manualmente en las páginas de diseño. |
| **Diseñador de plantillas** | Refine la estructura de la plantilla después del diseño inicial sin volver a crear los componentes desde cero. |

## Mover un componente a la página maestra

Un caso de uso común es mover elementos de encabezado repetidos, como un **logotipo bancario** y una **dirección bancaria**, de una página de diseño a la página maestra para que aparezcan en todas las páginas de la comunicación interactiva.

1. Abra la comunicación interactiva en el Editor de comunicaciones interactivas.

1. En la ficha **Diseño**, vaya a la página de diseño que contiene los componentes que desea mover.

1. Haga clic con el botón derecho en el componente del lienzo.

   Por ejemplo, haga clic con el botón derecho en el bloque de texto de la dirección del banco.

1. En el menú contextual, seleccione **Mover a** y luego elija **Página maestra**.

   ![Mover a la página maestra](/help/forms/interactive-communication/assets/move-to-master-page.png)

   El componente se quita de la página de diseño y se agrega a la página maestra en la misma posición visual. Ahora aparece en todas las páginas que utilizan esa página maestra.

1. Repita los pasos 3 y 4 para cada componente que desee en la página maestra.

   Por ejemplo, después de mover la dirección del banco, repita los mismos pasos para mover el logotipo del banco.

1. Seleccione la ficha **Principal** para comprobar que el logotipo y la dirección del banco aparecen en las posiciones esperadas.

   ![Mover a la página maestra](/help/forms/interactive-communication/assets/move-to-master-page2.png)

## Componentes aptos

No todos los tipos de componentes se pueden mover a la página maestra. Los siguientes tipos son **no elegibles** para esta acción:

| Tipo de componente no apto | Motivo |
|---------------------------|--------|
| Áreas de contenido | Defina las regiones donde fluye el contenido de la página de diseño; debe permanecer en páginas de diseño |
| Áreas de página | Contenedores de página estructurales vinculados a páginas individuales |
| Conjuntos de páginas | Agrupaciones de varias páginas; no se pueden mover de forma independiente |
| Fragmentos | Bloques de documento reutilizables administrados de forma independiente |
| Subformulario | Componentes de contenedor con su propio ámbito de diseño |
| Filas de tabla | Elementos de nivel de fila que pertenecen a una estructura de tabla |
| Celdas de tabla | Elementos de nivel de celda que pertenecen a una estructura de tabla |
| Botones de opción | Controles de selección que forman parte de una estructura de datos de formulario |

Los componentes con **bloqueo de contenido** o **bloqueo de diseño** aplicado tampoco son aptos. Elimine el bloqueo antes de moverlo o planifique la ubicación del componente en la página maestra al diseñar la plantilla. Ver [Bloqueo de plantilla en el editor de comunicaciones interactivas](/help/forms/interactive-communication/enable-template-lock.md).

## Preguntas frecuentes

**¿Cuál es la diferencia entre colocar un componente en la página maestra y copiarlo en todas las páginas de diseño?**
Un componente de la página principal se administra en un lugar: cualquier modificación que realice allí se aplicará automáticamente a todas las páginas que utilicen esa página principal. Las copias en páginas de diseño individuales deben actualizarse por separado, lo que hace que el mantenimiento sea propenso a errores y lleve tiempo.

**¿Puedo volver a mover un componente de la página maestra a una página de diseño?**
No hay ninguna acción directa de &quot;retroceder&quot;. Para devolver un componente a una página de diseño específica, agregue una nueva instancia de ese tipo de componente a la página de diseño y elimínelo de la página maestra.

**¿Por qué en el menú que aparece al hacer clic con el botón derecho en mi componente no se muestra Mover a > Página maestra?**
Es posible que el tipo de componente no sea apto (consulte la tabla de idoneidad anterior) o que el componente tenga aplicado un bloqueo de contenido o de diseño. Compruebe ambas condiciones y elimine cualquier bloqueo antes de intentarlo de nuevo. Mueva cada componente apto por separado; por ejemplo, mueva el logotipo del banco y la dirección del banco de uno en uno.

## Ver también

- [Implementar la numeración de páginas dinámica en el editor de comunicaciones interactivas](/help/forms/interactive-communication/implement-dynamic-page-numbering.md)
- [Bloqueo de plantilla en el Editor de comunicaciones interactivas](/help/forms/interactive-communication/enable-template-lock.md)
- [Crear una plantilla de comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication-template.md)
- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)
