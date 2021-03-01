---
product: adobe experience manager
description: estos son los metadatos necesarios para las páginas de documentación de AEMaaCS
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.es-ES
index: y
type: Documentación
solution-title: Adobe Experience Manager as a Cloud Service
solution-hub-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html
getting-started-title: Introducción
getting-started-url: https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/home.html
tutorials-title: Tutoriales
tutorials-url: https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html
translation-type: tm+mt
source-git-commit: 28de20620a7cc8a3df231abacde4b3daa98cbcdb
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 14%

---


# Metadatos para uso interno

Los metadatos en el sistema de creación de GitHub son jerárquicos y se definen con los siguientes niveles crecientes de precedentes.

1. metadata.md
1. ToC
1. Artículo

Los metadatos definidos en el archivo metadata.md se aplican a todo el repositorio, pero se pueden sobrescribir en los niveles de ToC y de artículo. Cualquier anulación de los metadatos debe realizarse en el nivel más bajo posible.

Los metadatos del repositorio de experience-manager-cloud-service.en son los mínimos requeridos.

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
* `contentOwner` (solo en el contenido de recursos principales de  `/help/assets`)
