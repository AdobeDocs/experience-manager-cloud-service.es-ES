---
title: Vista previa del contenido
description: Aprenda a utilizar el servicio de vista previa de AEM para obtener una vista previa del contenido antes de publicarlo.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 1804eacb5399dc38c97ff953031666711b9a0e4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 86%

---


# Vista previa del contenido {#previewing-content}

AEM ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenido previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible de manera pública.

Facilita la previsualización de experiencias de página que, de otra manera, no serían visibles desde el entorno de creación, como transiciones de página y otro contenido solo de publicación.

>[!NOTE]
>
>Tal como está el contenido *publicado* AEM Al entorno de vista previa, se puede acceder mediante una dirección URL (por lo que no necesita acceder a la dirección URL de la página de acceso a la página de acceso a la página).

Para obtener más información acerca de los entornos de vista previa, consulte el documento [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Publicación de contenido para su previsualización {#publishing-content-to-preview}

Puede publicar contenido en el servicio de vista previa utilizando la IU **Publicación administrada**.

1. En la consola Sites, seleccione la página o páginas que desee enviar para obtener una vista previa y haga clic en el botón **Administrar publicación**
1. En el asistente siguiente, seleccione **Vista previa** como destino

   ![publicación administrada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Haga clic en **Siguiente** y luego en **Publicación** para confirmar.

1. Un cuadro de diálogo mostrará las direcciones URL para acceder al contenido en el entorno de vista previa.

   >[!NOTE]
   >
   >Tal como está el contenido *publicado* AEM Al entorno de vista previa, se puede acceder mediante una dirección URL (por lo que no necesita acceder a la dirección URL de la página de acceso a la página de acceso a la página).

Como alternativa, para usar las direcciones URL mostradas en el asistente para ver el contenido de vista previa, también puede anteponer `preview-` a la URL de publicación de la instancia de producción.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte el documento [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información sobre cómo recuperar las direcciones URL de sus entornos.

El contenido también se puede publicar para previsualizarse mediante un [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow), con el parámetro `agentId` establecido en `preview`, o utilizando la [API de replicación](/help/operations/replication.md#replication-api) con un `AgentFilter` configurado para la vista previa.

## Cancelación de la publicación de contenido desde Vista previa {#unpublishing-content-from-preview}

Cancelar la publicación de contenido desde el entorno de **Vista previa** es básicamente el mismo proceso que [cancelar la publicación de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) del entorno de **Publicación**.

La única diferencia es que puede seleccionar el **Destino** a **Vista previa**.

## Información adicional {#further-information}

Consulte también lo siguiente:

* [Configuración de OSGi para el nivel de vista previa](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#configuring-osgi-settings-for-the-preview-tier)

* [Depuración de la vista previa mediante Developer Console](/help/implementing/preview-tier/preview-tier-configuring-osgi.md#debugging-preview-using-the-developer-console)