---
title: Asignación de miembros del equipo a perfiles de producto de Cloud Manager
description: Siga esta página para obtener información sobre cómo asignar miembros del equipo a perfiles de producto de Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# Asignar integrantes del equipo a perfiles de producto de Cloud Manager {#assign-team-members}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá a asignar miembros del equipo a perfiles de producto de Cloud Manager.

## Objetivo {#objective}

En el paso anterior de este recorrido, [Acceso al Admin Console,](admin-console.md) ahora ha aprendido a iniciar sesión en el Admin Console y comprobar sus privilegios como administrador del sistema. Ya está listo para permitir que los miembros de su equipo tengan acceso a Cloud Manager. Para ello, debe asignar perfiles de producto.

Al conceder a los usuarios acceso a una solución de Adobe, no necesariamente desea darles acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario. El Admin Console se utiliza para asignar perfiles de producto.

El primer paso es otorgar a los usuarios acceso a Cloud Manager. Cloud Manager le ofrece asistencia con las configuraciones de desarrollo empresarial y sus canalizaciones de CD/CI creadas específicamente, que están equipadas para garantizar pruebas exhaustivas y la máxima calidad del código para ofrecer experiencias excepcionales.

Después de leer este documento, debería poder hacer lo siguiente:

* Comprenda cuáles son los perfiles de producto.
* Comprenda qué es Cloud Manager.
* Conozca los tres perfiles de producto importantes de Cloud Manager: **Propietario empresarial**, **Administrador de implementación** y **Desarrollador**.
* Puede asignar miembros del equipo a perfiles de producto de Cloud Manager.

## Requisitos previos {#prerequisites}

Para asignar integrantes del equipo a perfiles de producto, necesitará tener detalles sobre los integrantes del equipo, que deberán acceder a AEM as a Cloud Service, lo que incluye:

* Nombres
* Direcciones de correo electrónico
* Funciones y responsabilidades

>[!TIP]
>
>Con el fin de realizar la incorporación, Adobe recomienda que agregue inicialmente usuarios que participarán en las tareas inmediatas, como administradores, desarrolladores y autores de contenido.
>
>Puede continuar con el proceso de incorporación sin agregar todos los usuarios. Una vez que haya terminado la incorporación, puede agregar usuarios adicionales.

## Perfiles de producto {#product-profiles}

Al conceder a los usuarios acceso a una solución de Adobe, no necesariamente desea darles acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario que se establecen con el Admin Console .

Por ejemplo, más adelante en este recorrido utilizará el Admin Console para otorgar a los usuarios acceso a la solución AEM asignando perfiles de producto para administradores AEM y autores AEM.

Sin embargo, el siguiente paso es conceder perfiles de producto para que los integrantes del equipo tengan acceso primero a Cloud Manager.

## Cloud Manager {#cloud-manager}

Como administrador del sistema, sabe que un proyecto as a Cloud Service AEM exitoso depende no solo de la creación de contenido asombroso mediante AEM, sino también del desarrollo y la implementación de su propio código personalizado y aplicaciones para entregar su contenido AEM.

Cloud Manager es una parte integral de AEM as a Cloud Service y se utiliza para administrar sus canalizaciones de CI/CD para la implementación de código, administrar sus repositorios de código y administrar sus entornos.

Para que su equipo pueda hacer cualquier otra cosa, debe integrarlos en Cloud Manager otorgándoles los perfiles de producto necesarios. Los siguientes pasos le muestran dónde encontrar el perfil de producto de Cloud Manager mediante el Admin Console y cómo asignarlo a los integrantes del equipo.

## Revisar perfiles de producto de Cloud Manager {#review-product-profiles}

Con el Admin Console puede ver la lista de perfiles de Cloud Manager.

