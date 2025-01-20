---
title: Cambios en la sincronización de grupos de usuarios y perfil de producto
description: Información sobre los cambios en la sincronización de grupos de usuarios y perfiles de producto que llegan a AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: cddfcddc0ca3652270bdb735e580386ac9ff1fc7
workflow-type: ht
source-wordcount: '361'
ht-degree: 100%

---

# Cambios en la sincronización de grupos de usuarios y perfil de producto {#changes-in-user-group-and-product-profile-synchronization}

Cada vez que se inicia sesión en AEM as a Cloud Service o se utiliza un token de acceso, los grupos de usuarios, perfiles de producto y servicios de perfil de producto de Adobe Admin Console se sincronizan con el repositorio de AEM como grupos.

Con las versiones de AEM superiores a 18751 (el 27 de enero se comenzará a lanzar una versión de mantenimiento en los entornos de producción), para reducir el desorden de la interfaz de usuario y optimizar el rendimiento, se producirán algunos cambios en el comportamiento de sincronización, lo que hará que aparezcan menos grupos en AEM. Se eliminarán dos categorías de grupos de AEM:

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

