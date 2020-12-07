---
title: Directrices de API de Java
description: AEM está basado en una rica pila de software de código abierto que expone muchas API de Java para su uso.
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Directrices de API de Java {#java-api-guidelines}

Adobe Experience Manager (AEM) está basado en una rica pila de software de código abierto que expone muchas API de Java para su uso durante el desarrollo.

AEM se basa en los cuatro siguientes conjuntos principales de API de Java en orden descendente de preferencia.

1. **Adobe Experience Manager (AEM)** : abstracciones de productos como páginas, recursos, flujos de trabajo, etc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)** : REST y abstracciones basadas en recursos como recursos, mapas de valores y solicitudes HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)** : abstracciones de datos y contenido como nodos, propiedades y sesiones.
1. **[OSGi (Apache Felix)](https://felix.apache.org)** - abstracciones de contenedor de aplicaciones OSGi como servicios y componentes (OSGi).

Si AEM proporciona una API, preferirla a Sling, JCR y OSGi. Si AEM no proporciona una API, prefiera Sling en lugar de JCR y OSGi.

Para obtener más información sobre estas directrices, consulte el documento [Comprender las optimizaciones de la API de Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
