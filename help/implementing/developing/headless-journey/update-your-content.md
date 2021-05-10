---
title: Cómo actualizar su contenido a través de las API de AEM Assets
description: En esta parte del Recorrido para desarrolladores sin encabezado de AEM, aprenda a utilizar la API de REST para acceder y actualizar el contenido de sus fragmentos de contenido.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 787af0d4994bf1871c48aadab74d85bd7c3c94fb
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 2%

---

# Cómo actualizar su contenido a través de las API de AEM Assets {#update-your-content}

>[!CAUTION]
>
>TRABAJO EN CURSO - La creación de este documento está en curso y no debe entenderse como completo o definitivo ni debe utilizarse con fines de producción.

En esta parte del [AEM Recorrido para desarrolladores sin encabezado,](overview.md) aprende a utilizar la API de REST para acceder y actualizar el contenido de sus fragmentos de contenido.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido sin AEM encabezado, [Cómo acceder al contenido a través de las API de envío de AEM](access-your-content.md), ha aprendido a acceder al contenido sin encabezado en AEM a través de la API de AEM GraphQL y ahora debería:

* Conocer GraphQL de alto nivel.
* Comprender cómo funciona la API de AEM GraphQL.
* Comprender algunas consultas de ejemplo prácticas.

Este artículo se basa en estos aspectos básicos para que pueda comprender cómo actualizar el contenido sin encabezado existente en AEM a través de la API de REST.

## Objetivo {#objective}

* **Audiencia**: Avanzadas
* **Objetivo**: Aprenda a utilizar la API de REST para acceder y actualizar el contenido de los fragmentos de contenido:
   * Introduzca la API HTTP de AEM Assets.
   * Presente y discuta la compatibilidad con fragmentos de contenido en la API.
   * Ilustrar detalles de la API.

<!--
  * Look at sample code to see how things work in practice.
-->

## ¿Por qué necesita la API HTTP de recursos para el fragmento de contenido {#why-http-api}

En la fase anterior del Recorrido sin encabezado, ha aprendido a utilizar la API de AEM GraphQL para recuperar el contenido mediante consultas.

Entonces, ¿por qué se necesita otra API?

La API HTTP de Assets le permite **Leer** su contenido, pero también le permite **Crear**, **Actualizar** y **Eliminar** contenido: acciones que no son posibles con la API de GraphQL.

La API de REST de Assets está disponible en cada instalación predeterminada de una versión reciente de Adobe Experience Manager as a Cloud Service.

## API de HTTP de Assets {#assets-http-api}

La [API HTTP de recursos](/help/assets/mac-api-assets.md) incluye lo siguiente:

* API de REST de recursos
* incluida la compatibilidad con fragmentos de contenido

La implementación actual de la API HTTP de Assets se basa en el estilo arquitectónico **REST**.

La API de REST de recursos permite a los desarrolladores de Adobe Experience Manager como Cloud Service acceder al contenido (almacenado en AEM) directamente a través de la API HTTP mediante operaciones **CRUD** (Crear, Leer, Actualizar, Eliminar).

Con estas operaciones, la API le permite operar Adobe Experience Manager como Cloud Service como CMS sin encabezado (Content Management System) al proporcionar Content Services a una aplicación JavaScript front-end. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON. Por ejemplo, las aplicaciones de una sola página (SPA), basadas en marcos o personalizadas, requieren contenido proporcionado a través de una API, a menudo en formato JSON.

>[!NOTE]
>
>No es posible personalizar la salida JSON desde la API de REST de Assets.

La API de REST de Assets:

* sigue el principio de HATEOAS
* implementa el formato SIREN

## Conceptos clave {#key-concepts}

La API de REST de recursos ofrece acceso de estilo REST a los recursos almacenados en una instancia de AEM.

Utiliza el extremo `/api/assets` y requiere la ruta del recurso para acceder a él (sin el `/content/dam` inicial).

* Esto significa que para acceder al recurso en:
   * `/content/dam/path/to/asset`
* Debe solicitar:
   * `/api/assets/path/to/asset`

