---
title: Buscar API de Assets
description: Aprenda a utilizar la API de Search Assets.
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Buscar API de Assets {#search-assets-api}

Todo [recursos aprobados](approve-assets.md) Los recursos disponibles en el repositorio de recursos de Experience Manager se pueden buscar y luego enviar a aplicaciones de flujo descendente integradas mediante una URL de entrega.

La búsqueda de los recursos aprobados adecuados desde el repositorio de Experience Manager es el primer paso para entregar recursos mediante la URL de entrega. La respuesta a la solicitud de búsqueda incluye una matriz de documentos JSON correspondientes a los recursos que cumplen los criterios de búsqueda. Cada documento JSON se identifica mediante una `id` , que se utiliza para componer la solicitud de envío de recursos.

![Descripción general del protocolo de carga binaria directa](assets/search-assets-api-overview.png)

Puede definir propiedades dentro de la solicitud de API de Search Assets para habilitar las siguientes funciones:

* **Búsqueda de texto completo**: utilice el `match` consulta para definir el texto que se va a buscar.  También puede utilizar operadores dentro de `match` consulta para filtrar los resultados.

* **Aplicar filtros**: utilice el `term` consulta para filtrar aún más los resultados definiendo un `key` y uno o varios valores. `key` identifica el campo cuyo valor debe coincidir y `value` representa con qué emparejar. Del mismo modo, puede utilizar la variable `range` consulta para definir un rango para un campo con las propiedades Mayor que (gt), Mayor que o igual a (gte), Menor que (lt) y Menor que o igual a (lte).

* **Ordenar resultados**: utilice el `OrderBy` para ordenar los resultados de búsqueda en función de uno o varios campos. Puede ordenar los resultados en orden ascendente o descendente.

* **Paginación**: utilice el `limit` y `cursor` propiedades para definir propiedades de paginación dentro de una solicitud de API de búsqueda. `limit` define el número máximo de elementos que se recuperarán en una respuesta de API. `cursor` facilita la recuperación del punto de partida para el siguiente conjunto de recursos definidos en la variable `limit` propiedad. Por ejemplo, si define `50` como límite en la solicitud de API, puede utilizar el `cursor` para iniciar y recuperar los siguientes 50 elementos mediante la siguiente solicitud de API.

## Buscar extremo de API de recursos {#search-assets-api-endpoint}

El punto final de una solicitud de API de recursos de búsqueda debe tener el siguiente formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

El dominio de envío tiene una estructura similar al dominio del entorno de creación de Experience Manager. La única diferencia es reemplazar el término `author` con `delivery`.

`pXXXX` hace referencia al ID de programa

`eYYYY` hace referencia al ID de entorno

## Método de solicitud de API de recursos de búsqueda {#search-assets-api-request-method}

POST

## Buscar encabezado de API de Assets {#search-assets-api-header}

Debe proporcionar los siguientes detalles al definir un encabezado en la API de búsqueda de recursos:

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

Para invocar la API de búsqueda, se requiere un token de IMS para definir en la variable `Authorization` detalles. El token de IMS se obtiene de una cuenta técnica. Consulte [Recuperar las credenciales de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para crear una nueva cuenta técnica. Consulte [Generación del token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para generar el token de IMS y utilizarlo correctamente en el encabezado de solicitud de API de Search Assets.

Para ver ejemplos de solicitudes, ejemplos de respuestas y códigos de respuesta, consulte [Buscar API de Assets](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).

