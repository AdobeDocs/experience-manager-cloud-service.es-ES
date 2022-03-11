---
title: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.10.0
description: Notas de la versión para Cloud Manager en AEM versión as a Cloud Service 2020.10.0
feature: Release Information
exl-id: 129d0dd8-3d6e-4cf0-b42e-5526f5cf0836
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 48%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.10.0 {#release-notes}

Esta página describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2020.10.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.10.0 es el 1 de octubre de 2020.

## Cloud Manager {#cloud-manager}

### Novedades {#what-is-new}

* La página Entornos se ha rediseñado.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* El contenedor de compilación de Cloud Manager ahora es compatible con la compilación de proyectos mediante Java 8 o Java 11. El sistema de herramientas Maven proporciona compatibilidad con Java 11.

* Se aumentó el número de variables de entorno por entorno a 200.

* La tarjeta Entorno de la página Información general ahora enumera hasta tres entornos. Los usuarios pueden seleccionar **Mostrar todo** para ir a la página Environment summary y ver una tabla con una lista completa de entornos.
Consulte [Entorno de visualización](/help/implementing/cloud-manager/manage-environments.md#viewing-environment) para obtener más información.


### Corrección de errores {#bug-fixes-cloud-manager}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Los botones Cancelar y Guardar de la página Edición de canalización no de producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Algunas veces al crear un nuevo programa, el nombre sugerido era un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.