Por ejemplo, para acceder a `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acceso:
>
>* `/api/assets` **no** necesita el uso del  `.model` selector.
>* `/content/path/to/page` **** requiere el uso del  `.model` selector.


El método HTTP determina la operación que se va a ejecutar:

* **GET** : para recuperar una representación JSON de un recurso o una carpeta
* **POST** : para crear nuevos recursos o carpetas
* **PUT** : para actualizar las propiedades de un recurso o una carpeta
* **DELETE** : para eliminar un recurso o una carpeta

>[!NOTE]
>
>Los parámetros del cuerpo de la solicitud o de la URL se pueden usar para configurar algunas de estas operaciones; por ejemplo, defina que una carpeta o un recurso deben crearse mediante una solicitud **POST**.

El formato exacto de las solicitudes admitidas se define en la documentación de referencia de la API.

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que las solicitudes posteriores (`write`) no se pueden combinar en una sola transacción que pueda tener éxito o fallar como una sola entidad.

### Seguridad {#security}

Si la API de REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, AEM filtro CORS debe configurarse correctamente.

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* Se explica el CORS/AEM
>* Vídeo: Desarrollo para CORS con AEM


En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso; consulte Trabajo con fragmentos de contenido.

Para obtener más información sobre las funciones disponibles mediante la API, consulte:

* La API de REST de Assets (recursos adicionales)
* Tipos de entidades, donde se explican las funciones específicas de cada tipo admitido (según corresponda a los fragmentos de contenido)

### Paginación {#paging}

La API de REST de recursos admite la paginación (para solicitudes de GET) mediante los parámetros de URL:

* `offset` - el número de la primera entidad (secundaria) que se va a recuperar
* `limit` - el número máximo de entidades devueltas

La respuesta contendrá información de paginación como parte de la sección `properties` de la salida SIREN. Esta propiedad `srn:paging` contiene el número total de entidades (secundarias) ( `total`), el desplazamiento y el límite ( `offset`, `limit`) según se especifica en la solicitud.

>[!NOTE]
>
>El paginación se suele aplicar a entidades de contenedor (es decir, carpetas o recursos con representaciones), ya que está relacionado con los elementos secundarios de la entidad solicitada.

#### Ejemplo: Paginación {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipos de entidad {#entity-types}

### Carpetas {#folders}

Las carpetas actúan como contenedores para los recursos y otras carpetas. Reflejan la estructura del repositorio de contenido AEM.

La API de REST de Assets expone el acceso a las propiedades de una carpeta; por ejemplo, su nombre, título, etc. Los recursos se exponen como entidades secundarias de carpetas y subcarpetas.

>[!NOTE]
>
>En función del tipo de recurso de los recursos secundarios y las carpetas, la lista de entidades secundarias puede contener ya el conjunto completo de propiedades que define la entidad secundaria correspondiente. Alternativamente, solo se puede exponer un conjunto reducido de propiedades para una entidad de esta lista de entidades secundarias.

### Assets {#assets}

Si se solicita un recurso, la respuesta devolverá sus metadatos; como título, nombre y otra información tal como se define en el esquema de recursos correspondiente.

Los datos binarios de un recurso se exponen como un vínculo SIREN de tipo `content`.

Los recursos pueden tener varias representaciones. Generalmente se exponen como entidades secundarias, siendo una excepción una representación en miniatura, que se expone como un vínculo de tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de contenido {#content-fragments}

Un fragmento de contenido es un tipo especial de recurso. Se pueden utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros.

Dado que existen varias diferencias con los recursos *estándar* (como imágenes o audio), se aplican algunas reglas adicionales para manejarlos.

#### Representación {#representation}

Fragmentos de contenido:

* No exponer ningún dato binario.
* Están completamente contenidos en la salida JSON (dentro de la propiedad `properties` ).

* También se consideran atómicos, es decir, los elementos y variaciones se exponen como parte de las propiedades del fragmento frente a como vínculos o entidades secundarias. Esto permite un acceso eficaz a la carga útil de un fragmento.

#### Modelos de contenido y fragmentos de contenido {#content-models-and-content-fragments}

Actualmente, los modelos que definen la estructura de un fragmento de contenido no se exponen a través de una API HTTP. Por lo tanto, el *consumidor* necesita conocer el modelo de un fragmento (al menos un mínimo), aunque la mayoría de la información se puede inferir de la carga útil; como tipos de datos, etc. forman parte de la definición.

Para crear un nuevo fragmento de contenido, se debe proporcionar la ruta (repositorio interno) del modelo.

#### Contenido asociado {#associated-content}

El contenido asociado no está expuesto actualmente.

## Uso de la API de REST de Assets {#using-aem-assets-rest-api}

El uso puede variar en función de si utiliza un entorno de publicación o autor de AEM, junto con su caso de uso específico.

* Se recomienda encarecidamente que la creación esté enlazada a una instancia de autor ([y actualmente no hay forma de replicar un fragmento para publicarlo con esta API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* La entrega es posible desde ambos, ya AEM sirve contenido solicitado solo en formato JSON.

   * El almacenamiento y el envío desde una instancia de autor AEM deben ser suficientes para las aplicaciones de biblioteca multimedia y detrás del firewall.

   * Para la entrega web activa, se recomienda una instancia de publicación AEM.

>[!CAUTION]
>
>La configuración de Dispatcher en AEM instancias de nube podría bloquear el acceso a `/api`.

>[!NOTE]
>
>Para obtener más información, consulte la [Referencia de API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). En concreto, [API de Adobe Experience Manager Assets - Fragmentos de contenido](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html).

### Lectura/Entrega {#read-delivery}

El uso se realiza mediante:

`GET /{cfParentPath}/{cfName}.json`

Por ejemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

La respuesta es un archivo JSON serializado con el contenido estructurado como en el fragmento de contenido. Las referencias se envían como direcciones URL de referencia.

Se pueden realizar dos tipos de operaciones de lectura:

* Al leer un fragmento de contenido específico por ruta, esto devuelve la representación JSON del fragmento de contenido.
* Leer una carpeta de fragmentos de contenido por ruta: esto devuelve las representaciones JSON de todos los fragmentos de contenido de la carpeta.

### Crear {#create}

El uso se realiza mediante:

`POST /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON del fragmento de contenido que se va a crear, incluido cualquier contenido inicial que se deba configurar en los elementos del fragmento de contenido. Es obligatorio establecer la propiedad `cq:model` y debe apuntar a un modelo de fragmento de contenido válido. Si no lo hace, se producirá un error. También es necesario agregar un encabezado `Content-Type` que esté configurado como `application/json`.

