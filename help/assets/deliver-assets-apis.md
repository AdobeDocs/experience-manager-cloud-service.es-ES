---
title: API de envío
description: Aprenda a utilizar las API de entrega.
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 5%

---

# API de envío {#delivery-apis}

Todos los [recursos aprobados](approve-assets.md) disponibles en el repositorio de recursos de Experience Manager se pueden [buscar](search-assets-api.md) y luego entregarse a aplicaciones integradas de flujo descendente mediante una URL de entrega.

Cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para la entrega de recursos a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

La siguiente imagen ilustra las direcciones URL de envío disponibles:

![API de envío](assets/delivery-url.png)

La siguiente tabla ilustra el uso de las distintas API de envío disponibles:

| API de envío | Descripción |
|---|---|
| [Representación binaria optimizada para la web del recurso en el formato de salida solicitado](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | Devuelve la representación binaria optimizada para la web del recurso en el formato de salida solicitado en función del ID de recurso enviado en la solicitud. Además, puede definir varios modificadores de imagen, como ancho, alto, giro, voltear, calidad, recorte, formato y [recorte inteligente](/help/assets/dynamic-media/image-profiles.md). Consulte los [detalles de la API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) para ver los formatos y modificadores de imagen admitidos.<br>Adobe recomienda usar esta API para todos los tipos de formato de imagen. |
| [Representación binaria optimizada para la web del recurso](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | API de conveniencia que aplica valores predeterminados a la representación binaria optimizada para la web del recurso devuelto en la respuesta. Los valores predeterminados incluyen un formato JPEG/WEBP estándar, calidad => 65 y anchura => 1024. |
| [binario subido original del recurso](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | Devuelve los binarios cargados originalmente para el recurso. Adobe recomienda utilizar esta API para tipos de formato de documento e imágenes de SVG. |
| [Representación pregenerada del recurso disponible en el entorno de creación de AEM Assets](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | Devuelve el flujo de bits de la representación de recursos disponible en el entorno de creación de AEM Assets en función del ID de recurso y el nombre de representación enviados en la solicitud. |
| [Metadatos de recursos](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | Devuelve las propiedades asociadas a un recurso como, por ejemplo, title, description, CreateDate, ModifyDate, etc. |
| [Contenedor del reproductor para el recurso de vídeo](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | Devuelve el contenedor del reproductor para el recurso de vídeo. Puede incrustar el reproductor en un elemento de HTML de iframe y reproducir el vídeo. |
| [Manifiestos de reproducción en el formato de salida seleccionado](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | Devuelve el archivo de manifiesto de reproducción del recurso de vídeo especificado en el formato de salida seleccionado. Debe crear un reproductor personalizado capaz de flujo adaptable a través de protocolos HLS o DASH para poder extraer el archivo de manifiesto de reproducción y reproducir el vídeo. |

Dynamic Media con funciones de OpenAPI también admite vídeos de formularios largos. Los vídeos de formato largo pueden admitir hasta 50 GB y 2 horas.

Para obtener información sobre las ofertas disponibles de Dynamic Media y sus capacidades, consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

## Extremos de API de envío {#delivery-apis-endpoint}

Los extremos de las API varían para cada API de entrega. Por ejemplo, el extremo de API para la API `Web-optimized binary representation of the asset in the requested output format` es:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

El dominio de envío tiene una estructura similar al dominio del entorno de creación de Experience Manager. La única diferencia es reemplazar el término `author` por `delivery`.

`pXXXX` hace referencia al ID de programa

`eYYYY` hace referencia al ID de entorno

Ver [detalles de la API](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets) para obtener más información.

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

Para invocar las API de entrega, se requiere un token de IMS en los detalles de `Authorization` para entregar un recurso restringido. El token de IMS se obtiene de una cuenta técnica. Consulte [Recuperar las credenciales de AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para crear una nueva cuenta técnica. Consulte [Generación del token de acceso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para generar el token de IMS y utilizarlo correctamente en el encabezado de solicitud de las API de entrega.


Para ver ejemplos de solicitudes, ejemplos de respuestas y códigos de respuesta, consulte [API de entrega](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).
