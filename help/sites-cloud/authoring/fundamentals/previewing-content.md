---
title: Vista previa del contenido
description: Aprenda a utilizar el servicio de vista previa de AEM para obtener una vista previa del contenido antes de publicarlo.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 66bc262b35f69b7877e4a01df9ab26395afd604d
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 93%

---


# Vista previa del contenido {#previewing-content}

AEM ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenido previsualizar la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible de manera pública.

Facilita la previsualización de experiencias de página que, de otra manera, no serían visibles desde el entorno de creación, como transiciones de página y otro contenido solo de publicación.

Para obtener más información acerca de los entornos de vista previa, consulte el documento [Administración de entornos.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>La publicación de un fragmento de experiencia para vista previa básicamente sigue el mismo procedimiento que para una página, aunque desde la consola o el editor de fragmentos de experiencias.

## Publicación de contenido para su previsualización {#publishing-content-to-preview}

Puede publicar contenido en el servicio de vista previa utilizando la IU **Publicación administrada**.

1. En la consola Sites, seleccione la página o páginas que desee enviar para obtener una vista previa y haga clic en el botón **Administrar publicación**
1. En el asistente siguiente, seleccione **Vista previa** como destino

   ![publicación administrada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Haga clic en **Siguiente** y luego en **Publicación** para confirmar.

1. Un cuadro de diálogo mostrará las direcciones URL para acceder al contenido en el entorno de vista previa.


Como alternativa, para usar las direcciones URL mostradas en el asistente para ver el contenido de vista previa, también puede anteponer `preview-` a la URL de publicación de la instancia de producción.

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

Consulte el documento [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información sobre cómo recuperar las direcciones URL de sus entornos.

El contenido también se puede publicar para previsualizarse mediante un [flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow), con el parámetro `agentId` establecido en `preview`, o utilizando la [API de replicación](/help/operations/replication.md#replication-api) con un `AgentFilter` configurado para la vista previa.

## Configuración de OSGi para el nivel de vista previa {#configuring-osgi-settings-for-the-preview-tier}

Los valores de las propiedades OSGi del nivel de vista previa se heredan del nivel de publicación. Sin embargo, los valores del nivel de vista previa pueden ser distintos del de publicación, configurando el parámetro `service` al valor `preview`. El siguiente ejemplo de una propiedad OSGi determina la dirección URL de un punto de conexión de integración.

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

Para obtener más información, consulte [esta sección](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) de la documentación de configuración de OSGi.

## Depuración de la vista previa mediante Developer Console {#debugging-preview-using-the-developer-console}

Siga estos pasos para depurar el nivel de vista previa mediante Developer Console:

* En [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleccione **-- Todas las previsualizaciones --** o un entorno de producción que incluya **prev** en el nombre
* Genere la información relevante para la instancia de vista previa
Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información sobre cómo obtener las direcciones URL de los entornos.
