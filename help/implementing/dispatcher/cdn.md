---
title: CDN en AEM as a Cloud Service
description: AEM AEM Aprenda a utilizar la CDN administrada por el y a apuntar su propia CDN a la CDN administrada por el administrador de la red de distribución de contenido (CDN) administrada por el administrador de la.
feature: Dispatcher
exl-id: a3f66d99-1b9a-4f74-90e5-2cad50dc345a
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 23%

---

# CDN en AEM as a Cloud Service {#cdn}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_cdn"
>title="CDN en AEM as a Cloud Service"
>abstract="AEM as a Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM."

AEM as a Cloud Service se envía con una CDN integrada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

AEM La CDN administrada por el cliente satisface la mayoría de los requisitos de rendimiento y seguridad. Para el nivel de publicación, los clientes pueden apuntar opcionalmente a él desde su propia CDN, que deben administrar. Este escenario se permite caso por caso, en función del cumplimiento de ciertos requisitos previos que incluyen, entre otros, que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

<!-- ERROR: NEITHER URL IS FOUND (HTTP ERROR 404) Also, see the following videos [Cloud 5 AEM CDN Part 1](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part1.html) and [Cloud 5 AEM CDN Part 2](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-cdn-part2.html) for additional information about CDN in AEM as a Cloud Service. -->

## AEM CDN administrado por el usuario  {#aem-managed-cdn}

Siga las secciones a continuación para utilizar la interfaz de usuario de autoservicio de Cloud Manager AEM con el fin de prepararse para la entrega de contenido mediante el uso de CDN de forma predeterminada para el uso de la red de distribución de contenido (CDN) que se utiliza de forma predeterminada:

