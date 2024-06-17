---
title: API HTTP de recursos
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Architect, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 5%

---

# [!DNL Adobe Experience Manager Assets] API HTTP {#assets-http-api}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

## Información general {#overview}

El [!DNL Assets] La API HTTP permite realizar operaciones de creación, lectura, actualización y eliminación (CRUD) en recursos digitales, incluidos metadatos, representaciones y comentarios, así como contenido estructurado mediante [!DNL Experience Manager] Fragmentos de contenido. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
> Hay disponible una implementación modernizada de OpenAPI de la API de administración de fragmentos de contenido. Para obtener toda la documentación, consulte [API de administración de fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). Se recomienda utilizar la nueva implementación de OpenAPI. El uso existente de la API HTTP de Assets para fragmentos de contenido debe migrarse a la nueva API abierta de administración de fragmentos de contenido.

Para acceder a la API:

1. Abra el documento de servicio de API en `https://[hostname]:[port]/api.json`.
1. Siga las [!DNL Assets] vínculo de servicio que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de la API es un archivo JSON para algunos tipos de MIME y un código de respuesta para todos los tipos de MIME. La respuesta JSON es opcional y es posible que no esté disponible, por ejemplo, para archivos de PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

>[!NOTE]
>
>Todas las llamadas de la API relacionadas con la carga o actualización de recursos o binarios en general (como representaciones) están en desuso para [!DNL Experience Manager] as a [!DNL Cloud Service] implementación. Para cargar binarios, utilice [API de carga binaria directa](developer-reference-material-apis.md#asset-upload) en su lugar.

## Fragmentos de contenido {#content-fragments}

A [Fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Se puede utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que existen varias diferencias con `standard` Recursos (como imágenes o documentos), algunas reglas adicionales se aplican a la gestión de fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

## Modelo de datos {#data-model}

El [!DNL Assets] La API HTTP expone dos elementos principales, carpetas y recursos (para recursos estándar). Además, expone elementos más detallados para los modelos de datos personalizados que describen el contenido estructurado en Fragmentos de contenido. Consulte [Modelos de datos de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obtener más información.

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

### Carpetas {#folders}

Las carpetas son como los directorios, como en los sistemas de archivos tradicionales. La carpeta solo puede contener recursos, carpetas o carpetas y recursos. Las carpetas tienen los siguientes componentes:

**Entidades**: las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name` es el nombre de la carpeta. Es igual que el último segmento de la ruta URL sin la extensión.
* `title` es un título opcional de la carpeta que se puede mostrar en lugar de su nombre.

>[!NOTE]
>
>Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente. El `jcr` prefijo de `jcr:title`, `jcr:description`, y `jcr:language` se han reemplazado por `dc` prefijo. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contiene los valores de `jcr:title` y `jcr:description`, respectivamente.

**Vínculos** Las carpetas muestran tres vínculos:

* `self`: vínculo a sí mismo.
* `parent`: vínculo a la carpeta principal.
* `thumbnail`: (Opcional) vínculo a una imagen en miniatura de la carpeta.

### Recursos {#assets}

Entrada [!DNL Experience Manager] un recurso contiene los siguientes elementos:

* Las propiedades y los metadatos del recurso.
* Archivo binario cargado originalmente del recurso.
* Varias representaciones según la configuración. Pueden ser imágenes de diferentes tamaños, vídeos de diferentes codificaciones o páginas extraídas de PDF o [!DNL Adobe InDesign] archivos.
* Comentarios opcionales.

Para obtener información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

Entrada [!DNL Experience Manager] una carpeta tiene los siguientes componentes:

* Entidades: las representaciones secundarias de los recursos.
* Propiedades.
* Vínculos.

## Funciones disponibles {#available-features}

El [!DNL Assets] La API HTTP incluye las siguientes funciones:

* [Recuperar una lista de carpetas](#retrieve-a-folder-listing).
* [Crear una carpeta](#create-a-folder).
* [Crear un recurso (obsoleto)](#create-an-asset)
* [Actualizar binario de recursos (obsoleto)](#update-asset-binary).
* [Actualizar metadatos del recurso](#update-asset-metadata).
* [Crear una representación de recursos](#create-an-asset-rendition).
* [Actualizar una representación de recursos](#update-an-asset-rendition).
* [Crear un comentario de recurso](#create-an-asset-comment).
* [Copiar una carpeta o un recurso](#copy-a-folder-or-asset).
* [Mover una carpeta o un recurso](#move-a-folder-or-asset).
* [Eliminar una carpeta, un recurso o una representación](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar la legibilidad, los siguientes ejemplos omiten las notaciones cURL completas. La notación se correlaciona con [Resty](https://github.com/micha/resty) que es un contenedor de scripts para cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperar una lista de carpetas {#retrieve-a-folder-listing}

Recupera una representación de sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitud**: `GET /api/assets/myFolder.json`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - OK - success.
* 404 - NO ENCONTRADO: la carpeta no existe o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

**Respuesta**: la clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la dirección URL a la que apunta el vínculo con una `rel` de `self`.

## Crear una carpeta. {#create-a-folder}

Crea un `sling`: `OrderedFolder` en la ruta determinada. If `*` se proporciona en lugar de un nombre de nodo, el servlet utiliza el nombre del parámetro como nombre de nodo. La solicitud acepta cualquiera de las siguientes opciones:

* Una representación de sirena de la nueva carpeta
* Un conjunto de pares de nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Son útiles para crear una carpeta directamente desde un formulario de HTML.

Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

Una llamada de API falla con un `500` código de respuesta si el nodo principal de la ruta proporcionada no existe. Una llamada a devuelve un código de respuesta `409` si la carpeta existe.

**Parámetros**: `name` es el nombre de la carpeta.

**Petición**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201 - CREADO: sobre creación correcta.
* 409 - CONFLICTO - si existe la carpeta.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear un recurso {#create-an-asset}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo crear un recurso. No puede crear un recurso mediante la API HTTP.

## Actualizar un binario de recursos {#update-asset-binary}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo actualizar los binarios de recursos. No se puede actualizar un binario de recursos mediante la API HTTP.

## Actualización de metadatos de un recurso {#update-asset-metadata}

Actualiza las propiedades de los metadatos del recurso. Si actualiza cualquier propiedad en la variable `dc:` , la API actualiza la misma propiedad en el `jcr` namespace. La API no sincroniza las propiedades en las dos áreas de nombres.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear una representación de recursos {#create-an-asset-rendition}

Crear una representación para un recurso. Si no se proporciona el nombre del parámetro de solicitud, se utilizará el nombre de archivo como nombre de representación.

**Parámetros**: los parámetros son `name` para el nombre de la representación y `file` como referencia de archivo.

**Petición**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de respuesta**

* 201: CREADO: si la representación se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitud**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si la representación se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Agregar un comentario en un recurso {#create-an-asset-comment}

**Parámetros**: los parámetros son `message` para el cuerpo del mensaje del comentario y `annotationData` para los datos de anotación en formato JSON.

**Solicitud**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si el comentario se ha creado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso disponible en la ruta proporcionada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - bien `infinity` o `0`. Uso de `0` solo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Uso `F` para evitar sobrescribir un recurso en el destino existente.

**Solicitud**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso en la ruta determinada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - bien `infinity` o `0`. Uso de `0` solo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Utilice una de estas opciones `T` para eliminar por la fuerza recursos existentes o `F` para evitar sobrescribir un recurso existente.

**Solicitud**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Eliminar una carpeta, un recurso o una representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta proporcionada.

**Petición**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Aceptar - si la carpeta se ha eliminado correctamente.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Sugerencias, prácticas recomendadas y limitaciones {#tips-limitations}

* Después del [!UICONTROL Tiempo de inactividad], un recurso y sus representaciones no están disponibles a través del [!DNL Assets] y a través de la API HTTP. La API devuelve el mensaje de error 404 si la variable [!UICONTROL Tiempo de activación] es en el futuro o [!UICONTROL Tiempo de inactividad] está en el pasado.

* La API HTTP de Assets no devuelve los metadatos completos. Las áreas de nombres están codificadas y solo se devuelven esas áreas de nombres. Para ver los metadatos completos, consulte la ruta del recurso `/jcr_content/metadata.json`.

* Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente al actualizarse mediante las API. El `jcr` prefijo de `jcr:title`, `jcr:description`, y `jcr:language` se han reemplazado por `dc` prefijo. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contiene los valores de `jcr:title` y `jcr:description`, respectivamente.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documentos de referencia del desarrollador para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
