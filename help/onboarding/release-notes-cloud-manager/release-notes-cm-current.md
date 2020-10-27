---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.10.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.10.0
translation-type: tm+mt
source-git-commit: 7fdbdd8bfe80d5f87d9917c905c8d04c4c277534
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 54%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.10.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.10.0 es el 1 de octubre de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* La página Entornos se ha rediseñado.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* El contenedor de generación de Cloud Manager ahora admite Java 8 y Java 11.

* Se aumentó el número de variables de entorno por entorno a 200.

* La tarjeta de Entorno de la página Información general ahora lista hasta tres entornos. Los usuarios pueden seleccionar el botón **Mostrar todo** para navegar hasta la página de resumen de Entornos y realizar la vista de una tabla con una lista completa de entornos.
Consulte [Ver Entorno](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.


### Corrección de errores {#bug-fixes-cloud-manager}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Los botones Cancelar y Guardar de la página Editar tubería no de producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Algunas veces al crear un nuevo programa, el nombre sugerido era un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.