---
title: CDN en AEM como servicio de nube
description: CDN en AEM como servicio de nube
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---


# CDN en AEM como servicio de nube {#cdn}

AEM as Cloud Service se suministra con una CDN integrada. Su principal propósito es reducir la latencia mediante la entrega de contenido procesable desde los nodos CDN en el borde, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM.

En total, AEM oferta dos opciones:

1. CDN gestionado por AEM: CDN incorporado de AEM. Se trata de una opción estrechamente integrada que no requiere una gran inversión de los clientes en el soporte de la integración de CDN con AEM.
1. CDN gestionado por el cliente apunta a CDN gestionado por AEM: el cliente señala su propia CDN a la CDN integrada de AEM. El cliente aún tendrá que administrar su propia CDN, pero la inversión en la integración con AEM es moderada.

La primera opción debe satisfacer la mayoría de los requisitos de seguridad y rendimiento del cliente. Además, requiere un esfuerzo mínimo del cliente.

La segunda opción se permitirá caso por caso. La decisión se basa en cumplir ciertos requisitos previos, como el hecho de que el cliente tenga una integración heredada con su proveedor de CDN que sea difícil de abandonar.

A continuación se presenta una matriz de decisiones para comparar las dos opciones. Encontrará información más detallada en las secciones siguientes.

| Detalles | CDN gestionado por AEM | CDN gestionado por el cliente señala a CDN de AEM |
|---|---|---|
| **Esfuerzo del cliente** | Ninguno, está completamente integrado. Solo es necesario que señale CNAME a la CDN gestionada por AEM. | Moderar la inversión de los clientes. El cliente debe administrar su propia CDN. |
| **Requisitos previos** | Ninguna | CDN existente que resulta oneroso de reemplazar. Debe mostrar una prueba de carga correcta antes de activarse. |
| **Experiencia de CDN** | Ninguna | Requiere al menos un recurso de ingeniería a tiempo parcial con conocimientos detallados de CDN que puedan configurar la CDN del cliente. |
| **Seguridad** | Administrado por Adobe. | Administrado por Adobe (y opcionalmente por el cliente en su propia CDN). |
| **Actuación** | Optimizado por Adobe. | Se beneficiará de algunas funciones de CDN de AEM, pero posiblemente de un pequeño rendimiento debido al salto adicional. **Nota**: Evita que la CDN del cliente pase a la CDN de Adobe lista para usar (probablemente sea eficaz). |
| **Almacenamiento en caché** | Admite encabezados de caché aplicados al despachante. | Admite encabezados de caché aplicados al despachante. |
| **Funciones de compresión de imágenes y vídeo** | Puede trabajar con Adobe Dynamic Media. | Puede trabajar con Adobe Dynamic Media o con una solución de vídeo/imagen CDN administrada por el cliente. |

## CDN gestionado por AEM  {#aem-managed-cdn}

La preparación para el envío de contenido mediante la CDN integrada de Adobe es sencilla, tal como se describe a continuación:

1. Proporcionará el certificado SSL firmado y la clave secreta a Adobe compartiendo un vínculo a un formulario seguro que contenga esta información. Coordine con la asistencia al cliente esta tarea.
   **Nota:** Aem como servicio de nube no admite certificados de dominio validados (DV).
1. Debe informar a la asistencia al cliente:
   * qué dominio personalizado debe asociarse con un determinado entorno, tal como se define en la identificación del programa y en la identificación del entorno.
   * si se necesita una lista blanca de IP para restringir el tráfico a un entorno determinado.
1. El servicio de asistencia al cliente coordinará con usted la temporización de un registro DNS CNAME, señalando a su FQDN `cdn.adobeaemcloud.com`.
1. Se le notificará cuando los certificados SSL caduquen para que pueda volver a enviar los nuevos certificados SSL.

**Restricción del tráfico**

De forma predeterminada, para una configuración de CDN administrada de Adobe, todo el tráfico público puede llegar al servicio de publicación, tanto para entornos de producción como de no producción (desarrollo y fase). Si desea limitar el tráfico al servicio de publicación para un entorno determinado (por ejemplo, limitar el ensayo por un rango de direcciones IP), debe trabajar con la asistencia al cliente para configurar estas restricciones.

## CDN de cliente apunta a CDN gestionado por AEM {#point-to-point-CDN}

Compatible si desea utilizar la CDN existente, pero no puede satisfacer los requisitos de una CDN administrada por el cliente. En este caso, usted administra su propia CDN, pero señala a la CDN administrada de Adobe.

Tenga en cuenta que:

1. Debe tener una CDN existente.
1. Debes administrarlo.
1. Debe ser capaz de configurar la CDN para que funcione con Aem como un servicio de nube; consulte las instrucciones de configuración a continuación.
1. Debe contar con expertos en ingeniería de CDN que estén disponibles en caso de que surjan problemas relacionados.
1. Debe realizar y superar correctamente una prueba de carga antes de ir a producción.

Instrucciones de configuración:

1. Configure el `X-Forwarded-Host` encabezado con el nombre de dominio.
1. Establezca el encabezado Host con el dominio de origen, que es la entrada de CDN de Adobe. El valor debe proceder de Adobe.
1. Envíe el encabezado SNI al origen. Al igual que el encabezado Host, el encabezado sni debe ser el dominio de origen.
1. Establezca el `X-Edge-Key`, que es necesario para enrutar el tráfico correctamente a los servidores AEM. El valor debe proceder de Adobe.

Antes de aceptar el tráfico activo, debe validar con el servicio de asistencia al cliente de Adobe que el enrutamiento de tráfico de extremo a extremo funciona correctamente.
