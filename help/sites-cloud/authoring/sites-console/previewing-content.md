---
title: Vista previa del contenido
description: Aprenda a utilizar el servicio de vista previa de AEM para obtener una vista previa del contenido antes de publicarlo.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: b93bcb5d26a63babf0b81c92a4fd85d358bfbea7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 65%

---


# Vista previa del contenido {#previewing-content}

AEM ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenido previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible de manera pública.

Facilita la previsualización de experiencias de página que, de otra manera, no serían visibles desde el entorno de creación, como transiciones de página y otro contenido solo de publicación.

>[!IMPORTANT]
>
>El acceso al entorno de vista previa requiere la configuración de una lista de permitidos IP. Para obtener más información, consulte [Acceso al servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#access-preview-service#access-preview-service).
>
>Para obtener más información acerca de todos los entornos, vea [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>Como el contenido está *publicado* en el entorno de vista previa, se puede acceder a él mediante una dirección URL.

## Publicación de contenido para su previsualización {#publishing-content-to-preview}

Puede publicar contenido en el servicio de vista previa utilizando la IU **Publicación administrada**.

1. En la consola Sitios, seleccione la página o páginas que desee enviar para obtener una vista previa y haga clic en el botón **Administrar publicación**.
1. En el asistente siguiente, seleccione **Vista previa** como destino.

   ![publicación administrada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Haga clic en **Siguiente** y luego en **Publicación** para confirmar.

1. Un cuadro de diálogo mostrará las direcciones URL para acceder al contenido en el entorno de vista previa.

   >[!NOTE]
   >
   >Como el contenido está *publicado* en el entorno de vista previa, se puede acceder a él mediante una dirección URL (por lo que no necesita acceder a AEM).

Como alternativa, para usar las direcciones URL mostradas en el asistente para ver el contenido de vista previa, también puede anteponer `preview-` a la URL de publicación de la instancia de producción.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información sobre cómo recuperar las direcciones URL de los entornos.

El contenido también se puede publicar para previsualizarse mediante un [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow), con el parámetro `agentId` establecido en `preview`, o utilizando la [API de replicación](/help/operations/replication.md#replication-api) con un `AgentFilter` configurado para la vista previa.

## Cancelación de la publicación de contenido desde Vista previa {#unpublishing-content-from-preview}

Cancelar la publicación de contenido desde el entorno de **Vista previa** es básicamente el mismo proceso que [cancelar la publicación de páginas](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages) del entorno de **Publicación**.

La única diferencia es que puede seleccionar el **Destino** a **Vista previa**.
