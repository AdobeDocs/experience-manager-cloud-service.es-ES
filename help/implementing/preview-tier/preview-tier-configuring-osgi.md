---
title: Configuración de OSGi para el nivel de vista previa
description: Obtenga información sobre cómo configurar el servicio de vista previa de AEM para previsualizar el contenido antes de publicarlo.
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 64%

---


# Configuración de OSGi para el nivel de vista previa {#configure-osgi-preview-tier}

AEM ofrece un servicio de vista previa de Sites que permite a los desarrolladores y autores de contenido obtener una vista previa de la experiencia final de un sitio web antes de que llegue al entorno de publicación y esté disponible públicamente.

Facilita la previsualización de una serie de experiencias que de otra manera no serían visibles desde el entorno de creación. Por ejemplo, transiciones de página, fragmentos de experiencia y otro contenido solo de publicación.

Los valores de las propiedades OSGi del nivel de vista previa se heredan del nivel de publicación. Sin embargo, los valores del nivel de vista previa pueden ser distintos del de publicación, configurando el parámetro `service` al valor `preview`.

>[!NOTE]
>
>Para obtener más información acerca de los entornos de vista previa, consulte el documento [Administración de entornos.](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## Configuración de OSGi para el nivel de vista previa {#configuring-osgi-settings-for-the-preview-tier}

El siguiente ejemplo de una propiedad OSGi determina la dirección URL de un punto de conexión de integración.

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
