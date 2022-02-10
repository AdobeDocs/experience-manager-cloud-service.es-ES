---
title: Asignación de miembros del equipo a perfiles de producto de Cloud Manager
description: Siga esta página para obtener información sobre cómo asignar miembros del equipo a perfiles de producto de Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---

# Asignar integrantes del equipo a perfiles de producto de Cloud Manager {#assign-team-members}

En el paso anterior de este recorrido, [Introducción al proceso de incorporación](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md), ya ha aprendido a iniciar sesión en el Admin Console y a ver sus privilegios como administrador del sistema. Ya está listo para asignar miembros del equipo a perfiles de producto de Cloud Manager.

## Objetivo {#objective}

Este documento resume cómo asignar miembros del equipo a perfiles de producto de Cloud Manager desde Adobe Admin Console. Una vez asignados, estos miembros pueden crear recursos de nube de acceso como se describe en el siguiente paso de este recorrido.

Después de leer esta sección debe poder:

* Comprenda por qué y cómo debe agregar miembros del equipo.
* Obtenga información sobre tres perfiles de producto importantes de Cloud Manager: **Propietario empresarial**, **Administrador de implementación** y **Desarrollador**.
* Asigne miembros del equipo a perfiles de producto de Cloud Manager.

>[!TIP]
>
>Con el fin de realizar la incorporación, el Adobe recomienda que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido. Puede continuar con el proceso de incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede agregar usuarios adicionales.

## Requisitos previos {#prerequisites}

Los siguientes requisitos previos deben cumplirse antes de iniciar esta sección. Debe:

* Sea administrador del sistema y comprenda los perfiles de producto de Cloud Manager.
   * Vuelva a la [Información general sobre el Recorrido de integración](onboarding-journey-overview.md) si no está familiarizado con estos conceptos.
* Comprender los conceptos básicos de Adobe Admin Console.
   * Vuelva a la [Información general sobre el Recorrido de integración](onboarding-journey-overview.md) si no está familiarizado con estos conceptos.
* Obtenga información detallada sobre los integrantes del equipo que deberán acceder a AEM as a Cloud Service, incluido
   * Nombres
   * Direcciones de correo electrónico
   * Funciones y responsabilidades

## Revisar perfiles de producto de Cloud Manager {#review-product-profiles}

Desde Adobe Admin Console puede ver la lista de perfiles de Cloud Manager.

1. Inicie sesión en Adobe Admin Console en [adminconsole.adobe.com](https://adminconsole.adobe.com/) y **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![AEM como producto](/help/journey-onboarding/assets/assign-team1.png)

1. Vaya a la **Cloud Manager** de la lista de todas las instancias.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Verá la lista de perfiles de producto preconfigurados de Cloud Manager.

   ![Perfiles de producto](/help/journey-onboarding/assets/assign-team3.png)

## Asignar usuarios al perfil de producto del propietario del negocio {#assign-users-business-owner}

Ya está listo para agregar usuarios y asignarlos al **Propietario empresarial** perfil de producto.

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto Propietario empresarial .

1. Inicie sesión en el Admin Console en [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) y **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior, seleccione **Agregar usuario**.

   ![Agregar usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Añadir detalles del usuario](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Propietario empresarial** perfil de producto para el usuario.

   * Asigne cada usuario al menos a un perfil de producto para que el usuario pueda acceder a Cloud Manager.
   * Recuerde asignarse como administrador del sistema a **Propietario empresarial** función.

   ![Asignación de usuarios](/help/journey-onboarding/assets/assign-team6.png)

1. Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

1. Repita estos pasos para los usuarios de su equipo.

Su equipo de Cloud Manager recién formado (incluido usted asignado al **Propietario empresarial** ). En el papel de **Propietario empresarial**, ya está a un paso de iniciar sesión en Cloud Manager y de habilitar la creación de sus recursos en la nube.

## Asignar usuarios al perfil de producto del administrador de implementación {#assign-users-deployment-manager}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager y agréguelos al perfil de producto de Deployment Manager.

1. Inicie sesión en el Admin Console en [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) y **Información general** selección de página **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior y, a continuación, seleccione **Agregar usuario**.

   ![Agregar usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Introducir ID](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Administrador de implementación** perfil de producto para el usuario.

   ![Asignar perfil](/help/journey-onboarding/assets/assign-team6.png).

## Asignar usuarios al perfil de producto del desarrollador {#assign-users-developer}

1. Identifique a los usuarios que administrarán los programas de Cloud Manager.

1. Inicie sesión en el Admin Console en [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) y **Información general** selección de página **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior y, a continuación, seleccione **Agregar usuario**.

   ![Agregar usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Agregar ID de usuario](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Desarrollador** perfil de producto para el usuario.

   ![Asignar perfil](/help/journey-onboarding/assets/assign-team6.png).

## Siguientes pasos {#whats-next}

En esta parte del recorrido de incorporación, ha aprendido todo sobre la asignación de los integrantes del equipo a las funciones del Admin Console. Ahora debería:

* Comprenda por qué y cómo debe agregar miembros del equipo.
* Comprenda tres perfiles de producto importantes de Cloud Manager: **Propietario empresarial**, **Administrador de implementación** y **Desarrollador**.
* Puede asignar miembros del equipo a perfiles de producto de Cloud Manager.

Ya está listo para continuar con su recorrido de incorporación revisando el documento [Configuración de recursos de Cloud mediante Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), donde aprenderá:

1. Para que otros propietarios de negocios creen programas, usted como administrador de sistemas asignado a la función **Propietario empresarial** , primero debe acceder e iniciar sesión en Cloud Manager.
1. Cómo un usuario con la variable **Propietario empresarial** puede iniciar sesión y configurar sus recursos de la nube, incluidos su programa y entornos de la nube.
1. Cómo los usuarios con la variable **Desarrollador** y **Administrador de implementación** las funciones de pueden acceder a Cloud Manager.

## Recursos adicionales {#additional-resources}

Se recomienda continuar con el recorrido de incorporación como se describió anteriormente. Estos son algunos recursos adicionales si desea profundizar en un tema en particular desde este recorrido.

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Perfiles de producto de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Información general sobre la identidad del Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
