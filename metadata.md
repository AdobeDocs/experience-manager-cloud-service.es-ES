---
product: adobe experience manager
description: Documentación de Adobe Experience Manager as a Cloud Service.
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.es-ES
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 5bc43af20dc8893303b1d1f4dc70939631933eb7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 68%

---


# Metadatos para uso interno

Los metadatos del sistema de creación de GitHub son jerárquicos y se definen con los siguientes niveles crecientes de precedentes.

1. metadata.md
1. TDC
1. Artículo

Los metadatos definidos en el archivo metadata.md se aplican a todo el repositorio, pero se pueden sobrescribir en los niveles de TDC y de artículo. Cualquier anulación de los metadatos debe realizarse en el nivel más bajo posible.

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

TDC

* `sub-product`
* `user-guide-title`

Artículo

* `title`
* `description`
* `contentOwner` (solo en el contenido de recursos principales de `/help/assets`)