1. Inicie sesión en Adobe Admin Console en [adminconsole.adobe.com](https://adminconsole.adobe.com/) y **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![AEM como producto](/help/journey-onboarding/assets/assign-team1.png)

1. Vaya a la **Cloud Manager** de la lista de todas las instancias.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Verá la lista de perfiles de producto preconfigurados de Cloud Manager.

   ![Perfiles de producto](/help/journey-onboarding/assets/assign-team3.png)

Los perfiles más importantes que se deben asignar como parte del proceso de incorporación inicial son:

* **Propietario empresarial** - Estos usuarios administran diferentes programas.
* **Administrador de implementación** : Estos usuarios implementan código de sus repositorios en entornos AEM en ejecución.
* **Desarrollador** - Estos usuarios desarrollan sus aplicaciones de AEM personalizadas y envían código a sus repositorios.

Sabiendo cuáles son estas funciones y qué hacen, revise su lista de integrantes del equipo para determinar quién necesita qué perfil. Tenga en cuenta que los usuarios pueden tener y a menudo tienen múltiples funciones en el equipo y, por lo tanto, también necesitan múltiples perfiles.

## Asignar el perfil de producto del propietario del negocio {#assign-business-owner}

Ya está listo para agregar usuarios y asignarlos al **Propietario empresarial** perfil de producto.

1. Identifique a los usuarios que necesitan administrar los programas de Cloud Manager. Estos serán sus **Propietarios de empresas**.

1. Inicie sesión en el Admin Console en `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` y **Información general** página, seleccione **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior, seleccione **Agregar usuario**.

   ![Adición del usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Añadir detalles del usuario](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Propietario empresarial** perfil de producto para el usuario.

   * Asigne cada usuario al menos a un perfil de producto para que el usuario pueda acceder a Cloud Manager.
   * Recuerde asignarse como administrador del sistema a **Propietario empresarial** función.

   ![Asignación de usuarios](/help/journey-onboarding/assets/assign-team6.png)

1. Haga clic en **Guardar** y se envía un correo electrónico de bienvenida al usuario que ha añadido. El usuario invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

1. Repita estos pasos para los usuarios de su equipo.

Su **Propietario empresarial** Se han asignado y ahora puede acceder a Cloud Manager. No olvide asignarse como administrador del sistema al **Propietario empresarial** perfil.

## Asignar el perfil de producto del administrador de implementación {#assign-deployment-manager}

1. Identifique a los usuarios que necesitan implementar código.

1. Inicie sesión en el Admin Console en `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` y **Información general** selección de página **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior y, a continuación, seleccione **Agregar usuario**.

   ![Adición del usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En el **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Introducir ID](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Administrador de implementación** perfil de producto para el usuario.

   ![Asignar perfil](/help/journey-onboarding/assets/assign-team6.png)

Su **Administrador de implementación** Se han asignado y ahora puede acceder a Cloud Manager. Según sus responsabilidades futuras, puede que también deba asignarse como administrador del sistema a **Administrador de implementación** perfil.

## Asignar el perfil de producto del desarrollador {#assign-developer}

1. Identifique a los usuarios que necesitan desarrollar aplicaciones AEM y administrar código.

1. Inicie sesión en el Admin Console en `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` y **Información general** selección de página **Adobe Experience Manager as a Cloud Service** producto de **Productos y servicios** tarjeta.

   ![Productos y servicios](/help/journey-onboarding/assets/assign-team1.png)

1. Seleccione el **Usuarios** en la barra de navegación superior y, a continuación, seleccione **Agregar usuario**.

   ![Adición del usuario](/help/journey-onboarding/assets/assign-team4.png)

1. En **Agregar usuarios a su equipo** , introduzca el ID de correo electrónico del usuario que desea agregar.

   * Si el Federated ID para los integrantes del equipo aún no se ha configurado, seleccione **Adobe ID** para el **Tipo de ID**.

   ![Agregar ID de usuario](/help/journey-onboarding/assets/assign-team5.png)

1. Haga clic en el botón más debajo de la etiqueta **Seleccionar productos o grupos de usuarios** encabezado para comenzar la selección de productos y seleccionar **Adobe Experience Manager as a Cloud Service** y asigne **Desarrollador** perfil de producto para el usuario.

   ![Asignar perfil](/help/journey-onboarding/assets/assign-team6.png).

Su **Desarrollador** Se han asignado y ahora puede acceder a Cloud Manager. Según sus responsabilidades futuras, puede que también deba asignarse como administrador del sistema a **Desarrollador** perfil.

## Siguientes pasos {#whats-next}

Felicitaciones! Su equipo de Cloud Manager recién formado (incluido usted asignado al **Propietario empresarial** ). En el papel de **Propietario empresarial**, ya está a un paso de iniciar sesión en Cloud Manager y de habilitar la creación de sus recursos en la nube.

En esta parte del recorrido de incorporación, ha aprendido a asignar los integrantes del equipo a los perfiles del Admin Console. Ahora debería hacer lo siguiente:

* Comprenda cuáles son los perfiles de producto.
* Comprenda qué es Cloud Manager.
* Conozca los tres perfiles de producto importantes de Cloud Manager: **Propietario empresarial**, **Administrador de implementación** y **Desarrollador**.
* Puede asignar miembros del equipo a perfiles de producto de Cloud Manager.

Ya está listo para continuar con su recorrido de incorporación revisando el documento [Acceso a Cloud Manager,](cloud-manager.md) donde aprenderá a acceder a Cloud Manager y a crear sus recursos de proyecto.

## Recursos adicionales {#additional-resources}

Se recomienda continuar con el recorrido de incorporación como se describió anteriormente. Estos son algunos recursos adicionales si desea profundizar en un tema en particular desde este recorrido.

* [Introducción a Cloud Manager](/help/onboarding/cloud-manager-introduction.md) : Obtenga información sobre Cloud Manager, los programas de Cloud Manager y los entornos.
* [Perfiles de producto de Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md) : Obtenga información sobre AEM equipo as a Cloud Service y los perfiles de producto.
* [Tipos de identidad en Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) : el sistema de administración de identidades de Adobe ayuda a los administradores a crear y administrar el acceso del usuario a aplicaciones y servicios. Adobe ofrece estos tipos de identidades o cuentas para autenticar y autorizar a los usuarios.

