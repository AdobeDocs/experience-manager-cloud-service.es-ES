---
title: Asignación de rutas para Edge Delivery Services
description: AEM Obtenga información sobre cómo asignar las rutas de página utilizadas en la instancia de creación de a las rutas de página públicas utilizadas en el sitio web y controlar qué contenido se publica en los Edge Delivery Services.
feature: Edge Delivery Services
role: User
source-git-commit: 51a2b453ccce39cb42c927a088bc088083545542
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Asignación de rutas para Edge Delivery Services {#path-mapping}

AEM Obtenga información sobre cómo asignar las rutas de página utilizadas en la instancia de creación de a las rutas de página públicas utilizadas en el sitio web y controlar qué contenido se publica en los Edge Delivery Services.

## Información general {#overview}

Para poder crear contenido de WYSIWYG AEM mediante el uso de la y publicarlo en Edge Delivery Services, debe configurar la asignación de ruta del proyecto. Esta asignación tiene dos propósitos.

* AEM Asigna y crea una relación entre las rutas de página utilizadas en la instancia de creación de y las rutas de página públicas utilizadas en el sitio web.
* Controla qué contenido (páginas, hojas, recursos, etc.) se publican para los Edge Delivery Services.

La asignación de ruta debe configurarse para cada proyecto de forma individual y según el contenido del proyecto y la estructura de la URL. AEM Lo utiliza el usuario durante la publicación de contenido y la edición de contenido en el [Editor universal.](/help/sites-cloud/authoring/universal-editor/navigation.md)

## Formato de configuración {#configuration-format}

El formato de la configuración de asignación de ruta de acceso contiene dos secciones (`mappings` y `includes`) similares al ejemplo siguiente.

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

### asignaciones {#mappings}

AEM La configuración de `mappings` contiene una matriz de rutas internas (en la instancia de creación de la) y rutas de URL externas (en el sitio web público).

El formato es `<internal paths>:<external path>`. Suele consistir en un mínimo de dos entradas.

1. La primera entrada del ejemplo es la asignación de ruta de las páginas del sitio web.
1. AEM La segunda entrada controla la asignación de `.helix/config.json` a la página de hoja de cálculo correspondiente en el repositorio de creación de la.

En este ejemplo, todas las páginas almacenadas bajo `/content/aem-boilerplate/...` serán de acceso público en el sitio de Edge Delivery Services directamente bajo `https://main--my-site--org.aem.live/....`.

>[!TIP]
>
>Todos los datos de tablas administrados como hojas de cálculo (p. ej., metadatos, redirecciones y taxonomía) se publican normalmente como `.json` direcciones URL de API en los Edge Delivery Services. Para ello, deben aparecer individualmente en la configuración de asignación.
>
>Consulte el documento [Uso de hojas de cálculo para administrar datos tabulares](/help/edge/wysiwyg-authoring/tabular-data.md) para obtener más información.

### incluye {#includes}

La configuración de `includes` controla qué rutas de contenido se replican realmente en los Edge Delivery Services. También puede contener cualquier matriz de rutas y, por lo general, contiene la página raíz de nivel superior del sitio.

Assets que se utiliza en páginas de Edge Delivery Services suele publicarse junto con la página web. AEM Se exportan automáticamente desde la instancia de creación de la a los Edge Delivery Services.

>[!TIP]
>
>Si tiene un caso de uso en el que desea que los recursos se publiquen directamente en los Edge Delivery Services (por ejemplo, desea que las imágenes o los PDF sean accesibles directamente por sus direcciones URL fuera del contexto de una página), también debe agregar las rutas DAM a la sección `includes` de la configuración.
>
>Por ejemplo, si una carpeta raíz de recursos como `/content/dam/my-site/documents` que contiene un conjunto de PDF debe ser de acceso público a través de `/assets/...`, se debe agregar una entrada a la sección `includes` de la configuración.

## Cómo configurar {#how-to-configure}

Las asignaciones de rutas se pueden configurar de una de las dos maneras siguientes, según la configuración del proyecto.

1. Si el proyecto está configurado para `aem.live` y usa el [servicio de configuración](https://www.aem.live/docs/config-service-setup) para las configuraciones centralizadas, la asignación de rutas para cada sitio se configura mediante este servicio de configuración.

   * Este es un ejemplo de solicitud de cURL para configurar asignaciones de ruta.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/{org}/sites/{site}/public.json \
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

1. Si el proyecto no utiliza el servicio de configuración, la asignación de rutas se configura mediante un archivo paths.json en el repositorio de GitHub de sus proyectos.

   * Vea [`https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json`](/https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/paths.json) para ver un ejemplo.

En ambos casos, una vez configuradas las asignaciones de rutas, puede comprobar la configuración a través de la URL de configuración de acceso público `https://<branch>--<site>--<org>.aem.page/config.json`.
