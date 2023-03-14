---
title: Revisión de recursos en carpetas y colecciones
description: Configure flujos de trabajo de revisión para los recursos de una carpeta o una colección y compártala con revisores o socios creativos para buscar comentarios.
contentOwner: AG
feature: Collections,Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 24%

---

# Revisión de recursos en carpetas y colecciones {#review-folder-assets-and-collections}

Con Adobe Experience Manager Assets, puede establecer flujos de trabajo de revisión específicos para recursos que se encuentran en una carpeta o en una colección. Puede compartirlo con revisores o socios creativos para que busquen sus comentarios. Puede asociar un flujo de trabajo de revisión a un proyecto o crear una tarea de revisión independiente.

Una vez compartidos los recursos, los revisores pueden aprobarlos o rechazarlos. Las notificaciones se envían en varias fases del flujo de trabajo para notificar a los destinatarios objetivo la finalización de diversas tareas. Por ejemplo, cuando comparte una carpeta o colección, el revisor recibe una notificación que le informa de que una carpeta o colección se ha compartido para su revisión.

Una vez que el revisor haya completado la revisión (aprueba o rechaza los recursos), recibirá una notificación de finalización de la revisión.

## Creación de una tarea de revisión para carpetas {#creating-a-review-task-for-folders}

1. En la interfaz de usuario de Assets, seleccione la carpeta para la que desea crear una tarea de revisión.
1. En la barra de herramientas, pulse o haga clic en el icono **[!UICONTROL Crear tarea de revisión]** para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver el icono en la barra de herramientas, pulse o haga clic en **[!UICONTROL Más]** y, a continuación, seleccione el icono.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) Desde el **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, la variable **[!UICONTROL Ninguno]** La opción está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la **[!UICONTROL Proyectos]** lista.

1. Introduzca un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]** lista.

   >[!NOTE]
   >
   >Los miembros/grupos del proyecto seleccionado están disponibles como aprobadores en la **[!UICONTROL Asignar a]** lista.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details](assets/task_details.png)

1. En la pestaña Advanced, introduzca una etiqueta para utilizar para crear el URI.

   ![review_name](assets/review_name.png)

1. Pulse o haga clic en **[!UICONTROL Enviar]** y, a continuación, pulse o haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Iniciar sesión en [!DNL Experience Manager Assets] como Aprobador y vaya a la interfaz de usuario de Assets. Para aprobar los recursos, pulse o haga clic en **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.

   ![notificación](assets/notification.png)

1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, pulse o haga clic en **[!UICONTROL Revisar]**.
1. En la página **[!UICONTROL Revisar tarea]**, seleccione los recursos y pulse o haga clic en el icono **[!UICONTROL Aprobar/Rechazar]** para aprobarlos o rechazarlos, según corresponda.

   ![review_task](assets/review_task.png)

1. Toque o haga clic en el icono **[!UICONTROL Completar]** de la barra de herramientas. En el cuadro de diálogo, introduzca un comentario y pulse o haga clic en él  **[!UICONTROL Completar]** para confirmar.
1. Vaya a la interfaz de usuario de Assets y abra la carpeta. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   **Vista de tarjeta**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Vista de lista**

   ![review_status_listview](assets/review_status_listview.png)

## Creación de una tarea de revisión para colecciones {#creating-a-review-task-for-collections}

1. En la página Colecciones, seleccione la colección para la que desea crear una tarea de revisión.
1. En la barra de herramientas, pulse o haga clic en el icono **[!UICONTROL Crear tarea de revisión]** para abrir la página **[!UICONTROL Revisar tarea]**. Si no puede ver el icono en la barra de herramientas, pulse o haga clic en **[!UICONTROL Más]** y, a continuación, seleccione el icono.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) Desde el **[!UICONTROL Proyecto]** , seleccione el proyecto al que desea asociar la tarea de revisión. De forma predeterminada, la variable **[!UICONTROL Ninguno]** La opción está seleccionada. Si no desea asociar ningún proyecto con la tarea de revisión, mantenga esta selección.

   >[!NOTE]
   >
   >Solo los proyectos para los que tenga permisos de nivel de editor (o superiores) serán visibles en la **[!UICONTROL Proyectos]** lista.

1. Introduzca un nombre para la tarea de revisión y seleccione un aprobador de la lista **[!UICONTROL Asignar a]** lista.

   >[!NOTE]
   >
   >Los miembros/grupos del proyecto seleccionado están disponibles como aprobadores en la **[!UICONTROL Asignar a]** lista.

1. Escriba una descripción, la prioridad de la tarea y la fecha de vencimiento de la tarea de revisión.

   ![task_details-collection](assets/task_details-collection.png)

1. Pulse o haga clic en **[!UICONTROL Enviar]** y, a continuación, pulse o haga clic en **[!UICONTROL Listo]** para cerrar el mensaje de confirmación. Se envía una notificación para la nueva tarea al aprobador.
1. Iniciar sesión en [!DNL Experience Manager Assets] como Aprobador y vaya a la consola Recursos. Para aprobar los recursos, pulse o haga clic en **[!UICONTROL Notificaciones]** y, a continuación, seleccione la tarea de revisión en la lista.
1. En la página **[!UICONTROL Revisar tarea]**, examine los detalles de la tarea de revisión y, a continuación, pulse o haga clic en **[!UICONTROL Revisar]**.
1. Todos los recursos de la colección están visibles en la página de revisión. Seleccione los recursos y pulse o haga clic en **[!UICONTROL Aprobar/rechazar]** para aprobar o rechazar recursos, según corresponda.

   ![review_task_collection](assets/review_task_collection.png)

1. Toque o haga clic en el icono **[!UICONTROL Completar]** de la barra de herramientas. En el cuadro de diálogo, introduzca un comentario y pulse o haga clic en él **[!UICONTROL Completar]** para confirmar.
1. Vaya a la consola Colecciones y abra la colección. Los iconos de estado de aprobación de los recursos aparecen en las vistas Tarjeta y Lista.

   **Vista de tarjeta**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Vista de lista**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)
