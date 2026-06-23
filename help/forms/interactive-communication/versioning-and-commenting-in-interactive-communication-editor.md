---
title: Crear versiones y comentarios en el editor de comunicaciones interactivas
description: Las versiones y los comentarios del editor de comunicaciones interactivas de AEM Forms permiten a las organizaciones crear documentos dinámicos impulsados por datos para una comunicación personalizada con los clientes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: ca9917c0-d8bb-4381-afab-7ab888d992e8
source-git-commit: efdfec8f3ce63a2931a78eeb4be3820e22b13a8d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# Crear versiones y comentarios en el editor de comunicaciones interactivas


Las comunicaciones interactivas permiten a las organizaciones crear documentos dinámicos basados en datos para una comunicación personalizada con los clientes. Para admitir una mejor colaboración, administración y flujos de trabajo de publicación controlados, el editor de comunicaciones interactivas proporciona funciones de versiones, revisión y comentarios.

Estas funciones ayudan a los autores a administrar varias iteraciones de una comunicación interactiva, capturar los comentarios de los revisores, volver a versiones anteriores y mantener un registro de auditoría claro durante todo el ciclo de vida del contenido.

## Versiones de comunicación interactiva

El control de versiones en el Editor de comunicaciones interactivas permite a los autores:

- Crear varias versiones de una comunicación interactiva

- Guardar cambios incrementales con etiquetas y comentarios significativos

- Revertir a cualquier versión anterior

- Comparar diferencias visualmente

- Mantener un control limpio para los ciclos de revisión, aprobación y publicación

Esto garantiza que los autores puedan experimentar, iterar y refinar los diseños de la comunicación interactiva a la vez que preservan el contexto histórico completo.

## Crear una versión de una comunicación interactiva

Utilice el control de versiones cuando desee conservar el estado actual de una comunicación interactiva antes de realizar actualizaciones.

Para crear una nueva versión:

1. Vaya a **Forms y documentos** y seleccione la comunicación interactiva que desee modificar.

1. En la esquina superior izquierda de la vista de recursos, seleccione la opción de carril y, a continuación, elija **Cronología** en las opciones del panel.

   ![Crear versión 1](/help/forms/interactive-communication/assets/create-version1.png)

1. El panel **Línea de tiempo** se abre a la izquierda y muestra el historial de actividades de la comunicación interactiva seleccionada, incluidas las anotaciones y las versiones anteriores.

   Por ejemplo, después de un ciclo de revisión, la cronología puede mostrar anotaciones como **actualizar dirección** y **Actualizar modelo del carro** junto con otras entradas de la actividad.

   ![Crear versión 2](/help/forms/interactive-communication/assets/create-version2.png)

1. En la parte inferior del panel **Cronología**, haga clic en **Guardar como versión**.

1. En el cuadro de diálogo **Crear nueva versión**, escriba una etiqueta de versión y un comentario opcional que describa el propósito o los cambios en esta versión.

   Por ejemplo, escriba **Incluye el nuevo logotipo del banco** como comentario de la versión.

   ![Crear versión 3](/help/forms/interactive-communication/assets/create-version3.png)

1. Haga clic en **Crear**.

   La entrada de nueva versión aparece en la cronología y un mensaje de éxito confirma que la versión se ha creado.

   ![Crear versión 4](/help/forms/interactive-communication/assets/create-version4.png)

Se agrega una nueva entrada de versión a la lista de versiones, que captura el estado actual de la comunicación interactiva.

## Actualizar una versión

Cada vez que modifique y guarde la comunicación interactiva, puede crear una nueva versión para capturar el estado actualizado.

Para agregar una nueva versión después de editar:

1. Abra **Forms y documentos** y seleccione la comunicación interactiva.

1. Abra el panel **Línea de tiempo** desde el carril izquierdo.

1. Siga los pasos de [Crear una versión de una comunicación interactiva](#create-a-version-of-an-interactive-communication) para guardar el estado actual con una etiqueta y un comentario nuevos.

Esto ayuda a los equipos a realizar un seguimiento del progreso y garantiza la transparencia en el ciclo vital.

## Revertir a una versión anterior

Si una comunicación interactiva debe volver a una configuración anterior:

1. Vaya a **Forms y documentos** y seleccione la comunicación interactiva.

1. Abra el panel **Línea de tiempo** desde el carril izquierdo.

1. En la cronología, seleccione la versión que desee restaurar. Por ejemplo, seleccione **Comunicación interactiva bancaria V1** con el comentario **Incluye el nuevo logotipo del banco**.

   ![Revertir versión 1](/help/forms/interactive-communication/assets/create-version5.png)

1. Haga clic en **Revertir a esta versión**.

   Un mensaje de éxito confirma que la comunicación interactiva se ha restaurado a la versión seleccionada. La cronología registra una entrada **Página restaurada**.

   ![Revertir versión 2](/help/forms/interactive-communication/assets/create-version6.png)

La comunicación interactiva se restaura a la versión seleccionada, lo que permite a los autores deshacer cambios no deseados o recuperarse de errores.

## Comparar dos versiones

Puede comparar dos versiones cualquiera de una comunicación interactiva en paralelo como vistas previas de PDF, lo que facilita identificar las diferencias de diseño y contenido estático sin abrir cada versión individualmente.

Para obtener instrucciones paso a paso, consulte [Comparar versiones de comunicaciones interactivas](/help/forms/interactive-communication/howto/compare-interactive-communication-versions.md).

## Agregar comentarios a una comunicación interactiva

Los comentarios permiten a los revisores y autores agregar notas generales directamente desde el panel **Cronología** en **Forms y documentos**.

Para agregar un comentario:

1. Vaya a **Forms y documentos** y seleccione la comunicación interactiva.

1. Abra el panel **Línea de tiempo** desde el carril izquierdo.

1. Escriba la nota en el campo **Comentario** de la parte inferior del panel **Escala de tiempo** y guárdela.

   Los comentarios aparecen en la cronología junto con anotaciones, entradas de versión y otras actividades. Por ejemplo, después de un ciclo de revisión, la cronología puede enumerar anotaciones como **actualizar dirección** y **Actualizar modelo de carro** por encima de los comentarios generales y el historial de versiones.

Para los comentarios de revisión posicionados y de nivel de componente (donde un revisor fija un comentario a un campo o sección específicos del lienzo), utilice la función Anotaciones en su lugar. Ver [Revisar y anotar una comunicación interactiva](/help/forms/interactive-communication/howto/review-and-annotate-interactive-communication.md).

## Ver también

- [Comparar versiones de comunicaciones interactivas](/help/forms/interactive-communication/howto/compare-interactive-communication-versions.md)
- [Revisar y anotar una comunicación interactiva](/help/forms/interactive-communication/howto/review-and-annotate-interactive-communication.md)
- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)
