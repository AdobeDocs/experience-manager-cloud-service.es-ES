---
title: Resumen del flujo de distribución de contenido
description: Resumen del flujo de distribución de contenido
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Flujo de distribución de contenido {#content-delivery}

La página actual detalla la entrega del contenido del servicio de publicación en AEM as a Cloud Service. La entrega de contenido del servicio de publicación incluye:

* CDN
* AEM dispatcher
* AEM publicar

El flujo de datos es el siguiente:

1. La dirección URL se agrega en el explorador
1. Solicitud realizada a CDN asignada en DNS a ese dominio
1. Si el contenido se almacena completamente en caché en CDN, CDN lo suministra al explorador
1. Si el contenido no se almacena en caché completamente, la CDN llama (proxy inverso) al despachante
1. Si el contenido se almacena completamente en caché en Dispatcher, Dispatcher lo sirve a la CDN
1. Si el contenido no se almacena en caché completamente, Dispatcher llama (proxy inverso) a la publicación AEM
1. El navegador procesa el contenido, que también puede almacenarlo en la caché, según los encabezados

De forma predeterminada, el tipo de contenido HTML/texto está configurado para caducar después de 300 segundos (5 minutos) en la capa de Dispatcher, un umbral que respetan tanto la caché de Dispatcher como la CDN. Durante las redistribuciones del servicio de publicación, la caché de Dispatcher se borra y, posteriormente, se caliente antes de que los nuevos nodos de publicación acepten el tráfico.

Las secciones siguientes proporcionan buenos detalles sobre la entrega de contenido, incluida la configuración de CDN y el almacenamiento en caché.

Está disponible información sobre la replicación del servicio de autor al servicio de publicación [here](/help/operations/replication.md).
