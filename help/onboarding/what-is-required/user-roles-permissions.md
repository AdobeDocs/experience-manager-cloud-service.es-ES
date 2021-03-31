---
title: Roles y permisos de usuario
description: En esta página se describen los roles y permisos de usuario. Siga esta página para aprender a añadir usuarios y asignarlos a funciones de Cloud Manager.
translation-type: tm+mt
source-git-commit: 4b9476b094438acd08c945f0102b029b6792cb88
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 10%

---


# Roles y permisos de usuario {#user-roles-permissions}

## Roles del usuario {#user-roles}

Muchas funciones de Cloud Manager requieren permisos específicos para funcionar y limitan las acciones que realiza en la interfaz de usuario en función de las funciones y los permisos asignados. En algunos casos, si no tiene el permiso para realizar una acción, el control de interfaz está presente, pero deshabilitado.

Si desea realizar una acción, pero no puede, compruebe la sección siguiente, [Funciones de usuario y permisos](#permissions). En función de su objetivo, puede ponerse en contacto con el administrador del sistema y solicitar la función que necesita.

Cloud Manager define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de implementación
* Administrador de programa
* Desarrollador

>[!NOTE]
>El perfil de desarrollador en Admin Console no está relacionado con la función de desarrollador en [!UICONTROL Cloud Manager].

## Visualización de las funciones {#view-roles}

Para ver su función en Cloud Manager, inicie sesión en la interfaz de usuario de Cloud Manager, seleccione el icono de perfil en la esquina superior derecha y seleccione **Funciones de usuario**, como se muestra en la figura siguiente.

>[!NOTE]
>Consulte [Navegar a Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) para obtener más información sobre el inicio de sesión en Cloud Manager.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### El perfil de producto de integración {#integration-product-profile}

Además de lo anterior, Cloud Manager creará automáticamente un perfil de producto denominado &quot;Integraciones - Cloud Service&quot;. Este perfil de producto se utiliza para las integraciones entre Adobe Experience Manager y otros productos de Adobe. Este perfil de producto **no debe** eliminarse. Si elimina accidentalmente este perfil, deberá volver a crearlo manualmente. El nombre para mostrar de este perfil **debe** ser `CM_CS_DEFAULT`.


## Roles y permisos de usuario {#permissions}

[!UICONTROL Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. ] Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el **Repositorio de Git**. Alternativamente, un propietario de una empresa tiene diferentes permisos que les permiten agregar y editar programas, agregar entornos y aprobar implementaciones.

Cada una de las funciones tiene permisos específicos asociados a cada función. En la tabla siguiente se resumen las funciones, se enumeran las funciones disponibles y las funciones que pueden ejecutar la función.

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programa | Desarrollador |
|--- |--- |--- |--- |--- |--- |
| Agregar programa | Agregar un nuevo programa. | x |  |  |  |
| Crear entorno | Crear Prod+Stage, Dev, Entornos. | x | x |  |  |
| Entorno de actualización | Actualice Prod+Stage, Dev, Entornos. | x | x |  |  |
| Eliminar entorno | Elimine Entornos Que No Sean De Prod, Dev Y . | x | x |  |  |
| Configuración de canalización | Configurar o editar canalización. |  | x |  |  |
| Ejecución de canalización | Inicie la canalización. | x | x |  |  |
| Ejecución de canalización | Rechazar/Aprobar Errores Importantes de Tres Niveles. | x | x | x |  |
| Ejecución de canalización | Proporcionar aprobación de GoLive. | x | x | x |  |
| Ejecución de canalización | Programar la implementación de producción. | x | x | x |  |
| Eliminación de canalización | Permite eliminar una canalización. |  | x |  |  |
| Cancelación de ejecución | Cancelar ejecución actual. |  | x |  |  |
| Generar token de acceso personal | Acceda a Git. |  | x |  | x |