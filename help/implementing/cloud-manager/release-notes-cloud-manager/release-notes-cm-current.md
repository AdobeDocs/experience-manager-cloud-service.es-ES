---
title: Notas de la versión para Cloud Manager 2023.1.0 en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión para Cloud Manager 2024.1.0 en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 33%

---


# Notas de la versión para Cloud Manager 2023.1.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión de Cloud Manager 2023.1.0 en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de Cloud Manager 2023.1.0 en AEM as a Cloud Service es el 19 de enero de 2023. La próxima versión está planificada para el 16 de febrero de 2023.

## Novedades {#what-is-new}

* Las mejoras de uso se realizaron actualizando estilos de cursor que distinguen entre dónde los usuarios pueden realizar acciones y el puntero predeterminado.

* Ahora, en las listas de entornos y ejecuciones de canalización, puede acceder a los detalles haciendo clic en la fila individual.

* Los informes de prueba de la interfaz de usuario personalizada ahora se copian en el almacenamiento de Cloud Manager y se puede acceder a ellos mediante una llamada de API de Cloud Manager.

* Los usuarios ahora pueden realizar la transición entre los estados de los widgets de Go-live utilizando flechas izquierda-derecha.

   ![Transiciones de utilidades de Go-live](assets/go-live-transitions.gif)

* Autoservicio [creación de programas habilitados para HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) ahora es posible cuando están disponibles los derechos y permisos correspondientes.

## Correcciones de errores {#bug-fixes}

* Cloud Manager impedirá que dos ejecuciones de canalización comiencen (o casi al mismo tiempo), evitando así errores de canalización.
