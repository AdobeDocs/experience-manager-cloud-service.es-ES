---
title: 'Agregar usuarios y funciones: lo que se necesita'
description: 'Agregar usuarios y funciones: lo que se necesita'
translation-type: tm+mt
source-git-commit: 936e42f273b75f0ea7776c51f57af44ec9e6d96f

---


# Agregar usuarios y funciones {#add-users-roles}


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