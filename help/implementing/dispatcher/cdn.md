---
title: CDN en AEM as a Cloud Service
description: CDN en AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: b6ae5cab872a3cca4eb41259f6c242b1fbeb98bb
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 5%

---


# CDN en AEM as a Cloud Service {#cdn}

AEM como Cloud Service se envía con una CDN integrada. Su principal propósito es reducir la latencia mediante la entrega de contenido procesable desde los nodos CDN en el borde, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

La CDN administrada por AEM satisfará la mayoría de los requisitos de rendimiento y seguridad del cliente. Para el nivel de publicación, los clientes pueden opcionalmente señalarlo desde su propia CDN, que deberán administrar. Esto se permitirá caso por caso, en función de cumplir ciertos requisitos previos, incluido, entre otros, el cliente que tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

## CDN administrado por AEM {#aem-managed-cdn}

Siga las secciones a continuación para utilizar la interfaz de usuario de autoservicio de Cloud Manager y prepararse para el envío de contenido mediante la CDN integrada de Adobe:

1. [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restricción del tráfico**

De forma predeterminada, para una configuración de CDN administrada por Adobe, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP), puede hacerlo de forma automática mediante la interfaz de usuario del Administrador de nube.

Consulte [Administración de Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para obtener más información.

>[!CAUTION]
>
>Solo las solicitudes de las IP permitidas serán atendidas por la CDN administrada de AEM. Si señala su propia CDN a la CDN administrada de AEM, asegúrese de que las IP de su CDN se incluyen en la lista de permitidos.

## CDN de cliente señala a AEM CDN administrada {#point-to-point-CDN}

Si un cliente debe utilizar su CDN existente, puede administrarlo y señalarlo a la CDN administrada por el Adobe, siempre que se satisfagan los siguientes requisitos:

* El cliente debe tener una CDN existente que sea onerosa de reemplazar.
* El cliente debe administrarlo.
* El cliente debe ser capaz de configurar el CDN para que funcione con AEM como Cloud Service; consulte las instrucciones de configuración a continuación.
* El cliente debe contar con expertos en ingeniería de CDN que estén disponibles en caso de que surjan problemas relacionados.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Establezca el encabezado `X-Forwarded-Host` con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es la entrada de CDN de Adobe. El valor debe proceder del Adobe.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado sni debe ser el dominio de origen.
1. Establezca `X-Edge-Key`, que es necesario para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder del Adobe.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

Existe potencialmente una pequeña visita de rendimiento debido al salto adicional, aunque es probable que los saltos de la CDN del cliente a la CDN administrada por el Adobe sean eficientes.

Tenga en cuenta que esta configuración de CDN de cliente es compatible con el nivel de publicación, pero no con el nivel de autor.

## Encabezados de geolocalización {#geo-headers}

La CDN administrada por Adobe agregará encabezados a cada solicitud con:

* código de país: `x-aem-client-country`
* código de continente: `x-aem-client-continent`

Los valores de los códigos de país son los códigos Alpha-2 descritos [aquí](https://en.wikipedia.org/wiki/ISO_3166-1).

Los valores de los códigos de continente son:

* AF África
* UNA Antártida
* AS Asia
* Europa
* Norteamérica
* OC Oceania
* Sudamérica

Esta información puede ser útil para casos de uso como redireccionar a una dirección URL diferente según el origen (país) de la solicitud. Aunque, en este caso de uso específico, la redirección no debe almacenarse en caché, ya que varía. Si es necesario, puede utilizar `Cache-Control: private` para evitar el almacenamiento en caché. Consulte también [Almacenamiento en caché](/help/implementing/dispatcher/caching.md#html-text).
