---
title: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.7.0
description: Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.7.0
feature: Release Information
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 9%

---

# Notas de la versión de las herramientas de migración en AEM versión as a Cloud Service 2022.7.0 {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración en AEM as a Cloud Service 2022.7.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v2.0.12 es el 19 de julio de 2022.

### Novedades {#what-is-new-ctt}

* Los usuarios que iniciaron sesión mediante LDAP ahora pueden ejecutar las funciones Comprobar tamaño y Asignación de usuarios en CTT.
* Para ayudar a depurar los problemas de conexión SSL/TLS durante las extracciones, los usuarios ahora pueden habilitar el registro SSL.
* Para ayudar a depurar los problemas de conectividad de origen, los nombres de subdominio ahora se imprimen en los registros cuando falla la conexión a Azure.
* Para ayudar a depurar los problemas durante la precopia, los registros de AzCopy ahora se anexan a los registros de extracción cuando falla la precopia.
* Para evitar resultados antiguos de Tamaño de comprobación, los usuarios solo podrán volver a ejecutar Tamaño de comprobación una vez que se haya completado un Tamaño de comprobación anterior.

### Correcciones de errores {#bug-fixes-ctt}

* Los registros de extracción anteriores aparecían después de eliminar y volver a crear un conjunto de migración. Esto se ha corregido.
* El botón Ver acción de progreso no estaba disponible para los conjuntos de migración con estado STOPPED. Esto se ha corregido.
* El botón Eliminar acción no estaba disponible para conjuntos de migración con una clave de extracción caducada. Esto se ha corregido.
* Se han corregido varios errores de la interfaz de usuario.

## Cloud Acceleration Manager {#cam-release}

### Fecha de la versión {#release-date-cam}

La fecha de versión de Cloud Acceleration Manager es el 15 de julio de 2022.

### Novedades {#what-is-new-cam}

* Cloud Acceleration Manager ahora proporciona a los usuarios la posibilidad de recuperar manualmente el token de migración para poder iniciar una ingesta cuando falla la recuperación automática. La recuperación automática puede fallar si los clientes han configurado una lista de IP permitidas que bloquea CAM o si un usuario no administrador intenta iniciar una ingesta. Consulte [Resolución de problemas](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) para obtener más información.
* Las tablas largas de la página de Complejidad de la migración ahora se pueden contraer para facilitar su uso.

