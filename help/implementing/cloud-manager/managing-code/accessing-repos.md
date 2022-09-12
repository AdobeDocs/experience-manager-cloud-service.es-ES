---
title: Acceso a repositorios
description: Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---

# Acceso a repositorios {#accessing-repos}

Obtenga información sobre cómo acceder y administrar su repositorio de Git mediante la administración de cuentas de Git de autoservicio desde Cloud Manager.

## Uso de la Administración de Cuentas de Repositorio de Autoservicio {#self-service-repos}

Cloud Manager facilita la recuperación de la información del repositorio mediante el uso de la variable **Acceder a información de repositorios** botón disponible de forma destacada en la tarjeta de canalización.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a **Canalizaciones** tarjeta de su **Información general del programa** y busque **Acceder a información de repositorios** para acceder y administrar su Repositorio de Git.

   ![Botón Acceder a Información de Repositorio en la tarjeta Entornos](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. Haga clic en el **Ver información de repositorios** para abrir un cuadro de diálogo para ver:

   * Dirección URL del repositorio de Git de Cloud Manager.
   * El nombre de usuario de Git.
   * La contraseña de Git, cuyo valor se muestra cuando se usa la variable **Generar contraseña** se hace clic en el botón .

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

Con estas credenciales, el usuario puede clonar una copia local del repositorio y realizar cambios en ese repositorio local, y cuando esté listo, puede volver a enviar cualquier cambio de código al repositorio de código remoto en Cloud Manager.

La variable **Acceder a información de repositorios** también está disponible en la **No producción** la pestaña canalización de **Canalizaciones** tarjeta.

![Botón Acceder a Información de Repositorio en la ficha que no es de producción](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>La variable **Acceder a información de repositorios** es visible para los usuarios con **Desarrollador** o **Administrador de implementación** funciones.
