---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.12.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.12.0 de
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 45%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2021.12.0 de {#release-notes}

AEM Esta página describe las notas de la versión de las herramientas de migración de as a Cloud Service 2021.12.0.

>[!NOTE]
>Para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service, haga clic [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

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

* Alternar añadido a la fase de ingesta en la herramienta de transferencia de contenido para permitir que los usuarios deshabiliten [copia previa](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) durante la ingesta. Para obtener velocidades de ingesta óptimas, la copia previa durante la ingesta debe deshabilitarse para conjuntos de migración pequeños o si solo se agregaron unos pocos blobs desde la última ingesta.
* La asignación de usuarios se ha actualizado para utilizar la API de administración de usuarios mejorada que le permite obtener 2000 usuarios a la vez, lo que mejora significativamente el rendimiento.
