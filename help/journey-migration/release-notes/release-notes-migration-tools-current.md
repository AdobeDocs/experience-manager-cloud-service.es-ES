---
title: Notas de la versión de las herramientas de migración de la versión 2024.09 de AEM as a Cloud Service
description: Notas de la versión de las herramientas de migración de la versión 2024.09.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 7%

---

# Notas de la versión de las herramientas de migración de la versión 2024.09.0 de AEM as a Cloud Service {#release-notes}

Esta página describe las notas de la versión de las herramientas de migración de AEM as a Cloud Service 2024.09.0.

## Herramienta de transferencia de contenido {#ctt-release}

### Fecha de la versión {#release-date-ctt}

La fecha de lanzamiento de la herramienta de transferencia de contenido v3.0.20 es el 28 de agosto de 2024.

### Novedades {#what-is-new-ctt}

* Los usuarios ya no se incorporarán con esta versión y, por este motivo, se ha eliminado la capacidad opcional de asignación de usuarios.
* Se ha añadido una opción de configuración OSGI para deshabilitar o habilitar la migración de entidades de seguridad durante la extracción y la ingesta (la configuración predeterminada es habilitarla)

### Corrección de errores {#bug-fixes-ctt}

* Se mejoró CTT para evitar un error al desproteger una clave secreta en la configuración de azcopy
* CTT ahora gestiona correctamente cualquier error al copiar los registros de AzCopy en la fase de validación
* Cambiar el directorio de registro de azcopy creado durante el proceso de extracción

## Analizador de prácticas recomendadas {#bpa-release}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.52 es el 4 de septiembre de 2024

### Novedades {#what-is-new-bpa}

* AEM Se ha introducido un nuevo patrón para detectar eventos basados en JCR en las pruebas de

### Corrección de errores {#bug-fixes-bpa}

* Se corrigieron falsos positivos
* Solidez mejorada para gestionar la respuesta redirigida desde Dispatcher
* Se ha corregido el error de no informar de la búsqueda de NCC para todos los idiomas en /apps/wcm/core/resources/language/
* se ha añadido una comprobación para detectar si una propiedad múltiple de un nodo no tiene valores

