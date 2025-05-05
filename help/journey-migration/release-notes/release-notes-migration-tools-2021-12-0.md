---
title: Notas de la versión para las herramientas de migración en la versión 2021.12.0 de AEM as a Cloud Service
description: Notas de la versión para las herramientas de migración en la versión 2021.12.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 38%

---

# Notas de la versión para las herramientas de migración en la versión 2021.12.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Vea [Notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las últimas notas de la versión.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.22 es el 1 de diciembre de 2021.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre la versión de ACS Commons utilizada.
* Capacidad para detectar y crear informes sobre la cantidad de usuarios y subgrupos de un grupo.
* Capacidad para detectar e informar sobre valores de propiedad de nodos en MongoDB que superen los 16 MB.

### Corrección de errores {#bug-fixes-bpa}

* La detección de componentes de Foundation se refinó para reducir los falsos negativos.
* Para los clientes de AEM Forms, se ha corregido la mensajería BPA con respecto a que `EMAIL_PDF_SUBMIT_ACTION` no está disponible en AEM as a Cloud Service.


## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.7.10 es el 8 de diciembre de 2021.

### Novedades {#what-is-new-ctt}

* Se agregó el conmutador a la fase de ingesta en la herramienta de transferencia de contenido para permitir que los usuarios deshabiliten la [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=es) durante la ingesta. Para obtener velocidades de ingesta óptimas, la copia previa durante la ingesta debe deshabilitarse para conjuntos de migración pequeños o si solo se agregaron unos pocos blobs desde la última ingesta.
* La asignación de usuarios se ha actualizado para utilizar la API de administración de usuarios mejorada que le permite obtener 2000 usuarios a la vez, lo que mejora significativamente el rendimiento.
