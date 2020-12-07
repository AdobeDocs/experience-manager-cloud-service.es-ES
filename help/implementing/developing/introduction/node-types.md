---
title: Tipos de nodos AEM
description: AEM se basa en Sling y utiliza un repositorio JCR con tipos de nodos ofrecidos por ambos, pero AEM también proporciona una serie de tipos de nodos propios.
translation-type: tm+mt
source-git-commit: 020cebfa714c098f032df963b7105503c741e748
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Tipos de nodos AEM {#aem-node-types}

Debido a que AEM se basa en Sling y utiliza un repositorio JCR, los tipos de nodos ofrecidos por ambos estándares están disponibles para su uso en AEM:

* [Tipos de nodos JCR](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Tipos de nodos Sling](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

Además de esto. AEM proporciona una serie de tipos de nodos personalizados. Para la lista más reciente con todas las propiedades asociadas, [utilice CRXDE](/help/implementing/developing/tools/crxde.md) para explorar la siguiente ruta en el repositorio de AEM:

`/jcr:system/jcr:nodeTypes`
