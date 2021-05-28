---
title: Directrices de API de Java
description: AEM está basado en una pila de software de código abierto que expone muchas API de Java para su uso.
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Directrices de API de Java {#java-api-guidelines}

Adobe Experience Manager (AEM) se basa en una rica pila de software de código abierto que expone muchas API de Java para su uso durante el desarrollo.

AEM se basa en los cuatro conjuntos principales de API de Java siguientes en orden descendente de preferencia.

1. **[Adobe Experience Manager (AEM)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/index.html)** : abstracciones de productos como páginas, recursos, flujos de trabajo, etc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)** : REST y abstracciones basadas en recursos como recursos, mapas de valores y solicitudes HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** : abstracciones de datos y contenido, como nodos, propiedades y sesiones.
1. **[OSGi (Apache Felix)](https://felix.apache.org)** : abstracciones de contenedor de aplicaciones OSGi como servicios y componentes (OSGi).

Si AEM proporciona una API, preferirla a Sling, JCR y OSGi. Si AEM no proporciona una API, entonces prefiera Sling antes que JCR y OSGi.

Para obtener más información sobre estas directrices, consulte el documento [Comprender las prácticas recomendadas de la API de Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