### Actualizar {#update}

El uso se realiza mediante

`PUT /{cfParentPath}/{cfName}`

El cuerpo debe contener una representación JSON de lo que se debe actualizar para el fragmento de contenido determinado.

Puede ser simplemente el título o la descripción de un fragmento de contenido, o un solo elemento, o todos los valores o metadatos de elementos.

### Eliminar {#delete}

El uso se realiza mediante:

`DELETE /{cfParentPath}/{cfName}`

Para obtener más información sobre el uso de la API REST de AEM Assets, puede hacer referencia a:

* API HTTP de Adobe Experience Manager Assets (recursos adicionales)
* Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets (recursos adicionales)

## Siguientes {#whats-next}

Ahora que ha completado esta parte del Recorrido para desarrolladores sin encabezado de AEM, debe:

* Comprender los conceptos básicos de la API HTTP de AEM Assets.
* Comprenda cómo se admiten los fragmentos de contenido en esta API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

Debería continuar con su recorrido sin AEM al revisar el documento [Cómo ponerlo todo juntos: su aplicación y su contenido en AEM sin encabezado](put-it-all-together.md) donde aprenderá a tomar su proyecto sin encabezado de AEM y prepararlo para su lanzamiento.

## Recursos adicionales {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [Principio de HATEOEA](https://en.wikipedia.org/wiki/HATEOAS)
* [Formato SIREN](https://github.com/kevinswiber/siren)
* [API de HTTP de Assets](/help/assets/mac-api-assets.md)
* [API de REST de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [Referencia de API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
* [AEM Core Components](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html)
* [Se explica el CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Vídeo: Desarrollo para CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

