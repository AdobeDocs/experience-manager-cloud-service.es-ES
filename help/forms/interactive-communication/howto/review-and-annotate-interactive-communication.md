---
title: Revisar y anotar una comunicación interactiva
description: Descubra cómo los revisores pueden anclar comentarios directamente a los componentes del lienzo de la comunicación interactiva y cómo los autores pueden rastrear y resolver esos comentarios sin salir del Editor de comunicaciones interactivas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Se aplica a AEM Forms."
exl-id: review-annotate-interactive-communication
source-git-commit: b11e1b28aabba9e03553dc9e9394bff111facfee
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 2%

---


# Revisar y anotar una comunicación interactiva

La revisión de una comunicación interactiva suele significar compartir capturas de pantalla, redactar correos electrónicos o mantener conversaciones paralelas, ninguna de las cuales se puede asociar al campo o sección exactos que se están discutiendo. Las anotaciones resuelven esto ofreciendo a los revisores una vista dedicada de solo lectura de la comunicación interactiva, donde pueden hacer clic en cualquier componente y dejar un comentario anclado en ese punto exacto del lienzo.

Todos los revisores comparten la misma vista de anotación, por lo que los comentarios son visibles para todos en un solo lugar. Las anotaciones solo existen durante el proceso de creación y revisión, pero nunca aparecen en la salida publicada o orientada al cliente.

| Quién | Ventaja |
|-----|---------|
| **Revisor** | Proporcione comentarios precisos en contexto sin editar la comunicación interactiva ni arriesgarse a realizar cambios accidentales. |
| **Autor (diseñador/propietario de comunicaciones interactivas)** | Reciba comentarios procesables vinculados a componentes específicos, con una forma clara de rastrear y cerrar cada elemento de revisión. |

## Antes de empezar

Los revisores y los autores deben estar asignados a los grupos de revisores y autores adecuados para poder acceder al lienzo de anotaciones o al flujo de trabajo de resolución.

>[!NOTE]
>
> Confirme los nombres de grupo exactos para su entorno con el administrador de AEM antes de asignar el acceso.

## Añadir una anotación

Siga estos pasos como revisor.

1. Vaya a **Forms y documentos**, seleccione la comunicación interactiva que desee revisar y haga clic en **Anotar** en la barra de herramientas.

   ![Anotar 1](/help/forms/interactive-communication/assets/add-annotate1.png)

   Se abre la vista de anotaciones **de solo lectura** con la comunicación interactiva en el lienzo.

   ![Anotar 2](/help/forms/interactive-communication/assets/add-annotate2.png)

1. Para adjuntar un comentario a un componente específico, haga clic en ese componente en el lienzo.

   ![Anotar 3](/help/forms/interactive-communication/assets/add-annotate3.png)

1. Escriba sus comentarios en el cuadro de comentarios y haga clic en el botón azul de publicación para guardar el comentario.

   ![Anotar 4](/help/forms/interactive-communication/assets/add-annotate4.png)

1. Repita los pasos 2 y 3 para cada componente que necesite comentarios.

   Por ejemplo, haga clic en el bloque de direcciones bancarias y agregue **Actualizar dirección**; a continuación, haga clic en la celda **Fabricar y modelo** de la tabla Detalles del vehículo y agregue **Actualizar modelo del vehículo**.

1. Cuando hayas terminado de agregar comentarios, haz clic en **Enviar comentarios**.

   ![Anotar 5](/help/forms/interactive-communication/assets/add-annotate5.png)

   Un mensaje de confirmación confirma que se han enviado sus comentarios. Cada comentario aparece como un pin de anotación en la ubicación seleccionada y los demás revisores pueden verlo inmediatamente.

## Revisar las anotaciones

Siga estos pasos como autor.

1. Vaya a **Forms y documentos**, seleccione la comunicación interactiva y haga clic en **Editar** para abrirla en el Editor de comunicaciones interactivas.

   ![Resolver 1](/help/forms/interactive-communication/assets/add-annotate6.png)

1. Seleccione un componente que muestre un pin de anotación del revisor.

   Por ejemplo, seleccione el bloque de dirección bancaria. En el panel **Propiedades**, expanda la sección **Comentarios** para ver la anotación adjunta. El comentario del revisor **actualizar dirección** aparece aquí.

   ![Resolver 2](/help/forms/interactive-communication/assets/add-annotate7.png)

1. Revise cada comentario y realice los cambios necesarios en el diseño.

   Por ejemplo, actualice el texto de la dirección del banco como lo solicite el revisor.

   ![Resolver 3](/help/forms/interactive-communication/assets/add-annotate8.png)

1. Una vez que hayas enviado un comentario, haz clic en **Resolver** en la sección **Comentarios**.

1. Repita los pasos del 2 al 4 para cada anotación restante.

   Por ejemplo, seleccione la celda **Fabricar y modelo** en la tabla Detalles del vehículo, actualice el valor a **Crear SX(O)** como se solicita en el comentario **Actualizar modelo de coche** y márquelo como **Resuelto**.

   ![Resolver 4](/help/forms/interactive-communication/assets/add-annotate9.png)

1. Haga clic en **Guardar**.

   ![Resolver 5](/help/forms/interactive-communication/assets/add-annotate10.png)

   Un pin de anotación resuelto cambia de abierto a cerrado (gris), lo que distingue entre los elementos de revisión completados y los que aún están pendientes. El comentario resuelto permanece visible en el historial, por lo que se conserva toda la pista de revisión.

## Consideraciones

- Los revisores y los autores deben asignarse a los grupos predeterminados adecuados. No se admiten configuraciones de grupo personalizadas.

- Si se reduce el tamaño de un componente después de colocar una anotación en él, el pasador permanece en la posición original en lugar de moverse con el límite del componente.

- No se admiten anotaciones en fragmentos dentro de un documento.

- Todavía no se admiten anotaciones en el componente **Table**.

## Preguntas frecuentes

**¿Cómo se adjunta un comentario a un campo específico en lugar de a un área general?**
Haga clic directamente en el componente en el lienzo de anotación. El pin se adjunta a ese componente y aparece a todos los revisores en la misma vista de anotación.

**¿Cómo sabe un autor qué componentes tienen anotaciones abiertas?**
Los anclajes de anotación se pueden ver directamente en el lienzo en el editor de comunicaciones interactivas. Al seleccionar un componente, se muestran todos sus comentarios adjuntos en el panel Propiedades.

**¿Aparecen anotaciones en la salida de PDF publicada?**
No. Las anotaciones solo forman parte del flujo de trabajo de creación y revisión. Nunca se incluyen en la salida publicada o orientada al cliente.

**¿Cuál es la diferencia entre una anotación y un comentario?**
Una anotación es un pin colocado vinculado a un componente específico en el lienzo, visible en la vista de anotaciones de solo lectura. Un comentario es una nota general adjunta a la comunicación interactiva en su conjunto, agregada desde el panel Comentarios en el editor. Consulte [Versiones y comentarios](/help/forms/interactive-communication/versioning-and-commenting-in-interactive-communication-editor.md) para obtener más información sobre los comentarios.

## Ver también

- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)
- [Bloqueo de plantilla en el Editor de comunicaciones interactivas](/help/forms/interactive-communication/enable-template-lock.md)
- [Crear versiones y comentarios en el editor de comunicaciones interactivas](/help/forms/interactive-communication/versioning-and-commenting-in-interactive-communication-editor.md)

