---
title: Notas de la versión para Cloud Manager 2023.4.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.4.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 50%

---


# Notas de la versión para Cloud Manager 2023.4.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión para Cloud Manager 2023.4.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de Cloud Manager 2023.4.0 en AEM as a Cloud Service es el 13 de abril de 2023. La próxima versión está planificada para el 11 de mayo de 2023.

## Novedades {#what-is-new}

* [El Tipo De Archivo Del Proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) se ha actualizado a la versión 41.

## Correcciones de errores {#bug-fixes}

* Cuando [certificate](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) caduca, [nombres de dominio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) y [LISTAS DE PERMITIDOS IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) asociado al certificado ya no se eliminará de la CDN.  En tales casos, el sitio seguirá siendo accesible.
* La interfaz de usuario de Cloud Manager proporcionará advertencias avanzadas más visibles de que la variable [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) está a punto de caducar.
* Se corrigió una situación poco habitual en la que los clientes no podían crear un nuevo entorno ni eliminarlo.
