---
title: Administración de principales
description: Administración de identidades para la migración, con Admin Console
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 1%

---

# Administración de principales {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Administración de principales"
>abstract="Descubra qué se debe hacer para administrar usuarios durante o después de una migración de contenido"

Antes de transferir contenido al entorno de nube de AEM as a Cloud Service, hay algunas tareas que se pueden llevar a cabo en el Admin Console.  Son: crear usuarios, crear grupos y asignar usuarios a grupos; estos usuarios y grupos existirán en IMS, el servicio Identity Management de Adobe, que se utiliza para administrar usuarios y grupos para todos los servicios basados en la nube de Adobe.

### Creación de grupos y sus usuarios en Admin Console

[Uso del Admin Console AEM para entidades principales de](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) proporciona instrucciones detalladas sobre cómo crear usuarios y grupos en IMS y cómo agregar los usuarios a los grupos al mismo tiempo o más tarde.  El documento incluye tres opciones para crearlos: manualmente a través del Admin Console, a través de la carga de CSV a través del Admin Console y a través de una herramienta de sincronización de usuarios.

La opción manual permite crear un grupo o usuario a la vez; la carga de CSV permite crear y vincular varios usuarios y grupos a la vez; y la herramienta de sincronización de usuarios permite utilizar un IDP existente para crear y administrar los usuarios y grupos de IMS.

AEM AEM Una vez que un usuario utiliza IMS para iniciar sesión en el servicio de mensajería, se crea una representación del usuario que se utiliza en el servicio de administración de correo electrónico  AEM AEM Además, cualquier grupo de IMS en el que se encuentre el usuario tendrá grupos de equivalentes creados en el mismo  AEM Estos usuarios y grupos de usuarios creados por IMS aún se administran principalmente mediante el Admin Console.

Una vez completada la migración de contenido, los grupos de IMS generalmente necesitan tener alguna configuración adicional para que los usuarios puedan acceder al contenido migrado.  Ver [Migrar identidades después de la migración](/help/journey-migration/managing-principals-after-migration.md)

AEM AEM Consulte también [Tutorial, usuarios, grupos y permisos de la](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) para obtener más información acerca de cómo se integran y administran los usuarios y grupos de IMS de y de los usuarios de IMS.
