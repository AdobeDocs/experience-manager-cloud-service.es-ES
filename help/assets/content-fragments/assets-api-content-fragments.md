---
title: Compatibilidad con fragmentos de contenido de Adobe Experience Manager as a Cloud Service en la API HTTP de Assets
description: Obtenga información sobre la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de AEM función de envío sin encabezado.
feature: Content Fragments,Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 2%

---

# Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Información general {#overview}

Obtenga información sobre la compatibilidad con fragmentos de contenido en la API HTTP de Assets, una parte importante de AEM función de envío sin encabezado.

>[!NOTE]
>
>La [API HTTP de recursos](/help/assets/mac-api-assets.md) incluye lo siguiente:
>
>* API de REST de recursos
>* incluida la compatibilidad con fragmentos de contenido

>
>La implementación actual de la API HTTP de Assets se basa en el estilo arquitectónico [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).

La [API REST de recursos](/help/assets/mac-api-assets.md) permite a los desarrolladores de Adobe Experience Manager como Cloud Service acceder al contenido (almacenado en AEM) directamente a través de la API HTTP, a través de operaciones CRUD (Crear, Leer, Actualizar, Eliminar).

La API le permite operar Adobe Experience Manager como Cloud Service como CMS (sistema de administración de contenido) sin encabezado al proporcionar servicios de contenido a una aplicación front-end de JavaScript. O cualquier otra aplicación que pueda ejecutar solicitudes HTTP y gestionar respuestas JSON.

Por ejemplo, [Aplicaciones de una sola página (SPA)](/help/implementing/developing/hybrid/introduction.md), basadas en marcos o personalizadas, requieren contenido proporcionado a través de la API HTTP, a menudo en formato JSON.

Aunque los [AEM componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) proporcionan una API muy completa, flexible y personalizable que puede servir las operaciones de lectura necesarias para este fin y cuya salida JSON se puede personalizar, sí requieren AEM conocimientos técnicos de WCM (Web Content Management) para la implementación, ya que deben alojarse en páginas basadas en plantillas AEM dedicadas. No todas SPA organizaciones de desarrollo tienen acceso directo a esos conocimientos.

Es entonces cuando se puede utilizar la API de REST de Assets. Permite a los desarrolladores acceder a los recursos (por ejemplo, imágenes y fragmentos de contenido) directamente, sin necesidad de incrustarlos primero en una página y entregar su contenido en formato JSON serializado.

>[!NOTE]
>
>No es posible personalizar la salida JSON desde la API de REST de Assets.

La API de REST de recursos también permite a los desarrolladores modificar el contenido mediante la creación de recursos nuevos, la actualización o la eliminación de recursos, fragmentos de contenido y carpetas existentes.

La API de REST de Assets:

