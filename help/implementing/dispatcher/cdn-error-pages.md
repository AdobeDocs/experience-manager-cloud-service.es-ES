---
title: Configuración de páginas de error de CDN
description: Obtenga información sobre cómo anular la página de error predeterminada alojando archivos estáticos en un almacenamiento autoalojado como Amazon S3 o Azure Blob Storage y haciendo referencia a ellos en un archivo de configuración que se implementa mediante la canalización de configuración de Cloud Manager.
feature: Dispatcher
exl-id: 1ecc374c-b8ee-41f5-a565-5b36445d3c7c
source-git-commit: 8489b40f45e6cbeb98288969bc9f6bd42815e2a6
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 1%

---

# Configuración de páginas de error de CDN {#cdn-error-pages}

En el improbable caso de que la [CDN administrado por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) AEM no puede alcanzar el origen de la, la CDN muestra de forma predeterminada una página de error genérica sin marca que indica que no se puede acceder al servidor. Puede anular la página de error predeterminada alojando archivos estáticos en un almacenamiento autoalojado como Amazon S3 o Azure Blob Storage, y haciendo referencia a ellos en un archivo de configuración que se implementa mediante [Canalización de configuración de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline).

## Configuración {#setup}

Para poder anular la página de error predeterminada, debe hacer lo siguiente:

* En primer lugar, cree esta carpeta y estructura de archivos en la carpeta de nivel superior del proyecto Git:

```
config/
     cdn.yaml
```

* En segundo lugar, la `cdn.yaml` el archivo de configuración debe contener metadatos y referencias de página de error, como se describe a continuación.

### Configuración {#configuration}

SPA La página de error se implementa como una aplicación de una sola página () y hace referencia a un puñado de propiedades, como se muestra en el ejemplo siguiente.  Los archivos estáticos a los que hacen referencia las direcciones URL deben alojarse en un servicio accesible por Internet como Amazon S3 o Azure Blob Storage.

Ejemplo de configuración:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_errorPages:
    spa:
      title: the error page
      icoUrl: https://www.example.com/error.ico
      cssUrl: https://www.example.com/error.css
      jsUrl: https://www.example.com/error.js
```

| Nombre | Propiedades permitidas | Significado |
|-----------|--------------------------|-------------|
| **balneario** | Título | Título de la página de error. |
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
