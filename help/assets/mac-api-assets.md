---
title: API HTTP de recursos
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en  [!DNL Experience Manager Assets].
contentOwner: AG
feature: Assets HTTP API
role: Developer, Admin
exl-id: a3b7374d-f24b-4d6f-b6db-b9c9c962bb8d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 5%

---

# Administrar recursos digitales con la API HTTP [!DNL Adobe Experience Manager Assets]{#assets-http-api}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

## Introducción a la API HTTP de AEM [!DNL Assets] {#overview}

La API HTTP de AEM [!DNL Assets] habilita las operaciones CRUD (crear, leer, actualizar y eliminar) en recursos digitales a través de una interfaz REST disponible en /`api/assets`. Estas operaciones se aplican a los metadatos de recursos, las representaciones y los comentarios. Incluye [compatibilidad con fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
> Hay disponible una implementación modernizada de OpenAPI de la API de administración de fragmentos de contenido. Para obtener documentación completa, consulte [API de administración de fragmentos de contenido](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/). Se recomienda utilizar la nueva implementación de OpenAPI. El uso existente de la API HTTP de Assets para fragmentos de contenido debe migrarse a la nueva API abierta de administración de fragmentos de contenido.

Para acceder a la API:

1. Abra el documento de servicio de API en `https://[hostname]:[port]/api.json`.
1. Seguir el vínculo de servicio [!DNL Assets] que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de la API es un archivo JSON para algunos tipos de MIME y un código de respuesta para todos los tipos de MIME. La respuesta JSON es opcional y es posible que no esté disponible, por ejemplo, para los archivos PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

>[!NOTE]
>
>Todas las llamadas de API relacionadas con la carga o actualización de recursos o binarios en general (como representaciones) están en desuso para [!DNL Experience Manager] como una implementación de [!DNL Cloud Service]. Para cargar binarios, usa [API de carga binaria directa](developer-reference-material-apis.md#asset-upload).

## Administrar fragmentos de contenido {#content-fragments}

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un recurso estructurado que almacena texto, números y fechas. Dado que existen varias diferencias entre los recursos de `standard` (como imágenes o documentos), algunas reglas adicionales se aplican al manejo de fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en la [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Consulte [API de AEM para la administración y entrega de contenido estructurado](/help/headless/apis-headless-and-content-fragments.md) para obtener una descripción general de las diversas API disponibles y una comparación de algunos de los conceptos involucrados.
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

## Examinar el modelo de datos {#data-model}

La API HTTP [!DNL Assets] expone principalmente dos elementos: carpetas y recursos estándar. También proporciona elementos detallados para los modelos de datos personalizados utilizados en fragmentos de contenido. Para obtener más información, consulte Modelos de datos de fragmentos de contenido. Consulte [Modelos de datos de fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obtener más información.

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

### Administración de carpetas {#folders}

Las carpetas son como los directorios, como en los sistemas de archivos tradicionales. Las carpetas pueden contener recursos, subcarpetas o ambos. Las carpetas tienen los siguientes componentes:

**Entidades**: las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name`: el nombre de la carpeta (el último segmento de la ruta de acceso de la dirección URL, sin la extensión).
* `title`: título opcional mostrado en lugar del nombre de la carpeta.

>[!NOTE]
>
>Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplaza por el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores de `jcr:title` y `jcr:description`, respectivamente.

**Vínculos** Las carpetas muestran tres vínculos:

* `self`: un vínculo a la carpeta en sí.
* `parent`: un vínculo a la carpeta principal.
* `thumbnail` (opcional): un vínculo a una imagen en miniatura de carpeta.

### Administración de recursos {#assets}

En [!DNL Experience Manager], un recurso contiene los siguientes elementos:

* **Propiedades y metadatos:** Información descriptiva sobre el recurso.
* **Archivo binario:** El archivo cargado originalmente.
* **Representaciones:** varias representaciones configuradas (como imágenes en varios tamaños, diferentes codificaciones de vídeo o páginas extraídas de archivos PDF/Adobe InDesign).
* **Comentarios (opcional):** Comentarios proporcionados por el usuario.

Para obtener información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

>[!NOTE]
>
>Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.

En [!DNL Experience Manager], una carpeta tiene los siguientes componentes:

* Entidades: las representaciones secundarias de los recursos.
* Propiedades.
* Vínculos.

## Explorar operaciones de API disponibles {#available-features}

La API HTTP [!DNL Assets] incluye las siguientes características:

* [Recuperar un listado de carpetas](#retrieve-a-folder-listing).
* [Crear una carpeta](#create-a-folder).
* [Crear un recurso (obsoleto)](#create-an-asset)
* [Actualizar binario de recursos (obsoleto)](#update-asset-binary).
* [Actualizar metadatos de recursos](#update-asset-metadata).
* [Crear una representación de recursos](#create-an-asset-rendition).
* [Actualizar una representación de recursos](#update-an-asset-rendition).
* [Crear un comentario de recurso](#create-an-asset-comment).
* [Copiar una carpeta o un recurso](#copy-a-folder-or-asset).
* [Mover una carpeta o un recurso](#move-a-folder-or-asset).
* [Eliminar una carpeta, recurso o representación](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar la legibilidad, los siguientes ejemplos omiten las notaciones cURL completas. La notación se correlaciona con [Resty](https://github.com/micha/resty), que es un contenedor de scripts para cURL.

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

**Respuesta**: La clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la dirección URL a la que apunta el vínculo con un `rel` de `self`.

## Crear una carpeta. {#create-a-folder}

Crea un(a) `sling`: `OrderedFolder` en la ruta dada. Si se proporciona `*` en lugar de un nombre de nodo, el servlet utiliza el nombre del parámetro como nombre de nodo. La solicitud acepta cualquiera de las siguientes opciones:

* Una representación de sirena de la nueva carpeta
* Un conjunto de pares nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Son útiles para crear una carpeta directamente desde un formulario de HTML.

Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

Una llamada de API produce un error con un código de respuesta `500` si el nodo principal de la ruta de acceso proporcionada no existe. Una llamada devuelve un código de respuesta `409` si la carpeta existe.

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

La creación de recursos no es compatible con esta API HTTP. Para crear recursos, use la API [carga de recursos](developer-reference-material-apis.md).

## Actualizar un binario de recursos {#update-asset-binary}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo actualizar los binarios de recursos. No se puede actualizar un binario de recursos mediante la API HTTP.

## Actualización de metadatos de un recurso {#update-asset-metadata}

Esta operación actualiza los metadatos del recurso. Al actualizar propiedades en el espacio de nombres `dc:`, se actualiza la propiedad `jcr:` correspondiente. Sin embargo, la API no sincroniza las propiedades en las dos áreas de nombres.

**Solicitud**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos de respuesta**: Los códigos de respuesta son:

* 200 - Correcto - si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO: si no se pudo encontrar el recurso o no se pudo acceder a él en el URI proporcionado.
* 412: ERROR DE CONDICIÓN PREVIA: si no se encuentra la colección raíz o no se puede acceder a ella.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear una representación de recursos {#create-an-asset-rendition}

Crear una representación para un recurso. Si no se proporciona el nombre del parámetro de solicitud, se utilizará el nombre de archivo como nombre de representación.

**Parámetros**: Los parámetros son:

`name`: para el nombre de representación.
`file`: archivo binario para la representación como referencia.

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

* `X-Destination`: un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - `infinity` o `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Use `F` para evitar que se sobrescriba un recurso en el destino existente.

**Solicitud**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos de respuesta**: Los códigos de respuesta son:

* 201: CREADO: si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO: si la carpeta/recurso se ha copiado a un destino existente.
* 412 - ERROR DE PRECONDICIÓN: si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso en la ruta determinada a un nuevo destino.

**Encabezados de solicitud**: Los parámetros son:

* `X-Destination`: un nuevo URI de destino dentro del ámbito de la solución API en el que copiar el recurso.
* `X-Depth` - `infinity` o `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Use `T` para eliminar a la fuerza un recurso existente o `F` para evitar sobrescribir un recurso existente.

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

## Siga las prácticas recomendadas y anote las limitaciones {#tips-limitations}

* Assets y sus representaciones dejarán de estar disponibles a través de la interfaz web [!DNL Assets] y la API HTTP cuando se llegue al [!UICONTROL Tiempo de inactividad]. La API devuelve un error 404 si el [!UICONTROL Tiempo de activación] es futuro o el [!UICONTROL Tiempo de inactividad] es anterior.

* La API HTTP de Assets devuelve solo un subconjunto de metadatos. Las áreas de nombres están codificadas y solo se devuelven esas áreas de nombres. Para ver los metadatos completos, consulte la ruta de recursos `/jcr_content/metadata.json`.

* Algunas propiedades de la carpeta o el recurso se asignan a un prefijo diferente al actualizarse mediante las API. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplaza por el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores de `jcr:title` y `jcr:description`, respectivamente.

**Explorar recursos relacionados**

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
>* [Documentos de referencia para desarrolladores para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)
