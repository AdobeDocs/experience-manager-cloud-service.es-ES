---
title: 'Derechos de acceso concedidos: ¿Qué es necesario?'
description: 'Derechos de acceso concedidos: ¿Qué es necesario?'
translation-type: tm+mt
source-git-commit: 4b62401fd1d0654cf758092176bd815a7fa56159
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 11%

---


# Derechos de acceso concedidos {#access-rights-granted}

Adobe creará un identificador de **Organización** para su empresa en el sistema Identity Management de Adobe (IMS), donde se podrán administrar todos sus usuarios y sus permisos. Cada usuario, que debe ser miembro de esta organización y se le otorgará acceso a cualquiera de los servicios [!UICONTROL Experience Cloud], tendrá que tener su propio **Adobe ID**.

## Tipos de identidad de usuario {#user-identity-types}

Para empezar a usar Adobe ID, visite [Administrar tipos de identidad de Adobe](https://helpx.adobe.com/enterprise/using/identity.html) para obtener instrucciones detalladas sobre cómo obtener un Adobe ID mediante uno de los tipos de identidad disponibles.

## Usuarios y funciones {#users-and-roles}

Una vez que Adobe haya creado una organización para su empresa, el administrador designado se añadirá como el primer miembro de esta organización. Al administrador se le otorgarán los permisos de administrador de forma predeterminada y se le asignará el [!UICONTROL producto] de **AEM Managed Services**, así como uno a más [!UICONTROL perfiles de producto] de **Cloud Manager**.

1. Una vez que el administrador del sistema le conceda acceso a Cloud Manager, recibirá un correo electrónico que le llevará a la página de inicio de sesión de Cloud Manager a la que también se puede acceder mediante [Adobe Experience Cloud](https://my.cloudmanager.adobe.com/).

1. En la página de aterrizaje de Cloud Manager, haga clic en **Administrar acceso**.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin5.png)

1. Una vez que haga clic en **Administrar acceso**, navegará a **Admin Console** desde donde podrá administrar las funciones de usuario o los permisos en Cloud Manager.

   ![](/help/onboarding/getting-access-to-aem-in-cloud/assets/sys-admin1.png)

   Desde el Admin Console puede realizar tareas de SysAdmin como:
   * [Administración de funciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-roles)
   * [Administración del acceso a la instancia de autor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#manage-access-aem)

      >[!NOTE]
      >Visite la sección [Usuarios y funciones](#users-roles) para obtener más información sobre los usuarios y las definiciones de funciones en Cloud Manager.

Con estos derechos concedidos, el administrador ahora se configura con un inicio de sesión único (mediante Adobe ID) para acceder a los servicios de [!UICONTROL Experience Cloud], iniciar sesión en los entornos de nube AEM y utilizar [!UICONTROL Cloud Manager].

## Usuarios y funciones {#users-roles}

Muchas funciones de [!UICONTROL Cloud Manager] requieren permisos específicos para funcionar.

[!UICONTROL Cloud ] Manager define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de programa
* Administrador de implementación
* Desarrollador

>[!CAUTION]
>
>Para utilizar [!UICONTROL Cloud Manager], debe tener un Adobe ID y Adobe Experience Manager as a Cloud Service Product Context.

### Definiciones de funciones {#role-definitions}

>[!NOTE]
>
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