1. [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [Administrar los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**Restricción de tráfico**

AEM De forma predeterminada, para una configuración de CDN administrada por el, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Puede limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitando el ensayo por un rango de direcciones IP) mediante la interfaz de usuario de Cloud Manager.

Consulte [administración de listas de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) para obtener más información.

>[!CAUTION]
>
>AEM Solo se atienden las solicitudes de las IP permitidas mediante CDN administradas administradas por la administración de la red de distribución de contenido (CDN) de la. AEM Si dirige su propia CDN a la CDN administrada por la CDN, asegúrese de que las IP de su CDN estén incluidas en la lista de permitidos.

### Configuración del tráfico en la CDN {#cdn-configuring-cloud}

Las reglas para configurar el tráfico y los filtros de CDN se pueden declarar en un archivo de configuración e implementarse en CDN mediante la [canalización de configuración de Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Para obtener más información, consulte [Configuración del tráfico en la red de distribución de contenido (CDN)](/help/implementing/dispatcher/cdn-configuring-traffic.md) y [Reglas de filtro de tráfico, incluidas las reglas WAF](/help/security/traffic-filter-rules-including-waf.md).

### Configuración de páginas de error de CDN {#cdn-error-pages}

AEM Se puede configurar una página de error de CDN para anular la página predeterminada sin marca que se proporciona al explorador en el improbable evento de que no se pueda acceder a la página de error de CDNo. Para obtener más información, consulte [Configuración de páginas de error de CDN](/help/implementing/dispatcher/cdn-error-pages.md).

## La CDN del cliente apunta a la CDN administrada por AEM {#point-to-point-CDN}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_byocdn"
>title="La CDN del cliente apunta a una CDN administrada de AEM"
>abstract="AEM as a Cloud Service ofrece una opción para que los clientes utilicen su CDN existente. Para el nivel de publicación, los clientes pueden apuntar opcionalmente a él desde su propia CDN, que deben administrar. Este escenario se permite caso por caso, en función del cumplimiento de ciertos requisitos previos que incluyen, entre otros, que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar."

AEM Si un cliente debe utilizar su CDN existente, puede administrarla y dirigirla a la CDN administrada por el cliente, siempre que se cumplan las condiciones siguientes:

* El cliente debe tener una CDN existente que sería oneroso reemplazar.
* El cliente debe administrarlo.
* El cliente debe poder configurar la CDN para que funcione con AEM as a Cloud Service; consulte las instrucciones de configuración que se presentan a continuación.
* El cliente debe tener expertos en CDN de ingeniería que estén disponibles en caso de que surjan problemas relacionados.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Dirija su CDN a la entrada de la CDN de Adobe como su dominio de origen. Por ejemplo, `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. Configure SNI para la entrada de CDN de Adobe.
1. Configure el encabezado Host en el dominio de origen. Por ejemplo: `Host:publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`.
1. AEM Establezca el encabezado `X-Forwarded-Host` con el nombre de dominio para que pueda determinar el encabezado de host. Por ejemplo: `X-Forwarded-Host:example.com`.
1. Establezca `X-AEM-Edge-Key`. El valor debe proceder del Adobe.

   * Necesario para que la CDN de Adobe AEM pueda validar el origen de las solicitudes y pasar los encabezados `X-Forwarded-*` a la aplicación de. Por ejemplo, `X-Forwarded-For` se usa para determinar la dirección IP del cliente. Por lo tanto, es responsabilidad del llamador de confianza (es decir, la CDN administrada por el cliente) garantizar la corrección de los encabezados `X-Forwarded-*` (consulte la nota a continuación).
   * Opcionalmente, el acceso a la entrada de CDN de Adobe se puede bloquear cuando `X-AEM-Edge-Key` no está presente. Informe al Adobe de si necesita acceso directo a la entrada de CDN de Adobe (que se debe bloquear).

Consulte la sección [Configuraciones de proveedor de CDN de muestra](#sample-configurations) para ver ejemplos de configuración de los principales proveedores de CDN.

Antes de aceptar tráfico en directo, debe validar con la asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

Después de obtener `X-AEM-Edge-Key`, puede probar que la solicitud se enruta correctamente de la siguiente manera.

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
>Al utilizar su propia CDN, no es necesario instalar dominios y certificados en Cloud Manager. El enrutamiento en la CDN de Adobe se realiza utilizando el dominio predeterminado `publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com`, que debe enviarse en el encabezado de la solicitud `Host`. Si se sobrescribe el encabezado de la solicitud `Host` con un nombre de dominio personalizado, la CDN de Adobe puede enrutar la solicitud incorrectamente.


>[!NOTE]
>
>AEM Los clientes que administran su propia CDN deben garantizar la integridad de los encabezados que se envían a través de la CDN de la red de distribución de contenido (CDN) de la. Por ejemplo, se recomienda que los clientes borren todos los encabezados `X-Forwarded-*` y los establezcan en valores conocidos y controlados. Por ejemplo, `X-Forwarded-For` debe contener la dirección IP del cliente, mientras que `X-Forwarded-Host` debe contener el host del sitio.

>[!NOTE]
>
>Los entornos de programa de zona protegida no admiten una CDN proporcionada por el cliente.

AEM El salto adicional entre la CDN del cliente y la CDN del cliente solo es necesario si se produce una pérdida de caché. Al utilizar las estrategias de optimización de caché descritas en este artículo, la adición de una CDN de cliente solo debe introducir una latencia insignificante.

Esta configuración de CDN del cliente es compatible con el nivel de publicación, pero no delante del de creación.

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

AEM La CDN gestionada por el grupo de usuarios agrega encabezados a cada solicitud con lo siguiente:

* código de país: `x-aem-client-country`
* código de continente: `x-aem-client-continent`

>[!NOTE]
>
>Si hay una CDN administrada por el cliente, estas cabeceras reflejan la ubicación del servidor proxy CDN de los clientes en lugar del cliente real. Por lo tanto, para la CDN administrada por el cliente, la CDN de los clientes debe administrar los encabezados de geolocalización.

Los valores de los códigos de país son los códigos Alpha-2 que se describen [aquí](https://en.wikipedia.org/wiki/ISO_3166-1).

Los valores de los códigos de continente son:

* AF África
* UNA Antártida
* AS Asia
* UE Europa
* NA América del Norte
* OC Oceanía
* SA América del Sur

Esta información puede resultar útil para casos de uso, como redirigir a una dirección URL diferente en función del origen (país) de la solicitud. Utilice el encabezado Vary para almacenar en caché las respuestas que dependen de la información geográfica. Por ejemplo, las redirecciones a una página de aterrizaje de un país específico siempre deben contener `Vary: x-aem-client-country`. Si es necesario, puede usar `Cache-Control: private` para evitar el almacenamiento en caché. Consulte también [Almacenamiento en caché](/help/implementing/dispatcher/caching.md#html-text).
