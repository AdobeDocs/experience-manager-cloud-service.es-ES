---
title: API de HTTP de Assets
description: Cree, lea, actualice, elimine y administre recursos digitales mediante la API HTTP en [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 1%

---


# API de HTTP de Assets {#assets-http-api}

## Información general {#overview}

La API HTTP de Recursos permite crear-leer-actualizar-eliminar (CRUD) operaciones en recursos digitales, incluidos metadatos, representaciones y comentarios, junto con contenido estructurado que utiliza [!DNL Experience Manager] fragmentos de contenido. Se expone en `/api/assets` y se implementa como API de REST. Incluye [compatibilidad con fragmentos de contenido](/help/assets/content-fragments/assets-api-content-fragments.md).

Para acceder a la API:

1. Abra el documento del servicio API en `https://[hostname]:[port]/api.json`.
1. Siga el vínculo del servicio Recursos que lleva a `https://[hostname]:[server]/api/assets.json`.

La respuesta de API es un archivo JSON para algunos tipos MIME y un código de respuesta para todos los tipos MIME. La respuesta JSON es opcional y puede que no esté disponible, por ejemplo, para archivos PDF. Confíe en el código de respuesta para realizar más análisis o acciones.

Después del [!UICONTROL Tiempo de inactividad], un recurso y sus representaciones no están disponibles a través de la interfaz web [!DNL Assets] ni a través de la API HTTP. La API devuelve un mensaje de error 404 si el [!UICONTROL Tiempo de activación] está en el futuro o [!UICONTROL Tiempo de inactividad] está en el pasado.

>[!NOTE]
>
>Todas las llamadas de API relacionadas con la carga o actualización de recursos o archivos binarios en general (como las representaciones) se eliminan para AEM como una implementación de Cloud Service. Para cargar binarios, utilice [API de carga binaria directa](developer-reference-material-apis.md#asset-upload-technical) en su lugar.

## Fragmentos de contenido {#content-fragments}

Un [fragmento de contenido](/help/assets/content-fragments/content-fragments.md) es un tipo especial de recurso. Puede utilizarse para acceder a datos estructurados, como textos, números, fechas, entre otros. Dado que existen varias diferencias con los `standard` recursos (como imágenes o documentos), algunas reglas adicionales se aplican a la administración de fragmentos de contenido.

Para obtener más información, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

## modelo Data {#data-model}

La API HTTP de Recursos expone dos elementos principales, carpetas y recursos (para recursos estándar).

Además, expone elementos más detallados para los modelos de datos personalizados que describen el contenido estructurado en fragmentos de contenido. Consulte [Modelos de datos de fragmento de contenido](/help/assets/content-fragments/assets-api-content-fragments.md#content-models-and-content-fragments) para obtener más información.

### Carpetas {#folders}

Las carpetas son como directorios en sistemas de archivos tradicionales. Son contenedores para otras carpetas o aserciones. Las carpetas tienen los siguientes componentes:

**Entidades**: Las entidades de una carpeta son sus elementos secundarios, que pueden ser carpetas y recursos.

**Propiedades**:

* `name` es el nombre de la carpeta. Es lo mismo que el último segmento de la ruta de URL sin la extensión.
* `title` es un título opcional de la carpeta que se puede mostrar en lugar de su nombre.

>[!NOTE]
>
>Algunas propiedades de carpeta o recurso se asignan a un prefijo diferente. El prefijo `jcr` de `jcr:title`, `jcr:description` y `jcr:language` se reemplazan con el prefijo `dc`. Por lo tanto, en el JSON devuelto, `dc:title` y `dc:description` contienen los valores de `jcr:title` y `jcr:description`, respectivamente.

**** VínculosCarpetas muestra tres vínculos:

* `self`:: Vínculo a sí mismo.
* `parent`:: Vínculo a la carpeta principal.
* `thumbnail`:: (Opcional) vínculo a una imagen en miniatura de la carpeta.

### Assets {#assets}

En [!DNL Experience Manager] un recurso contiene los siguientes elementos:

* Propiedades y metadatos del recurso.
* Varias representaciones, como la representación original (que es el recurso cargado originalmente), una miniatura y otras representaciones. Las representaciones adicionales pueden ser imágenes de diferentes tamaños, codificaciones de vídeo diferentes o páginas extraídas de archivos PDF o Adobe InDesign.
* Comentarios opcionales.

Para obtener más información sobre los elementos de los fragmentos de contenido, consulte [Compatibilidad con fragmentos de contenido en la API HTTP de Experience Manager Assets](/help/assets/content-fragments/assets-api-content-fragments.md).

En [!DNL Experience Manager] una carpeta tiene los siguientes componentes:

* Entidades: Los hijos de los activos son sus representaciones.
* Propiedades.
* Vínculos.

## Funciones disponibles {#available-features}

La API HTTP de Assets incluye las siguientes funciones:

* Recupere una lista de carpetas.
* Crear una carpeta.
* Crear un recurso (desaprobado).
* Actualizar el binario de recursos (desaprobado).
* Actualice los metadatos del recurso.
* Cree una representación de recursos.
* Actualizar una representación de recursos.
* Cree un comentario de recurso.
* Copie una carpeta o un recurso.
* Mover una carpeta o un recurso.
* Elimine una carpeta, recurso o representación.

>[!NOTE]
>
>Para facilitar la lectura, en los siguientes ejemplos se omite la notación completa de cURL. De hecho, la notación sí se correlaciona con [Resty](https://github.com/micha/resty), que es un contenedor de secuencias de comandos para `cURL`.

<!-- TBD: The Console Manager is not available now. So how to configure the below? 

**Prerequisites**

* Go to `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.
-->

## Recuperar una lista de carpetas {#retrieve-a-folder-listing}

Recupera una representación sirena de una carpeta existente y de sus entidades secundarias (subcarpetas o recursos).

**Solicitud**:  `GET /api/assets/myFolder.json`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - OK - éxito.
* 404 - NO ENCONTRADO - la carpeta no existe o no es accesible.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

**Respuesta**: La clase de la entidad devuelta es un recurso o una carpeta. Las propiedades de las entidades contenidas son un subconjunto del conjunto completo de propiedades de cada entidad. Para obtener una representación completa de la entidad, los clientes deben recuperar el contenido de la dirección URL señalada por el vínculo con un `rel` de `self`.

## Cree una carpeta  . {#create-a-folder}

Crea un nuevo `sling`: `OrderedFolder` en la ruta dada. Si se proporciona un `*` en lugar de un nombre de nodo, el servlet utiliza el nombre del parámetro como nombre de nodo. Se acepta como datos de solicitud una representación sirena de la nueva carpeta o un conjunto de pares nombre-valor, codificados como `application/www-form-urlencoded` o `multipart`/ `form`- `data`, útiles para crear una carpeta directamente desde un formulario HTML. Además, las propiedades de la carpeta se pueden especificar como parámetros de consulta URL.

Una llamada de API falla con un código de respuesta `500` si el nodo principal de la ruta proporcionada no existe. Una llamada devuelve un código de respuesta `409` si la carpeta ya existe.

**Parámetros**:  `name` es el nombre de la carpeta.

**Solicitar**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - sobre la creación exitosa.
* 409 - CONFLICTO - si la carpeta ya existe.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Crear un recurso {#create-an-asset}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo crear un recurso mediante API. La creación de un recurso mediante la API HTTP está en desuso.

## Actualizar un binario de recursos {#update-asset-binary}

Consulte [carga de recursos](developer-reference-material-apis.md) para obtener información sobre cómo actualizar los binarios de recursos mediante API. La actualización de un binario de recursos mediante la API HTTP está en desuso.

## Actualizar metadatos de un recurso {#update-asset-metadata}

Actualiza las propiedades de metadatos de recurso. Si actualiza cualquier propiedad de la Área de nombres `dc:`, la API actualiza la misma propiedad en la Área de nombres `jcr`. La API no sincroniza las propiedades de las dos Áreas de nombres.

**Solicitud**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - Correcto: si el recurso se ha actualizado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Crear una representación de recursos {#create-an-asset-rendition}

Cree una nueva representación de recursos para un recurso. Si no se proporciona el nombre del parámetro de solicitud, el nombre del archivo se utiliza como nombre de representación.

**Parámetros**: Los parámetros son  `name` para el nombre de la representación y  `file` como referencia de archivo.

**Solicitar**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Códigos de respuesta**

* 201 - CREADO - si la representación se ha creado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Actualizar una representación de recursos {#update-an-asset-rendition}

Las actualizaciones reemplazan respectivamente una representación de recursos con los nuevos datos binarios.

**Solicitud**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - Correcto: si la representación se ha actualizado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Añadir un comentario en un recurso {#create-an-asset-comment}

Crea un nuevo comentario de recurso.

**Parámetros**: Los parámetros son  `message` para el cuerpo del mensaje del comentario y  `annotationData` para los datos de anotación en formato JSON.

**Solicitud**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si Comment se ha creado correctamente.
* 404 - NO ENCONTRADO - si no se pudo encontrar o acceder al recurso en el URI proporcionado.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Copiar una carpeta o un recurso {#copy-a-folder-or-asset}

Copia una carpeta o un recurso disponible en la ruta proporcionada a un nuevo destino.

**Encabezados** de solicitud: Los parámetros son:

* `X-Destination` - un nuevo URI de destino dentro del ámbito de la solución API al que copiar el recurso.
* `X-Depth` -  `infinity` o  `0`. El uso de `0` sólo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Se utiliza  `F` para evitar la sobrescritura de un recurso en el destino existente.

**Solicitud**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO - si la carpeta o el recurso se ha copiado en un destino existente.
* 412 - ERROR DE PRECONDICIÓN - si falta un encabezado de solicitud.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Mover una carpeta o un recurso {#move-a-folder-or-asset}

Mueve una carpeta o un recurso de la ruta dada a un nuevo destino.

**Encabezados** de solicitud: Los parámetros son:

* `X-Destination` - un nuevo URI de destino dentro del ámbito de la solución API al que copiar el recurso.
* `X-Depth` -  `infinity` o  `0`. El uso de `0` sólo copia el recurso y sus propiedades y no sus elementos secundarios.
* `X-Overwrite` - Utilice  `T` para forzar la eliminación de recursos existentes o  `F` para evitar la sobrescritura de recursos existentes.

**Solicitud**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Códigos** de respuesta: Los códigos de respuesta son:

* 201 - CREADO - si la carpeta o el recurso se ha copiado en un destino no existente.
* 204 - SIN CONTENIDO - si la carpeta o el recurso se ha copiado en un destino existente.
* 412 - ERROR DE PRECONDICIÓN - si falta un encabezado de solicitud.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.

## Eliminar una carpeta, un recurso o una representación {#delete-a-folder-asset-or-rendition}

Elimina un recurso (-tree) en la ruta proporcionada.

**Solicitar**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Códigos** de respuesta: Los códigos de respuesta son:

* 200 - Correcto: si la carpeta se ha eliminado correctamente.
* 412 - ERROR DE PRECONDICIÓN: si no se encuentra la colección raíz o no se puede obtener acceso a ella.
* 500 - ERROR DEL SERVIDOR INTERNO - si algo más sale mal.
