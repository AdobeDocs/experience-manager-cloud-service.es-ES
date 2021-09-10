---
title: Acceso a repositorios
seo-title: Accessing Repositories
description: Esta página describe cómo puede acceder y administrar el repositorio Git.
seo-description: Follow this page to learn how to access and manage your Git repository.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# Acceso a repositorios {#accessing-repos}

Puede acceder a su repositorio Git y administrarlo mediante la administración de cuentas Git de autoservicio desde la interfaz de usuario de Cloud Manager.

## Uso de la administración de cuentas de repositorios de autoservicio {#self-service-repos}

Utilice el botón **Access Repo Info** disponible en la interfaz de usuario de Cloud Manager, de forma más destacada en la tarjeta de canalización.

1. Vaya a la tarjeta **Canalizaciones** desde la página **Información general del programa**.

1. Verá la opción **Access Repo Info** para acceder y administrar su repositorio Git.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

   Además, si selecciona la pestaña **Non-Production** canalización, también verá la opción **Access Repo Info**.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >La opción **Access Repo Info** es visible para los usuarios con la función de Desarrollador o Administrador de implementación. Al hacer clic en este botón, se abre un cuadro de diálogo que permite al usuario encontrar la URL de su repositorio Git de Cloud Manager junto con su nombre de usuario y contraseña.

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

   Las consideraciones importantes para administrar su Git en Cloud Manager son:

   * **URL**: La URL del repositorio
   * **Nombre de usuario**: El nombre de usuario
   * **Contraseña**: Valor que se muestra cuando se hace clic en el botón **Generar contraseña**.


      >[!NOTE]
      >Un usuario puede extraer una copia de su código y realizar cambios en el repositorio de código local. Cuando esté listo, el usuario puede devolver los cambios de código al repositorio de código remoto en Cloud Manager.
