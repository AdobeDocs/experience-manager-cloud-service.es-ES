---
title: Asignar perfiles de producto de AEM
description: Una vez configurados los recursos de la nube, deberá otorgar a su equipo acceso a AEM mediante perfiles de producto de AEM.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '878'
ht-degree: 100%

---

# Asignar perfiles de producto de AEM {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="Asignar perfiles de producto de AEM"
>abstract="No tiene derecho a utilizar Experience Manager Assets. Póngase en contacto con su administrador o administradora."

En esta parte del [recorrido de incorporación](overview.md), aprenderá a conceder acceso a su equipo a AEM mediante los perfiles de producto de AEM.

## Objetivo {#objective}

Una vez que haya leído el documento anterior, [Creación de entornos](create-environments.md), de este recorrido de incorporación, y tenga configurados los recursos de la nube, deberá conceder a su equipo acceso a AEM mediante los perfiles de producto de AEM. Como administrador del sistema, puede hacerlo asignando perfiles de producto de AEM.

Después de leer este documento, debería poder comprender lo siguiente:

* Qué son los perfiles de producto de AEM.
* Añadir integrantes del equipo al perfil de producto Usuario de AEM.
* Añadir integrantes del equipo al perfil de producto Administradores de AEM.

## Perfiles de producto de AEM {#aem-product-profiles}

Para utilizar AEM, los integrantes del equipo deben estar asignados al menos a un perfil de producto de AEM. Los permisos para acceder a Cloud Manager no serán suficientes. Los usuarios deben pertenecer a uno de los dos perfiles de producto:

* `AEM Users`: Este grupo incluye usuarios normales que realizan tareas diarias de creación de contenido.
* `AEM Administrators`: Este grupo incluye a los usuarios responsables de las funciones avanzadas o AEM.

>[!NOTE]
>
>Todos los usuarios asignados a un perfil de producto de AEM as a Cloud Service tienen acceso de solo lectura a Cloud Manager a través de la función del **Usuario de Cloud Manager**.
>
>Los usuarios con solo la función de **Usuario de Cloud Manager** pueden iniciar sesión en Cloud Manager y navegar a los entornos de creación de AEM (si existen) utilizando las opciones del menú Programas. La función de **Usuario de Cloud Manager** no es suficiente para acceder a los detalles del programa. Si se necesita dicho acceso, el administrador del sistema debe otorgar a los usuarios funciones adicionales.
>Consulte la [Sección Recursos adicionales a continuación](#additional-resources) para obtener más información sobre las funciones de usuario de Cloud Manager.

>[!CAUTION]
>
>No edite ni elimine los perfiles de producto llamados Administradores de AEM o Usuarios de AEM. La edición de estos nombres de perfil puede interrumpir el inicio de sesión en la instancia de la nube de AEM.

## Requisitos previos {#prerequisites}

Antes de comenzar a leer esta sección, debe tener disponible la siguiente información sobre su equipo, que utilizará AEM.

* Nombres
* Direcciones de correo electrónico
* Funciones y responsabilidades

>[!TIP]
>
>Con el fin de realizar la incorporación, Adobe recomienda que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.

## Ver perfiles de producto de AEM {#view-profiles}

Siga estos pasos para ver los perfiles de producto de AEM desde Admin Console.

1. Inicie sesión en Admin Console en [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

1. Desde la página **Información general**, seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios**.

   ![Tarjeta Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Desplácese y seleccione la instancia.

   ![Seleccionar instancia](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Verá la lista de perfiles de producto de AEM as a Cloud Service que se pueden asignar a un usuario según sus funciones.

   ![Perfiles de producto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Agregar integrantes del equipo a perfiles de producto {#add-team-members}

Ahora que está familiarizado con los perfiles disponibles, puede asignarlos según sea necesario a los integrantes del equipo.

Estas tareas requieren que sea administrador del sistema con el perfil de producto de Cloud Manager **Propietario empresarial**.

1. Vaya al programa desde Cloud Manager y seleccione el botón **Administrar acceso** del contexto del entorno de interés.

   ![Administrar acceso](/help/journey-onboarding/assets/add-team1.png)

1. Una nueva pestaña le lleva a Admin Console desde el que tiene acceso a la instancia de autor del entorno. Seleccione **Administradores de AEM** o **Usuarios de AEM** en función de los permisos que se le deben otorgar a esta persona.

   ![Asignar acceso](/help/journey-onboarding/assets/add-team2.png)

1. Seleccione `AEM Administrator` o `AEM User` y haga clic en **Agregar usuario** como se muestra a continuación, y envíe los detalles necesarios para completar la adición del miembro del equipo.

   ![Agregar miembro del equipo](/help/journey-onboarding/assets/add-team3.png)

1. Repita estos pasos para todos los entornos, incluidos desarrollo, ensayo y producción, si tiene disponible la información de los integrantes del equipo que necesitan acceso.

El usuario que ha agregado ahora tendrá acceso a los servicios de autor de AEM as a Cloud Service.

## ¿Fin del recorrido? {#the-end}

¡Enhorabuena! Los usuarios que asignó a perfiles de producto de AEM as a Cloud Service ahora están listos para acceder al entorno de creación de AEM y comenzar a crear contenido con AEM as a Cloud Service. Del mismo modo, los desarrolladores ahora pueden acceder a Cloud Manager para utilizar Git para almacenar código de aplicación personalizado e implementarlo. En este sentido, el recorrido de incorporación se ha completado y los usuarios ahora pueden utilizar AEMaaCS.

Sin embargo, si desea comprender mejor cómo utilizan el sistema los autores y desarrolladores, puede continuar con dos partes opcionales de este recorrido de integración:

* [Tareas del desarrollador y del administrador de implementación](developers.md): aquí aprenderá cómo acceden los desarrolladores a Git para almacenar su código personalizado e implementarlo mediante canalizaciones de Cloud Manager.
* [Tareas del usuario de AEM](aem-users.md): aquí aprenderá a acceder al entorno de AEM donde puede empezar a crear contenido.

## Recursos adicionales {#additional-resources}

Los siguientes son recursos opcionales adicionales si desea ir más allá del contenido del recorrido de incorporación.

* [Perfiles de producto y equipo de AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md): aprenda cómo los perfiles de producto y equipo de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones con licencia de Adobe.
* [Administración de productos y acceso de usuarios en Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console): aprenda a utilizar Admin Console para administrar el acceso de uso.
* [Guía de configuración del acceso a AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=es): consulte esta explicación abreviada para obtener más información sobre la configuración de los usuarios de IMS de Adobe, los grupos de usuarios y los perfiles de producto en el Admin Console.

