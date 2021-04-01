---
title: API de HTTP de Assets
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en [!DNL Experience Manager Assets].
contentOwner: AG
feature: API HTTP de recursos, API
role: Desarrollador,Arquitecto,Administrador
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] API HTTP  {#assets-http-api}

## Información general {#overview}

La API HTTP [!DNL Assets] permite operaciones create-read-update-delete (CRUD) en recursos digitales, incluidos metadatos, representaciones y comentarios, junto con contenido estructurado que utiliza fragmentos de contenido [!DNL Experience Manager]. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md).

Para acceder a la API:

1. Abra el documento del servicio API en `https://[hostname]:[port]/api.json`.
1. Siga el enlace del servicio [!DNL Assets] que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de API es un archivo JSON para algunos tipos MIME y un código de respuesta para todos los tipos MIME. La respuesta JSON es opcional y es posible que no esté disponible, por ejemplo para archivos PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

>[!NOTE]
>
>Todas las llamadas a la API relacionadas con la carga o actualización de recursos o binarios en general (como las representaciones) quedan obsoletas para la implementación [!DNL Experience Manager] como [!DNL Cloud Service]. Para cargar binarios, utilice [API de carga binaria directa](developer-reference-material-apis.md#asset-upload-technical) en su lugar.

## Fragmentos de contenido {#content-fragments}

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Se puede utilizar para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que existen varias diferencias con los `standard` recursos (como imágenes o documentos), algunas reglas adicionales se aplican para administrar fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en la  [!DNL Experience Manager Assets] API HTTP](/help/assets/content-fragments/assets-api-content-fragments.md).

## modelo Data {#data-model}

