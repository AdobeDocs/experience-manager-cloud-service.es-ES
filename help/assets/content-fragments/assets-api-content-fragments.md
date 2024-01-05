---
title: Compatibilidad con fragmentos de contenido de Adobe Experience Manager as a Cloud Service en la API HTTP de Assets
description: Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de entrega sin encabezado de Adobe Experience Manager.
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 11%

---

# Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Información general {#overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/assets-api-content-fragments.html) |
| AEM as a Cloud Service | Este artículo |

Obtenga información acerca de la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de la función de entrega sin encabezado de Adobe Experience Manager AEM ().

>[!NOTE]
>
>El [API HTTP de Assets](/help/assets/mac-api-assets.md) incluye:
>
>* La API de REST de Recursos
>* incluye compatibilidad con los fragmentos de contenido
>
>La implementación actual de la API HTTP de Assets se basa en la variable [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) estilo arquitectónico.

>[!NOTE]
>
>Para obtener la información más reciente sobre las API de Experience Manager, visite también [API de Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

El [API de REST de Assets](/help/assets/mac-api-assets.md) permite a los desarrolladores de Adobe Experience Manager as a Cloud Service AEM acceder al contenido (almacenado en la) directamente a través de la API HTTP mediante las operaciones CRUD (crear, leer, actualizar, eliminar).

La API de le permite utilizar Adobe Experience Manager as a Cloud Service como un CMS (Sistema de administración de contenido) sin encabezado proporcionando servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON.

Por ejemplo, [SPA Aplicaciones de una sola página ()](/help/implementing/developing/hybrid/introduction.md), basado en el marco de trabajo o personalizado, requieren contenido proporcionado mediante la API HTTP, a menudo en formato JSON.

While [AEM Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) AEM Proporcionan una API personalizable que puede servir las operaciones de lectura necesarias para este fin y cuya salida JSON se puede personalizar, requieren conocimientos prácticos de WCM (Administración de contenido web) para la implementación de la aplicación. AEM Esto se debe a que deben alojarse en páginas basadas en plantillas de informes dedicadas a la. SPA No todas las organizaciones de desarrollo de la tienen acceso directo a esos conocimientos.

Es entonces cuando se puede utilizar la API de REST de Assets. Permite a los desarrolladores acceder a recursos (por ejemplo, imágenes y fragmentos de contenido) directamente, sin necesidad de incrustarlos primero en una página, y enviar su contenido en formato JSON serializado.

>[!NOTE]
>
>No es posible personalizar la salida JSON desde la API de REST de Assets.

La API de REST de Assets también permite a los desarrolladores modificar contenido: creando nuevos recursos, fragmentos de contenido y carpetas, actualizándolos o eliminándolos.

La API de REST de Assets:

* sigue al [Principio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa el [Formato de SIRENA](https://github.com/kevinswiber/siren)

## Requisitos previos {#prerequisites}

La API de REST de Recursos está disponible en cada instalación predeterminada de una versión reciente de Adobe Experience Manager as a Cloud Service.

## Conceptos clave {#key-concepts}

Las ofertas de API de REST de Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)AEM Acceso de tipo a a recursos almacenados en una instancia de.

Utiliza el `/api/assets` punto final y requiere la ruta del recurso para acceder a él (sin el interlineado `/content/dam`).

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
* **POST** : para crear recursos o carpetas
* **PUT**: actualizar las propiedades de un recurso o carpeta.
* **DELETE**: eliminar un recurso o carpeta.

>[!NOTE]
>
>El cuerpo de solicitud o los parámetros de URL se pueden usar para configurar algunas de estas operaciones; por ejemplo, definir que una carpeta o un recurso deben crearse mediante una solicitud **POST**.

El formato exacto de las solicitudes admitidas se define en la variable [Referencia de API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) documentación.

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que los siguientes (`write`) las solicitudes no se pueden combinar en una sola transacción que podría realizarse correctamente o fallar como una sola entidad.

### AEM AEM API de REST de (Assets) frente a componentes de {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API de REST de Assets<br/> </td>
   <td>AEM Componente<br/> (componentes que utilizan modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso admitidos</td>
   <td>De uso general.</td>
   <td><p>SPA Optimizado para el consumo en una aplicación de una sola página () o en cualquier otro contexto (consumo de contenido).</p> <p>También puede contener información de diseño.</p> </td>
  </tr>
  <tr>
   <td>Operaciones compatibles</td>
   <td><p>Crear, leer, actualizar, eliminar.</p> <p>Con operaciones adicionales, según el tipo de entidad.</p> </td>
   <td>Sólo lectura.</td>
  </tr>
  <tr>
   <td>Acceso</td>
   <td><p>Se puede acceder a ella directamente.</p> <p>Utiliza el <code>/api/assets </code>extremo, asignado a <code>/content/dam</code> (en el repositorio).</p> 
   <p>Una ruta de ejemplo tendría este aspecto: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>AEM AEM Se debe hacer referencia a él a través de un componente de la en una página de la aplicación.</p> <p>Utiliza el <code>.model</code> para crear la representación JSON.</p> <p>Una ruta de ejemplo tendría este aspecto:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Seguridad</td>
   <td><p>Se pueden seleccionar varias opciones.</p> <p>Se propone OAuth; se puede configurar por separado de la configuración estándar.</p> </td>
   <td>AEM Utiliza la configuración estándar.</td>
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

AEM Si la API de REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, el filtro CORS debe estar configurado correctamente.

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* [Explicación de CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [AEM Vídeo: Desarrollo de CORS con la aplicación de la tecnología de la información (04:06).](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso. Consulte [Uso de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

Para obtener más información sobre las funciones disponibles a través de la API, consulte:

* El [API de REST de Assets](/help/assets/mac-api-assets.md)
* [Tipos de entidad](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), donde se explican las funciones específicas de cada tipo admitido (según corresponda a los fragmentos de contenido)

### Paginación {#paging}

La API de REST de Assets admite la paginación (para solicitudes de GET) mediante los parámetros de URL:

* `offset` : el número de la primera entidad (secundaria) que se va a recuperar.
* `limit` : el número máximo de entidades devueltas

La respuesta contiene información de paginación como parte de `properties` de la salida SIREN. Esta `srn:paging` contiene el número total de entidades (secundarias) ( `total`), el desplazamiento y el límite ( `offset`, `limit`) tal como se especifica en la solicitud.

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

Las carpetas actúan como contenedores para recursos y otras carpetas. AEM Reflejan la estructura del repositorio de contenido de la.

La API de REST de Assets expone el acceso a las propiedades de una carpeta. Por ejemplo, su nombre y título. Los recursos se exponen como entidades secundarias de carpetas y subcarpetas.

>[!NOTE]
>
>Según el tipo de recurso de los recursos y carpetas secundarios, la lista de entidades secundarias puede contener ya el conjunto completo de propiedades que define la entidad secundaria correspondiente. Alternativamente, solo se puede exponer un conjunto reducido de propiedades para una entidad de esta lista de entidades secundarias.

### Assets {#assets}

Si se solicita un recurso, la respuesta devolverá sus metadatos, como el título, el nombre y otra información tal como se define en el esquema de recursos correspondiente.

Los datos binarios de un recurso se exponen como un vínculo SIREN de tipo `content`.

Los recursos pueden tener varias representaciones. Normalmente se exponen como entidades secundarias, una excepción es una representación en miniatura, que se expone como un vínculo de tipo `thumbnail` ( `rel="thumbnail"`).

### Fragmentos de contenido {#content-fragments}

A [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Pueden utilizarse para acceder a datos estructurados, como textos, números, fechas, etc.

Dado que existen varias diferencias con *standard* recursos (como imágenes o audio), se aplican algunas reglas adicionales para administrarlos.

#### Representación {#representation}

Fragmentos de contenido:

* No exponga ningún dato binario.
* Están contenidos en la salida JSON (dentro de la variable `properties` property).

* También se consideran atómicos. Es decir, los elementos y las variaciones se exponen como parte de las propiedades del fragmento en lugar de como vínculos o entidades secundarias. Esto permite un acceso eficiente a la carga útil de un fragmento.

#### Modelos de contenido y fragmentos de contenido {#content-models-and-content-fragments}

Actualmente, los modelos que definen la estructura de un fragmento de contenido no se exponen a través de una API HTTP. Por lo tanto, el *consumidor* debe conocer el modelo de un fragmento (al menos un mínimo), aunque la mayoría de la información se puede inferir de la carga útil, ya que los tipos de datos, etc., forman parte de la definición.

Para crear un fragmento de contenido, se debe proporcionar la ruta (del repositorio interno) del modelo.

#### Contenido asociado {#associated-content}

El contenido asociado no se expone.

## Utilización {#using}

AEM El uso puede variar en función de si utiliza un entorno de autor o publicación de, junto con el caso de uso específico.

* Se recomienda que la creación esté enlazada a una instancia de autor ([y actualmente no hay medios para replicar un fragmento para publicarlo con esta API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* La entrega es posible desde ambos, ya que AEM sirve contenido solicitado solo en formato JSON.

   * AEM El almacenamiento y el envío desde una instancia de autor de la deberían ser suficientes para las aplicaciones de biblioteca de medios detrás del cortafuegos.

   * AEM Para la entrega web en directo, se recomienda una instancia de publicación de la.

>[!CAUTION]
>
>AEM La configuración de Dispatcher en las instancias de nube de puede bloquear el acceso a `/api`.

>[!NOTE]
>
>Consulte la [Referencia de API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). En particular, la [API de Adobe Experience Manager Assets: fragmentos de contenido](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).

## Restricciones {#limitations}

Hay algunas limitaciones:

* **Actualmente no se admiten modelos de fragmento de contenido**: no se pueden leer ni crear. Para poder crear o actualizar un fragmento de contenido existente, los desarrolladores deben conocer la ruta correcta al modelo de fragmento de contenido. Actualmente, el único método para obtener una descripción general de estos es a través de la IU de administración.
* **Las referencias se omiten**. Actualmente no hay comprobaciones sobre si se hace referencia a un fragmento de contenido existente. Por lo tanto, por ejemplo, si elimina un fragmento de contenido, podrían producirse problemas en una página que contenga una referencia al fragmento de contenido eliminado.
* **Tipo de datos JSON** La salida de la API de REST del *Tipo de datos JSON* es *salida basada en cadenas*.

## Códigos de estado y mensajes de error {#status-codes-and-error-messages}

Los siguientes códigos de estado se pueden ver en las circunstancias relevantes:

* **200** (OK)

  Devuelto cuando:

   * solicitud de un fragmento de contenido mediante `GET`
   * actualización correcta de un fragmento de contenido mediante `PUT`

* **201** (Creado)

  Devuelto cuando:

   * creación correcta de un fragmento de contenido mediante `POST`

* **404** (No encontrado)

  Devuelto cuando:

   * el fragmento de contenido solicitado no existe

* **500** (Error interno del servidor)

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

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte lo siguiente:

* [Documentación de la API HTTP de Assets](/help/assets/mac-api-assets.md)
* [AEM Sesión de Gem de: OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html)
