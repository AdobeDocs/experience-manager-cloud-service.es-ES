---
title: CDN en AEM as a Cloud Service
description: CDN en AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 15%

---

# CDN en AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM."

AEM as a Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

La CDN administrada por AEM satisface la mayoría de los requisitos de rendimiento y seguridad del cliente. Para el nivel de publicación, los clientes pueden opcionalmente apuntar a él desde su propia CDN, que deben administrar. Este escenario se permite caso por caso, en función de cumplir ciertos requisitos previos, incluido, entre otros, el cliente que tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## CDN administrada por AEM  {#aem-managed-cdn}

Siga las secciones a continuación para utilizar la interfaz de usuario de autoservicio de Cloud Manager para prepararse para la entrega de contenido mediante AEM CDN predeterminada:

1. [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Administrar los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restricción de tráfico**

De forma predeterminada, para una configuración de CDN administrada por AEM, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Puede limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP) mediante la interfaz de usuario de Cloud Manager.

Consulte [Administrar listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para obtener más información.

>[!CAUTION]
>
>Solo las solicitudes de las IP permitidas son atendidas por AEM CDN gestionado. Si dirige su propia CDN a la CDN administrada por AEM, asegúrese de que las IP de su CDN estén incluidas en la lista de permitidos.

## La CDN del cliente apunta a la CDN administrada por AEM {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="La CDN del cliente apunta a una CDN administrada de AEM"
>abstract="AEM as a Cloud Service ofrece una opción para que los clientes utilicen su CDN existente. Para el nivel de publicación, los clientes pueden opcionalmente apuntar a él desde su propia CDN, que deben administrar. Este escenario se permite caso por caso, en función de cumplir ciertos requisitos previos, incluido, entre otros, el cliente que tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar."

Si un cliente debe utilizar su CDN existente, puede administrarla y señalarla a la CDN administrada por AEM, siempre que se cumplan las condiciones siguientes:

* El cliente debe tener una CDN existente que sea onerosa de reemplazar.
* El cliente debe administrarlo.
* El cliente debe poder configurar la CDN para que funcione con AEM as a Cloud Service; consulte las instrucciones de configuración que se presentan a continuación.
* El cliente debe tener expertos en CDN de ingeniería que estén disponibles en caso de que surjan problemas relacionados con el caso.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Asigne su CDN a la entrada de la CDN de Adobe como su dominio de origen. Por ejemplo, `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Establezca SNI en la entrada de la CDN de Adobe.
1. Establezca el encabezado Host en el dominio de origen. Por ejemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Configure las variables `X-Forwarded-Host` con el nombre de dominio para AEM determinar el encabezado de host. Por ejemplo: `X-Forwarded-Host:example.com`.
1. Establecer `X-AEM-Edge-Key`. El valor debe proceder del Adobe.

   * Necesario para que la CDN de Adobe pueda validar el origen de las solicitudes y pasar el `X-Forwarded-*` encabezados a la aplicación AEM. Por ejemplo,`X-Forwarded-For` se usa para determinar la IP del cliente. Por lo tanto, se convierte en responsabilidad del llamador de confianza (es decir, la CDN administrada por el cliente) garantizar la exactitud de la variable `X-Forwarded-*` encabezados (consulte la nota siguiente).
   * Opcionalmente, el acceso a la entrada de la CDN de Adobe se puede bloquear cuando se `X-AEM-Edge-Key` no está presente. Informe a Adobe si necesita acceso directo a la entrada de CDN de Adobe (para bloquearlo).

Consulte la [Ejemplos de configuraciones de proveedor de CDN](#sample-configurations) para obtener ejemplos de configuración de los principales proveedores de CDN.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

Después de obtener la variable `X-AEM-Edge-Key`, puede probar que la solicitud se ha enrutado correctamente de la siguiente manera.

En Linux®:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

En Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>Al utilizar su propia CDN, no es necesario instalar dominios y certificados en Cloud Manager. El enrutamiento en la CDN de Adobe se realiza utilizando el dominio predeterminado `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` que deben enviarse en la solicitud `Host` encabezado. Sobrescritura de la solicitud `Host` con un nombre de dominio personalizado puede hacer que la solicitud sea enrutada incorrectamente por la CDN de Adobe.


>[!NOTE]
>
>Los clientes que administran su propia CDN deben garantizar la integridad de los encabezados que se envían a AEM CDN. Por ejemplo, se recomienda que los clientes borren todos los `X-Forwarded-*` encabezados y definirlos en valores conocidos y controlados. Por ejemplo, `X-Forwarded-For` debe contener la dirección IP del cliente, mientras que `X-Forwarded-Host` debe contener el host del sitio.

>[!NOTE]
>
>Los entornos de programa de espacio aislado no admiten una CDN proporcionada por el cliente.

El salto adicional entre la CDN del cliente y la CDN AEM solo es necesario si falta una caché. Al utilizar las estrategias de optimización de caché descritas en este artículo, la adición de una CDN de cliente solo debería introducir una latencia insignificante.

Esta configuración de CDN de cliente es compatible con el nivel de publicación, pero no con el nivel de creación.

### Ejemplos de configuraciones de proveedor de CDN {#sample-configurations}

A continuación se presentan varios ejemplos de configuración de varios proveedores líderes de CDN.

**Akamai**

![Akamai1](assets/akamai1.png "Akamai")
![Akamai2](assets/akamai2.png "Akamai")

**Amazon CloudFront**

![CloudFront1](assets/cloudfront1.png "Amazon CloudFront")
![CloudFront2](assets/cloudfront2.png "Amazon CloudFront")

**Cloudflare**

![Cloudflare1](assets/cloudflare1.png "Cloudflare")
![Cloudflare2](assets/cloudflare2.png "Cloudflare")

## Encabezados de geolocalización {#geo-headers}

La CDN administrada por AEM añade encabezados a cada solicitud con:

* código de país: `x-aem-client-country`
* código de continente: `x-aem-client-continent`

>[!NOTE]
>
>Si hay una CDN administrada por el cliente, estos encabezados reflejan la ubicación del servidor proxy CDN del cliente en lugar del cliente real. Por lo tanto, para la CDN administrada por el cliente, los encabezados de geolocalización deben ser administrados por la CDN de los clientes.

Los valores de los códigos de país son los códigos alfa-2 descritos [here](https://en.wikipedia.org/wiki/ISO_3166-1).

Los valores de los códigos continentales son:

* AF África
* Una Antártida
* AS Asia
* UE
* Norteamérica
* OC Oceania
* Sudamérica

Esta información puede resultar útil para casos de uso como, por ejemplo, redirigir a una URL diferente en función del origen (país) de la solicitud. Utilice el encabezado Vary para almacenar en caché las respuestas que dependen de la información geográfica. Por ejemplo, las redirecciones a una página de aterrizaje de país específica siempre deben contener `Vary: x-aem-client-country`. Si es necesario, puede utilizar `Cache-Control: private` para evitar el almacenamiento en caché. Consulte también [Almacenamiento en caché](/help/implementing/dispatcher/caching.md#html-text).
