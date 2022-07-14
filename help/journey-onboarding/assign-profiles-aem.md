---
title: Asignación AEM perfiles de producto
description: Una vez configurados los recursos de nube, deberá otorgar a su equipo acceso a AEM mediante AEM perfiles de producto.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# Asignación AEM perfiles de producto {#assign-profiles-aem}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a otorgar acceso a su equipo a AEM mediante AEM perfiles de producto.

## Objetivo {#objective}

Una vez que haya leído el documento anterior en este recorrido de incorporación, [Crear entornos,](create-environments.md) y tenga configurados los recursos de nube, deberá otorgar a su equipo acceso a AEM mediante perfiles de producto AEM. Como administrador del sistema, puede hacerlo asignando AEM perfiles de producto.

Después de leer este documento debe comprender:

* Qué son AEM perfiles de producto.
* Cómo añadir integrantes del equipo a AEM perfil de producto Usuario.
* Cómo añadir integrantes del equipo al perfil de producto de AEM administradores.

## Perfiles de producto de AEM {#aem-product-profiles}

Para utilizar AEM, los integrantes del equipo deben estar asignados al menos a un perfil de producto AEM. Los permisos para acceder a Cloud Manager no serán suficientes. Los usuarios deben pertenecer a uno de los dos perfiles de producto:

* `AEM Users` - Este grupo incluye usuarios normales que realizan tareas diarias de creación de contenido.
* `AEM Administrators` - Este grupo incluye a los usuarios responsables de las funciones avanzadas o AEM.

Todos los usuarios asignados a un perfil de producto de AEM también tendrán acceso de solo lectura a Cloud Manager. El acceso de escritura a Cloud Manager se puede conceder a través de otros perfiles de producto.

## Requisitos previos {#prerequisites}

Antes de comenzar a leer esta sección, debe tener disponible la siguiente información sobre su equipo, que utilizará AEM.

* Nombres
* Direcciones de correo electrónico
* Funciones y responsabilidades

>[!TIP]
>
>Con el fin de incorporarlo, le recomendamos que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el resto de la incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede escalar a un mayor número de usuarios más adelante.

## Ver perfiles AEM producto {#view-profiles}

Siga estos pasos para ver los perfiles de producto AEM del Admin Console.

1. Inicie sesión en el Admin Console en [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. En el **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Tarjeta de productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Desplácese y seleccione la instancia.

   ![Seleccionar instancia](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Verá la lista de AEM perfiles de producto as a Cloud Service que se pueden asignar a un usuario según sus funciones.

   ![Perfiles de producto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Agregar integrantes del equipo a perfiles de producto {#add-team-members}

Ahora que está familiarizado con los perfiles disponibles, puede asignarlos según sea necesario a los integrantes del equipo.

Estas tareas requieren que sea administrador del sistema con el **Propietario empresarial** Perfil de producto de Cloud Manager.

1. Vaya al programa desde Cloud Manager y seleccione la **Administrar acceso** del contexto del entorno de interés.

   ![Administrar acceso](/help/journey-onboarding/assets/add-team1.png)

1. Una nueva pestaña le lleva al Admin Console desde el que tiene acceso a la instancia de autor del entorno. Select **Administradores de AEM** o **AEM usuarios** en función de los permisos que se le deben otorgar a esta persona.

   ![Asignar acceso](/help/journey-onboarding/assets/add-team2.png)

1. Select `AEM Administrator` o `AEM User` y haga clic en **Agregar usuario** como se muestra a continuación, y envíe los detalles necesarios para completar la adición del miembro del equipo.

   ![Agregar miembro del equipo](/help/journey-onboarding/assets/add-team3.png)

1. Repita estos pasos para todos los entornos, incluidos desarrollo, ensayo y producción, si tiene disponible la información de los integrantes del equipo que necesitan acceso.

El usuario que ha agregado ahora tendrá acceso a los AEM servicios de Autor as a Cloud Service.

## ¿Fin del recorrido? {#the-end}

¡Felicitaciones! Los usuarios que asignó a AEM perfiles de producto as a Cloud Service ahora están listos para acceder al entorno de creación de AEM y comenzar a crear contenido con AEM as a Cloud Service. Del mismo modo, los desarrolladores ahora pueden acceder a Cloud Manager para utilizar Git para almacenar código de aplicación personalizado e implementarlo. En este sentido, el recorrido de incorporación se ha completado y los usuarios ahora pueden utilizar AEMaaCS.

Sin embargo, si desea comprender mejor cómo utilizan el sistema los autores y desarrolladores, puede continuar con dos partes opcionales de este recorrido de integración:

* [Tareas del desarrollador y del administrador de implementación](developers.md) : aquí aprenderá cómo acceden los desarrolladores a Git para almacenar su código personalizado e implementarlo mediante canalizaciones de Cloud Manager.
* [Tareas del usuario AEM](aem-users.md) - Dónde aprenderá a acceder al entorno de AEM donde puede empezar a crear contenido.

## Recursos adicionales {#additional-resources}

* [Administración de productos y acceso de usuarios en Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) : Aprenda a utilizar el Admin Console para administrar el acceso de uso.
* [Configuración del acceso a AEM guía](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en) : Consulte esta explicación abreviada para obtener más información sobre la configuración de los usuarios de IMS de Adobe, los grupos de usuarios y los perfiles de producto en el Admin Console.

