---
title: Vista previa del contenido
description: Aprenda a utilizar el servicio de vista previa de AEM para obtener una vista previa del contenido antes de publicarlo.
source-git-commit: 9b4ac173c55380cbc06de64677470818aa801df4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# Vista previa del contenido {#previewing-content}

>[!NOTE]
>
>La función Vista previa forma parte de la versión 2021.5.0 y se implementará gradualmente en las próximas semanas.

AEM ofrece un servicio de vista previa de sitios diseñado para permitir que los desarrolladores y autores de contenido obtengan una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente.

Facilita la previsualización de experiencias de página que de otra manera no serían visibles desde el entorno de creación, como transiciones de página y otro contenido solo de publicación.

## Publicar contenido para previsualizar {#publishing-content-to-preview}

Puede publicar contenido en el servicio de vista previa utilizando la IU de publicación administrada de la siguiente manera:

1. Seleccione la página o páginas que desee enviar para obtener una vista previa en la consola Sitios y haga clic en el botón **Administrar publicación**
1. En el asistente siguiente, seleccione **Preview** como destino

   ![publicación gestionada](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. Haga clic en **Siguiente** y luego en **Publicar** para confirmar.

A continuación, verá el contenido de vista previa y anexe **preview** a la URL de publicación de la instancia de producción. La dirección URL debe crearse de esta manera:

```
https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
```

Consulte [Administrar los entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/manage-your-environment.html?lang=en) para obtener más información sobre cómo obtener las direcciones URL de los entornos.

