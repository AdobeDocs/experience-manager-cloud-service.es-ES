---
title: Notas de la versión 2020.2.0
description: Notas de la versión 2020.2.0
translation-type: tm+mt
source-git-commit: 6c719411ffa7bd814a515e302024ac433f173207
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 77%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.2.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.2.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.2.0 es el 13 de febrero de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* Se ha actualizado la versión del arquetipo de Adobe Experience Manager a la versión 22.
* Los entornos de fase y producción de los programas de Sandbox/Demo ahora se pueden actualizar a través de la interfaz de usuario de Cloud Manager.
* Las URL utilizadas en las notificaciones de Experience Cloud se optimizaron para evitar una redirección adicional.
* Los pasos de ejecución de la canalización que agotaron el tiempo de espera ahora lo indican explícitamente.
* El paso Escaneo de código tiene ahora un registro descargable.
* La hoja de cálculo que contiene los problemas detectados durante el escaneo de código tiene ahora una columna con un vínculo a la documentación de la regla específica.

### Corrección de errores {#bug-fixes}

* Las políticas de seguridad del navegador a veces evitaban que ciertos botones de la pantalla de ejecución de la canalización funcionaran correctamente.
* Los vínculos Información general, Entornos y Actividad a veces estaban disponibles en la página de aterrizaje de Cloud Manager.
* Ciertos errores en la implementación podrían impedir erróneamente que se crearan nuevas canalizaciones.
