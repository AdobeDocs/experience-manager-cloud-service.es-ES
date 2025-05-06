---
title: Asignación de rutas para Edge Delivery Services
description: Aprenda a asignar rutas de página utilizadas en la instancia de creación de AEM a rutas de página públicas utilizadas en el sitio web y a controlar qué contenido se publica en Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 3d68135d-e84c-4bf4-93d1-38a0be70ce4a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '567'
ht-degree: 100%

---

# Asignación de rutas para Edge Delivery Services {#path-mapping}

Aprenda a asignar rutas de página utilizadas en la instancia de creación de AEM a rutas de página públicas utilizadas en el sitio web y a controlar qué contenido se publica en Edge Delivery Services.

## Información general {#overview}

Para poder crear contenido WYSIWYG mediante AEM y publicarlo en Edge Delivery Services, debe configurar la asignación de rutas del proyecto. Esta asignación tiene dos propósitos.

* Se asigna y se crea una relación entre las rutas de página utilizadas en su instancia de creación de AEM y las rutas de página públicas utilizadas en su sitio web.
* Controla qué contenido (páginas, hojas, recursos, etc.) se publica en Edge Delivery Services.

La asignación de ruta debe configurarse para cada proyecto de forma individual y según el contenido del proyecto y la estructura de la URL. AEM lo utiliza durante la publicación de contenido y al editar contenido en el [editor universal](/help/sites-cloud/authoring/universal-editor/navigation.md).

## Formato de configuración {#configuration-format}

El formato de la configuración de asignación de rutas contiene dos secciones (`mappings` y `includes`) similares al ejemplo siguiente.

```json
{
  "mappings": [
    "/content/aem-boilerplate/:/",
    "/content/aem-boilerplate/configuration:/.helix/config.json"
  ],
  "includes:" [
    "/content/aem-boilerplate/"
  ]
}
```

### mappings {#mappings}

La configuración `mappings` contiene una matriz de rutas internas (en la instancia de creación de AEM) y rutas URL externas (en el sitio web público).

El formato es `<internal paths>:<external path>`. Suele consistir en un mínimo de dos entradas.

1. La primera entrada del ejemplo es la asignación de rutas de las páginas del sitio web.
1. La segunda entrada controla la asignación de `.helix/config.json` a la página de hoja de cálculo correspondiente en el repositorio de creación de AEM.

En este ejemplo, todas las páginas almacenadas en `/content/aem-boilerplate/...` serán de acceso público en el sitio de Edge Delivery Services directamente en `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Todos los datos tabulares administrados como hojas de cálculo (por ejemplo, metadatos, redireccionamientos y taxonomía) suelen publicarse como URL de API `.json` en Edge Delivery Services. Para ello, deben aparecer individualmente en la configuración de asignación.
>
>Consulte el documento [Uso de hojas de cálculo para administrar datos tabulares](/help/edge/wysiwyg-authoring/tabular-data.md) para obtener más información.

### includes {#includes}

La configuración `includes` controla qué rutas de contenido se replican realmente en Edge Delivery Services. También puede contener cualquier matriz de rutas y, por lo general, contiene la página raíz de nivel superior del sitio.

Los recursos utilizados en las páginas de Edge Delivery Services suelen publicarse junto a la página web. Se exportarán desde la instancia de creación de AEM a Edge Delivery Services automáticamente.

>[!TIP]
>
>Si tiene un caso de uso en el que desea que los recursos se publiquen directamente en Edge Delivery Services (por ejemplo, desea que se pueda acceder directamente a las imágenes o a los PDF mediante sus URL fuera del contexto de una página), deberá añadir también las rutas DAM a la sección `includes` de la configuración.
>
>Por ejemplo, si una carpeta raíz de recursos como `/content/dam/my-site/documents` que contiene un conjunto de PDF debe ser de acceso público a través de `/assets/...`, se debe añadir una entrada a la sección `includes` de la configuración.

## Cómo realizar la configuración {#how-to-configure}

Las asignaciones de rutas se pueden configurar de una de las dos maneras siguientes, según la configuración del proyecto.

1. Si el proyecto está configurado para `aem.live` y usa el [servicio de configuración](https://www.aem.live/docs/config-service-setup) para las configuraciones centralizadas, la asignación de rutas para cada sitio se configura mediante este servicio de configuración.

   * Este es un ejemplo de solicitud de cURL para configurar asignaciones de ruta.

   ```text
   curl --request POST \
     --url https://admin.aem.page/config/{org}/sites/{site}/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: ......' \
     --data '{
       "paths": {
       "mappings": [
         "/content/aem-boilerplate/:/",
         "/content/aem-boilerplate/configuration:/.helix/config.json"
       ],
       "includes": [
         "/content/aem-boilerplate/"
       ]
   }
   }'
   ```

1. Si el proyecto no utiliza el servicio de configuración, la asignación de rutas se configura mediante un archivo `paths.json` en el repositorio de GitHub de los proyectos.

   * Consulte [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) para ver un ejemplo.

En ambos casos, una vez configuradas las asignaciones de rutas, puede comprobar la configuración a través de la URL de configuración de acceso público `https://<branch>--<site>--<org>.aem.page/config.json`.
