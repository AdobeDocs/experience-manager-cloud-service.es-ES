---
product: adobe experience manager
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.es-ES
index: y
type: Documentation
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://docs.adobe.com/content/help/en/experience-manager-cloud-service/landing/home.html
getting-started-title: Introducción
getting-started-url: https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/overview/home.html
tutorials-title: Tutoriales
tutorials-url: https://docs.adobe.com/content/help/es-ES/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: d311c87c1ae1cdfe9f50d41750aecbab960dc7ef
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 20%

---


# Metadatos para uso interno

Los metadatos en el sistema de creación de GitHub son jerárquicos y se definen con los siguientes niveles crecientes de precedentes.

1. metadata.md
1. ToC
1. Artículo

Los metadatos definidos en el archivo metadata.md se aplican a toda la repo, pero se pueden anular en los niveles de ToC y de artículo. Cualquier anulación de los metadatos debe realizarse en el nivel más bajo posible.

Los metadatos de la repo experience-manager-cloud-service.en son los mínimos requeridos.

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

Artículo

* `title`
* `description`
* `contentOwner` (solo en el contenido de recursos principales en `/help/assets`)

Encontrará información adicional sobre los metadatos en la guía de creación [interna.](https://docs.adobe.com/help/en/collaborative-doc-instructions/collaboration-guide/markdown/metadata.html#solution-metadata)
