---
title: Limitaciones de Dynamic Media
description: Obtenga información sobre las prácticas recomendadas y los límites aplicados al crear un conjunto de imágenes o un conjunto de giros, o al cargar un PDF. Obtenga información también sobre las combinaciones de navegador web y sistema operativo no compatibles con los visores de Dynamic Media.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Viewers,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: f93db6f59d927b2e302f2c0d7d103ca73e9b4824
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 4%

---

# Limitaciones de Dynamic Media

En las secciones siguientes se describen las limitaciones de Dynamic Media.

Este tema incluye las siguientes secciones:

* [Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos](#best-practice-enforced-limits)
* [Combinaciones de navegador web y sistema operativo no compatibles con los visores de Dynamic Media](#unsupported-browser-os)

## Prácticas recomendadas y límites aplicados por Dynamic Media en los tipos de recursos {#best-practice-enforced-limits}

Cuando se crea un conjunto de giros o un conjunto de imágenes, o se cargan PDF para la extracción de páginas, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Recurso: tipo de límite | Práctica recomendada | Límite impuesto | Cambio al límite el 31 de diciembre de 2022 |
| --- | --- | --- | --- |
| **Imagen** - Número de recortes inteligentes por imagen | 5 | 100 | 20 |
| **Todos los conjuntos** - Número de activos duplicados por conjunto | Sin duplicados | 20 | No aplicable |
| **Todos los conjuntos** - Número máximo de activos por conjunto | 5 a 10 imágenes por conjunto | 1000 | No aplicable |
| **Conjunto de giros** - Número máximo de filas/columnas por conjunto 2D | 12 a 18 imágenes por conjunto | 1000 | No aplicable |
| **PDF** - Número máximo de páginas para un PDF a tener en cuenta para la extracción |  | 5000 (para nuevas cargas) | 100 (para todos los PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinaciones de navegador web y sistema operativo no compatibles con los visores de Dynamic Media {#unsupported-browser-os}

Los visores de Dynamic Media no admiten las siguientes combinaciones de navegador web y sistema operativo.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Actualización de Internet Explorer 11 + Windows Phone 8.1
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite
