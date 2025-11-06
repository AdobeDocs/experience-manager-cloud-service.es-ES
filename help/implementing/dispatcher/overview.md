---
title: Información general sobre el flujo de distribución de contenido
description: Obtenga más información sobre el flujo de datos de entrega de contenido y cómo publicar el contenido
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 87%

---

# Flujo de distribución de contenido {#content-delivery}

La página actual detalla la distribución del contenido del servicio de publicación en AEM as a Cloud Service. La distribución de contenido del servicio de publicación incluye lo siguiente:

* La red de distribución de contenido (CDN)
* Dispatcher de AEM
* Editor de AEM

El flujo de datos es el siguiente:

1. La dirección URL se agrega al explorador
1. Se realiza la solicitud a la CDN asignada en DNS a ese dominio
1. Si el contenido se almacena completamente en caché en CDN, CDN lo suministra al explorador
1. Si el contenido no se almacena en la caché completamente, la CDN llama (proxy inverso) al Dispatcher
1. Si el contenido se almacena completamente en la caché en Dispatcher, Dispatcher lo sirve a la red de distribución de contenido (CDN)
1. Si el contenido no se almacena en la caché completamente, Dispatcher llama (proxy inverso) a la publicación de AEM
1. El explorador procesa el contenido, que también puede almacenarlo en la caché, según los encabezados

De forma predeterminada, el tipo de contenido HTML/texto está configurado para caducar después de 300 segundos (5 minutos) en la capa del Dispatcher, un umbral que respeta tanto la caché del Dispatcher como la CDN. Durante las reimplementaciones del servicio de publicación, la caché de Dispatcher se borra y, posteriormente, se calienta antes de que los nuevos nodos de publicación acepten el tráfico.

Las siguientes secciones proporcionan detalles sobre la distribución de contenido:

* [Configuración de la CDN](/help/implementing/dispatcher/cdn.md)
* [Almacenamiento en caché](/help/implementing/dispatcher/caching.md)

Para obtener información acerca de la replicación del servicio de autor al servicio de publicación, vea [Replicación](/help/operations/replication.md).
