---
title: Notas de la versión de la versión 2020.3.0
description: Notas de la versión de la versión 2020.3.0
translation-type: tm+mt
source-git-commit: bcbb50f467a0e3b3047e2bb872a8fe39a9f02a1a

---


# Release Notes for AEM as a Cloud Service 2020.3.0 {#release-notes}

En la sección siguiente se describen las Notas de la versión generales de Experience Manager como servicio de nube 2020.3.0.

## Cloud Manager {#cloud-manager}

La fecha de versión de la versión 2020.3.0 de Cloud Manager es el 5 de marzo de 2020.

Siga esta sección para conocer las novedades y las actualizaciones de la versión 2020.3.0 de Cloud Manager.

### Novedades {#what-is-new}

* El registro del paso de compilación ya está disponible mientras se ejecuta el paso de compilación.
* Algunos de los mensajes de la página de detalles de ejecución de la canalización se han editado para mayor claridad.

### Corrección de errores {#bug-fixes}

* Los archivos de registro para los pasos de prueba funcionales del producto y personalizado no se podían descargar a través de la interfaz de usuario.
* Cuando no se pudo crear el repositorio de Git para un programa de servicios en la nube, los usuarios en la función de administrador de implementación a veces no podían recuperarse de este error.
* Algunas actividades de usuario durante la creación de un programa de simulación de pruebas podrían provocar errores en la creación del programa antes de que se creara la canalización sin producción.
* La instancia efímera de SonarQube utilizada en el paso de compilación ocasionalmente no se iniciaba dentro del tiempo de espera configurado.
* La creación simultánea de entornos de desarrollo en el mismo programa de servicios en la nube podría encontrar una condición en la que solo uno se pudiera crear correctamente.
* Las notificaciones de Experience Cloud para programas de servicios en la nube no se recibían de forma coherente.
* En proyectos específicos, los objetos *ResourceResolver siempre deben cerrarse* producirían una excepción de puntero nulo; sin embargo, esto no afectó a la ejecución de la canalización.

