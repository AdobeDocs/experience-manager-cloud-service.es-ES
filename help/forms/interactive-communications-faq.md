---
title: 'Preguntas más frecuentes: comunicaciones interactivas'
description: Preguntas frecuentes sobre las comunicaciones interactivas en AEM Forms as a Cloud Service, que abarcan patrones de visualización, anotaciones, comparación de versiones, etc.
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 4cc1bff3-edfb-4826-b914-2a2231b703f9
source-git-commit: 8043d0bd709962023f4828a6fffa2939788538b2
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# Preguntas más frecuentes: comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

## General

**Q: ¿Puedo importar un XDP existente en el editor de comunicaciones interactivas?**
Sí, puede importar un XDP existente y utilizarlo como punto de partida. Las funciones no admitidas se resaltan durante el proceso de importación.

**Q: ¿Está disponible el editor de comunicaciones interactivas para implementaciones locales?**
No, el editor solo está disponible para implementaciones de Forms as a Cloud Service.

## Patrones de visualización

**Q: ¿Qué es un patrón de visualización y en qué se diferencia de los enlaces de datos?**
Un patrón de visualización controla cómo se *presenta* un valor de campo a los usuarios en la vista previa del lienzo y en la salida generada; por ejemplo, si aplica formato a un número como moneda (1.234,21 $) o como cadena de texto como número de teléfono (555) 123-4567). El valor almacenado subyacente no cambia. Por el contrario, el enlace de datos controla *de dónde* proviene el valor del campo, conectando el campo a un modelo de datos o elemento de esquema.

**Q: ¿Qué tipos de campo admiten patrones de visualización?**
Los patrones de visualización son compatibles con los componentes Cuadro de texto, Campo numérico, Campo de fecha, Campo de fecha y hora y Variable no enlazada. Cada tipo de campo utiliza la sintaxis de cláusula de imagen XFA adecuada para su tipo de datos.

**Q: mi patrón de visualización de fecha no funciona; el campo muestra el valor sin procesar en lugar del resultado con formato. ¿Qué sucede?**
Los campos Fecha y Fecha/Hora requieren que el valor subyacente se ajuste al formato **ISO 8601**. Para los campos Fecha, proporcione valores en formato `YYYY-MM-DD` (por ejemplo, `2007-04-01`). Para los campos Fecha/Hora, use el formato `YYYY-MM-DDTHH:MM` (por ejemplo, `2007-04-01T14:30`). Los valores que no siguen la norma ISO 8601 se muestran tal cual, sin aplicar el patrón de visualización.

**Q: ¿Puedo definir un patrón personalizado que no esté en la lista predefinida?**
Sí. Puede escribir una **cláusula de imagen XFA** personalizada directamente en el campo Patrón de visualización del panel Propiedades. Consulte los símbolos de cláusula de imagen para cada tipo de campo en las páginas de referencia de componentes correspondientes.

## Revisión y anotaciones

**Q: ¿Cuál es la diferencia entre los comentarios y las anotaciones en las comunicaciones interactivas?**
**Los comentarios** son notas generales agregadas a una CI desde el panel Comentarios; se adjuntan al documento en su totalidad, no a componentes específicos. Las **anotaciones** están posicionadas, pines de revisión a nivel de componente: un revisor abre un lienzo de anotación de solo lectura, hace clic en cualquier componente del diseño y deja un comentario anclado a ese punto exacto. Todos los revisores comparten la misma vista de anotación. A continuación, los autores pueden marcar cada anotación como Resuelta desde el Editor IC.

**Q: ¿Puede un revisor editar accidentalmente la CI mientras deja anotaciones?**
No. El lienzo de anotación es una vista de solo lectura dedicada. Los revisores solo pueden agregar o ver anclajes de comentarios; no pueden modificar ningún componente de la CI.

**Q: ¿Qué sucede con una anotación después de marcarla como Resuelta?**
Las anotaciones resueltas permanecen visibles con fines de historial, pero aparecen como chinchetas cerradas (grises) que las distinguen visualmente de los elementos de comentarios abiertos (activos). Esto permite a los equipos realizar un seguimiento del progreso de la revisión sin perder la pista de auditoría.

**Q: ¿Se admiten anotaciones en todos los componentes?**
Todavía no. Actualmente no se admiten anotaciones en las partes de fragmento de un documento y en el componente Tabla. Las anotaciones en otros componentes son totalmente compatibles.

## Comparación de versiones

**Q: ¿Qué puedo ver al comparar dos versiones?**
Ambas versiones se abren en paralelo como vistas previas de PDF, para que pueda inspeccionar visualmente las diferencias de diseño y contenido estático. No se incluyen los valores de los campos dinámicos; solo se comparan el diseño procesado y el texto estático.

**Q: ¿Cómo se inicia una comparación de versiones?**
Vaya a **Forms > Forms y documentos**, seleccione la CI, haga clic en **Comparar versión** en la barra de herramientas de acciones y elija la versión que desea comparar. Se abre una nueva pestaña con ambas versiones mostradas una al lado de la otra.

**Q: ¿Puedo ver cambios de texto específicos dentro de un párrafo al comparar versiones?**
No. Si se ha reescrito o reorganizado un párrafo, ambas páginas se procesarán de forma idéntica a su PDF de origen. No hay diferencia de texto en línea: la comparación es solo visual.

## Tablas

**Q: ¿Puedo combinar celdas en una tabla?**
Sí. Seleccione dos o más celdas consecutivas dentro de la misma fila, haga clic con el botón derecho y elija **Combinar celdas**. Solo se pueden combinar celdas consecutivas dentro de la misma fila. Las combinaciones entre filas no son totalmente compatibles. Consulte [Combinar y dividir celdas de tabla](/help/forms/interactive-communication/howto/merge-and-split-table-cells.md).

**Q: ¿Puedo deshacer una combinación de celdas?**
Sí. Haga clic con el botón derecho en la celda combinada, seleccione **Dividir celda** y especifique el número de columnas en las que desea dividir (hasta el número original de celdas combinadas).

## Página maestra

**Q: ¿Cómo hago que un componente aparezca en todas las páginas de una comunicación interactiva?**
Mueva el componente a la página maestra. Haga clic con el botón derecho en un componente apto de una página de diseño y seleccione **Mover a > Página maestra**. El componente se quita de la página de diseño y se coloca en la página maestra en la misma posición visual, de modo que aparece de forma coherente en todas las páginas que comparten esa página maestra. Consulte [Mover un componente a la página maestra](/help/forms/interactive-communication/howto/move-component-to-master-page.md).

**Q: ¿Qué tipos de componentes no se pueden mover a la página maestra?**
Los siguientes tipos no son aptos para la acción Mover a página maestra: áreas de contenido, áreas de página, conjuntos de páginas, fragmentos, subformulario, filas de tabla, celdas de tabla y botones de opción. Los componentes con un bloqueo de contenido o de diseño aplicado tampoco son aptos.
