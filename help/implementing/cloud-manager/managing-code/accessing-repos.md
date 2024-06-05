---
title: Acceso a repositorios
description: Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 85%

---


# Acceso a repositorios {#accessing-repos}

Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.

## Uso de la administración de cuentas de repositorio de autoservicio {#self-service-repos}

Cloud Manager facilita la recuperación de la información del repositorio mediante el uso del botón **Acceder a la info del repositorio** disponible de forma destacada en la tarjeta de canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la tarjeta **Canalizaciones** de la página **Información general del programa** y busque el botón **Acceder a la info del repositorio** para acceder y administrar su repositorio de Git.

   ![Botón Acceder a la info del repositorio en la tarjeta Entornos](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Haga clic en el botón **Ver información de repositorios** para abrir un cuadro de diálogo para ver lo siguiente:

   * La dirección URL del repositorio de Git de Cloud Manager.
   * El nombre de usuario de Git.
   * La contraseña de Git, cuyo valor se muestra cuando se hace clic en el botón **Generar contraseña**.

   ![Vista de información de repositorios](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con estas credenciales, el usuario puede clonar una copia local del repositorio y realizar cambios en ese repositorio local, y cuando esté listo, puede volver a enviar cualquier cambio de código al repositorio de código remoto en Cloud Manager.

La opción **Acceder a la info del repositorio** también está disponible en la pestaña de la canalización **No producción** de la tarjeta **Canalizaciones**.

![Botón Acceder a la info del repositorio en la pestaña No producción](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>La opción **Acceder a la info del repositorio** es visible para los usuarios con funciones **Desarrollador** o **Administrador de implementación**.

## Revocar una contraseña de acceso {#revoke-password}

Puede revocar una contraseña de acceso en cualquier momento. Para ello, por favor [cree un ticket de asistencia para esta solicitud.](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;support-tab=home#support)

El billete se tratará con alta prioridad y debe ser revocado en el plazo de un día.
