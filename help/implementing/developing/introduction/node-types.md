---
title: Tipos de nodos AEM
description: AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodos ofrecidos por ambos, pero AEM también proporciona una gama de sus propios tipos de nodos.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
source-git-commit: 08559417c8047c592f2db54321afe68836b75bd1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 5%

---

# Tipos de nodos AEM {#aem-node-types}

Debido a que AEM se basa en Sling y utiliza un repositorio JCR, los tipos de nodos ofrecidos por ambos estándares están disponibles para su uso en AEM:

* [Tipos de nodos JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de nodos Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Además de estos. AEM proporciona una amplia gama de tipos de nodos personalizados. Para la lista más actual con todas las propiedades asociadas, [usar CRXDE](/help/implementing/developing/tools/crxde.md) para examinar la siguiente ruta en el repositorio de AEM:

`/jcr:system/jcr:nodeTypes`
