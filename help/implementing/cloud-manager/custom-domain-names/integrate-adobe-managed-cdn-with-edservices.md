---
title: Integración de Edge Delivery Services con CDN administrada por Adobe en Cloud Manager
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# Integración de Edge Delivery Services con CDN administrada por Adobe en Cloud Manager {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe Managed CDN (AMC-D) se integra de forma nativa con Edge Delivery Services para ofrecerle experiencias de gran rendimiento y distribución global para Adobe Experience Manager (AEM) Sites.

Juntos, le ofrecen los siguientes beneficios:

* Una CDN lista para usar y de nivel empresarial administrada por Adobe.
* Una capa de entrega de Edge moderna que acelera las solicitudes, optimiza el almacenamiento en caché y protege contra ataques comunes.
* Flujo de trabajo unificado de Cloud Manager para la administración de dominios, los certificados SSL y las implementaciones impulsadas por canalización.

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Opciones de implementación de Edge Delivery Services en CDN administrada por Adobe en Cloud Manager {#deployment-options}

En este tema se explican las dos formas de implementar Edge Delivery Services en CDN administrada por Adobe en Cloud Manager y, lo que es igualmente importante, se le ayuda a decidir qué opción es la mejor para su caso de uso.

Edge Delivery Services se puede configurar mediante una de las dos opciones siguientes. Cada una tiene diferentes capacidades.

|  | Opción de implementación | Documento de clave | Capacidad | Ideal para |
| --- | --- | --- | --- | --- |
| Opción 1 | *Con* un entorno de AEM as a Cloud Service (AEMaaCS) existente | [Configurar un proxy desde un entorno existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | La canalización de configuración suele estar disponible para entornos AEMaaCS | Equipos que ya ejecutan Sites en Cloud Manager y desean un aumento rápido y de bajo riesgo del rendimiento. |
| Opción 2 | *Sin* un entorno AEMaaCS existente; conocido como &quot;entorno Edge&quot; independiente. | [Configurar un sitio de Edge Delivery sin un entorno existente](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | Actualmente, la canalización de configuración solo está disponible para entornos de Edge a través del programa limitado de Beta.<br>Consulte [Agregar canalización de configuración de Edge Delivery](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline). | Nuevas compilaciones o migraciones que deseen adoptar la arquitectura de Edge Delivery completa y el enrutamiento granular. |

<!-- Ultimately this URL above will need to be updated on GA -->

| Opción | Resumen | Ideal para | Documentos clave |
| --- | --- | --- | --- |
| Proxy CDN administrado por Adobe | Frentes de CDN administrados por Adobe y un entorno de AEM Sites existente. Su canalización actual de Sites sigue siendo el &quot;origen&quot;, mientras que AMC-D gestiona el almacenamiento en caché de Edge y la finalización de TLS. | Equipos que ya ejecutan Sites en Cloud Manager y desean un aumento rápido y de bajo riesgo del rendimiento. | Configuración de un proxy AMC-D |
| Configuración de la canalización con originSelectors | Una canalización de configuración de Edge Delivery dedicada publica contenido estático y dinámico directamente en Edge. `originSelectors` enruta el tráfico entre AMC-D y sus niveles de autor/publicación de AEM. | Nuevas compilaciones o migraciones que deseen adoptar la arquitectura de Edge Delivery completa y el enrutamiento granular. | Configuración de la canalización de Edge Delivery |

>[!TIP]
>
>¿No está seguro de qué ruta escoger? Consulte [Elegir un modelo de implementación](#choose-deployment-model) a continuación para ver las directrices de decisión.

## Elija un modelo de implementación {#choose-deployment-model}

Ambos modelos pueden coexistir dentro del mismo programa de Cloud Manager, lo que permite migraciones por fases.

| Si tú... | Entonces use... |
| :--- | :--- |
| Necesita un despliegue rápido y con cambios mínimos, y ya aloja Sites en Cloud Manager | Proxy AMC-D |
| Planifique la reestructuración del contenido para Edge Delivery o desee un enrutamiento preciso entre varios orígenes | Configurar canalización de envío de Edge + `originSelectors` |

## Requisitos previos {#prerequisites}

1. Incorporar el sitio en Cloud Manager: necesario para ambos modelos de implementación. Seguir Incorporación a un sitio de AEM.

2. Traer su propio Git (BYOG) (opcional): si almacena el código del sitio fuera de Adobe Git, complete la incorporación de BYOG.

3. Licencia de Edge Delivery: Asegúrese de que su programa tenga licencia para Edge Delivery Services.


