---
title: CDN en AEM as a Cloud Service
description: CDN en AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
translation-type: tm+mt
source-git-commit: b063fee5e088d6dfe5bd6be2b842e6bae48ee4a9
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 7%

---

# CDN en AEM as a Cloud Service {#cdn}

AEM como Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

La CDN administrada AEM satisfará la mayoría de los requisitos de rendimiento y seguridad del cliente. Para el nivel de publicación, los clientes pueden opcionalmente apuntar a él desde su propia CDN, que deberán administrar. Esto se permitirá caso por caso, en función de cumplir ciertos requisitos previos, incluido, entre otros, el cliente que tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

## AEM CDN administrado {#aem-managed-cdn}

Siga las secciones a continuación para utilizar la interfaz de usuario de autoservicio de Cloud Manager para prepararse para la entrega de contenido mediante la CDN predeterminada de AEM:

1. [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restricción de tráfico**

De forma predeterminada, para una configuración de CDN administrada AEM, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por una serie de direcciones IP), puede hacerlo de forma automática mediante la interfaz de usuario de Cloud Manager.

Consulte [Administración de Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para obtener más información.

>[!CAUTION]
>
>Solo las solicitudes de las IP permitidas serán atendidas por la CDN administrada de AEM. Si señala su propia CDN a la CDN administrada de AEM, asegúrese de que las IP de su CDN estén incluidas en la lista de permitidos.

## La CDN del cliente apunta a AEM CDN administrada {#point-to-point-CDN}

Si un cliente debe utilizar su CDN existente, puede administrarla y señalarla a la CDN administrada de AEM, siempre que se cumplan las condiciones siguientes:

* El cliente debe tener una CDN existente que sea onerosa de reemplazar.
* El cliente debe administrarlo.
* El cliente debe poder configurar la CDN para que funcione con AEM como Cloud Service; consulte las instrucciones de configuración que se indican a continuación.
* El cliente debe tener expertos en CDN de ingeniería que estén disponibles en caso de que surjan problemas relacionados.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Establezca el encabezado `X-Forwarded-Host` con el nombre de dominio. Por ejemplo: `X-Forwarded-Host:example.com`.
1. Establezca el encabezado del host con el dominio de origen, que es la entrada de la CDN de AEM. Por ejemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado SNI debe ser el dominio de origen.
1. Establezca `X-Edge-Key` o `X-AEM-Edge-Key` (si su CDN elimina `X-Edge-*`). El valor debe proceder del Adobe.
   * Esto es necesario para que la CDN de Adobe pueda validar el origen de las solicitudes y pasar los encabezados `X-Forwarded-*` a la aplicación de AEM. Por ejemplo, AEM utiliza `X-Forwarded-Host` para determinar el encabezado del host y `X-Forwarded-For` para determinar la IP del cliente. Por lo tanto, es responsabilidad del llamador de confianza (es decir, la CDN administrada por el cliente) garantizar la exactitud de los encabezados `X-Forwarded-*` (consulte la nota a continuación).
   * Opcionalmente, el acceso a la entrada de la CDN de Adobe se puede bloquear cuando no está presente una `X-Edge-Key`. Informe a Adobe si necesita acceso directo a la entrada de CDN de Adobe (para ser bloqueado).

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

>[!NOTE]
>
>Los clientes que administran su propia CDN deben garantizar la integridad de los encabezados que se envían a AEM CDN. Por ejemplo, se recomienda que los clientes borren todos los encabezados `X-Forwarded-*` y los configuren en valores conocidos y controlados. Por ejemplo, `X-Forwarded-For` debe contener la dirección IP del cliente, mientras que `X-Forwarded-Host` debe contener el host del sitio.

Existe potencialmente una pequeña visita de rendimiento debido al salto adicional, aunque es probable que los saltos de la CDN del cliente a la CDN administrada de AEM sean eficientes.

Tenga en cuenta que esta configuración de CDN de cliente es compatible con el nivel de publicación, pero no delante del nivel de creación.

## Encabezados de geolocalización {#geo-headers}

La CDN administrada de AEM agrega encabezados a cada solicitud con:

* código de país: `x-aem-client-country`
* código de continente: `x-aem-client-continent`

Los valores de los códigos de país son los códigos alfa-2 descritos [aquí](https://en.wikipedia.org/wiki/ISO_3166-1).

Los valores de los códigos continentales son:

* AF África
* Una Antártida
* AS Asia
* UE
* Norteamérica
* OC Oceania
* Sudamérica

Esta información puede resultar útil para casos de uso como, por ejemplo, redirigir a una URL diferente en función del origen (país) de la solicitud. Utilice el encabezado Vary para almacenar en caché las respuestas que dependen de la información geográfica. Por ejemplo, las redirecciones a una página de aterrizaje de país específica siempre deben contener `Vary: x-aem-client-country`. Si es necesario, puede utilizar `Cache-Control: private` para evitar el almacenamiento en caché. Consulte también [Almacenamiento en caché](/help/implementing/dispatcher/caching.md#html-text).
