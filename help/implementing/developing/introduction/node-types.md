---
title: Tipos de nodos AEM
description: AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodo ofrecidos por ambos, pero AEM también proporciona un rango de sus propios tipos de nodo.
exl-id: 82cc28ca-37e2-4ca3-b3e4-cc03bbc5bdf5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 6%

---

# Tipos de nodos AEM {#aem-node-types}

Dado que AEM se basa en Sling y utiliza un repositorio JCR, los tipos de nodo ofrecidos por ambos estándares están disponibles para su uso en AEM:

* [Tipos de nodos JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de nodos de Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Además de estos. AEM proporciona una amplia gama de tipos de nodos personalizados. Para obtener la lista más actual con todas las propiedades asociadas, [use CRXDE](/help/implementing/developing/tools/crxde.md) para examinar la siguiente ruta en el repositorio de AEM:

`/jcr:system/jcr:nodeTypes`
