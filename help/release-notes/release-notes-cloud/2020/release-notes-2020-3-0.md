---
title: Notas de la versión 2020.3.0
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.3.0."
exl-id: 0393c789-3999-4e51-be83-269d6eabd3f3
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 92%

---

# AEM Notas de la versión de as a Cloud Service 2020.3.0 {#release-notes}

Esta página describe las notas de la versión generales de Experience Manager as a Cloud Service 2020.3.0.

## Fecha de lanzamiento {#release-date}

La fecha de versión de Experience Manager as a Cloud Service 2020.3.0 es el 5 de marzo de 2020.

## Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.3.0.

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
