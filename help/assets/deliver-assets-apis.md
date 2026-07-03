---
title: API de envío
description: Aprenda a utilizar las API de entrega.
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: fa93e2079ad5a2840b5e58c5b83cb288606bda97
workflow-type: tm+mt
source-wordcount: '1879'
ht-degree: 6%

---

# API de envío {#delivery-apis}

Todos los [recursos aprobados](approve-assets.md) disponibles en el repositorio de recursos de Experience Manager se pueden [buscar](search-assets-api.md) y luego entregarse a aplicaciones integradas de flujo descendente mediante una URL de entrega.

Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para la entrega de recursos a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

La siguiente imagen ilustra las direcciones URL de envío disponibles:

![API de envío](assets/delivery-url.png)

La siguiente tabla ilustra el uso de las distintas API de envío disponibles:

| API de entrega | Descripción |
|---|---|
| [Representación binaria optimizada para la web del recurso en el formato de salida solicitado](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat) | Devuelve la representación binaria optimizada para la web del recurso en el formato de salida solicitado en función del ID de recurso enviado en la solicitud. Además, puede definir varios modificadores de imagen, como anchura, altura, rotación, voltear, calidad, recorte, formato y [recorte inteligente](/help/assets/dynamic-media/image-profiles.md). Consulte los [detalles de la API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat) para ver los formatos y modificadores de imagen admitidos.<br>Adobe recomienda usar esta API para todos los tipos de formato de imagen. |
| [Representación binaria optimizada para la web del recurso](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAsset) | API de conveniencia que aplica valores predeterminados a una representación binaria optimizada para la web del recurso devuelto en la respuesta. Los valores predeterminados incluyen un formato JPEG/WEBP estándar, calidad => 65 y anchura => 1024. |
| [binario subido original del recurso](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetOriginal) | Devuelve los binarios cargados originalmente para el recurso. Adobe recomienda utilizar esta API para tipos de formato de documento e imágenes de SVG. |
| [Representación pregenerada del recurso disponible en el entorno de creación de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetRendition) | Devuelve el flujo de bits de la representación de recursos disponible en el entorno de creación de AEM Assets en función del ID de recurso y el nombre de representación enviados en la solicitud. |
| [Metadatos de recursos](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetMetadata) | Devuelve las propiedades asociadas a un recurso, como título, descripción, CreateDate, ModifyDate, etc. |
| [Contenedor del reproductor para el recurso de vídeo](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoPlayerDelivery) | Devuelve el contenedor del reproductor para el recurso de vídeo. Puede incrustar el reproductor en un elemento de HTML de iframe y reproducir el vídeo. |
| [Manifiestos de reproducción en el formato de salida seleccionado](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/videoManifestDelivery) | Devuelve el archivo de manifiesto de reproducción del recurso de vídeo especificado en el formato de salida seleccionado. Debe crear un reproductor personalizado capaz de flujo adaptable a través de protocolos HLS o DASH para poder extraer el archivo de manifiesto de reproducción y reproducir el vídeo. |

