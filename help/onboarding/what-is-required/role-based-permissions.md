---
title: Permisos basados en roles
description: Permisos basados en roles
translation-type: tm+mt
source-git-commit: 3c56d94f9922cb65b91912dd96eb8aa60efc2b53
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 23%

---


# Permisos basados en roles {#role-based-permissions}

[!UICONTROL Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. ] Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el repositorio **Git**. Como alternativa, un propietario de una empresa tiene permisos diferentes que les permiten definir los Indicadores de rendimiento clave (KPI) y aprobar las implementaciones.

## Permisos de usuario {#user-permissions}

Cada una de las funciones tiene permisos específicos, tareas preconfiguradas o permisos asociados a cada función. Esta tabla lista las funciones disponibles y las funciones que pueden ejecutar la función.

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programa | Desarrollador |
|--- |--- |--- |--- |--- |--- |
| Añadir Programa | Añadir un nuevo Programa. | x |  |  |  |
| Crear Entorno | Crear Entornos Prod+Stage, Dev y Playground. | x | x |  |  |
| Actualizar Entorno | Actualice los Entornos Prod+Stage, Dev y Playground. | x | x |  |  |
| Eliminar Entorno | Elimine Entornos No Prod, Dev Y Playground. | x | x |  |  |
| Eliminar Entorno | Eliminar Entorno Prod+Stage. |  |  |  |  |
| Configuración de programa | Configurar Programas (incluidos KPI). | x |  |  |  |
| Configuración de programa | Obtener acceso de confirmación. |  | x |  | x |
| Configuración de tubería | Configurar o editar tubería. |  | x |  |  |
| Ejecución de canalización | Inicio de la tubería. | x | x |  |  |
| Ejecución de canalización | Rechazar o aprobar errores importantes de tres niveles. | x | x | x |  |
| Ejecución de canalización | Proporcionar aprobación de GoLive. | x | x | x |  |
| Ejecución de canalización | Programar la implementación de producción. | x | x | x |  |
| Ejecución de canalización | Reanudar tubería de producción. |  |  |  |  |
| Eliminación de tubería | Permite la eliminación de una canalización. |  | x |  |  |
| Cancelación de ejecución | Cancelar ejecución actual. |  | x |  |  |
| Administrar Entorno | Añada el segmento Publish-Dispatcher desde la pantalla Administrar Entorno. | x | x |  |  |  |
| Actualización push | Canalización de actualización de inicio Push. |  |  |  |  |
| Generar Token de acceso personal | Acceso a Git. |  | x |  | x |

