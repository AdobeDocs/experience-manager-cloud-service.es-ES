---
title: Encabezados HTTP personalizados
description: Aprenda a configurar encabezados HTTP personalizados que se envían al motor de comercio, junto con los que ya envía CIF.
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---


# Encabezados HTTP personalizados {#custom-http-headers}

Aprenda a configurar encabezados HTTP personalizados que se envían al motor de comercio, junto con los que ya envía CIF.

## Información general {#overview}

Para obtener más control sobre su back-end, los autores pueden configurar encabezados HTTP personalizados que se envían al motor de comercio, junto con los que ya envía CIF. Los casos de uso comunes incluyen configuraciones de varias tiendas en las que puede utilizar encabezados HTTP para controlar la respuesta del back-end de comercio.

>[!NOTE]
>
>Los desarrolladores siempre pueden configurar encabezados HTTP personalizados mediante la configuración del cliente de GraphQL.
>

## Configuración {#configuration}

Para configurar los encabezados HTTP personalizados, primero debe definirlos. Los encabezados HTTP personalizados deben definirse primero agregándolos a la configuración del servicio `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` mediante una configuración OSGi.

Puede configurar los valores de los encabezados HTTP en la página Configuración de Cloud Service para su proyecto:

1. Vaya a la página de configuración de Cloud Service en Herramientas > Cloud Services > Configuración de CIF
1. Abra una configuración existente o cree una
1. Vaya a la pestaña &quot;Avanzado&quot; y busque el campo múltiple &quot;Encabezados HTTP personalizados&quot;. Puede seleccionar los encabezados definidos anteriormente y asignarles valores.

Los componentes que utilizan la configuración de servicio en la nube anterior enviarán estos encabezados HTTP con cada solicitud de GraphQL.

## Restricciones {#restrictions}

Aunque el servicio permite definir cualquier nombre de encabezado, incluidos los estándar, no estarán disponibles para su configuración. En otras palabras, no se pueden anular los encabezados HTTP estándar con esta función. Encontrará una lista de nombres de encabezados restringidos en [documentos web mdn: encabezados HTTP.](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) Además de estos, hay dos encabezados más que no se pueden usar:

* &quot;Tienda&quot;: CIF la utiliza para identificar la tienda Adobe Commerce
* &quot;Preview-Version&quot;: utilizado por CIF para recuperar productos clasificados
