---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.7.0
description: Notas de la versión de Experience Manager para 2020.7.0
translation-type: tm+mt
source-git-commit: f96a9b89bb704b8b8b8eb94cdb5f94cc42890ec8
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 87%

---


# Notas de la versión de AEM as a Cloud Service 2020.7.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.7.0.

## Novedades de Cloud Manager {#cloud-manager}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.7.0.

### Fecha de la versión {#release-date}

La fecha de versión de [!UICONTROL Cloud Manager] versión 2020.7.0 es 9 de julio de 2020.

### Novedades {#what-is-new-cloud-manager}

* Se rediseñó la página entornos.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* Se aumentó el número de variables de entorno por entorno a 200.

* El contenedor de generación de Cloud Manager ahora admite Java 8 y Java 11.

* Las canalizaciones de Cloud Manager ahora admiten las variables y los secretos establecidos por el cliente.
Consulte [Variables](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) de canalización para obtener más detalles.

### Corrección de errores {#bug-fixes-cm}

* Antes de que se crearan completamente los entornos, el vínculo de Cloud Manager a la consola de desarrollador no se activaba correctamente.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostraba la opción de anular la hibernación o hibernar el entorno de un programa simulador para pruebas.

* Las opciones **Cancelar** y **Guardar** de la página de edición de la canalización sin producción no siempre estaban visibles.

* Ciertos errores en el proceso de calidad del código podrían ocasionar que el archivo de registro no se genere correctamente.

* Algunas veces al crear un nuevo programa, el nombre sugerido era un duplicado de un nombre de programa existente.

* Algunos registros de pasos de canalización de gran tamaño no se podían descargar de forma consistente a través de la interfaz de usuario.

* La validación de los nombres de entornos tenía un error por un paso.

* En ocasiones, la página Entornos mostraba los segmentos de publicación y envío cuando no había ninguno presente.

### Problemas conocidos {#known-issues}

* Debido a un cambio en la forma de calcular la cobertura del código, la versión _mínima_ del complemento Jacoco es ahora 0.7.5.201505241946 (publicada en mayo de 2015). Los clientes que hagan referencia explícita a una versión anterior recibirán un mensaje de error en el proceso de calidad del código.

## Novedades de Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Consulte esta sección para conocer las novedades y las actualizaciones de Cloud Manager versión 1.0.2.

### Corrección de errores {#cra-bug-fixes}

* La versión anterior de CRA no se podía ejecutar en Adobe Experience Manager (AEM) 6.1. Se agregó compatibilidad explícita para permitir usuarios en el grupo de administradores.

   Consulte [Instalar CRA en AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) para obtener más información.

* La marca de tiempo de caducidad que se muestra en el informe de resumen era incorrecta.

* CRA detectaba componentes personalizados duplicados.

* En AEM 6.1, la inspección de contenido se cerraba antes de completar toda la inspección. Se añadió la gestión de excepciones para permitir que el inspector omita y continúe hasta completar toda la inspección.

