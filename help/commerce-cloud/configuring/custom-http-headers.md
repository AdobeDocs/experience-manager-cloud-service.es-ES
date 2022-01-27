---
title: Encabezados HTTP personalizados
description: Configuración de encabezados HTTP personalizados
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# Encabezados HTTP personalizados {#custom-http-headers}

## Información general {#overview}

Para obtener más control sobre su backend, los autores pueden configurar encabezados HTTP personalizados que se enviarán al motor de comercio, junto con los que ya envía CIF. Los casos de uso comunes incluyen configuraciones de varias tiendas en las que puede utilizar encabezados HTTP para controlar la respuesta del back-end de comercio.

>[!NOTE]
>
>Los desarrolladores siempre pueden configurar encabezados HTTP personalizados mediante la configuración de cliente de GraphQL.

## Configuración {#configuration}

Para configurar los encabezados HTTP personalizados, primero debe definirlos. Los encabezados HTTP personalizados deben definirse primero agregándolos al `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configuración del servicio mediante una configuración OSGi.

Puede configurar los valores de los encabezados HTTP en la página Configuración del Cloud Service del proyecto:

1. Vaya a la página de configuración del Cloud Service en Herramientas -> Cloud Services -> Configuración del CIF
1. Abrir una configuración existente o crear una nueva
1. Vaya a la pestaña &quot;Avanzado&quot; y busque los campos múltiples &quot;Encabezados HTTP personalizados&quot;. Puede seleccionar los encabezados que definió anteriormente y asignarles valores.

Los componentes que utilizan la configuración de servicio en la nube anterior enviarán estos encabezados HTTP con cada solicitud de GraphQL.

## Restricciones {#restrictions}

Aunque el servicio permite definir cualquier nombre de encabezado, incluidos los estándar, no estarán disponibles para configurarlos. En otras palabras, no puede anular los encabezados HTTP estándar usando esta función. Se puede encontrar una lista de nombres de encabezado restringidos [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). Además de estos, hay dos encabezados más que no se pueden usar:

* &quot;Tienda&quot;: lo utiliza CIF para identificar la tienda de Adobe Commerce.
* &quot;Preview-Version&quot;: se utiliza en el CIF para recuperar productos clasificados
