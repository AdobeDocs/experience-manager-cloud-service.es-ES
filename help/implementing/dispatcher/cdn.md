---
title: CDN en AEM as a Cloud Service
description: CDN en AEM as a Cloud Service
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
source-git-commit: c419da88ccfe97cf8b80e68ddd402196c2ec58e3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 12%

---

# CDN en AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN en AEM as a Cloud Service"
>abstract="AEM Como Cloud Service, se envía con una CDN integrada. Su propósito principal es reducir la latencia mediante la entrega de contenido almacenable en caché desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM."

AEM Como Cloud Service, se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

AEM La CDN gestionada por el cliente satisfará la mayoría de los requisitos de rendimiento y seguridad. Para el nivel de publicación, los clientes pueden señalarlo opcionalmente desde su propia CDN, que deberán administrar. Esto se permitirá caso por caso, en función de cumplir con ciertos requisitos previos, incluidos, entre otros, que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

Consulte también los siguientes vídeos [AEM Cloud 5 CDN, parte 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) y [AEM Cloud 5 CDN, parte 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) AEM para obtener más información sobre CDN en as a Cloud Service.

## AEM CDN administrado por la  {#aem-managed-cdn}

AEM Siga las secciones a continuación para utilizar la interfaz de usuario de autoservicio de Cloud Manager para prepararse para la entrega de contenido mediante el uso de CDN de forma predeterminada:

