---
title: Perfiles de AEM as a Cloud Service Team y de producto
description: Aprenda cómo los perfiles de equipo y de producto de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones de Adobe con licencia.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 85%

---


# Perfiles de AEM as a Cloud Service Team y de producto {#product-profiles}

Aprenda cómo los perfiles de equipo y de producto de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones de Adobe con licencia.

## Perfiles de producto {#profiles}

Al conceder a un usuario acceso a una solución de Adobe específica, no es necesario que les proporcione acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario. Están disponibles y son accesibles a través de [Admin Console](/help/journey-onboarding/admin-console.md).

## Perfiles de producto de AEM as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service es una oferta totalmente nativa de la nube que ofrece AEM como servicio. Ofrece AEM de forma nativa en la nube, con nuevos atributos como “siempre activado”, “siempre actuales”, “siempre seguros” y “siempre a escala”. Al mismo tiempo, conserva la propuesta de valor principal que proporciona AEM como plataforma personalizable a los clientes y permite que los equipos de clasificación empresarial se integren en sus procedimientos de desarrollo y envío. Consulte [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para obtener más información sobre AEM as a Cloud Service.

Los integrantes del equipo de AEM as a Cloud Service se agregan y asignan a uno o más de los siguientes perfiles de producto a través de Admin Console durante la incorporación.

* **AEM Administradores de** AEM : Un administrador de la se suele asignar a desarrolladores, en particular a desarrolladores que necesitan acceso, por ejemplo, a los entornos de desarrollo. El perfil de producto del administrador de AEM se utiliza para otorgar privilegios de administrador en la instancia de AEM asociada.

* **Usuarios de AEM**: Los usuarios de AEM son los usuarios de su organización que utilizan AEM as a Cloud Service generalmente para crear contenido. AEM Estos usuarios deben acceder a la documentación de para realizar sus tareas a la vez que lo hacen El perfil de producto de los usuarios de AEM suele asignarse a un autor de contenido de AEM que crea y revisa el contenido. Este contenido puede ser de muchos tipos, como páginas, recursos, publicaciones, etc. El perfil de producto de AEM de los usuarios que se muestra a continuación se asigna a estos miembros.

![Perfiles de producto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Todos los usuarios asignados a un perfil de producto de AEM as a Cloud Service tienen acceso de solo lectura a Cloud Manager a través de la función del **Usuario de Cloud Manager**.
>
>Los usuarios con solo la función de **Usuario de Cloud Manager** pueden iniciar sesión en Cloud Manager y navegar a los entornos de creación de AEM (si existen) utilizando las opciones del menú **Programas**. La función de **Usuario de Cloud Manager** no es suficiente para acceder a los detalles del programa. Si se necesita dicho acceso, el administrador del sistema debe otorgar a los usuarios funciones adicionales.

>[!WARNING]
>
>El nombre del perfil del producto **Administradores de AEM** no debe cambiarse. Cambiar el nombre del perfil del producto **Administradores de AEM** quitará los derechos de administrador de todos los usuarios asignados a dicho perfil.

>[!TIP]
>
>* Para obtener más información acerca de los perfiles de producto de AEM, consulte [Asignación de perfiles de producto de AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Para obtener más información sobre el proceso de incorporación, consulte [recorrido de incorporación](/help/journey-onboarding/overview.md).

## Perfiles de producto de Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager tiene perfiles de producto preconfigurados que se pueden considerar como permisos basados en roles. El administrador del sistema es responsable de configurar el equipo de Cloud Manager asignándolo a estos perfiles de producto.

>[!TIP]
>
>Consulte [Permisos basados en funciones en Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obtener más información.

Cada uno de los perfiles de producto tiene permisos específicos asociados a ellos.

* **Propietario del negocio**
   * AEM En este rol tiene permiso para agregar un nuevo programa o editar un programa, agregar o actualizar un entorno, implementar código en un entorno de trabajo o ejecutar comprobaciones de calidad del código de un entorno de trabajo.
   * Este usuario es responsable de definir los indicadores clave de rendimiento (KPI), aprobar implementaciones de producción y anular errores importantes de tres niveles cuando sea necesario.
* **Administrador de implementación**
   * AEM En esta función, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en un entorno de trabajo, o ejecutar comprobaciones de calidad del código en un entorno de trabajo, o bien, ejecutar comprobaciones de calidad del código.
   * Este usuario gestiona las operaciones de implementación y utiliza Cloud Manager para ejecutar implementaciones de ensayo/producción, editar las canalizaciones CI/CD, aprobar errores importantes de tres niveles cuando sea necesario y puede acceder al repositorio de Git.
* **Desarrollador**
   * En este rol, tiene permiso para generar tokens de acceso personal para acceder a Git.
   * Este usuario desarrolla y prueba el código de aplicación personalizado y emplea principalmente Cloud Manager para ver el estado de implementación y puede acceder al repositorio de Git para confirmaciones de código.
* **Administrador de programa**
   * En este rol, tiene permiso para programar canalizaciones, anular las puertas de calidad de tres niveles y proporcionar la aprobación de producción.
   * Este usuario emplea Cloud Manager para realizar la configuración del equipo, revisar el estado y ver los indicadores clave de rendimiento (KPI) y puede aprobar errores importantes de tres niveles cuando sea necesario.

Se puede asignar un usuario a varios perfiles de producto. Por ejemplo, si se asignan ambos roles, **Propietario del negocio** y **Administrador de implementación** a un usuario, le da la suma de estos permisos.

Su equipo de Cloud Manager incluirá al menos lo siguiente:

* Un **Propietario del negocio**, que suele ser también el administrador del sistema y debe ser la primera persona en iniciar sesión y acceder a Cloud Manager
* Un **Administrador de implementación**
* Un **Desarrollador**

>[!NOTE]
>
>Para que se le conceda acceso a AEM as a Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto: `AEM Users` o `AEM Administrators`. Los permisos para administrar Cloud Manager no serán suficientes.

>[!TIP]
>
>* Para obtener más información sobre los perfiles de producto de Cloud Manager, consulte [Asignación de integrantes del equipo a perfiles de producto de Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Para obtener más información sobre el proceso de incorporación, consulte [recorrido de incorporación](/help/journey-onboarding/overview.md).
