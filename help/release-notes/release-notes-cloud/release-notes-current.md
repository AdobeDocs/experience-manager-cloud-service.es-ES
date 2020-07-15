---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.7.0
description: Notas de la versión de Experience Manager para 2020.7.0
translation-type: tm+mt
source-git-commit: 74abf1c4cc6ae449a81e3e40d073bfcb23b056e8
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 29%

---


# Notas de la versión de AEM as a Cloud Service 2020.7.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.7.0.

## Novedades de Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.7.0.

### Fecha de la versión {#release-date}

La fecha de versión de [!UICONTROL Cloud Manager] versión 2020.7.0 es el 9 de julio de 2020.

### Novedades {#what-is-new-cloud-manager}

* La página entornos se ha rediseñado.

* Los entornos en hibernación ahora muestran un estado discreto en Cloud Manager cuando están en hibernación.

* El contenedor de compilación de Cloud Manager ahora admite Java 8 y Java 11.

### Corrección de errores {#bug-fixes-cm}

* El vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente antes de que se crearan los entornos por completo.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de deshibernar/hibernar el entorno de un Programa de Simulador para pruebas.

* Las opciones **Cancelar** y **Guardar** de la página de edición de la canalización sin producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Al crear un nuevo programa, el nombre sugerido a veces devolvía un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error de desactivación por uno.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.