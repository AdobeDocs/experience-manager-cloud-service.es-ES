---
title: Flujo de actividad en la cronología
description: Este artículo describe cómo mostrar los registros de actividad de los recursos en la cronología.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 24%

---

# Ver registros de operaciones de recursos en el flujo de actividades {#activity-stream-in-timeline}

Esta función muestra los registros de actividad de los recursos en la cronología. Si realiza cualquiera de las siguientes operaciones relacionadas con recursos en [!DNL Experience Manager Assets], la función Flujo de actividad actualiza la cronología para reflejar la actividad.

Las siguientes operaciones se registran en el flujo de actividad:

* Crear
* Eliminar
* Descargar (incluidas representaciones)
* Publicación
* Cancelar publicación
* Aprobar
* Rechazar
* Mover

Los registros de actividad que se mostrarán en la cronología se recuperan de la ubicación `/var/audit/com.day.cq.dam/content/dam` en CRX, donde se almacenan los archivos de registro. Además, la actividad de la cronología se registra cuando se cargan nuevos recursos o cuando se modifican y se registran los recursos existentes [!DNL Experience Manager] mediante [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) o [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Los flujos de trabajo transitorios no se muestran en la cronología porque no se guarda información del historial para estos flujos de trabajo.

Para ver el flujo de actividad, realice una o varias de las operaciones en el recurso, selecciónelo y, a continuación, elija **[!UICONTROL Cronología]** de la lista GlobalNav.

<!-- ![timeline-2](assets/timeline-2.png) -->

La cronología muestra el flujo de actividad para las operaciones que realiza en los recursos.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>La ubicación de almacenamiento de registro predeterminada para las tareas **[!UICONTROL Publicar]** y **[!UICONTROL Cancelar la publicación]** es `/var/audit/com.day.cq.replication/content`. Para las tareas **[!UICONTROL Mover]**, la ubicación predeterminada es `/var/audit/com.day.cq.wcm.core.page`.
