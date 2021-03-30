---
title: 'Tareas del administrador del sistema '
description: Siga esta página para aprender a añadir usuarios y asignarlos a funciones de Cloud Manager como administrador del sistema
translation-type: tm+mt
source-git-commit: fdf8416b281b14e3dd49d1e28c3c241ddfd2d342
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Tareas del administrador del sistema {#add-users-assign}

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
