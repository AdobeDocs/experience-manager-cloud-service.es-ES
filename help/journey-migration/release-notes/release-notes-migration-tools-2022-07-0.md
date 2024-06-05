---
title: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.7.0 de
description: AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.7.0 de
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 9%

---

# AEM Notas de la versión de las herramientas de migración de la versión as a Cloud Service 2022.7.0 de {#release-notes}

AEM Esta página describe las notas de la versión para las herramientas de migración de la versión 2022.7.0 de as a Cloud Service.

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.30 es el 27 de julio de 2022.

### Novedades {#what-is-new-bpa}

* BPA ahora puede detectar e informar sobre el tamaño total del índice de Lucene migrable, que es el índice de Lucene total, excluyendo `/oak:index/lucene` y `/oak:index/damAssetLucene`.
* Se ha agregado un nuevo patrón en BPA para detectar y crear informes sobre el uso del diccionario i18n personalizado. AEM Translator.html no está disponible en el diccionario as a Cloud Service y el diccionario i18n personalizado debe implementarse desde Git mediante la canalización CI/CD de Cloud Manager.

### Correcciones de errores {#bug-fixes-bpa}

* BPA informaba de la falta de representaciones originales para los fragmentos de contenido. Dado que los fragmentos de contenido no tienen representaciones, esta comprobación ahora se omite para los fragmentos de contenido.
* La opción de filtrar los resultados de ACS Commons no aparecía en la interfaz de usuario de BPA. Esto se ha corregido.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v2.0.12 es el 19 de julio de 2022.

### Novedades {#what-is-new-ctt}

* Los usuarios que iniciaron sesión mediante LDAP ahora pueden ejecutar las funciones Comprobar tamaño y Asignación de usuarios en CTT.
* Para ayudar a depurar los problemas de conexión SSL/TLS durante las extracciones, los usuarios ahora pueden habilitar el registro SSL.
* Para ayudar a depurar los problemas de conectividad de origen, los nombres de subdominio ahora se imprimen en los registros cuando falla la conexión a Azure.
* Para ayudar a depurar los problemas durante la precopia, los registros de AzCopy ahora se anexan a los registros de extracción cuando falla la precopia.
* Para evitar resultados de comprobación de tamaño antiguos, los usuarios solo pueden volver a ejecutar Comprobar tamaño después de que se haya completado una comprobación de tamaño anterior.

### Correcciones de errores {#bug-fixes-ctt}

* Los registros de extracción anteriores aparecían después de eliminar y volver a crear un conjunto de migración. Esto se ha corregido.
* El botón de acción Ver progreso no estaba disponible para conjuntos de migración con estado DETENIDO. Esto se ha corregido.
* El botón Eliminar acción no estaba disponible para conjuntos de migración con una clave de extracción caducada. Esto se ha corregido.
* Se han corregido varios errores de IU.

## Cloud Acceleration Manager {#cam-release}

### Fecha de lanzamiento {#release-date-cam}

La fecha de lanzamiento de Cloud Acceleration Manager es el 15 de julio de 2022.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager ahora proporciona a los usuarios que recuperan manualmente el token de migración para poder iniciar una ingesta cuando falle la recuperación automática. La recuperación automática puede fallar si los clientes han configurado una lista de IP permitidas que bloquee CAM o si un usuario que no es administrador intenta iniciar una ingesta. Consulte [Solución de problemas](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) para obtener más información.
* Las tablas largas de la página Complejidad de la migración ahora se pueden contraer para facilitar su uso.
