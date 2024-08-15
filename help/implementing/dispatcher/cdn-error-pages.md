---
title: Configuración de páginas de error de CDN
description: Obtenga información sobre cómo anular la página de error predeterminada alojando archivos estáticos en un almacenamiento autoalojado como Amazon S3 o Azure Blob Storage y haciendo referencia a ellos en un archivo de configuración que se implementa mediante la canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
role: Admin
source-git-commit: 85cef99dc7a8d762d12fd6e1c9bc2aeb3f8c1312
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---


# Configuración de páginas de error de CDN {#cdn-error-pages}

En el improbable caso de que [CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) administrado por el Adobe AEM no pueda alcanzar el origen de la, la CDN proporciona de forma predeterminada una página de error genérica sin marca que indica que no se puede llegar al servidor. Puede anular la página de error predeterminada alojando archivos estáticos en un almacenamiento autoalojado como Amazon S3 o Azure Blob Storage y haciendo referencia a ellos en un archivo de configuración que se implementa mediante la canalización de configuración de Cloud Manager [config.](/help/operations/config-pipeline.md#managing-in-cloud-manager)

## Configuración {#setup}

Para poder anular la página de error predeterminada, debe hacer lo siguiente:

1. Cree un archivo con el nombre `cdn.yaml` o similar, haciendo referencia a la sección de sintaxis siguiente.

1. Coloque el archivo en algún lugar bajo una carpeta de nivel superior llamada *config* o similar, como se describe en [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#folder-structure).

1. Cree una canalización de configuración en Cloud Manager, tal como se describe en [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Implemente la configuración de.

### Sintaxis {#syntax}

SPA La página de error se implementa como una aplicación de una sola página () y hace referencia a un puñado de propiedades, como se muestra en el ejemplo siguiente.  Los archivos estáticos a los que hacen referencia las direcciones URL deben alojarse en un servicio accesible por Internet como Amazon S3 o Azure Blob Storage.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```
Consulte [Uso de canalizaciones de configuración](/help/operations/config-pipeline.md#common-syntax) para obtener una descripción de las propiedades sobre el nodo de datos. El valor de la propiedad kind debe ser *CDN* y la propiedad `version` debe establecerse en *1*.


| Nombre | Propiedades permitidas | Significado |
|-----------|--------------------------|-------------|
| **spa** | Título | Título de la página de error. |
|     | icoUrl | URL de un archivo de icono. |
|     | cssUrl | URL de un archivo CSS. |
|     | jsUrl | URL de un archivo JavaScript. |

### Ejemplo de HTML generado {#sample-generated-html}

El código de HTML generado por la CDN y entregado al cliente, como un explorador, se parecerá (pero no es idéntico) al siguiente fragmento:

```
<!DOCTYPE html>
<html lang="en">
    <head>
        ...
        <title>the error page</title>
        <link rel="icon" href="https://www.example.com/error.ico">
        <link rel="stylesheet" href="https://www.example.com/error.css">
    </head>
    <body>
        ...
        <div id="root" status="403"></div>
        <script src="https://www.example.com/error.js"> </script>
    </body>
</html>
```

### Pruebas {#testing}

Para realizar pruebas, llame al punto final dedicado con el código de error admitido, por ejemplo:

```
curl "https://publish-pXXXXX-eXXXXXX.adobeaemcloud.com/cdnstatus?code=403"
```

Los códigos admitidos son: 403, 404, 406, 500 y 503.

De este modo, se almacena directamente en déclencheur el controlador de error de CDN para probar la respuesta sintética de un código de error determinado.
