---
title: Buscar API de Assets
description: Aprenda a utilizar la API de Search Assets.
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: ef5161d89083284544283c8e059c5817faacbbb3
workflow-type: tm+mt
source-wordcount: '1394'
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

Para invocar la API de búsqueda, se requiere un token de IMS para definir en los detalles de `Authorization`. El token de IMS se obtiene de una cuenta técnica. Consulte [Recuperar las credenciales de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para crear una nueva cuenta técnica. Consulte [Generación del token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para generar el token de IMS y utilizarlo correctamente en el encabezado de solicitud de API de recursos de búsqueda.

Para ver ejemplos de solicitudes, ejemplos de respuestas y códigos de respuesta, consulte [Buscar API de Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/search).

## Preguntas frecuentes {#faqs-search-assets-apis}

### ¿Qué es la API de Search Assets en Dynamic Media con OpenAPI y qué hace? {#search-assets-api-overview}

La API de Assets de búsqueda de Dynamic Media con OpenAPI permite buscar recursos aprobados en el repositorio de Adobe Experience Manager Assets y enviarlos a aplicaciones de flujo descendente integradas mediante una URL de entrega. La búsqueda de recursos aprobados es el primer paso en el flujo de trabajo de entrega: la respuesta de la API devuelve una matriz de documentos JSON para cada recurso que cumple los criterios de búsqueda, cada uno identificado por un campo de ID que se utiliza para componer la solicitud de entrega de recursos. La API de Search Assets admite la búsqueda de texto completo, la búsqueda basada en filtros, la ordenación de resultados y la paginación dentro de una sola solicitud.

### ¿Qué capacidades de búsqueda admite la API de Search Assets? {#search-assets-api-capabilities}

La API de Assets de búsqueda de Dynamic Media con OpenAPI admite cuatro funciones de búsqueda principales. La búsqueda de texto completo utiliza la consulta de coincidencia para buscar texto y admite operadores para filtrar resultados. La búsqueda basada en filtros utiliza el término consulta para filtrar los resultados por una clave y uno o varios valores, o la consulta de rango para filtrar por un rango de valores utilizando los operadores mayor que, mayor o igual que, menor que y menor o igual que. La ordenación de resultados utiliza la propiedad OrderBy para ordenar los resultados en función de uno o varios campos en orden ascendente o descendente. La paginación utiliza las propiedades limit y cursor para controlar el número de resultados devueltos por solicitud y para recuperar páginas de resultados posteriores.

### ¿Cómo realizo una búsqueda de texto completo mediante la API de Search Assets? {#search-assets-api-full-text-search}

La búsqueda de texto completo en Dynamic Media con la API de Assets de búsqueda de OpenAPI se realiza mediante la propiedad match query en el cuerpo de la solicitud. Defina el texto que desea buscar dentro de la consulta de coincidencia. Los operadores también se pueden utilizar dentro de la consulta de coincidencia para filtrar aún más los resultados devueltos. La consulta de coincidencia busca en los recursos aprobados del repositorio de AEM Assets y devuelve una matriz JSON de recursos coincidentes, cada uno identificado por un campo de ID utilizado para componer la dirección URL de entrega.

### ¿Cómo filtro los resultados de búsqueda mediante la API de Search Assets? {#search-assets-api-filters}

La API de Assets de búsqueda de Dynamic Media con OpenAPI admite dos tipos de consultas de filtro. El término consulta filtra los resultados especificando una clave (que identifica el campo con el que debe coincidir) y uno o varios valores con los que debe coincidir. El rango filtra los resultados de consulta para un campo específico utilizando un rango definido con los siguientes operadores: Mayor que (gt), Mayor que o igual a (gte), Menor que (lt) y Menor que o igual a (lte). Ambos tipos de consulta se pueden utilizar dentro de la misma solicitud de API para aplicar varios filtros simultáneamente.

### ¿Cómo funciona la paginación en la API de Search Assets? {#search-assets-api-pagination}

La paginación en Dynamic Media con la API Search Assets de OpenAPI se controla mediante dos propiedades en la solicitud: limit y cursor. La propiedad limit define el número máximo de recursos que se recuperarán en una sola respuesta de API. La propiedad cursor define el punto de partida del siguiente conjunto de recursos en función del límite definido. Por ejemplo, si se establece un límite de 50 en la primera solicitud, se devuelven los 50 primeros recursos coincidentes; la propiedad cursor en la siguiente solicitud recupera los 50 recursos siguientes, lo que permite el recorrido secuencial de grandes conjuntos de resultados.

### ¿Cómo puedo ordenar los resultados de búsqueda devueltos por la API de Search Assets? {#search-assets-api-sort}

Los resultados de búsqueda en Dynamic Media con la API de Search Assets de OpenAPI se ordenan mediante la propiedad OrderBy del cuerpo de la solicitud. Especifique uno o varios campos en la propiedad OrderBy para ordenar los resultados. La ordenación se puede aplicar en orden ascendente o descendente. Se pueden combinar varios campos de ordenación para aplicar la ordenación por capas en los resultados de búsqueda devueltos por la API.

### ¿Cuál es el formato de punto de conexión para la API de Search Assets? {#search-assets-api-endpoint=faqs}

El extremo de la API de Assets de búsqueda de Dynamic Media con OpenAPI debe seguir este formato: https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search. El dominio de envío tiene una estructura similar al dominio de entorno de creación de AEM; la única diferencia es reemplazar el término autor por envío. En la dirección URL, pXXXX hace referencia al ID de programa y AAAA hace referencia al ID de entorno. La API de Search Assets utiliza el método de solicitud HTTP POST.

### ¿Qué encabezados son necesarios para llamar a la API de Search Assets? {#search-assets-api-headers}

La API de Assets de búsqueda de Dynamic Media con OpenAPI requiere cuatro campos de encabezado: Content-Type establecido en application/json, X-Adobe-Accept-Experimental establecido en 1, Autorización como token de portador que contiene el token de IMS y X-Api-Key que contiene la clave de API. El token de IMS se obtiene de una cuenta técnica creada con el flujo de trabajo de credenciales de AEM as a Cloud Service. La cuenta técnica debe crearse y el token de acceso debe generarse antes de poder invocar la API de Search Assets.

### ¿Qué función desempeña el campo de ID en la respuesta de la API de Search Assets? {#search-assets-api-response-id}

Cada documento JSON de la respuesta de la API de Search Assets corresponde a un recurso que cumple los criterios de búsqueda y se identifica con un campo de ID. Este campo de ID es el identificador de recurso utilizado para componer la solicitud de entrega de recursos; se pasa como parámetro assetId en Dynamic Media con la URL de punto de conexión de la API de entrega de OpenAPI. La captura del ID a partir de la respuesta de búsqueda es un paso necesario en el flujo de trabajo completo de búsqueda para encontrar y enviar un recurso aprobado a través de una URL de entrega.