---
title: Vista previa del contenido
description: Aprenda a utilizar el servicio de vista previa de AEM para obtener una vista previa del contenido antes de publicarlo.
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: c30470b321a4fba8c8de9becb62c518faff05498
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Vista previa del contenido {#previewing-content}

>[!NOTE]
>
>La función Vista previa forma parte de la versión 2021.5.0 y se implementará gradualmente en las próximas semanas.

AEM ofrece un servicio de vista previa de sitios diseñado para permitir que los desarrolladores y autores de contenido obtengan una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente.

Facilita la previsualización de experiencias de página que de otra manera no serían visibles desde el entorno de creación, como transiciones de página y otro contenido solo de publicación.

## Publicar contenido para previsualización {#publishing-content-to-preview}

Puede publicar contenido en el servicio de vista previa utilizando la IU de publicación administrada de la siguiente manera:

1. Seleccione la página o páginas que desee enviar para obtener una vista previa en la consola Sitios y haga clic en el botón **Administrar publicación**
1. En el asistente siguiente, seleccione **Preview** como destino

   ![publicación gestionada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Haga clic en **Siguiente** y luego en **Publicar** para confirmar.

1. Un cuadro de diálogo mostrará las direcciones URL para acceder al contenido en el entorno de vista previa.

   O para ver el contenido de vista previa, también puede anexar **preview** a la URL de publicación de la instancia de producción.

   La dirección URL debe crearse de esta manera:

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

Consulte [Administrar los entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) para obtener más información sobre cómo obtener las direcciones URL de los entornos.

El contenido también se puede publicar para obtener una vista previa mediante un [Flujo de trabajo del árbol de contenido de publicación](/help/operations/replication.md#publish-content-tree-workflow) con el parámetro agentId establecido para la vista previa o mediante la [API de replicación](/help/operations/replication.md#replication-api) con un AgentFilter configurado para la vista previa.

## Configuración de OSGi para el nivel de vista previa {#configuring-osgi-settings-for-the-preview-tier}

Los valores de las propiedades OSGI de su capa de vista previa se heredan del nivel de publicación, pero los valores de este nivel se pueden distinguir del del de publicación mediante valores específicos del entorno que establecen el parámetro de servicio con el valor &quot;preview&quot;. Tomemos el ejemplo siguiente de una propiedad OSGI que determina la dirección URL de un extremo de integración:

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

* En [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools), seleccione **— Todas las previsualizaciones —** o un entorno de producción que incluya **prev** en su nombre
* Generar la información relevante para la instancia de vista previa
Consulte [Administrar los entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) para obtener más información sobre cómo obtener las direcciones URL de los entornos.
