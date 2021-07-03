---
title: Flujo de actividad en la cronología
description: Este artículo describe cómo mostrar los registros de actividad de los recursos en la cronología.
contentOwner: AG
feature: Informes de activos,Administración de activos
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 23%

---

# Ver registros de operaciones de recursos en el flujo de actividades {#activity-stream-in-timeline}

Esta función muestra los registros de actividad de los recursos en la cronología. Si realiza cualquiera de las siguientes operaciones relacionadas con recursos en [!DNL Experience Manager Assets], la función Flujo de actividad actualiza la cronología para reflejar la actividad.

Las siguientes operaciones se registran en el flujo de actividad:

* Crear
* Eliminar
* Descargar (incluidas las representaciones)
* Publicación
* Cancelar publicación
* Aprobar
* Rechazar
* Mover

Los registros de actividad que se mostrarán en la cronología se recuperan de la ubicación `/var/audit/com.day.cq.dam/content/dam` en CRX, donde se almacenan los archivos de registro. Además, la actividad de la cronología se registra cuando se cargan nuevos recursos o cuando se modifican y se registran en [!DNL Experience Manager] los recursos existentes mediante [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) o [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

>[!NOTE]
>
>Los flujos de trabajo transitorios no se muestran en la cronología, ya que no se guarda información de historial para estos flujos de trabajo.

Para ver el flujo de actividad, realice una o más de las operaciones en el recurso, seleccione el recurso y, a continuación, elija **[!UICONTROL Línea de tiempo]** en la lista Navegador global.

<!-- ![timeline-2](assets/timeline-2.png) -->

La cronología muestra el flujo de actividad de las operaciones que realiza en los recursos.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>La ubicación de almacenamiento de registro predeterminada para las tareas **[!UICONTROL Publicar]** y **[!UICONTROL Cancelar la publicación]** es `/var/audit/com.day.cq.replication/content`. Para las tareas **[!UICONTROL Mover]**, la ubicación predeterminada es `/var/audit/com.day.cq.wcm.core.page`.