La API HTTP [!DNL Assets] expone dos elementos, carpetas y recursos principales (para recursos estándar). Además, expone elementos más detallados para los modelos de datos personalizados que describen contenido estructurado en fragmentos de contenido. Consulte [Modelos de datos de fragmento de contenido](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obtener más información.

### Carpetas {#folders}

Las carpetas son como directorios, como en los sistemas de archivos tradicionales. La carpeta solo puede contener recursos, solo carpetas, o carpetas y recursos. Las carpetas tienen los siguientes componentes:

**Entidades**: Las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name` es el nombre de la carpeta. Es el mismo que el último segmento de la ruta URL sin la extensión.
* `title` es un título opcional de la carpeta que se puede mostrar en lugar de su nombre.

>[!NOTE]
>
>Algunas propiedades de carpeta o recurso se asignan a un prefijo diferente. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplaza por el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores `jcr:title` y `jcr:description`, respectivamente.

**** LinksFolders expone tres vínculos:

* `self`: Vínculo a sí mismo.
* `parent`: Enlace a la carpeta principal.
* `thumbnail`: (Opcional) vínculo a una imagen en miniatura de la carpeta.

### Assets {#assets}

En [!DNL Experience Manager] un recurso contiene los siguientes elementos:

* Propiedades y metadatos del recurso.
* Archivo binario cargado originalmente del recurso.
* Varias representaciones tal y como están configuradas. Pueden ser imágenes de diferentes tamaños, vídeos de diferentes codificaciones o páginas extraídas de archivos PDF o [!DNL Adobe InDesign].
* Comentarios opcionales.

Para obtener información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Recursos de Experience Manager](/help/assets/content-fragments/assets-api-content-fragments.md).

En [!DNL Experience Manager] una carpeta tiene los siguientes componentes:

* Entidades: Los elementos secundarios de los activos son sus representaciones.
* Propiedades.
* Vínculos.

## Funciones disponibles {#available-features}

La API HTTP [!DNL Assets] incluye las siguientes funciones:

* [Recupere una lista de carpetas](#retrieve-a-folder-listing).
* [Crear una carpeta](#create-a-folder).
* [Crear un recurso (obsoleto)](#create-an-asset)
* [Actualizar binario de recursos (obsoleto)](#update-asset-binary).
* [Actualizar metadatos de recursos](#update-asset-metadata).
* [Crear una representación de recursos](#create-an-asset-rendition).
* [Actualizar una representación de recursos](#update-an-asset-rendition).
* [Cree un comentario](#create-an-asset-comment) de recurso.
* [Copiar una carpeta o un recurso](#copy-a-folder-or-asset).
* [Mover una carpeta o un recurso](#move-a-folder-or-asset).
* [Eliminar una carpeta, un recurso o una representación](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>Para facilitar la lectura, en los ejemplos siguientes se omiten todas las notaciones cURL. La notación se correlaciona con [Resty](https://github.com/micha/resty), que es un envoltorio de script para cURL.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recupere una carpeta que enumere {#retrieve-a-folder-listing}

Recupera una representación sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitud**:  `GET /api/assets/myFolder.json`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - OK - éxito.
* 404 - NO ENCONTRADO - la carpeta no existe o no es accesible.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

**Respuesta**: La clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la URL señalada por el vínculo con `rel` de `self`.

## Cree una carpeta  . {#create-a-folder}

Crea un `sling`: `OrderedFolder` en la ruta dada. Si se proporciona `*` en lugar de un nombre de nodo, el servlet utiliza el nombre de parámetro como nombre de nodo. La solicitud acepta cualquiera de las siguientes opciones:

* Una representación sirena de la nueva carpeta
* Conjunto de pares de nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`. Son útiles para crear una carpeta directamente desde un formulario HTML.

Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta de URL.

Una llamada de API falla con un código de respuesta `500` si el nodo principal de la ruta proporcionada no existe. Una llamada devuelve un código de respuesta `409` si existe la carpeta.

**Parámetros**:  `name` es el nombre de la carpeta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - sobre la creación correcta.
* 409 - CONFLICTO - si existe la carpeta.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear un recurso {#create-an-asset}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo crear un recurso. No puede crear un recurso mediante la API HTTP.

## Actualizar un binario de recursos {#update-asset-binary}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo actualizar los binarios de recursos. No se puede actualizar un binario de recursos mediante la API HTTP.

## Actualización de metadatos de un recurso {#update-asset-metadata}

Actualiza las propiedades de metadatos de Asset. Si actualiza cualquier propiedad en el espacio de nombres `dc:`, la API actualiza la misma propiedad en el espacio de nombres `jcr`. La API no sincroniza las propiedades de las dos áreas de nombres.

**Solicitud**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - Correcto: si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Crear una representación de recursos {#create-an-asset-rendition}

Cree una representación para un recurso. Si no se proporciona el nombre del parámetro de solicitud, el nombre del archivo se utiliza como nombre de representación.

**Parámetros**: Los parámetros son  `name` para el nombre de la representación y  `file` como referencia de archivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de respuesta**

* 201 - CREADO - si la representación se ha creado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitud**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - Correcto: si la representación se ha actualizado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Añadir un comentario en un recurso {#create-an-asset-comment}

**Parámetros**: Los parámetros son  `message` para el cuerpo del mensaje del comentario y  `annotationData` para los datos de anotación en formato JSON.

**Solicitud**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si Comment se ha creado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso disponible en la ruta de acceso proporcionada a un nuevo destino.

**Solicitar encabezados**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución de API al que copiar el recurso.
* `X-Depth` -  `infinity` o  `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Utilice  `F` para evitar sobrescribir un recurso en el destino existente.

**Solicitud**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO - si la carpeta o el recurso se ha copiado en un destino existente.
* 412 - PRECONDITION ERROR - si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso en la ruta dada a un nuevo destino.

**Solicitar encabezados**: Los parámetros son:

* `X-Destination` : un nuevo URI de destino dentro del ámbito de la solución de API al que copiar el recurso.
* `X-Depth` -  `infinity` o  `0`. Al usar `0` solo se copia el recurso y sus propiedades, y no sus elementos secundarios.
* `X-Overwrite` - Utilice  `T` para eliminar por la fuerza un recurso existente o  `F` para evitar sobrescribir un recurso existente.

**Solicitud**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO - si la carpeta o el recurso se ha copiado en un destino existente.
* 412 - PRECONDITION ERROR - si falta un encabezado de solicitud.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Eliminar una carpeta, un recurso o una representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta proporcionada.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - OK - si la carpeta se ha eliminado correctamente.
* 412 - PRECONDICIÓN FALLIDA - si no se puede encontrar o acceder a la colección raíz.
* 500 - ERROR INTERNO DEL SERVIDOR - si algo más sale mal.

## Sugerencias, prácticas recomendadas y limitaciones {#tips-limitations}

* Después del [!UICONTROL Tiempo de inactividad], un recurso y sus representaciones no están disponibles a través de la interfaz web [!DNL Assets] y a través de la API HTTP. La API devuelve un mensaje de error 404 si el [!UICONTROL Tiempo de activación] está en el futuro o el [!UICONTROL Tiempo de inactividad] está en el pasado.

* Algunas propiedades de la carpeta o del recurso se asignan a un prefijo diferente al actualizarse mediante API. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplaza por el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores `jcr:title` y `jcr:description`, respectivamente.

>[!MORELIKETHIS]
>
>* [Documentos de referencia del desarrollador para [!DNL Assets]](/help/assets/developer-reference-material-apis.md)