1. [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Administrar los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

>[!NOTE]
>
>Los dominios personalizados se admiten en Cloud Manager **solo** si utiliza CDN administrada por AEM. Si trae su propia CDN y [la dirige a la CDN administrada por AEM](#point-to-point-CDN) tendrá que usar esa CDN específica para administrar dominios, no Cloud Manager.

**Restricción del tráfico**

AEM De forma predeterminada, para una configuración de CDN administrada de forma, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo mediante un rango de direcciones IP), puede hacerlo de forma autoservicio a través de la interfaz de usuario de Cloud Manager.

Consulte [Administrar listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para obtener más información.

>[!CAUTION]
>
>AEM CDN administrada solo atiende las solicitudes de las IP permitidas por CDN administrada por la administración de la. AEM Si dirige su propia CDN a la CDN administrada por el CDN, asegúrese de que las IP de su CDN se incluyan en la lista de permitidos.

## AEM Los puntos de CDN del cliente a CDN administrada de {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="AEM Los puntos de CDN del cliente a CDN administrada de"
>abstract="AEM Como Cloud Service, ofrece a los clientes una opción para utilizar su CDN existente. Para el nivel de publicación, los clientes pueden señalarlo opcionalmente desde su propia CDN, que deberán administrar. Esto se permitirá caso por caso, en función de cumplir con ciertos requisitos previos, incluidos, entre otros, que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar."

AEM Si un cliente debe utilizar su CDN existente, puede administrarla y dirigirla a la CDN administrada de la forma más segura, siempre que cumpla los siguientes requisitos:

* El cliente debe tener una CDN existente que sería oneroso reemplazar.
* El cliente debe administrarlo.
* AEM El cliente debe poder configurar la red de distribución de contenido (CDN) para que funcione con el as a Cloud Service de la; consulte las instrucciones de configuración que se presentan a continuación.
* El cliente debe tener expertos en CDN de ingeniería que estén disponibles en caso de que surjan problemas relacionados.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Dirija su CDN a la entrada de la CDN de Adobe como su dominio de origen. Por ejemplo, `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. SNI también debe configurarse como la entrada de la CDN de Adobe.
1. Configure el encabezado Host en el dominio de origen. Por ejemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Configure las variables `X-Forwarded-Host` AEM encabezado con el nombre de dominio para que pueda determinar el encabezado del host. Por ejemplo: `X-Forwarded-Host:example.com`.
1. Configurar `X-AEM-Edge-Key`. El valor debe proceder del Adobe.

   * Esto es necesario para que la CDN de Adobe pueda validar el origen de las solicitudes y pasar el `X-Forwarded-*` AEM encabezados a la aplicación de la. Por ejemplo,`X-Forwarded-For` se utiliza para determinar la IP del cliente. Por lo tanto, es responsabilidad del llamador de confianza (es decir, la CDN administrada por el cliente) garantizar la corrección de la llamada `X-Forwarded-*` encabezados (consulte la nota siguiente).
   * De forma opcional, el acceso a la entrada de CDN de Adobe se puede bloquear cuando se `X-AEM-Edge-Key` no está presente. Informe al Adobe si necesita acceso directo a la entrada de CDN de Adobe (para bloquear).

Consulte la [Configuraciones de proveedor de CDN de muestra](#sample-configurations) para ver ejemplos de configuración de los principales proveedores de CDN.

Antes de aceptar tráfico en directo, debe validar con la asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

Después de obtener la `X-AEM-Edge-Key`, puede probar que la solicitud se enruta correctamente de la siguiente manera.

En Linux:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

En Windows:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com --header "X-Forwarded-Host: example.com" --header "X-AEM-Edge-Key: <PROVIDED_EDGE_KEY>"
```

>[!NOTE]
>
>Al utilizar su propia CDN, no es necesario instalar dominios y certificados en Cloud Manager. El enrutamiento en la CDN de Adobe se realizará utilizando el dominio predeterminado `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com` que debe enviarse en la solicitud `Host` encabezado. Sobrescritura de la solicitud `Host` un encabezado con un nombre de dominio personalizado puede hacer que la solicitud sea enrutada incorrectamente por la CDN de Adobe.


>[!NOTE]
>
>AEM Los clientes que administran su propia CDN deben garantizar la integridad de los encabezados que se envían a través de CDN de la. Por ejemplo, se recomienda que los clientes borren todo `X-Forwarded-*` y configúrelos en valores conocidos y controlados. Por ejemplo, `X-Forwarded-For` debe contener la dirección IP del cliente, mientras que `X-Forwarded-Host` debe contener el host del sitio.

>[!NOTE]
>
>Los entornos de programa de zona protegida no admiten una CDN proporcionada por el cliente.

AEM El salto adicional entre la CDN del cliente y la CDN de la solo es necesario en caso de que se pierda una caché. Al utilizar las estrategias de optimización de caché descritas en este artículo, la adición de una CDN de cliente solo debe introducir una latencia insignificante.

Tenga en cuenta que esta configuración de CDN del cliente es compatible con el nivel de publicación, pero no delante del de creación.

### Configuraciones de proveedor de CDN de muestra {#sample-configurations}

A continuación se presentan varios ejemplos de configuración de varios proveedores de CDN líderes.

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

AEM La CDN gestionada por el administrador agrega encabezados a cada solicitud con:

* código de país: `x-aem-client-country`
* código de continente: `x-aem-client-continent`

>[!NOTE]
>
>En el caso de la CDN administrada por el cliente, estas cabeceras reflejarán la ubicación del servidor proxy de CDN de los clientes, en lugar del cliente real.  Por lo tanto, para la CDN administrada por el cliente, la CDN de los clientes debe administrar los encabezados de geolocalización.

Los valores de los códigos de país son los códigos alfa-2 descritos [aquí](https://en.wikipedia.org/wiki/ISO_3166-1).

Los valores de los códigos de continente son:

* AF África
* UNA Antártida
* AS Asia
* UE Europa
* NA América del Norte
* OC Oceanía
* SA América del Sur

Esta información puede resultar útil para casos de uso, como redirigir a una dirección URL diferente en función del origen (país) de la solicitud. Utilice el encabezado Vary para almacenar en caché las respuestas que dependen de la información geográfica. Por ejemplo, las redirecciones a una página de aterrizaje de un país específico siempre deben contener `Vary: x-aem-client-country`. Si es necesario, puede utilizar `Cache-Control: private` para evitar el almacenamiento en caché. Consulte también [Almacenamiento en caché](/help/implementing/dispatcher/caching.md#html-text).
