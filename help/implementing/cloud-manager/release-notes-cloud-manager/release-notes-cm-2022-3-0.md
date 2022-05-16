---
title: Notas de la versión para Cloud Manager 2022.3.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 52%

---

# Notas de la versión para Cloud Manager 2022.3.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de la versión de Cloud Manager 2022.3.0 en AEM as a Cloud Service es el 10 de marzo de 2022. La próxima versión está planificada para el 7 de abril de 2022.

## Novedades {#what-is-new}

* Se puede acceder al registro de entorno de AEM con la función de desarrollador.

## Correcciones de errores {#bug-fixes}

* Un subconjunto de repositorios Git creados manualmente tenía un valor de nombre incorrecto que impedía que la función de reutilización de artefactos de compilación fuera efectiva. Los nombres de esos repositorios se han cambiado y los usuarios verán el nombre corregido en la IU/API de Cloud Manager.
* Los artefactos de compilación de las canalizaciones que no son de producción se reutilizaron de forma incorrecta en las canalizaciones full stack de producción.
* Al añadir o editar una canalización de calidad de código, ya no se muestran las opciones para gestionar errores de métricas.
* Algunas configuraciones de variables de canalización inesperadas podrían causar en el paso de compilación.
