---
title: Limitaciones de Dynamic Media
description: Conozca las prácticas recomendadas y los límites aplicados al crear un conjunto de imágenes o un conjunto de giros, o al cargar un PDF. Obtenga información también sobre las combinaciones de explorador web y sistema operativo no admitidas para Dynamic Media.
contentOwner: Rick Brough
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 3%

---

# Limitaciones de Dynamic Media

Las secciones siguientes describen las limitaciones de Dynamic Media.

Este tema incluye las siguientes secciones:

* [Prácticas recomendadas y límites impuestos por Dynamic Media en los tipos de recursos](#best-practice-enforced-limits)
* [Combinaciones de explorador web y sistema operativo no admitidas para Dynamic Media](#unsupported-browser-os)

## Prácticas recomendadas y límites impuestos por Dynamic Media en los tipos de recursos {#best-practice-enforced-limits}

Al crear un conjunto de giros o de imágenes, o al cargar PDF para la extracción de páginas, Adobe recomienda las siguientes prácticas recomendadas y aplica los límites siguientes:

| Recurso: tipo de límite | Práctica recomendada | Límite impuesto |
| --- | --- | --- |
| **Imagen** - Número de recortes inteligentes por imagen | 5 | 100 |
| **Todos los conjuntos** - Número de recursos duplicados por conjunto | No hay duplicados | 20 |
| **Todos los conjuntos** - Número máximo de recursos por conjunto | 5-10 imágenes por conjunto | 1000 |
| **Conjunto de giros** - Número máximo de filas/columnas por conjunto 2D | 12 a 18 imágenes por conjunto | 1000 |
| **PDF** - Número máximo de páginas para que un PDF se considere para la extracción |  | 100 (para todos los PDF) |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Combinaciones de explorador web y sistema operativo no admitidas para Dynamic Media {#unsupported-browser-os}

Dynamic Media no admite las siguientes combinaciones de explorador web y sistema operativo.

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1 Update
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9 Mavericks
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

<!-- ## End of support for TLS 1.0 and 1.1 {#tls}

CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022)

Effective September 30, 2022, Adobe Dynamic Media will end support for the following:

* TLS (Transport Layer Security) 1.0 and 1.1
* The following weak ciphers in TLS 1.2:
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
  * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_RSA_WITH_AES_256_GCM_SHA384`
  * `TLS_RSA_WITH_AES_256_CBC_SHA256`
  * `TLS_RSA_WITH_AES_256_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_AES_128_GCM_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA256`
  * `TLS_RSA_WITH_AES_128_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
  * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
  * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
  * `TLS_RSA_WITH_SDES_EDE_CBC_SHA` -->

