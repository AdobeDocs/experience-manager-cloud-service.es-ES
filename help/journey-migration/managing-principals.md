---
title: Administración de principales
description: Administración de principales para la migración mediante Admin Console
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# Administración de principales {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Administración de principales"
>abstract="Descubra qué se debe hacer para administrar usuarios durante o después de una migración de contenido"

Antes de transferir contenido al entorno en la nube de AEM as a Cloud Service, hay algunas tareas que se pueden llevar a cabo en Admin Console.  Estas tareas son crear usuarios, crear grupos y asignar usuarios a grupos; estos usuarios y grupos existirán en IMS, el servicio Identity Management de Adobe, que se utiliza para administrar usuarios y grupos para todos los servicios basados en la nube de Adobe.

## Creación de grupos y sus usuarios en Admin Console

[Uso de Admin Console para principales de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) proporciona instrucciones detalladas sobre cómo crear usuarios y grupos en IMS, y cómo añadir los usuarios a los grupos al mismo tiempo o más tarde.  El documento incluye tres opciones para crearlos: manualmente con Admin Console, con la carga de CSV a través de Admin Console y con una herramienta de sincronización de usuarios.

La opción manual permite crear un grupo o usuario a la vez; la carga de CSV permite crear y vincular varios usuarios y grupos a la vez; y la herramienta de sincronización de usuarios permite utilizar un IDP existente para crear y administrar los usuarios y grupos de IMS.

Una vez que un usuario utiliza IMS para iniciar sesión en AEM, se creará una representación de AEM del usuario.  Además, todos los grupos de IMS en los que se encuentre el usuario tendrán grupos de AEM equivalentes creados en AEM.  Estos usuarios y grupos de AEM creados por IMS se siguen administrando principalmente mediante Admin Console.

Una vez completada la migración de contenido, los grupos de IMS generalmente necesitan tener alguna configuración adicional para que los usuarios puedan acceder al contenido migrado.  Consulte [Migrar principales después de la migración](/help/journey-migration/managing-principals-after-migration.md)

Consulte también [Tutorial de usuarios, grupos y permisos de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) para obtener más información acerca de cómo se integran y administran los usuarios y grupos de IMS y de AEM.
