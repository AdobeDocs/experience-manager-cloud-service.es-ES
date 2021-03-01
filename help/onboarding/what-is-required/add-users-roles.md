---
title: 'Agregar usuarios y funciones: ¿Qué es necesario?'
description: 'Agregar usuarios y funciones: ¿Qué es necesario?'
translation-type: tm+mt
source-git-commit: 2c21414edd6c3178d05c818d2bf57aa152b5956b
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 6%

---


# Agregar usuarios y funciones {#add-users-roles}


Muchas funciones de [!UICONTROL Cloud Manager] requieren permisos específicos para funcionar.

[!UICONTROL Cloud ] Manager define actualmente cuatro funciones para los usuarios que rigen la disponibilidad de funciones específicas:

* Propietario del negocio
* Administrador de programa
* Administrador de implementación
* Desarrollador

>[!CAUTION]
>
>Para utilizar [!UICONTROL Cloud Manager], debe tener un Adobe ID y el contexto de producto de Adobe Experience Manager as a Cloud Service.

## Definiciones de funciones {#role-definitions}

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
| Autor de contenido | Generalmente no interactúa con [!UICONTROL Cloud Manager]. Puede utilizar el conmutador de programa [!UICONTROL Cloud Manager] (con navegación desde [!UICONTROL Experience Cloud]) para acceder a AEM. |

## El perfil de producto de integración {#integration-product-profile}

Además de lo anterior, Cloud Manager creará automáticamente un perfil de producto denominado &quot;Integraciones - Cloud Service&quot;. Este perfil de producto se utiliza para las integraciones entre Adobe Experience Manager y otros productos de Adobe. Este perfil de producto **no debe** eliminarse. Si elimina accidentalmente este perfil, deberá volver a crearlo manualmente. El nombre para mostrar de este perfil **debe** ser `CM_CS_DEFAULT`.
