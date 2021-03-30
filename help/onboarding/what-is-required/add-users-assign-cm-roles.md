---
title: 'Adición de usuarios y asignación de funciones de Cloud Manager '
description: Siga esta página para aprender a añadir usuarios y asignarlos a funciones de Cloud Manager
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 6%

---


# Adición de usuarios y asignación de funciones de Cloud Manager {#add-users-assign}

Adobe creará un identificador de **Organización** para su empresa en el sistema Identity Management de Adobe (IMS), donde se podrán administrar todos sus usuarios y sus permisos. Cada usuario, que debe ser miembro de esta organización y se le otorgará acceso a cualquiera de los servicios [!UICONTROL Experience Cloud], tendrá que tener su propio **Adobe ID**.

## Explicación de las funciones de usuario {#user-roles}

Muchas funciones de Cloud Manager requieren permisos específicos para funcionar.

Cloud Manager define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de implementación
* Administrador de programa
* Desarrollador

>[!NOTE]
>El perfil de desarrollador en Admin Console no está relacionado con la función de desarrollador en [!UICONTROL Cloud Manager].

La siguiente tabla resume las funciones:

| [!UICONTROL Funciones de Cloud ] Manager | Descripción |
|--- |--- |
| Propietario del negocio | Responsable de definir KPI, aprobar implementaciones de producción y anular errores importantes de tres niveles. |
| Administrador de programa | Utiliza [!UICONTROL Cloud Manager] para realizar la configuración del equipo, revisar el estado y ver los KPI. Pueden aprobar errores importantes de tres niveles. |
| Administrador de implementación | Gestiona las operaciones de implementación. Utiliza [!UICONTROL Cloud Manager] para ejecutar implementaciones de fase/producción. Puede editar canalizaciones de CI/CD. Pueden aprobar errores importantes de tres niveles. Puede obtener acceso al repositorio de Git. |
| Desarrollador | Desarrolla y prueba el código de aplicación personalizado. Se utiliza principalmente [!UICONTROL Cloud Manager] para ver el estado. Puede obtener acceso al repositorio de Git para la confirmación de código. |
| Autor de contenido | Generalmente no interactúa con [!UICONTROL Cloud Manager]. Puede utilizar el [!UICONTROL Cloud Manager] conmutador de programas (habiendo navegado desde [!UICONTROL Experience Cloud]) para acceder a AEM. |

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

## Adición de usuarios {#add-users}

>[!NOTE]
>Debe ser administrador del sistema para agregar un usuario.

1. Si es administrador del sistema, vaya al [Admin Console](https://adminconsole.adobe.com). También puede navegar hasta Cloud Manager, donde verá el botón **Administrar acceso**, como se describe a continuación.

1. Haga clic en el botón **Administrar acceso**, situado en la parte superior derecha de la página de aterrizaje de Cloud Manager, para abrir el Admin Console en una pestaña nueva.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

   Desde el **Admin Console**, puede agregar usuarios a Cloud Manager y asignarlos a funciones, denominadas perfiles de producto en Admin Console.

1. Seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios** como se muestra a continuación.

   ![](/help/onboarding/what-is-required/assets/admin-console-1.png)

1. Seleccione la pestaña **Users** en la barra de acciones y, a continuación, seleccione **Add User**.

   ![](/help/onboarding/what-is-required/assets/admin-console-2.png)

1. Seleccione el usuario y asigne las funciones o perfiles de producto correspondientes de Cloud Manager al usuario, como se muestra a continuación.

   ![](/help/onboarding/what-is-required/assets/admin-console-3.png)

   >[!NOTE]
   >Consulte las secciones anteriores, [Roles de usuario y permisos](#user-roles) y [permisos asociados con definiciones de rol](#permissions) para asegurarse de que a los usuarios adecuados se les asignen las funciones correctas en el **Admin Console**.

   Ahora, ha agregado usuarios a Adobe Experience Manager as a Cloud Service Product Context y está configurado con las funciones o perfiles de producto adecuados.

   Por ejemplo, si tiene la función de:

   * ***Propietario empresarial***, tiene permiso para agregar un nuevo programa o editar un programa, agregar o actualizar un entorno, añadir, editar o eliminar la canalización y ejecutar cualquier canalización, e implementar código en AEM entorno o calidad de código.

   * ***Administrador de implementación***, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en AEM entorno o calidad del código.

   * ***Desarrollador***, tiene permiso para generar un token de acceso personal para acceder a Git.

      >[!NOTE]
      > Se puede asignar a un usuario varias funciones. Por ejemplo, si asigna las funciones Propietario empresarial y Administrador de implementación a un usuario, se le proporcionará la combinación o suma de estos permisos.
