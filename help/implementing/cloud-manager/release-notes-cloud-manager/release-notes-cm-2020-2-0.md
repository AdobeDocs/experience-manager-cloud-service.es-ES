---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.2.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.2.0
feature: Release Information
exl-id: 3f3324d9-53db-458d-9523-2e0d5d6dc3f7
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 66%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.2.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2020.2.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.2.0 es el 13 de febrero de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Se ha actualizado la versión del arquetipo de Adobe Experience Manager a la versión 22.
* Los entornos de fase y producción de los programas de Sandbox/Demo ahora se pueden actualizar a través de la interfaz de usuario de Cloud Manager.
* Las URL utilizadas en las notificaciones de Experience Cloud se optimizaron para evitar una redirección adicional.
* Los pasos de ejecución de la canalización que agotaron el tiempo de espera ahora lo indican explícitamente.
* El paso Escaneo de código tiene ahora un registro descargable.
* La hoja de cálculo que contiene los problemas detectados durante el escaneo de código tiene ahora una columna con un vínculo a la documentación de la regla específica.

### Corrección de errores  {#bug-fixes}

* Las políticas de seguridad del navegador a veces evitaban que ciertos botones de la pantalla de ejecución de la canalización funcionaran correctamente.
* Los vínculos Información general, Entornos y Actividad a veces estaban disponibles en la página de aterrizaje de Cloud Manager.
* Ciertos errores en la implementación podrían impedir erróneamente que se crearan nuevas canalizaciones.
