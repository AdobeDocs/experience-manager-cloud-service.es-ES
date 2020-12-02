---
title: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.7.0
description: Notas de la versión de Cloud Manager en AEM como Cloud Service, versión 2020.7.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 73%

---


# Notas de la versión de Cloud Manager en Adobe Experience Manager como Cloud Service 2020.7.0 {#release-notes}

Esta página describe las Notas de la versión de Cloud Manager en AEM como Cloud Service 2020.7.0.

## Fecha de la versión {#release-date}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.7.0 es el 9 de julio de 2020.

## Novedades {#whats-new-cloud-manager}

* Se rediseñó la página entornos.

* Cuando están en hibernación, los entornos en hibernación ahora muestran un estado discreto en Cloud Manager.

* Se aumentó el número de variables de entorno por entorno a 200.

* Las canalizaciones de Cloud Manager ahora admiten las variables y los secretos establecidos por el cliente.

   Consulte [Variables de canalización](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#pipeline-variables) para obtener más detalles.

* Ahora se admiten repositorios privados de Maven enlazados a autenticación.

* El contenedor de generación de Cloud Manager ahora admite Java 8 y Java 11.
Consulte [Uso de la compatibilidad con Java 11](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support) para obtener más detalles.

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

* Debido a un cambio en la forma de calcular la cobertura del código, la versión *mínima* del complemento Jacoco es ahora 0.7.5.201505241946 (publicada en mayo de 2015). Los clientes que hagan referencia explícita a una versión anterior reciben un mensaje de error en el proceso de calidad del código.