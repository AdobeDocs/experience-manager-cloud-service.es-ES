---
title: Permisos basados en roles
description: Permisos basados en roles
translation-type: tm+mt
source-git-commit: e59fe55c255d5239a561a9fb878faa81d17b4b48

---


# Permisos basados en roles {#role-based-permissions}

[!UICONTROL Cloud Manager] tiene funciones preconfiguradas con los permisos adecuados. Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el repositorio **Git**. Como alternativa, un propietario de una empresa tiene permisos diferentes que les permiten definir los Indicadores de rendimiento clave (KPI) y aprobar las implementaciones.

## Permisos de usuario {#user-permissions}

Cada función tiene permisos específicos, tareas preconfiguradas o permisos asociados a cada función. Esta tabla enumera las funciones disponibles y las funciones que pueden ejecutar la función.

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programas | Desarrollador | CSE |
|--- |--- |--- |--- |--- |--- |--- |
| Leer aplicación | Leer KPI de programa. | x | x | x | x | x |
| Escribir aplicación | Configuración o edición del programa. | x |  |  |  |  |
| Entorno de lectura | Consulte Detalles del entorno. | x | x | x | x | x |
| Crear ejecución | Iniciar canalización. | x | x | x |  |  |
| Leer ejecución | Consulte el estado de la ejecución. | x | x | x | x | x |
| Reanudar ejecución | Puede reanudar la ejecución cuando esté en pausa. | x | x | x |  | x |
| Ejecución Aprobar implementación en producción | Proporcione la aprobación de GoLive. | x | x | x |  |  |
| Implementación de programación de ejecución en producción | Programar la implementación de producción. | x | x | x |  | x |
| Implementación de ejecución en producción | Implemente la aplicación en producción cuando esté en pausa para la supervisión de CSE. |  |  |  |  | x |
| Cancelación de ejecución | Cancelar la ejecución actual. | x | x | x |  |  |
| Errores de control de calidad de anulación de ejecución | Aprobar Errores Importantes De Puerta De Calidad. | x | x | x |  |  |
| Creación de tubería | Configurar / Editar tubería. |  | x |  |  |  |
| Lectura de tubería | Consulte Detalles de canalización. | x | x | x | x | x |
| Escritura de tubería | Configurar / Editar tubería. |  | x |  |  |  |
| Aprobación de modificación de tubería | Permite editar la opción Propietario de la empresa. |  | x |  |  |  |
| Implementación administrada de modificación de tubería | Permite editar la opción Supervisión de CSE. |  | x |  |  |  |
| Lectura del paso | Consulte los resultados de las métricas de calidad de los pasos. | x | x | x | x | x |
