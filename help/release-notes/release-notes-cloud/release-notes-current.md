---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.7.0
description: Notas de la versión de Experience Manager para 2020.7.0
translation-type: tm+mt
source-git-commit: 66f066fe55ef872b62d4dcee711d3c7077bfccd1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 20%

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

* El número de variables de entorno por entorno se ha aumentado a 200.

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

## Novedades del analizador de preparación para la nube {#cloud-readiness-analyzer}

Siga esta sección para conocer las novedades y las actualizaciones de la versión v1.0.2 del analizador de preparación para la nube.

### Corrección de errores {#cra-bug-fixes}

* La versión anterior de CRA no se pudo ejecutar en Adobe Experience Manager (AEM) 6.1. Se agregó compatibilidad explícita para permitir usuarios en el grupo de administradores.

   Consulte [Instalación de CRA en AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obtener más información.

* La marca de tiempo de caducidad que se muestra en el informe de resumen es incorrecta.

* CRA estaba detectando componentes personalizados de duplicado.

* En AEM 6.1, la inspección de contenido se cerraba antes de completar la inspección completa. Se ha añadido la gestión de excepciones para permitir que el inspector se omita y continúe hasta que se complete la inspección completa.

