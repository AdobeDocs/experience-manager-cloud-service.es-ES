---
title: Permisos basados en roles
description: Permisos basados en roles
translation-type: tm+mt
source-git-commit: 1765cc81bcd6b3404642efbd3ddde27047583f85

---


# Permisos basados en roles {#role-based-permissions}

[!UICONTROL Cloud Manager] tiene funciones preconfiguradas con los permisos adecuados. Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el repositorio **Git**. Como alternativa, un propietario de una empresa tiene permisos diferentes que les permiten definir los Indicadores de rendimiento clave (KPI) y aprobar las implementaciones.

## Permisos de usuario {#user-permissions}

Cada función tiene permisos específicos, tareas preconfiguradas o permisos asociados a cada función. Esta tabla enumera las funciones disponibles y las funciones que pueden ejecutar la función.

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programas | Desarrollador |
|--- |--- |--- |--- |--- |--- |
| Agregar programa | Agregar un nuevo programa. | x |  |  |  |
| Crear entorno | Cree Entornos Prod+Stage, Dev Y Playground. | x | x |  |  |
| Entorno de actualización | Actualice Los Entornos Prod+Stage, Dev Y Playground. | x | x |  |  |
| Eliminar entorno | Elimine Entornos No Prod, Dev Y Playground. | x | x |  |  |
| Eliminar entorno | Eliminar Entorno Prod+Stage. |  |  |  |  |
| Configuración del programa | Configurar el programa (incluidos los KPI). | x |  |  |  |
| Configuración del programa | Obtener acceso de confirmación. |  | x |  | x |
| Configuración de tubería | Configurar o editar tubería. |  | x |  |  |
| Ejecución de canalización | Inicie la canalización. | x | x |  |  |
| Ejecución de canalización | Rechazar o aprobar errores importantes de tres niveles. | x | x | x |  |
| Ejecución de canalización | Proporcione la aprobación de GoLive. | x | x | x |  |
| Ejecución de canalización | Programar la implementación de producción. | x | x | x |  |
| Ejecución de canalización | Reanudar tubería de producción. |  |  |  |  |
| Administrar entorno | Agregue el segmento Publish-Dispatcher desde la pantalla Administrar entorno. | x | x |  |  |  |
| Actualización push | Iniciar la canalización de actualización push. |  |  |  |  |
| Generar token de acceso personal | Generar token de acceso personal. |  | x |  | x |

