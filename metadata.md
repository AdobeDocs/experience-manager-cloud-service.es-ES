---
product: adobe experience manager
description: Documentación de Adobe Experience Manager as a Cloud Service.
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.es-ES
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
cloud: Experience Cloud
translation-type: tm+mt
source-git-commit: 6908b5215dcbff0692d4e03dd1588ca5d34aeffe
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 7%

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
