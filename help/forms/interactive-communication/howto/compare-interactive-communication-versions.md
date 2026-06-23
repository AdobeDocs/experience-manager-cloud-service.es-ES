---
title: Comparar versiones de comunicaciones interactivas
description: Obtenga información sobre cómo abrir dos versiones de una comunicación interactiva en paralelo como vistas previas de PDF para inspeccionar las diferencias de diseño y contenido antes de publicarla.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: compare-interactive-communication-versions
source-git-commit: b817bcb02c4ff6ac369973ef658d9fcbdce95c51
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 2%

---


# Comparar versiones de comunicaciones interactivas

Cuando una comunicación interactiva pasa por varias rondas de edición, puede resultar difícil saber exactamente qué ha cambiado entre dos estados guardados. Puede abrir dos versiones cualesquiera en paralelo como vistas previas de PDF, lo que facilita la detección de cambios de diseño, adiciones o eliminaciones de componentes y cambios de contenido estático, sin tener que abrir cada versión individualmente o comparar capturas de pantalla manualmente.

| Quién | Ventaja |
|-----|---------|
| **Autor (diseñador/propietario de comunicaciones interactivas)** | Compruebe que las ediciones entre ciclos de revisión producen los cambios esperados antes de publicar. |
| **Revisor de contenido** | Confirme que las revisiones de autor abordaron los comentarios de una versión anterior sin introducir nuevos problemas. |

>[!NOTE]
>
> Esta comparación abarca **solo diseño y contenido estático**. Los valores de campo dinámico rellenados durante la ejecución no se representan en la vista de comparación.

## Antes de empezar

Asegúrese de haber guardado al menos una versión de la comunicación interactiva que desee comparar con el diseño actual.

Para crear una versión, abre **Forms y documentos**, selecciona la comunicación interactiva, abre el panel **Cronología** del carril izquierdo y haz clic en **Guardar como versión**. Consulte [Creación de versiones y comentarios en el editor de comunicaciones interactivas](/help/forms/interactive-communication/versioning-and-commenting-in-interactive-communication-editor.md) para obtener instrucciones paso a paso.

Después de guardar la versión, actualice la comunicación interactiva en el editor para que el diseño actual difiera de la versión guardada. Necesita una versión guardada y un estado actual modificado para poder compararlos.

## Actualizar la comunicación interactiva

Después de crear una versión, abra la comunicación interactiva en el Editor de comunicaciones interactivas y actualice el diseño.

Por ejemplo, después de guardar la **comunicación interactiva bancaria versión 1**, puede actualizar el logotipo del banco, revisar los detalles del préstamo y cambiar la información del vehículo en la tabla:

- Reemplace el encabezado bancario basado en texto con una imagen de logotipo de banco
- Actualizar detalles del préstamo, como el número de referencia de la solicitud, el importe del préstamo aprobado, el ejercicio del préstamo y la fecha de inicio del IME
- Actualice el valor **Marca y modelo** y el nombre del concesionario en la tabla Detalles del vehículo

![Se ha actualizado la comunicación interactiva](/help/forms/interactive-communication/assets/compare-ic1.png)

Haz clic en **Guardar** cuando termines de editar. El diseño actual ya está listo para compararlo con la versión guardada.

## Comparar dos versiones

1. Vaya a **Forms y documentos** y seleccione la comunicación interactiva que desee comparar.

1. Abra el panel **Línea de tiempo** desde el carril izquierdo.

1. En la cronología, busque la versión guardada que desee comparar. Por ejemplo, seleccione **Comunicación interactiva bancaria versión 1** con el comentario **Esta versión incluye un nuevo logotipo bancario y detalles actualizados**.

1. Haga clic en **Comparar con actual**.

   ![Comparar con actual](/help/forms/interactive-communication/assets/compare-ic2.png)

   Se abre una nueva pestaña con ambas versiones mostradas una al lado de la otra como vistas previas de PDF. La versión guardada aparece a la izquierda y la versión actual a la derecha.

   ![Comparación en paralelo](/help/forms/interactive-communication/assets/comapre-ic3.png)

   Desplácese por las vistas previas para inspeccionar las diferencias de diseño y contenido página por página. Por ejemplo, la comparación resalta cambios en el logotipo del banco, detalles del préstamo e información del vehículo, como el modelo del coche y el nombre del concesionario.

## Consideraciones

- **Bloques de texto grandes:** Si se ha reescrito o reorganizado un párrafo o bloque de texto, ambas páginas se representan de forma idéntica a su PDF de origen. No hay diferencia de texto en línea, la comparación es solo visual y el texto modificado no está marcado.

- **Datos dinámicos:** Los valores de campo dinámico no se incluyen en la comparación. Solo están visibles el diseño estático y el contenido de cada versión.

## Preguntas frecuentes

**¿Cuántas versiones puedo comparar a la vez?**
Puede comparar dos versiones a la vez: la seleccionada y la actual. Se abren en paralelo en una nueva pestaña.

**¿Puedo comparar una versión con una versión distinta a la actual?**
El selector de versiones siempre se compara con la versión actual. Para comparar dos versiones no actuales, revierte temporalmente a la versión anterior y, a continuación, usa **Comparar con actual** de nuevo.

**¿Es posible descargar o exportar la vista de comparación?**
No. La comparación en paralelo es sólo una herramienta de revisión visual; no se puede exportar desde el editor.

## Ver también

- [Crear versiones y comentarios en el editor de comunicaciones interactivas](/help/forms/interactive-communication/versioning-and-commenting-in-interactive-communication-editor.md)
- [Revisar y anotar una comunicación interactiva](/help/forms/interactive-communication/howto/review-and-annotate-interactive-communication.md)
- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)

