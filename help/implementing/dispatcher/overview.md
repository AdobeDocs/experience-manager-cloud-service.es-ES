---
title: Información general del flujo de Envío de contenido
description: Información general del flujo de Envío de contenido
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---


# Flujo de distribución de contenido {#content-delivery}

Los detalles de la página actual publican el envío de contenido del servicio en AEM como Cloud Service. El envío de contenido del servicio de publicación incluye:

* CDN
* AEM despachante
* AEM publicación

El flujo de datos es el siguiente:

1. La dirección URL se agrega al explorador
1. Solicitud realizada a CDN asignada en DNS a ese dominio
1. Si el contenido se almacena completamente en caché en CDN, CDN lo proporciona al explorador
1. Si el contenido no se almacena completamente en caché, la CDN llama (proxy inverso) al distribuidor
1. Si el contenido se almacena completamente en la caché del despachante, el despachante lo proporciona a la CDN
1. Si el contenido no se almacena completamente en caché, el despachante llama (proxy inverso) a la publicación AEM
1. El navegador procesa el contenido, que también puede almacenarlo en caché, según los encabezados

De forma predeterminada, el tipo de contenido HTML/texto está configurado para caducar después de 300 segundos (5 minutos) en la capa del despachante, un umbral que respetan tanto la caché del despachante como la CDN. Durante las redistribuciones del servicio de publicación, la caché del despachante se borra y se calienta posteriormente antes de que los nuevos nodos de publicación acepten el tráfico.

Las secciones a continuación proporcionan buenos detalles sobre el envío de contenido, incluida la configuración de CDN y el almacenamiento en caché.

La información sobre la replicación del servicio de creación al servicio de publicación está disponible [aquí](/help/operations/replication.md).
