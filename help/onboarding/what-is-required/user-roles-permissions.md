---
title: Funciones de Cloud Manager
description: En esta página se describen los roles y permisos de usuario. Siga esta página para aprender a añadir usuarios y asignarlos a funciones de Cloud Manager.
translation-type: tm+mt
source-git-commit: 7b5973aef0d3296a54bcf1e57bda616cdd618346
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 8%

---


# Funciones de Cloud Manager {#user-roles-permissions}

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

Para ver sus funciones en Cloud Manager, inicie sesión en la interfaz de usuario de Cloud Manager, seleccione el icono de perfil en la esquina superior derecha y seleccione **Funciones de usuario**, como se muestra en la figura siguiente.

>[!NOTE]
>Consulte [Navegar a Cloud Manager](/help/onboarding/what-is-required/navigate-to-cloud-manager.md) para obtener más información sobre el inicio de sesión en Cloud Manager.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### El perfil de producto de integración {#integration-product-profile}

Además de lo anterior, Cloud Manager creará automáticamente un perfil de producto denominado &quot;Integraciones - Cloud Service&quot;. Este perfil de producto se utiliza para las integraciones entre Adobe Experience Manager y otros productos de Adobe. Este perfil de producto **no debe** eliminarse. Si elimina accidentalmente este perfil, deberá volver a crearlo manualmente. El nombre para mostrar de este perfil **debe** ser `CM_CS_DEFAULT`.


## Roles y permisos de usuario {#permissions}

[!UICONTROL Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. ] Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el repositorio de Git. Alternativamente, un propietario de una empresa tiene diferentes permisos que les permiten agregar y editar programas, agregar entornos y aprobar implementaciones.

Cada una de las funciones tiene permisos específicos asociados a ella. Por ejemplo, si tiene la función de:

* ***Propietario empresarial***, tiene permiso para agregar un nuevo programa o editar un programa, agregar o actualizar un entorno, añadir, editar o eliminar la canalización y ejecutar cualquier canalización, e implementar código en AEM entorno o calidad de código.

* ***Administrador de implementación***, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en AEM entorno o calidad del código.

* ***Desarrollador***, tiene permiso para generar un token de acceso personal para acceder a Git.

   >[!NOTE]
   > Se puede asignar a un usuario varias funciones. Por ejemplo, si asigna las funciones Propietario empresarial y Administrador de implementación a un usuario, se le proporcionará la combinación o suma de estos permisos.


La siguiente tabla resume las funciones junto con sus permisos asociados dentro de Cloud Manager.

| Permiso | Descripción | Propietario del negocio | Administrador de implementación | Administrador de programa | Desarrollador |
|--- |--- |--- |--- |--- |--- |
| Agregar programa<br>Editar programa | Agregar un nuevo programa.<br>Editar un programa: Agregar o quitar soluciones o complementos | x |  |  |  |
| Crear entorno | Crear Prod+Stage, Dev, Entornos. | x | x |  |  |
| Entorno de actualización | Actualice Prod+Stage, Dev, Entornos. | x | x |  |  |
| Eliminar entorno de desarrollo | Eliminar entornos de desarrollo. | x | x |  |  |
| Configuración de canalización | Configurar o editar canalización. |  | x |  |  |
| Ejecución de canalización | Inicie la canalización. | x | x |  |  |
| Ejecución de canalización | Rechazar/Aprobar Errores Importantes de Tres Niveles. | x | x | x |  |
| Ejecución de canalización | Proporcionar aprobación de GoLive. | x | x | x |  |
| Ejecución de canalización | Programar la implementación de producción. | x | x | x |  |
| Eliminación de canalización | Permite eliminar una canalización. |  | x |  |  |
| Cancelación de ejecución | Cancelar ejecución actual. |  | x |  |  |
| Generar token de acceso personal | Acceda a Git. |  | x |  | x |

