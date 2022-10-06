---
title: Creación y administración de revisiones para recursos de formularios
seo-title: Creating and managing reviews for assets in forms
description: Una revisión es un mecanismo que permite a uno o más revisores realizar comentarios sobre un recurso disponible en un formulario.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 100%

---


# Creación y administración de revisiones para recursos de formularios{#creating-and-managing-reviews-for-assets-in-forms}

## Revisión {#review}

Una revisión es un mecanismo que permite a uno o más revisores realizar comentarios sobre un recurso disponible en un formulario.

## Configurar una revisión {#setting-up-a-review}

1. Vaya a la pestaña Formularios y seleccione un formulario.
1. Si el recurso no tiene ninguna revisión en curso, aparecerá el icono Iniciar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) en la barra de acciones. Haga clic en el icono Iniciar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).
1. Especifique la siguiente información:

   * Nombre de la revisión: obligatorio. Puede contener caracteres alfanuméricos, guiones o guiones bajos.
   * Descripción de la revisión: opcional, la descripción del objetivo/contenido de la revisión.
   * Fecha límite de la revisión: opcional: la fecha en la que finaliza la revisión. Si se sobrepasa la fecha límite, la tarea aparece como “Vencida”.
   * Revisores: es obligatorio especificar al menos uno. Utilice el cuadro combinado para añadir revisores. Al escribir un nombre, se muestran todos los nombres coincidentes; seleccione uno y haga clic en Agregar.

1. Rellene todos los detalles restantes y haga clic en Iniciar.

### Acciones asociadas a la configuración de una revisión {#actions-that-occur-when-a-review-is-set-up}

Esta sección describe lo que sucede cuando se crea o configura una revisión.

1. Se crea una nueva tarea de revisión y se asigna al iniciador de la revisión.
1. A todos los revisores se les asigna una tarea de revisión. La tarea aparece en la sección Notificaciones. Un revisor puede hacer clic en una notificación o ir a la Bandeja de entrada para ver la tarea. Un revisor puede hacer clic en para abrir la tarea de revisión, ver el formulario y empezar a añadir comentarios.

   ![Alerta de notificación del revisor](assets/noti.png)

   Alerta de notificación del revisor

1. El cuadro de comentarios está disponible para el iniciador y para los revisores del recurso. Otros usuarios pueden ver los comentarios, pero no pueden agregar nuevos.

## Administrar una revisión {#managing-a-review}

>[!NOTE]
>
>Solo se pueden modificar las revisiones en progreso. Las revisiones completadas no se pueden modificar.

1. Vaya a la pestaña Formularios y seleccione un formulario.

1. Si un recurso tiene una revisión en curso y usted es el iniciador de la revisión, aparece el icono Administrar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) en la barra de acciones. Solo el iniciador de revisión puede administrar (actualizar/finalizar) la revisión.

   Haga clic en el icono Administrar revisión ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   El icono Administrar revisión está deshabilitado para los usuarios distintos del iniciador.

1. Aparece una pantalla que muestra información:

   * **Nombre de la revisión**: no se puede editar.

   * **Descripción de la revisión**: disponible para edición.

   * **Fecha límite de la revisión**: disponible para edición. Se puede modificar la fecha límite para establecer cualquier fecha y hora posterior a la fecha y la hora actuales.

   * **Revisores**: disponible para edición. Puede agregar o quitar revisores. Si una tarea ha vencido, solo podrá agregar revisores una vez que amplíe la fecha límite hasta pasada la fecha actual.

1. Edite los campos necesarios y, a continuación, haga clic en Actualizar.

   ![Revisar el estado actualizado en el Administrador de tareas](assets/tskmgr.png)

   Revisar el estado actualizado en el Administrador de tareas

1. Para finalizar la revisión, haga clic en Finalizar.

### Acciones asociadas a la modificación de una revisión {#actions-that-occur-when-a-review-is-modified}

Esta sección describe lo que sucede cuando se modifica o finaliza una revisión:

1. Si se modifica la descripción de la revisión, se actualiza la tarea correspondiente de los revisores y el iniciador.
1. Si se modifica la fecha límite de la revisión, se actualiza la tarea correspondiente de los revisores a la nueva fecha.

1. Si se quita un revisor:

   ![Eliminación de un revisor](assets/removeduser.png)

   Eliminación de un revisor

   1. Si la tarea asignada está incompleta, finaliza.
   1. El revisor ya no puede realizar comentarios en el recurso.

1. Si se agrega un revisor:

   ![Adición de un revisor](assets/addedreviewer.png)

   Adición de un revisor

   1. Se crea una tarea de revisión y se asigna al revisor que se acaba de agregar.
   1. El revisor que se acaba de agregar puede añadir comentarios en el recurso.

1. Cuando finaliza una revisión:

   1. **Revisores**: se finaliza la tarea incompleta relacionada con la revisión de cada uno de los revisores. La tarea ya no aparece como “Pendiente” en la sección Notificaciones del revisor.
   1. **Iniciador**: la tarea asignada al iniciador de la revisión se marca como completada y se quita de la sección Notificación del iniciador de la revisión.
   1. **Todos**: la revisión se muestra en la sección Revisiones anteriores. No se pueden añadir más comentarios.

