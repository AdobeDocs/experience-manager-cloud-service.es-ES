---
title: Notas de la versión 2020.2.0
description: Notas de la versión 2020.2.0
translation-type: ht
source-git-commit: e9514d2ba625a7df8a8126f5b0ab74b975eeda51

---


# Notas de la versión de AEM as a Cloud Service 2020.2.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.2.0.

## Cloud Manager {#cloud-manager}

La fecha de lanzamiento de la versión 2020.2.0 de Cloud Manager es el 13 de febrero de 2020.

Siga esta sección para conocer las novedades y las actualizaciones de la versión 2020.2.0 de Cloud Manager.

### Novedades {#what-is-new}

* Se ha actualizado la versión del arquetipo de Adobe Experience Manager a la versión 22.
* Los entornos de fase y producción de los programas de Sandbox/Demo ahora se pueden actualizar a través de la interfaz de usuario de Cloud Manager.
* Las direcciones URL utilizadas en las notificaciones de Experience Cloud se optimizaron para evitar una redirección adicional.
* Los pasos de ejecución de la canalización que agotaron el tiempo de espera ahora lo indican explícitamente.
* El paso Escaneo de código tiene ahora un registro descargable.
* La hoja de cálculo que contiene problemas detectados durante el escaneo de código tiene ahora una columna con un vínculo a la documentación de la regla específica.

### Corrección de errores {#bug-fixes}

* Las políticas de seguridad del navegador a veces evitaban que ciertos botones de la pantalla de ejecución de la canalización funcionaran correctamente.
* Los vínculos Información general, Entornos y Actividad a veces estaban disponibles en la página de aterrizaje de Cloud Manager.
* Ciertos errores en la implementación podrían impedir erróneamente que se crearan nuevas canalizaciones.