---
title: Flujo de Actividad en la línea de tiempo
description: En este artículo se describe cómo mostrar los registros de actividades de los recursos en la línea de tiempo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 40%

---


# Registros de operaciones de recursos de Vista en el flujo de actividades {#activity-stream-in-timeline}

Esta función muestra los registros de actividades de los recursos en la línea de tiempo. Si realiza cualquiera de las siguientes operaciones relacionadas con recursos en Recursos Adobe Experience Manager (AEM), la función de flujo de Actividad actualiza la línea de tiempo para reflejar la actividad.

Las siguientes operaciones se registran en el flujo de actividad:

* Crear
* Eliminar
* Descargar (incluidas las representaciones)
* Publicación
* Cancelar publicación
* Aprobar
* Rechazar
* Mover

Los registros de actividad que se mostrarán en la cronología se recuperan de la ubicación `/var/audit/com.day.cq.dam/content/dam` en CRX, donde se almacenan los archivos de registro. Además, la actividad de la cronología se registra cuando se cargan nuevos recursos o cuando se modifican y se registran en AEM los recursos existentes mediante [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) o la [aplicación de escritorio de AEM](https://docs.adobe.com/content/help/es-ES/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Los flujos de trabajo transitorios no se muestran en la línea de tiempo, ya que no se guarda la información del historial de estos flujos de trabajo.

Para realizar la vista del flujo de actividad, realice una o varias de las operaciones en el recurso, selecciónelo y, a continuación, elija **[!UICONTROL Línea de tiempo]** en la lista de GlobalNav.

<!-- ![timeline-2](assets/timeline-2.png) -->

La línea de tiempo muestra el flujo de actividad de las operaciones que realiza en los recursos.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>La ubicación de almacenamiento de registro predeterminada para las tareas **[!UICONTROL Publicar]** y **[!UICONTROL Cancelar la publicación]** es `/var/audit/com.day.cq.replication/content`. Para las tareas **[!UICONTROL Mover]**, la ubicación predeterminada es `/var/audit/com.day.cq.wcm.core.page`.