>[!IMPORTANT]
>
>Puede probar cualquier modificador, lo cual no suele estar disponible a través de API experimentales. Por ejemplo, Haga clic aquí para obtener más información sobre cómo usar las [API experimentales](https://developer.adobe.com/experience-cloud/experience-manager-apis/guides/how-to/#experimental-apis) y la [lista completa de modificadores](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

Dynamic Media con funciones de OpenAPI también admite vídeos de formularios largos. Los vídeos de formato largo pueden admitir hasta 50 GB y 2 horas.

Para obtener información sobre las ofertas de Dynamic Media disponibles, consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

>[!NOTE]
>
>Los clientes de DM Prime pueden utilizar modificadores de imagen básicos como rotar, recortar, voltear, alto, anchura y calidad. Las imágenes inteligentes no son compatibles con AVIF para clientes de DM Prime.

## Extremos de API de envío {#delivery-apis-endpoint}

Los extremos de las API varían para cada API de entrega. Por ejemplo, el extremo de API para la API `Web-optimized binary representation of the asset in the requested output format` es:

El dominio de envío tiene una estructura similar al dominio del entorno de creación de Experience Manager. La única diferencia es reemplazar el término `author` por `delivery`.

`pXXXX` hace referencia al ID de programa

`eYYYY` hace referencia al ID de entorno

Ver [detalles de la API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#tag/Assets) para obtener más información.

## Método de solicitud de API de envío {#delivery-api-request-method}

GET

## Encabezado de API de envío {#deliver-assets-api-header}

Debe proporcionar los siguientes detalles al definir un encabezado en el encabezado de las API de envío:

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

Para invocar las API de entrega, se requiere un token de IMS en los detalles de `Authorization` para entregar un recurso restringido. El token de IMS se obtiene de una cuenta técnica. Consulte [Recuperar las credenciales de AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis) para crear una nueva cuenta técnica. Consulte [Generación del token de acceso](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis) para generar el token de IMS y utilizarlo correctamente en el encabezado de solicitud de las API de entrega.


Para ver ejemplos de solicitudes, ejemplos de respuestas y códigos de respuesta, consulte [API de entrega](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/#operation/getAssetSeoFormat).

## Preguntas frecuentes {#delivery-apis-faqs}

### ¿Qué es Dynamic Media con las API de envío de OpenAPI y qué habilitan? {#delivery-apis-overview}

Dynamic Media con las API de entrega de OpenAPI permiten que los recursos aprobados almacenados en Adobe Experience Manager Assets se entreguen a aplicaciones de flujo descendente integradas a través de una URL de entrega. Hay siete API distintas disponibles que abarcan la entrega de imágenes, la entrega binaria original, la entrega de representación pregenerada, la recuperación de metadatos de recursos, la incrustación del reproductor de vídeo y la entrega de manifiesto de reproducción de vídeo. Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de envío sin necesidad de volver a publicar ni intervenir manualmente.

### ¿Con qué rapidez aparecen las actualizaciones de recursos en las direcciones URL de la API de entrega después de realizar cambios en los AEM Assets? {#delivery-api-ttl-updates}

Las actualizaciones de recursos aprobados en AEM Assets son visibles en todas las interfaces de creación y publicación en menos de 10 minutos. Dynamic Media con las API de entrega de OpenAPI utilizan un valor corto de tiempo de vida de 10 minutos configurado para la entrega de recursos a través de CDN. Esto significa que las actualizaciones de versión, las modificaciones de metadatos y otros cambios realizados en los recursos aprobados en DAM se propagan automáticamente a las direcciones URL de entrega en un plazo de 10 minutos sin requerir la invalidación manual de la caché.

### ¿Qué API de entrega debo utilizar para enviar recursos de imagen? {#delivery-api-image-recommendation}

La representación binaria optimizada para la web del recurso en la API de formato de salida solicitada es la API recomendada para todos los tipos de formato de imagen. Esta API devuelve la representación binaria optimizada para la web del recurso en el formato de salida solicitado en función del ID de recurso enviado en la solicitud. Admite varios modificadores de imagen, como anchura, altura, rotación, voltear, calidad, recorte, formato y recorte inteligente. Para los tipos de formato de documento y las imágenes de SVG, se recomienda el binario cargado original de la API de recursos en su lugar.

### ¿Qué modificadores de imagen admite la representación binaria optimizada para la web de la API de entrega? {#delivery-api-image-modifiers}

La representación binaria optimizada para la web del recurso en la API de formato de salida solicitada admite modificadores de imagen como anchura, altura, rotación, voltear, calidad, recorte, formato y recorte inteligente. Estos modificadores se pueden definir como parámetros en la solicitud de URL de envío para transformar el recurso en el momento de la entrega sin modificar el recurso original almacenado en los AEM Assets.

### ¿Qué devuelve de forma predeterminada la API de entrega de representación binaria optimizada para la web? {#delivery-api-defaults}

La representación binaria optimizada para la web de conveniencia de la API de recursos se aplica de forma predeterminada al recurso devuelto en la respuesta. Los valores predeterminados son el formato JPEG o WEBP, la calidad de 65 y la anchura de 1024 píxeles. Esta API es adecuada cuando no se requiere un formato de salida específico o control de modificador y una representación optimizada para la web estándar es suficiente para la aplicación descendente.

### ¿Qué API de envío debo usar para documentos e imágenes de SVG? {#delivery-api-documents-svg}

El binario cargado original de la API de recursos es la API recomendada para tipos de formato de documento e imágenes de SVG. Esta API devuelve el binario cargado originalmente para el recurso sin aplicar transformaciones de optimización web. Para todos los demás tipos de formato de imagen, se recomienda la API de representación binaria optimizada para la web en el formato de salida solicitado.

### ¿Cómo puedo recuperar representaciones generadas previamente de un recurso mediante las API de entrega? {#delivery-api-pre-generated-renditions}

La representación pregenerada del recurso disponible en la API del entorno de creación de AEM Assets devuelve el flujo de bits de una representación específica en función del ID de recurso y el nombre de representación enviados en la solicitud. La representación ya debe existir en el entorno de creación de AEM Assets para poder recuperarse mediante esta API. Esta API es distinta de la API binaria optimizada para la web que genera la salida bajo demanda mediante modificadores de imagen.

### ¿Cómo incrusto y reproduzco un recurso de vídeo mediante las API de entrega? {#delivery-api-video-player}

El contenedor del reproductor para la API de recursos de vídeo devuelve un contenedor del reproductor para un recurso de vídeo que se puede incrustar en un elemento HTML de iframe para habilitar la reproducción de vídeo en la página. En los casos que requieran implementaciones de reproductor personalizadas con flujo adaptable, la API de manifiesto de reproducción en el formato de salida seleccionado devuelve el archivo de manifiesto de reproducción para el recurso de vídeo especificado en formato HLS o DASH. Se debe crear un reproductor personalizado capaz de flujo adaptable a través de protocolos HLS o DASH para consumir el archivo de manifiesto y reproducir el vídeo.

### ¿Cuál es el tamaño máximo de archivo de vídeo y la duración que admite Dynamic Media con las API de envío de OpenAPI? {#delivery-api-video-limits}

Dynamic Media con las API de entrega de OpenAPI admiten vídeos de formato largo de hasta 50 GB de tamaño de archivo y hasta 2 horas de duración. Estos límites se aplican a los recursos de vídeo entregados a través del contenedor del reproductor y a los manifiestos de reproducción de las API de entrega.

### ¿Cómo está estructurada la URL del extremo de la API de entrega? {#delivery-api-endpoint-structure}

La dirección URL del extremo de la API de entrega para la representación binaria optimizada para la web en el formato de salida solicitado sigue esta estructura: https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}. El dominio de envío tiene una estructura similar al dominio de entorno de creación de AEM; la única diferencia es reemplazar el término autor por envío. En la dirección URL, pXXXX hace referencia al ID de programa y AAAA hace referencia al ID de entorno. Todas las API de entrega utilizan el método de petición HTTP GET.

### ¿Qué autenticación se requiere para llamar a Dynamic Media con las API de envío de OpenAPI? {#delivery-api-authentication}

Llamar a Dynamic Media con las API de entrega de OpenAPI requiere un token de IMS en el encabezado Autorización para entregar recursos restringidos. El encabezado debe incluir dos campos: If-None-Match como valor de cadena y Authorization como token de portador que contenga el token de IMS. El token de IMS se obtiene de una cuenta técnica creada con el flujo de trabajo de credenciales de AEM as a Cloud Service. La cuenta técnica debe configurarse y el token de acceso debe generarse antes de invocar cualquier API de entrega.

### ¿Qué son las API de envío experimentales y cómo puedo acceder a ellas? {#delivery-api-experimental}

Las API de envío experimentales permiten probar modificadores de imagen que aún no están disponibles de forma general. Se accede a las API experimentales mediante un formato de ruta de URL que incluye el modificador y una fecha de caducidad, por ejemplo: /adobe/experimental/advancemodifiers-expires-YYYYMMDD/assets. La lista completa de modificadores experimentales disponibles está documentada en Adobe Developer Console. Las API experimentales están pensadas para fines de prueba y están sujetas a cambios antes de su disponibilidad general.

### ¿Qué funciones de modificador de imagen están disponibles para los clientes de Dynamic Media Prime en comparación con Dynamic Media Ultimate? {#delivery-api-prime-vs-ultimate-modifiers}

Los clientes de Dynamic Media Prime pueden utilizar modificadores de imagen básicos como rotar, recortar, voltear, alto, ancho y calidad mediante las API de entrega. Imágenes inteligentes está disponible para los clientes de Dynamic Media Prime, excepto que el formato AVIF no es compatible con Imágenes inteligentes en Dynamic Media Prime. Los clientes de Dynamic Media Ultimate tienen acceso a toda la gama de modificadores de imagen y funciones de imágenes inteligentes, incluida la compatibilidad con formatos AVIF.