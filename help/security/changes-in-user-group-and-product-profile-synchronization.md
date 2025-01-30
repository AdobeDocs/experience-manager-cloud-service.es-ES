---
title: Cambios en la sincronización de grupos de usuarios y perfil de producto
description: Información sobre los cambios en la sincronización de grupos de usuarios y perfiles de producto que llegan a AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: 5c103fcce1ae47bc89f4f572d89967c62c1f7603
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 79%

---

# Cambios en la sincronización de grupos de usuarios y perfil de producto {#changes-in-user-group-and-product-profile-synchronization}

Cada vez que se inicia sesión en AEM as a Cloud Service o se utiliza un token de acceso, los grupos de usuarios, perfiles de producto y servicios de perfil de producto de Adobe Admin Console se sincronizan con el repositorio de AEM como grupos.

AEM A partir de la 19149 de la versión de mantenimiento de la, el comportamiento de sincronización de grupos se cambia para reducir el desorden de la IU y optimizar el rendimiento. AEM En concreto, ya no se sincronizará la pertenencia a grupos de usuarios de las dos categorías de grupos de usuarios que se indican a continuación:

1. Grupos de AEM con sufijo `GROUP_NAME_SUFFIX`. Estos grupos no aparecen en Adobe Developer Console, pero sí en la pantalla Administración de grupos de AEM, como se muestra a continuación. En el improbable caso de que su aplicación AEM haga referencia a estos grupos, asegúrese de usar grupos de usuarios de Adobe Admin Console sin ese sufijo.

   ![Grupos eliminados 1](/help/security/assets/removed-groups-1.png)

1. Los grupos de AEM asociados a los perfiles de producto de Adobe Admin Console no relacionados con el entorno específico. Esto puede incluir perfiles de producto que:

   * estén relacionados con otros productos de Adobe
   * estén relacionados con otros programas de AEM
   * estén relacionados con otros entornos de AEM en el mismo programa de AEM
   * estén relacionados con Cloud Manager (por ejemplo, `Business Owner - Cloud Service`)

   Por ejemplo, en la imagen siguiente, hay muchas filas con el patrón `AEM Administrators-<suffix>` o `AEM Users-<suffix>` donde el sufijo no está relacionado con el entorno actual.

   ![Grupos eliminados 2](/help/security/assets/removed-groups-2.png)

Puede comprobar qué sufijo está relacionado con el entorno actual seleccionando Administrar **Acceso - Perfiles de autor** (o **Perfiles de publicación**) en el menú de acción del entorno en Cloud Manager.

![Comprobar sufijos](/help/security/assets/suffix-check.png)

Esto le llevará a Adobe Admin Console, como se muestra en la captura de pantalla siguiente. Tenga en cuenta que `<suffix>` puede ser un conjunto aleatorio de caracteres o más bien el nivel y los identificadores de programa y entorno (por ejemplo, `author - Program 12345 - Environment 45678`).

![Sufijos en Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

En el improbable caso de que la aplicación AEM haga referencia a un grupo que ya no va a aparecer en AEM, asegúrese de usar en su lugar i) un perfil de producto de la instancia correcta de AEM o ii) un grupo de usuarios de Adobe Admin Console.

Las pertenencias de grupo del usuario se sincronizan cuando inicia sesión en el entorno y se eliminan de los grupos no relacionados con el entorno actual. Los propios grupos permanecen e incluyen usuarios que no han iniciado sesión desde que se habilitó la función.
