---
title: CDN en AEM as a Cloud Service
description: CDN en AEM as a Cloud Service
translation-type: tm+mt
source-git-commit: 14d08529eeee0f9881e668eed6273cfa57f1360f
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 4%

---


# CDN en AEM as a Cloud Service {#cdn}

AEM como Cloud Service se envía con una CDN integrada. Su principal propósito es reducir la latencia mediante la entrega de contenido procesable desde los nodos CDN en el borde, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

La CDN administrada por AEM satisfará la mayoría de los requisitos de rendimiento y seguridad del cliente. Para el nivel de publicación, los clientes pueden opcionalmente señalarlo desde su propia CDN, que deberán administrar. Esto se permitirá caso por caso, en función de cumplir ciertos requisitos previos, incluido, entre otros, el cliente que tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

## CDN administrado por AEM  {#aem-managed-cdn}

Siga estos pasos para prepararse para el envío de contenido mediante la CDN predeterminada del Adobe:

1. Proporcione el certificado SSL firmado y la clave secreta para Adobe compartiendo un vínculo a un formulario seguro que contenga esta información. Coordine con la asistencia al cliente esta tarea. Adobe admite hasta 10 certificados SSL para un programa.
   **Nota:** Aem como Cloud Service no admite certificados de dominio validados (DV). Además, debe ser un certificado X.509 TLS de una entidad de certificación de confianza (CA) con una clave privada RSA de 2048 bits que coincida.
1. Informar a la asistencia al cliente:
   * qué dominios personalizados deben asociarse con un determinado entorno, tal como se define en la identificación del programa y la identificación del entorno. Se admiten hasta 100 dominios para un entorno determinado y los dominios no pueden contener comodines. Tenga en cuenta que los dominios personalizados del lado del autor no son compatibles.
   * si se necesita alguna inclusión en la lista de permitidos IP para restringir el tráfico a un entorno determinado.
1. Coordine con el servicio de atención al cliente la temporización de los cambios necesarios en los registros DNS. Las instrucciones son diferentes en función de si se necesita un registro de apex:
   * si no se necesita un registro apex, los clientes deben establecer el registro DNS CNAME para que apunte a su FQDN `cdn.adobeaemcloud.com`.
   * si se necesita un registro apex, cree un registro A que apunte a las siguientes IP: 151.101.3.10, 151.101.67.10, 151.101.131.10, 151.101.195.10. Los clientes necesitan un registro apex si el FQDN deseado coincide con la zona DNS. Esto se puede probar usando el comando Unix dig para ver si el valor SOA de la salida coincide con el dominio. Por ejemplo, el comando `dig anything.dev.adobeaemcloud.com` devuelve un SOA (Inicio de Autoridad, es decir, la zona) de `dev.adobeaemcloud.com` modo que no es un registro APEX, mientras que `dig dev.adobeaemcloud.com` devuelve un SOA de `dev.adobeaemcloud.com` modo que es un registro apex.
1. Se le notificará cuando los certificados SSL caduquen para que pueda volver a enviar los nuevos certificados SSL.

**Restricción del tráfico**

De forma predeterminada, para una configuración de CDN administrada por Adobe, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP), debe trabajar con la asistencia al cliente para configurar estas restricciones.

## CDN de cliente señala a AEM CDN administrada {#point-to-point-CDN}

Si un cliente debe utilizar su CDN existente, puede administrarlo y señalarlo a la CDN administrada por el Adobe, siempre que se satisfagan los siguientes requisitos:

* El cliente debe tener una CDN existente que sea onerosa de reemplazar.
* El cliente debe administrarlo.
* El cliente debe ser capaz de configurar el CDN para que funcione con AEM como Cloud Service; consulte las instrucciones de configuración a continuación.
* El cliente debe contar con expertos en ingeniería de CDN que estén disponibles en caso de que surjan problemas relacionados.
* El cliente debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Configure el `X-Forwarded-Host` encabezado con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es la entrada de CDN de Adobe. El valor debe proceder del Adobe.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado sni debe ser el dominio de origen.
1. Establezca el `X-Edge-Key`, que es necesario para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder del Adobe.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.

Existe potencialmente una pequeña visita de rendimiento debido al salto adicional, aunque es probable que los saltos de la CDN del cliente a la CDN administrada por el Adobe sean eficientes.

Tenga en cuenta que esta configuración de CDN de cliente es compatible con el nivel de publicación, pero no con el nivel de autor.
