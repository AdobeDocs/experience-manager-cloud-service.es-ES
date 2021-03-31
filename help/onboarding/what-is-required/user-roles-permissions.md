---
title: Roles y permisos de usuario
description: En esta página se describen los roles y permisos de usuario. Siga esta página para aprender a añadir usuarios y asignarlos a funciones de Cloud Manager.
translation-type: tm+mt
source-git-commit: 2779b20f3b4c13ef604fa2ad61f17c836e228422
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 9%

---


# Roles y permisos de usuario {#user-roles-permissions}

Adobe creará un identificador de **Organización** para su empresa en el sistema Identity Management de Adobe (IMS), donde se podrán administrar todos sus usuarios y sus permisos. Cada usuario, que debe ser miembro de esta organización y se le otorgará acceso a cualquiera de los servicios [!UICONTROL Experience Cloud], tendrá que tener su propio **[Adobe ID](/help/onboarding/what-is-required/get-your-adobe-id.md)**.

## Roles del usuario {#user-roles}

Muchas funciones de Cloud Manager requieren permisos específicos para funcionar.

Muchas funciones de Cloud Manager requieren permisos específicos para funcionar y limitan las acciones que realiza en la interfaz de usuario en función de las funciones y los permisos asignados. En algunos casos, si no tiene el permiso para realizar una acción, el control de interfaz está presente, pero deshabilitado.

Si desea realizar una acción, pero no puede, marque [permisos asociados con definiciones de funciones](#permissions). En función de su objetivo, puede ponerse en contacto con el administrador del sistema y solicitar la función que necesita.

Cloud Manager define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de implementación
* Administrador de programa
* Desarrollador

>[!NOTE]
>El perfil de desarrollador en Admin Console no está relacionado con la función de desarrollador en [!UICONTROL Cloud Manager].

## Definiciones de funciones {#role-definitions}

La siguiente tabla resume las funciones:

| [!UICONTROL Funciones de Cloud ] Manager | Descripción |
|--- |--- |
| Propietario del negocio | Responsable de definir KPI, aprobar implementaciones de producción y anular errores importantes de tres niveles. |
| Administrador de programa | Utiliza [!UICONTROL Cloud Manager] para realizar la configuración del equipo, revisar el estado y ver los KPI. Pueden aprobar errores importantes de tres niveles. |
| Administrador de implementación | Gestiona las operaciones de implementación. Utiliza [!UICONTROL Cloud Manager] para ejecutar implementaciones de fase/producción. Puede editar canalizaciones de CI/CD. Pueden aprobar errores importantes de tres niveles. Puede obtener acceso al repositorio de Git. |
| Desarrollador | Desarrolla y prueba el código de aplicación personalizado. Se utiliza principalmente [!UICONTROL Cloud Manager] para ver el estado. Puede obtener acceso al repositorio de Git para la confirmación de código. |
| Autor de contenido | Generalmente no interactúa con [!UICONTROL Cloud Manager]. Puede utilizar el [!UICONTROL Cloud Manager] conmutador de programas (habiendo navegado desde [!UICONTROL Experience Cloud]) para acceder a AEM. |

## Visualización de las funciones {#view-roles}

Para ver su función en Cloud Manager, inicie sesión en la interfaz de usuario de Cloud Manager, seleccione el icono de perfil en la esquina superior derecha y seleccione **Funciones de usuario**, como se muestra en la figura siguiente.

![](/help/onboarding/what-is-required/assets/admin-console-9.png)

### El perfil de producto de integración {#integration-product-profile}

Además de lo anterior, Cloud Manager creará automáticamente un perfil de producto denominado &quot;Integraciones - Cloud Service&quot;. Este perfil de producto se utiliza para las integraciones entre Adobe Experience Manager y otros productos de Adobe. Este perfil de producto **no debe** eliminarse. Si elimina accidentalmente este perfil, deberá volver a crearlo manualmente. El nombre para mostrar de este perfil **debe** ser `CM_CS_DEFAULT`.


## Permisos asociados con definiciones de roles {#permissions}

[!UICONTROL Cloud Manager tiene funciones preconfiguradas con los permisos adecuados. ] Por ejemplo, un desarrollador desarrolla código y tiene permiso para insertar el código en el **Repositorio de Git**. Alternativamente, un propietario de una empresa tiene diferentes permisos que les permiten definir los indicadores de rendimiento clave (KPI) y aprobar las implementaciones.


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