* sigue el [principio de HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa el formato [SIREN](https://github.com/kevinswiber/siren)

## Requisitos previos {#prerequisites}

La API de REST de Assets está disponible en cada instalación predeterminada de una versión reciente de Adobe Experience Manager as a Cloud Service.

## Conceptos clave {#key-concepts}

La API de REST de recursos ofrece acceso de estilo [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) a los recursos almacenados en una instancia de AEM.

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

El formato exacto de las solicitudes admitidas se define en la documentación [API Reference](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) .

### Comportamiento transaccional {#transactional-behavior}

Todas las solicitudes son atómicas.

Esto significa que las solicitudes posteriores (`write`) no se pueden combinar en una sola transacción que pueda tener éxito o fallar como una sola entidad.

### API de REST de AEM (Assets) y componentes AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspecto</td>
   <td>API de REST de recursos<br/> </td>
   <td>Componente AEM<br/> (componentes que utilizan modelos Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casos de uso compatibles</td>
   <td>Finalidad general.</td>
   <td><p>Optimizado para el consumo en una aplicación de una sola página (SPA) o en cualquier otro contexto (que consuma contenido).</p> <p>También puede contener información de diseño.</p> </td>
  </tr>
  <tr>
   <td>Operaciones compatibles</td>
   <td><p>Crear, Leer, Actualizar, Eliminar.</p> <p>Con operaciones adicionales según el tipo de entidad.</p> </td>
   <td>Solo lectura.</td>
  </tr>
  <tr>
   <td>Acceso</td>
   <td><p>Se puede acceder directamente.</p> <p>Utiliza el extremo <code>/api/assets </code>, asignado a <code>/content/dam</code> (en el repositorio).</p> 
   <p>Un ejemplo de ruta sería el siguiente: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Se debe hacer referencia a través de un componente AEM en una página AEM.</p> <p>Utiliza el selector <code>.model</code> para crear la representación JSON.</p> <p>Un ejemplo de ruta sería el siguiente:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Seguridad</td>
   <td><p>Es posible usar varias opciones.</p> <p>Se propone OAuth; se puede configurar de forma independiente de la configuración estándar.</p> </td>
   <td>Utiliza AEM configuración estándar.</td>
  </tr>
  <tr>
   <td>Observaciones arquitectónicas</td>
   <td><p>El acceso de escritura normalmente se dirige a una instancia de autor.</p> <p>La lectura también se puede dirigir a una instancia de publicación.</p> </td>
   <td>Como este método es de solo lectura, normalmente se utilizará para publicar instancias.</td>
  </tr>
  <tr>
   <td>Salida</td>
   <td>Salida SIREN basada en JSON: versátil, pero poderosa. Permite navegar dentro del contenido.</td>
   <td>salida propietaria basada en JSON; configurable a través de modelos Sling. Navegar por la estructura de contenido es difícil de implementar (pero no necesariamente imposible).</td>
  </tr>
 </tbody>
</table>

### Seguridad {#security}

Si la API de REST de Assets se utiliza en un entorno sin requisitos de autenticación específicos, AEM filtro CORS debe configurarse correctamente.

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* [Se explica el CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
>* [Vídeo: Desarrollo para CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

>


En entornos con requisitos de autenticación específicos, se recomienda OAuth.

## Funciones disponibles {#available-features}

Los fragmentos de contenido son un tipo específico de recurso; consulte [Trabajo con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md).

Para obtener más información sobre las funciones disponibles mediante la API, consulte:

* La [API de REST de recursos](/help/assets/mac-api-assets.md)
* [Tipos de entidades](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), donde se explican las funciones específicas de cada tipo admitido (según corresponda a los fragmentos de contenido)

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

## Tipos de entidades {#entity-types}

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

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Se pueden utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros.

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

## Utilización {#using}

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

## Restricciones     {#limitations}

Existen algunas limitaciones:

* **Actualmente no se admiten** modelos de fragmentos de contenido: no se pueden leer ni crear. Para poder crear un fragmento de contenido nuevo o actualizar uno existente, los desarrolladores deben conocer la ruta correcta al modelo de fragmento de contenido. Actualmente, el único método para obtener una descripción general de estos es a través de la interfaz de usuario de administración.
* **Las referencias se ignoran**. Actualmente no hay comprobaciones para comprobar si se hace referencia a un fragmento de contenido existente. Por lo tanto, por ejemplo, si elimina un fragmento de contenido, pueden producirse problemas en una página que contenga una referencia al fragmento de contenido eliminado.
* **Tipo de datos JSON** El resultado de la API de REST del tipo de datos  *JSON* está basado actualmente en  *cadenas*.

## Códigos de estado y mensajes de error {#status-codes-and-error-messages}

Los siguientes códigos de estado se pueden ver en las circunstancias relevantes:

* **200**  (Aceptar) Devuelto cuando:

   * solicitud de un fragmento de contenido mediante `GET`
   * actualización correcta de un fragmento de contenido mediante `PUT`

* **201** (Creado) Devuelto cuando:

   * crear correctamente un fragmento de contenido mediante `POST`

* **404**  (No encontrado) Devuelto cuando:

   * el fragmento de contenido solicitado no existe

* **500**  (Error interno del servidor)

   >[!NOTE]
   >
   >Se devuelve este error:
   >
   >* cuando se ha producido un error que no se puede identificar con un código específico
   >* cuando la carga útil dada no era válida


   A continuación se enumeran escenarios comunes en los que se devuelve este estado de error, junto con el mensaje de error (monospace) generado:

   * La carpeta principal no existe (al crear un fragmento de contenido mediante `POST`)
   * No se proporciona ningún modelo de fragmento de contenido (falta cq:model), no se puede leer (debido a una ruta de acceso no válida o a un problema de permisos) o no hay un modelo de fragmento válido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * No se pudo crear el fragmento de contenido (potencialmente un problema de permisos):

      * `Could not create content fragment`
   * El título o la descripción no se pudieron actualizar:

      * `Could not set value on content fragment`
   * No se pudieron establecer los metadatos:

      * `Could not set metadata on content fragment`
   * No se encontró el elemento de contenido o no se pudo actualizar

      * `Could not update content element`
      * `Could not update fragment data of element`

   Los mensajes de error detallados generalmente se devuelven de la siguiente manera:

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

## Referencia de API {#api-reference}

Consulte aquí las referencias de API detalladas:

* [API de Adobe Experience Manager Assets: Fragmentos de contenido](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/assets-api-content-fragments/index.html)

* [API de HTTP de Assets](/help/assets/mac-api-assets.md)

   * [Funciones disponibles](/help/assets/mac-api-assets.md#available-features)

## Recursos adicionales {#additional-resources}

Para obtener más información, consulte:

* [Documentación de la API HTTP de Assets](/help/assets/mac-api-assets.md)
* [AEM sesión de Gem: OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
