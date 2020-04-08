---
title: Notas de la versión 2020.3.0
description: Notas de la versión 2020.3.0
translation-type: tm+mt
source-git-commit: 55abc080701134c5067598dd39fe825048e077d4

---


# Notas de la versión de AEM as a Cloud Service 2020.3.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.3.0.

## Cloud Manager {#cloud-manager}

La fecha de lanzamiento de la versión 2020.3.0 de Cloud Manager es el jueves, 5 de marzo de 2020.

Siga esta sección para conocer las novedades y las actualizaciones de la versión 2020.3.0 de Cloud Manager.

### Novedades {#what-is-new}

* El registro del paso de compilación ya está disponible mientras este se ejecuta.
* Algunos mensajes de la página de detalles de ejecución de la canalización se han editado para mayor claridad.

### Corrección de errores {#bug-fixes}

* Los archivos de registro para la prueba funcional personalizada y de producto no se podían descargar a través de la interfaz de usuario.
* Cuando no se pudo crear el repositorio Git para un programa de Cloud Service, en algunos casos los usuarios en la función de administrador de implementación no podían recuperarse de este error.
* Algunas actividades de usuario durante la creación de un programa de simulación de pruebas provocaban errores al crear el programa antes de que se creara la canalización sin producción.
* La instancia efímera de SonarQube utilizada en el paso de compilación no se iniciaba dentro del tiempo de espera configurado en algunas ocasiones.
* La creación simultánea de entornos de desarrollo en el mismo programa de Cloud Service encontraba una condición en la que solo uno se podía crear correctamente.
* Las notificaciones de Experience Cloud para programas de Cloud Service no se recibían de forma coherente.
* En determinados proyectos, los mensajes *objetos ResourceResolver siempre se deben cerrar* producía una Null Pointer Exception; sin embargo, esto no afectó a la ejecución de la canalización.

