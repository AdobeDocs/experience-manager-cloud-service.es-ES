---
title: Compatibilidad con fragmentos de contenido de Adobe Experience Manager as a Cloud Service en la API HTTP de Assets
description: Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de entrega sin encabezado de Adobe Experience Manager.
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: 04d1f4f312c9cd256430a2134b308e45dde2c4d7
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 14%

---

# Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Información general {#overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

>[!CAUTION]
>
>La compatibilidad con fragmentos de contenido en la API HTTP de Assets ahora está [obsoleta](/help/release-notes/deprecated-removed-features.md).
>
>Ha sido reemplazado por [Entrega de fragmentos de contenido con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) junto con [API de administración de fragmentos de contenido y modelos de fragmentos de contenido](/help/headless/content-fragment-openapis.md).

Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de entrega sin encabezado de Adobe Experience Manager (AEM).

>[!NOTE]
>
>Consulte [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

>[!NOTE]
>
>La [API HTTP de Assets](/help/assets/mac-api-assets.md) incluye:
>
>* La API de REST de Recursos
>* incluye compatibilidad con los fragmentos de contenido
>
>La implementación actual de la API HTTP de Assets se basa en el estilo de arquitectura [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).

>[!NOTE]
>
>Para obtener la información más reciente sobre las API de Experience Manager, visita [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

La [API de REST de Assets](/help/assets/mac-api-assets.md) permite a los desarrolladores de Adobe Experience Manager as a Cloud Service acceder al contenido (almacenado en AEM) directamente a través de la API HTTP mediante las operaciones CRUD (Crear, Leer, Actualizar, Eliminar).

La API le permite utilizar Adobe Experience Manager as a Cloud Service como CMS sin encabezado (sistema de administración de contenido) proporcionando servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON.

Por ejemplo, [las aplicaciones de una sola página (SPA)](/help/implementing/developing/hybrid/introduction.md), basadas en un marco de trabajo o personalizadas, requieren contenido proporcionado a través de la API HTTP, a menudo en formato JSON.

Aunque [Componentes principales de AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) proporcionan una API personalizable que puede servir las operaciones de lectura necesarias para este fin y cuya salida JSON se puede personalizar, requieren el conocimiento WCM (Administración de contenido web) de AEM para la implementación. Esto se debe a que deben alojarse en páginas basadas en plantillas de AEM específicas. No todas las organizaciones de desarrollo de la SPA tienen acceso directo a esos conocimientos.

Es entonces cuando se puede utilizar la API de REST de Assets. Permite a los desarrolladores acceder a recursos (por ejemplo, imágenes y fragmentos de contenido) directamente, sin necesidad de incrustarlos primero en una página, y enviar su contenido en formato JSON serializado.

>[!NOTE]
>
>No es posible personalizar la salida JSON desde la API de REST de Assets.

La API de REST de Assets también permite a los desarrolladores modificar contenido: creando nuevos recursos, fragmentos de contenido y carpetas, actualizándolos o eliminándolos.

La API de REST de Assets:

* sigue el [principio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa [formato SIREN](https://github.com/kevinswiber/siren)

## Requisitos previos {#prerequisites}

La API de REST de Recursos está disponible en cada instalación predeterminada de una versión reciente de Adobe Experience Manager as a Cloud Service.

## Conceptos clave {#key-concepts}

La API de REST de Assets ofrece acceso de tipo [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) a los recursos almacenados en una instancia de AEM.

Utiliza el extremo `/api/assets` y requiere la ruta del recurso para acceder a él (sin el `/content/dam` inicial).

* Esto significa que para acceder al recurso en:
   * `/content/dam/path/to/asset`
* Solicitud:
   * `/api/assets/path/to/asset`

Por ejemplo, para acceder a `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Acceso:
>
>* `/api/assets` **no** necesita el uso del selector `.model`.
>* `/content/path/to/page` **sí** necesita el uso del selector `.model`.

El método HTTP determina la operación que se va a ejecutar:

* **GET**: recuperar una representación JSON de un recurso o una carpeta.
* **POST**: para crear recursos o carpetas
* **PUT**: actualizar las propiedades de un recurso o carpeta.
* **DELETE**: eliminar un recurso o carpeta.

>[!NOTE]
>
>El cuerpo de solicitud o los parámetros de URL se pueden usar para configurar algunas de estas operaciones; por ejemplo, definir que una carpeta o un recurso deben crearse mediante una solicitud **POST**.

El formato exacto de las solicitudes admitidas se define en la [Documentación de referencia de la API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference).

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que las solicitudes posteriores (`write`) no se pueden combinar en una sola transacción que se realice correctamente o que falle como una sola entidad.

### API de REST de AEM (Assets) frente a componentes de AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API DE REST DE Assets<br/> </td>
   <td>Componente de AEM <br/> (componentes que utilizan modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso admitidos</td>
   <td>De uso general.</td>
   <td><p>Optimizado para el consumo en una aplicación de una sola página (SPA) o en cualquier otro contexto (consumo de contenido).</p> <p>También puede contener información de diseño.</p> </td>
  </tr>
  <tr>
   <td>Operaciones compatibles</td>
   <td><p>Crear, leer, actualizar, eliminar.</p> <p>Con operaciones adicionales, según el tipo de entidad.</p> </td>
   <td>Sólo lectura.</td>
  </tr>
  <tr>
   <td>Acceso</td>
   <td><p>Se puede acceder a ella directamente.</p> <p>Utiliza el extremo <code>/api/assets </code>, asignado a <code>/content/dam</code> (en el repositorio).</p> 
   <p>Una ruta de ejemplo tendría este aspecto: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Se debe hacer referencia a él a través de un componente de AEM en una página de AEM.</p> <p>Utiliza el selector <code>.model</code> para crear la representación JSON.</p> <p>Una ruta de ejemplo tendría este aspecto:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Seguridad</td>
   <td><p>Se pueden seleccionar varias opciones.</p> <p>Se propone OAuth; se puede configurar por separado de la configuración estándar.</p> </td>
   <td>Utiliza la configuración estándar de AEM.</td>
  </tr>
  <tr>
   <td>Observaciones arquitectónicas</td>
   <td><p>El acceso de escritura suele dirigirse a una instancia de autor.</p> <p>Read también se puede dirigir a una instancia de Publish.</p> </td>
   <td>Dado que este método es de solo lectura, generalmente se utiliza para instancias de publicación.</td>
  </tr>
  <tr>
   <td>Salida</td>
   <td>Salida SIREN basada en JSON: detallada, pero potente. Permite navegar dentro del contenido.</td>
   <td>Salida propia basada en JSON; configurable mediante modelos Sling. La navegación por la estructura de contenido es difícil de implementar (pero no necesariamente imposible).</td>
  </tr>
 </tbody>
</table>

### Seguridad {#security}

Si la API de REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, el filtro CORS de AEM debe configurarse correctamente.

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* [Explicación de CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=es)
>* [Vídeo: desarrollo para CORS con AEM (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html?lang=es)
>

En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso. Consulte [Uso de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

Para obtener más información sobre las funciones disponibles a través de la API, consulte:

* La [API de REST de Assets](/help/assets/mac-api-assets.md)
* [Tipos de entidad](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), donde se explican las características específicas de cada tipo admitido (según corresponda a los fragmentos de contenido)

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

### Paginación {#paging}

La API de REST de Assets admite la paginación (para solicitudes de GET) mediante los parámetros de URL:

* `offset`: el número de la primera entidad (secundaria) que se va a recuperar
* `limit`: el número máximo de entidades devueltas

La respuesta contiene información de paginación como parte de la sección `properties` de la salida SIREN. Esta propiedad `srn:paging` contiene el número total de entidades (secundarias) ( `total`), el desplazamiento y el límite ( `offset`, `limit`) especificados en la solicitud.

>[!NOTE]
>
>La paginación se aplica normalmente a entidades contenedoras (es decir, carpetas o activos con representaciones), en lo que se refiere a las tareas secundarias de la entidad solicitada.

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

Las carpetas actúan como contenedores para recursos y otras carpetas. Reflejan la estructura del repositorio de contenido de AEM.

La API de REST de Assets expone el acceso a las propiedades de una carpeta. Por ejemplo, su nombre y título. Assets se expone como entidades secundarias de carpetas y subcarpetas.

>[!NOTE]
>
>Según el tipo de recurso de los recursos y carpetas secundarios, la lista de entidades secundarias puede contener ya el conjunto completo de propiedades que define la entidad secundaria correspondiente. Alternativamente, solo se puede exponer un conjunto reducido de propiedades para una entidad de esta lista de entidades secundarias.

### Recursos {#assets}

Si se solicita un recurso, la respuesta devolverá sus metadatos, como el título, el nombre y otra información tal como se define en el esquema de recursos correspondiente.

Los datos binarios de un recurso se exponen como un vínculo SIREN de tipo `content`.

Assets puede tener varias representaciones. Normalmente se exponen como entidades secundarias; una excepción es una representación en miniatura, que se expone como un vínculo de tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de contenido {#content-fragments}

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Pueden utilizarse para acceder a datos estructurados, como textos, números, fechas, etc.

Dado que existen varias diferencias entre los recursos *estándar* (como imágenes o audio), se aplican algunas reglas adicionales para administrarlos.

#### Representación {#representation}

Fragmentos de contenido:

* No exponga ningún dato binario.
* Están contenidas en la salida JSON (dentro de la propiedad `properties`).

* También se consideran atómicos. Es decir, los elementos y las variaciones se exponen como parte de las propiedades del fragmento en lugar de como vínculos o entidades secundarias. Esto permite un acceso eficiente a la carga útil de un fragmento.

#### Modelos de contenido y fragmentos de contenido {#content-models-and-content-fragments}

Actualmente, los modelos que definen la estructura de un fragmento de contenido no se exponen a través de una API HTTP. Por lo tanto, *consumer* debe conocer el modelo de un fragmento (como mínimo), aunque la mayoría de la información se puede inferir de la carga útil, ya que los tipos de datos, etc., forman parte de la definición.

Para crear un fragmento de contenido, se debe proporcionar la ruta (del repositorio interno) del modelo.

#### Contenido asociado {#associated-content}

El contenido asociado no se expone.

## Utilización {#using}

El uso puede variar en función de si utiliza un entorno de AEM Author o Publish junto con el caso de uso específico.

* Se recomienda que la creación esté enlazada a una instancia de autor ([ y actualmente no hay medios para replicar un fragmento para publicarlo mediante esta API (](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* La entrega es posible desde ambos, ya que AEM sirve contenido solicitado solo en formato JSON.

   * El almacenamiento y el envío desde una instancia de autor de AEM deberían ser suficientes para las aplicaciones de biblioteca de medios detrás del cortafuegos.

   * Para la entrega web en directo, se recomienda una instancia de publicación de AEM.

>[!CAUTION]
>
>La configuración de Dispatcher en las instancias de nube de AEM podría bloquear el acceso a `/api`.

>[!NOTE]
>
>Consulte la [Referencia de API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). En particular, la [API de Adobe Experience Manager Assets: fragmentos de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

## Limitaciones {#limitations}

Hay algunas limitaciones:

* **Actualmente no se admiten los modelos de fragmento de contenido**: no se pueden leer ni crear. Para poder crear o actualizar un fragmento de contenido existente, los desarrolladores deben conocer la ruta correcta al modelo de fragmento de contenido. Actualmente, el único método para obtener una descripción general de estos es a través de la IU de administración.
* **Se omiten las referencias**. Actualmente no hay comprobaciones sobre si se hace referencia a un fragmento de contenido existente. Por lo tanto, por ejemplo, si elimina un fragmento de contenido, podrían producirse problemas en una página que contenga una referencia al fragmento de contenido eliminado.
* **Tipo de datos JSON** La salida de la API de REST de *tipo de datos JSON* es *salida basada en cadenas*.

## Códigos de estado y mensajes de error {#status-codes-and-error-messages}

Los siguientes códigos de estado se pueden ver en las circunstancias relevantes:

* **200** (OK)

  Devuelto cuando:

   * solicitando un fragmento de contenido mediante `GET`
   * se actualizó correctamente un fragmento de contenido mediante `PUT`

* **201** (Creado)

  Devuelto cuando:

   * se creó correctamente un fragmento de contenido mediante `POST`

* **404** (no encontrado)

  Devuelto cuando:

   * el fragmento de contenido solicitado no existe

* **500** (error interno del servidor)

  >[!NOTE]
  >
  >Se devuelve este error:
  >
  >* cuando se ha producido un error que no se puede identificar con un código específico
  >* cuando la carga útil proporcionada no era válida

  A continuación se enumeran los escenarios comunes en los que se devuelve este estado de error, junto con el mensaje de error (monoespacio) generado:

   * La carpeta principal no existe (al crear un fragmento de contenido mediante `POST`)
   * No se ha proporcionado ningún modelo de fragmento de contenido (falta cq:model), no se puede leer (debido a una ruta no válida o a un problema de permisos) o no hay ningún modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * No se ha podido crear el fragmento de contenido (potencialmente un problema de permisos):

      * `Could not create content fragment`

   * No se han podido actualizar el título o la descripción:

      * `Could not set value on content fragment`

   * No se pudieron establecer los metadatos:

      * `Could not set metadata on content fragment`

   * El elemento de contenido no se ha podido encontrar o actualizar

      * `Could not update content element`
      * `Could not update fragment data of element`

  Los mensajes de error detallados se devuelven de la siguiente manera:

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## Referencia de la API {#api-reference}

Consulte aquí las referencias detalladas de la API:

* [API de Adobe Experience Manager Assets: fragmentos de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [API HTTP de recursos](/help/assets/mac-api-assets.md)

   * [Funciones disponibles](/help/assets/mac-api-assets.md#available-features)

* Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte lo siguiente:

* [Documentación de la API HTTP de Assets](/help/assets/mac-api-assets.md)
* [Sesión de AEM Gem: OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html?lang=es)
