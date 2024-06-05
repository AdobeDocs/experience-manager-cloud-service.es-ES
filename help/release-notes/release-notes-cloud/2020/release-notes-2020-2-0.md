---
title: Notas de la versión 2020.2.0
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.2.0."
exl-id: 005c4756-44c6-4af5-9b0c-0fc07bd211a0
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 91%

---

# AEM Notas de la versión de as a Cloud Service 2020.2.0 {#release-notes}

Esta página describe las notas de la versión generales de Experience Manager as a Cloud Service 2020.2.0.

## Fecha de lanzamiento {#release-date}

La fecha de versión de Experience Manager as a Cloud Service 2020.2.0 es el 13 de febrero de 2020.

## Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.2.0.

### Novedades {#what-is-new}

* Se ha actualizado la versión del arquetipo de Adobe Experience Manager a la versión 22.
* Los entornos de fase y producción de los programas de zona protegida/Demo ahora se pueden actualizar a través de la interfaz de usuario de Cloud Manager.
* Las URL utilizadas en las notificaciones de Experience Cloud se optimizaron para evitar una redirección adicional.
* Los pasos de ejecución de la canalización que agotaron el tiempo de espera ahora lo indican explícitamente.
* El paso Escaneo de código tiene ahora un registro descargable.
* La hoja de cálculo que contiene los problemas detectados durante el escaneo de código tiene ahora una columna con un vínculo a la documentación de la regla específica.

### Correcciones de errores  {#bug-fixes}

* Las políticas de seguridad del explorador a veces evitaban que ciertos botones de la pantalla de ejecución de la canalización funcionaran correctamente.
* Los vínculos Información general, Entornos y Actividad a veces estaban disponibles en la página de aterrizaje de Cloud Manager.
* Ciertos errores en la implementación podrían impedir erróneamente que se crearan nuevas canalizaciones.
