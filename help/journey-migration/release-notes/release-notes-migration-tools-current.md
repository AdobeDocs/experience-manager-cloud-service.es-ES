---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2021.12.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2021.12.0
feature: Release Information
source-git-commit: a1c57a9d8165c9e67ce270a3f0c2ad80c75b7196
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2021.12.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic en [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.22 es el 1 de diciembre de 2021.

### Novedades {#what-is-new-bpa}

* Capacidad para detectar e informar sobre la versión de ACS commons utilizado.
* Capacidad para detectar y crear informes sobre la cantidad de usuarios y subgrupos de un grupo.
* Capacidad para detectar e informar sobre valores de propiedad de nodos en MongoDB que superen los 16 MB.

### Corrección de errores {#bug-fixes-bpa}

* La detección de componentes de base se refinó para reducir los falsos negativos.
* Para los clientes de AEM Forms, mensajería BPA con respecto a `EMAIL_PDF_SUBMIT_ACTION` no está disponible en AEM as a Cloud Service se ha corregido.


## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.7.10 es el 8 de diciembre de 2021.

### Novedades {#what-is-new-ctt}

* Alternar agregada a la fase de ingesta en la herramienta de transferencia de contenido para permitir que los usuarios desactiven [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante la ingesta. Para lograr velocidades de ingesta óptimas, la precopia durante la ingesta debe deshabilitarse para los conjuntos de migración pequeños o si solo se han añadido unos pocos blobs desde la última ingesta.
* Asignación de usuarios actualizada para utilizar la API de administración de usuarios mejorada que le permite obtener 2000 usuarios a la vez, lo que mejora significativamente el rendimiento.
