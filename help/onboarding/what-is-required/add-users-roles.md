---
title: 'Agregar usuarios y funciones: lo que se necesita'
description: 'Agregar usuarios y funciones: lo que se necesita'
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Agregar usuarios y funciones: lo que se necesita {#add-users-roles}


Muchas funciones de [!UICONTROL Cloud Manager] requieren permisos específicos para funcionar. Por ejemplo, solo algunos usuarios pueden establecer los Indicadores de rendimiento clave (KPI) para un programa. Estos permisos se agrupan lógicamente en funciones.

[!UICONTROL Cloud Manager] define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de programas
* Administrador de implementación
* Desarrollador

>[!CAUTION]
>
>Para utilizar [!UICONTROL Cloud Manager], debe tener un Adobe ID y el contexto de producto de los servicios gestionados de Adobe.

## Definiciones de funciones {#role-definitions}

>[!NOTE]
>
>El personaje de desarrollador en Admin Console no está relacionado con el rol de desarrollador en [!UICONTROL Cloud Manager].

La siguiente tabla resume los roles:

| [!UICONTROL Funciones del Administrador] de nube | Descripción |
|--- |--- |
| Propietario del negocio | Responsable de definir KPI, aprobar implementaciones de producción y anular errores importantes de tres niveles. |
| Administrador de programas | Utiliza [!UICONTROL Cloud Manager] para realizar la configuración del equipo, revisar el estado y ver KPI. Puede aprobar errores importantes de tres niveles. |
| Administrador de implementación | Gestiona las operaciones de implementación. Utiliza [!UICONTROL Cloud Manager] para ejecutar implementaciones de fase/producción. Puede editar las tuberías de CD/CI. Puede aprobar errores importantes de tres niveles. Puede obtener acceso al repositorio Git. |
| Desarrollador | Desarrolla y prueba el código de aplicación personalizado. Utiliza principalmente [!UICONTROL Cloud Manager] para ver el estado. Puede obtener acceso al repositorio Git para la confirmación de código. |
| Autor de contenido | Generalmente no interactúa con [!UICONTROL Cloud Manager]. Puede utilizar el conmutador de programas [!UICONTROL Cloud Manager] (tras haber navegado desde [!UICONTROL Experience Cloud]) para acceder a AEM. |

## Uso de la Consola de administración para crear un perfil {#using-admin-console-to-create-a-profile}

Las funciones se administran para [!UICONTROL Cloud Manager] desde Adobe Admin Console. Los miembros específicos de funciones se proporcionan agregando el usuario a un perfil de producto de [!UICONTROL Cloud Manager] en Admin Console.

Puede asignar miembros de funciones específicas agregando el usuario a un perfil [!UICONTROL de] producto de **Cloud Manager** en Adobe Admin Console, una ubicación central para administrar las autorizaciones de Adobe en toda la organización. Para obtener más información sobre Adobe Admin Console, consulte la documentación de [Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html).

>[!NOTE]
>
>Para acceder a la consola de administración y configurar su equipo (usuarios y funciones), abra un navegador y visite [https://adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise).

Para proporcionar los permisos adecuados basados en funciones a los usuarios de [!UICONTROL Cloud Manager] , un administrador de la **organización** del cliente debe crear nuevos perfiles de producto en el contexto de producto de los servicios [!UICONTROL gestionados de] AEM.

Para proporcionar los permisos adecuados basados en roles a los usuarios de [!UICONTROL Cloud Manager] , como administrador debe crear cuatro nuevos perfiles de producto en el contexto de producto de los servicios [!UICONTROL gestionados de] AEM que correspondan a cada una de las cuatro funciones de [!UICONTROL Cloud Manager] :

* Propietario del negocio
* Administrador de implementación
* Desarrollador
* Administrador de programas

Puede crear o agregar usuarios o grupos a estos perfiles de producto con la Consola [de](https://adminconsole.adobe.com/) administración para [!UICONTROL Cloud Manager], como se muestra en la figura siguiente:

1. Inicie sesión en la consola de administración y haga clic en **Nuevo perfil** para agregar un nuevo perfil.

1. Rellene los campos para configurar una nueva función para [!UICONTROL Cloud Manager].

   Introduzca el nombre **** del perfil y **el nombre** para crear un nuevo perfil. Además, puede seleccionar un grupo **de** permisos para el perfil.

   Haga clic en **Listo** para completar el paso de creación del perfil.

   >[!NOTE]
   >
   >Al crear estos perfiles de producto, el nombre **para** mostrar debe ser el valor técnico definido por [!UICONTROL Cloud Manager] (consulte la tabla siguiente). El nombre **del** perfil puede ser cualquier cosa, aunque para evitar confusiones, se recomienda usar los valores de la columna Nombre *del perfil* recomendado que aparece a continuación. Para ello, al crear el perfil de producto, desactive la casilla **Igual que el nombre** de perfil y especifique el valor correspondiente como nombre **de** visualización.

   | **Función** | **Nombre para mostrar (obligatorio)** | **Nombre de perfil recomendado** |
   |---|---|---|
   | Propietario del negocio | CM_BUSINESS_OWNER_ROLE_PROFILE | [!UICONTROL Administrador] de nube: función de propietario del negocio |
   | Administrador de implementación | CM_DEPLOYMENT_MANAGER_ROLE_PROFILE | [!UICONTROL Administrador] de nube: función de administrador de implementación |
   | Desarrollador | CM_DEVELOPER_ROLE_PROFILE | [!UICONTROL Cloud Manager] : función de desarrollador |
   | Administrador de programas | CM_PROGRAM_MANAGER_ROLE_PROFILE | [!UICONTROL Administrador] de nube - Función Administrador de programas |

1. Una vez creado el perfil de producto, puede agregar usuarios (o grupos) a los perfiles de producto.


