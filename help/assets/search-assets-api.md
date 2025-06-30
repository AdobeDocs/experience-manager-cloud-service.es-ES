---
title: Buscar API de Assets
description: Aprenda a utilizar la API de Search Assets.
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Buscar API de Assets {#search-assets-api}

Todos los [recursos aprobados](approve-assets.md) disponibles en el repositorio de recursos de Experience Manager se pueden buscar y luego enviar a aplicaciones de flujo descendente integradas usando una URL de envío.

La búsqueda de los recursos aprobados adecuados desde el repositorio de Experience Manager es el primer paso para entregar recursos mediante la URL de entrega. La respuesta a la solicitud de búsqueda incluye una matriz de documentos JSON correspondientes a los recursos que cumplen los criterios de búsqueda. Cada documento JSON se identifica con un campo `id`, que se utiliza para componer la solicitud de entrega de recursos.

![Descripción general del protocolo de carga binaria directa](assets/search-assets-api-overview.png)

Puede definir propiedades dentro de la solicitud de API de Search Assets para habilitar las siguientes funciones:

* **Búsqueda de texto completo**: use la consulta `match` para definir el texto que desea buscar.  También puede usar operadores dentro de la consulta `match` para filtrar los resultados.

* **Aplicar filtros**: utilice la consulta `term` para filtrar aún más los resultados definiendo `key` y uno o varios valores. `key` identifica el campo cuyo valor debe coincidir y `value` representa con qué debe coincidir. Del mismo modo, puede utilizar la consulta `range` para definir un intervalo para un campo mediante las propiedades Mayor que (gt), Mayor que o igual a (gte), Menor que (lt) y Menor que o igual a (lte).

* **Ordenar resultados**: use la propiedad `OrderBy` para ordenar los resultados de búsqueda en función de uno o varios campos. Puede ordenar los resultados en orden ascendente o descendente.

* **Paginación**: use las propiedades `limit` y `cursor` para definir propiedades de paginación dentro de una solicitud de API de búsqueda. La propiedad `limit` define el número máximo de elementos que se recuperarán en una respuesta de API. La propiedad `cursor` facilita la recuperación del punto de partida para el siguiente conjunto de recursos definidos en la propiedad `limit`. Por ejemplo, si define `50` como el límite en la solicitud de API, puede utilizar la propiedad `cursor` para iniciar y recuperar los siguientes 50 elementos mediante la siguiente solicitud de API.

## Buscar extremo de API de recursos {#search-assets-api-endpoint}

El punto final de una solicitud de API de recursos de búsqueda debe tener el siguiente formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

El dominio de envío tiene una estructura similar al dominio del entorno de creación de Experience Manager. La única diferencia es reemplazar el término `author` por `delivery`.

`pXXXX` hace referencia al ID de programa

`eYYYY` hace referencia al ID de entorno

## Método de solicitud de API de recursos de búsqueda {#search-assets-api-request-method}

PUBLICAR

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

Para invocar la API de búsqueda, se requiere un token de IMS para definir en los detalles de `Authorization`. El token de IMS se obtiene de una cuenta técnica. Consulte [Recuperar las credenciales de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=es#fetch-the-aem-as-a-cloud-service-credentials) para crear una nueva cuenta técnica. Consulte [Generación del token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=es#generating-the-access-token) para generar el token de IMS y utilizarlo correctamente en el encabezado de solicitud de API de recursos de búsqueda.

Para ver ejemplos de solicitudes, ejemplos de respuestas y códigos de respuesta, consulte [Buscar API de Assets](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).
