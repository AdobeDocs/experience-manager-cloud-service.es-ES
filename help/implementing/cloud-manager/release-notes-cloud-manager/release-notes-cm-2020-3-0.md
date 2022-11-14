---
title: Notas de la versión para Cloud Manager en la versión 2020.3.0 de AEM as a Cloud Service
description: Notas de la versión para Cloud Manager en la versión 2020.3.0 de AEM as a Cloud Service
feature: Release Information
exl-id: 2ff62ba5-a657-4739-b646-1e948332bf79
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# Notas de la versión para Cloud Manager en Adobe Experience Manager as a Cloud Service 2020.3.0 {#release-notes}

Esta página describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2020.3.0.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2020.3.0 es el 5 de marzo de 2020.

### Novedades {#what-is-new}

* El registro del paso de generación ya está disponible mientras este se ejecuta.
* Algunos mensajes de la página de detalles de ejecución de la canalización se han editado para mayor claridad.

### Correcciones de errores  {#bug-fixes}

* Los archivos de registro para la prueba funcional personalizada y de producto no se podían descargar a través de la interfaz de usuario.
* Cuando hay un error al crear el repositorio Git para un programa de Cloud Service, en algunos casos los usuarios con el rol de administrador de implementación no podían recuperarse de este error.
* Algunas actividades de usuario durante la creación de un programa de zona protegida provocaban errores al crear el programa antes de que se creara la canalización sin producción.
* La instancia efímera de SonarQube utilizada en el paso de generación, en algunas ocasiones no se iniciaba dentro del tiempo de espera configurado.
* La creación simultánea de entornos de desarrollo en el mismo programa de Cloud Service encontraba una condición en la que solo uno se podía crear correctamente.
* Las notificaciones de Experience Cloud para programas de Cloud Service no se recibían de forma coherente.
* En determinados proyectos, los objetos *ResourceResolver siempre se deben cerrar* produciría una Null Pointer Exception; sin embargo, esto no afectó a la ejecución de la canalización.
