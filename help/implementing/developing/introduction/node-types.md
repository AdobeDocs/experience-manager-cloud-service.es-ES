---
title: Tipos de nodos AEM
description: AEM AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodo ofrecidos por ambos, pero también proporciona un rango de tipos de nodo propios.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 6%

---

# Tipos de nodos AEM {#aem-node-types}

AEM AEM Debido a que se basa en Sling y utiliza un repositorio JCR, los tipos de nodo ofrecidos por ambos estándares están disponibles para su uso en los siguientes:

* [Tipos de nodos JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de nodos de Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Además de estos. AEM proporciona una amplia gama de tipos de nodos personalizados. Para la lista más actual con todas las propiedades asociadas, [usar CRXDE](/help/implementing/developing/tools/crxde.md) AEM para examinar la siguiente ruta en el repositorio de la:

`/jcr:system/jcr:nodeTypes`
