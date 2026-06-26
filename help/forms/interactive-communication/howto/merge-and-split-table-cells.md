---
title: Combinar y dividir celdas de tabla en el editor de comunicaciones interactivas
description: Aprenda a combinar celdas de tabla adyacentes en una sola celda y a dividir una celda combinada de nuevo en varias columnas para crear diseños de tabla flexibles en el Editor de comunicaciones interactivas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Se aplica a AEM Forms."
exl-id: merge-split-table-cells-ic-editor
source-git-commit: b11e1b28aabba9e03553dc9e9394bff111facfee
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---


# Combinar y dividir celdas de tabla en el editor de comunicaciones interactivas

Las cuadrículas de tabla estándar son uniformes de forma predeterminada, cada fila tiene el mismo número de celdas del mismo tamaño. Muchos diseños del mundo real requieren más flexibilidad: un encabezado que abarque varias columnas, una fila de resumen que ocupe todo el ancho de la tabla o celdas agrupadas que unan visualmente los datos relacionados. Puede combinar celdas adyacentes en una fila para lograr estos diseños y dividir cualquier celda previamente combinada en columnas individuales cada vez que necesite revisar la estructura.

| Quién | Ventaja |
|-----|---------|
| **Autor (diseñador de comunicaciones interactivas/diseñador de diseño)** | Generar facturas, programaciones y tablas de comparación con encabezados de expansión o celdas agrupadas sin salir del Editor de comunicaciones interactivas. |

## Combinar celdas

1. En el Editor de comunicaciones interactivas, haga clic en la primera celda que desee incluir en la combinación.

1. Mantenga presionado **Shift** y haga clic en la última celda del rango para seleccionar todas las celdas consecutivas de la misma fila.

1. Haga clic con el botón derecho en la selección, seleccione **Combinar** y, a continuación, elija **Combinar celdas**.

   ![Combinar celdas](/help/forms/interactive-communication/assets/split-merge-table1.png)

   Las celdas seleccionadas se combinan en una sola celda combinada. El contenido y el formato de la primera celda de la selección se conservan; el contenido de las celdas siguientes se descarta.

   Por ejemplo, en una tabla Detalles del vehículo, puede combinar celdas consecutivas en la fila de encabezado para crear una etiqueta de expansión como **Detalles del vehículo**.

**Qué se debe tener en cuenta:**

- Solo puede combinar celdas consecutivas y dentro de la misma fila. No se admite la selección de celdas en varias filas.
- Después de la combinación sólo se conservan el contenido y el formato de la primera celda.

## Dividir una celda combinada

1. Haga clic con el botón secundario en la celda combinada que desee dividir.

1. Seleccione **Split** y, a continuación, elija **Split Cell**.

   ![Dividir celda](/help/forms/interactive-communication/assets/split-merge-table2.png)

1. En el cuadro de diálogo **Dividir celda**, escriba el número de columnas en las que dividir la celda.

1. Haga clic en **Aceptar** para aplicar.

   ![Cuadro de diálogo de celda dividida](/help/forms/interactive-communication/assets/split-merge-table3.png)

   El valor **Máximo de columnas** que se muestra en el cuadro de diálogo representa el máximo en el que puede dividirse, igual al número de celdas que se combinaron originalmente. Por ejemplo, si se combinaron dos celdas, **Máximo de columnas** es 2.

   | Valor de división | Resultado |
   |-------------|--------|
   | 2 | La celda se divide de nuevo en 2 celdas individuales |
   | 1 | La celda permanece como una sola celda (sin cambios) |

   La estructura de la tabla se actualiza automáticamente. Cualquier valor entre 1 y el valor **Máximo de columnas** es válido.

## Consideración

La combinación de celdas que abarcan varias filas no es totalmente compatible y puede producir resultados inesperados. Realizar operaciones de combinación solo en celdas consecutivas de la misma fila.

## Preguntas frecuentes

**¿Puedo combinar celdas en filas y columnas?**
No. Solo se pueden combinar celdas consecutivas de la misma fila. Las combinaciones entre filas (que abarcan varias filas) no son totalmente compatibles y pueden producir resultados inesperados.

**¿Qué sucede con el contenido de las celdas que combino?**
Se conservan el contenido y el formato de la primera celda de la selección. El contenido de las celdas restantes se descarta cuando se aplica la combinación.

**¿Cómo sé el número máximo de columnas en las que puedo dividir una celda combinada?**
El cuadro de diálogo de división muestra el valor **Máximo de columnas**, que es igual al número de celdas que se combinaron originalmente para crear la celda.

## Ver también

- [Componente Tabla en el editor de comunicaciones interactivas](/help/forms/interactive-communication/table.md)
- [Crear una tabla dinámica en el editor de comunicaciones interactivas](/help/forms/interactive-communication/dynamic-table-in-interactive-communication-editor.md)
- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)

