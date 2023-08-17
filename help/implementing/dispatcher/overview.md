---
title: Información general sobre el flujo de distribución de contenido
description: Obtenga más información sobre el flujo de datos de entrega de contenido y cómo publicar el contenido
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: d1da8559da856e028a5dcad1d0c0b2c00176af0c
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 45%

---

# Flujo de distribución de contenido {#content-delivery}

La página actual detalla la distribución del contenido del servicio de publicación en AEM as a Cloud Service. La distribución de contenido del servicio de publicación incluye lo siguiente:

* La red de distribución de contenido (CDN)
* Dispatcher de AEM
* AEM editor de

El flujo de datos es el siguiente:

1. La dirección URL se agrega al explorador
1. Se realiza la solicitud a la CDN asignada en DNS a ese dominio
1. Si el contenido se almacena completamente en caché en CDN, CDN lo suministra al explorador
1. Si el contenido no está completamente en caché, la CDN llama (proxy inverso) a Dispatcher
1. Si el contenido se almacena completamente en caché en Dispatcher, Dispatcher se lo proporciona a la CDN
1. AEM Si el contenido no está completamente en caché, Dispatcher llama (proxy inverso) a la publicación para que se realice la publicación en el servidor de correo electrónico
1. El explorador procesa el contenido, que también puede almacenarlo en la caché, según los encabezados

De forma predeterminada, el HTML/texto del tipo de contenido está configurado para que caduque después de 300 segundos (5 minutos) en Dispatcher, un umbral que respetan tanto la caché de Dispatcher como la CDN. Durante las reimplementaciones del servicio de publicación, la caché de Dispatcher se borra y se calienta antes de que los nuevos nodos de publicación acepten el tráfico.

Las secciones siguientes proporcionan información más detallada sobre la entrega de contenido:
* [Configuración de la CDN](/help/implementing/dispatcher/cdn.md)
* [Almacenamiento en caché](/help/implementing/dispatcher/caching.md)


Está disponible información sobre la replicación del servicio de autor al servicio de publicación [aquí](/help/operations/replication.md).
