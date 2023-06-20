---
title: Encabezados HTTP personalizados
description: Configuración de encabezados HTTP personalizados
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 5%

---

# Encabezados HTTP personalizados {#custom-http-headers}

## Información general {#overview}

Para obtener más control sobre su back-end, los autores pueden configurar encabezados HTTP personalizados que se envían al motor de comercio, junto con los que ya envía CIF. Los casos de uso comunes incluyen configuraciones de varias tiendas en las que puede utilizar encabezados HTTP para controlar la respuesta del back-end de comercio.

>[!NOTE]
>
>Los desarrolladores siempre pueden configurar encabezados HTTP personalizados mediante la configuración del cliente de GraphQL.
>

## Configuración {#configuration}

Para configurar los encabezados HTTP personalizados, primero debe definirlos. Los encabezados HTTP personalizados deben definirse primero agregándolos a la variable `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` configuración del servicio mediante una configuración OSGi.

Puede configurar los valores de los encabezados HTTP en la página Configuración de Cloud Service de su proyecto:

1. Vaya a la página de configuración del Cloud Service en Herramientas -> Cloud Services -> Configuración del CIF
1. Abra una configuración existente o cree una nueva
1. Vaya a la pestaña &quot;Avanzado&quot; y busque el campo múltiple &quot;Encabezados HTTP personalizados&quot;. Puede seleccionar los encabezados definidos anteriormente y asignarles valores.

Los componentes que utilizan la configuración de servicio en la nube anterior enviarán estos encabezados HTTP con cada solicitud de GraphQL.

## Restricciones {#restrictions}

Aunque el servicio permite definir cualquier nombre de encabezado, incluidos los estándar, no estarán disponibles para su configuración. En otras palabras, no se pueden anular los encabezados HTTP estándar con esta función. Se puede encontrar una lista de nombres de encabezado restringidos [aquí](https://developer.mozilla.org/es-ES/docs/Web/HTTP/Headers). Además de estos, hay dos encabezados más que no se pueden utilizar:

* &quot;Tienda&quot;: utilizada por CIF para identificar la tienda Adobe Commerce
* &quot;Preview-Version&quot;: utilizado por CIF para recuperar productos clasificados
