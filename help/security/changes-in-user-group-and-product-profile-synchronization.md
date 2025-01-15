---
title: Cambios en la sincronización de grupos de usuarios y perfiles de producto
description: Obtenga información acerca de los cambios en la sincronización de grupos de usuarios y perfiles de producto que llegan a AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 0b097ab3-bf1d-4d43-9e19-d544594844ef
source-git-commit: cddfcddc0ca3652270bdb735e580386ac9ff1fc7
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Cambios en la sincronización de grupos de usuarios y perfiles de producto {#changes-in-user-group-and-product-profile-synchronization}

Cada vez que un usuario inicia sesión en AEM as a Cloud Service o se utiliza un token de acceso, los grupos de usuarios, los perfiles de producto y los servicios de perfil de producto de Adobe Admin Console AEM se sincronizan en el repositorio de como grupos.

AEM AEM Con versiones superiores a 18751 (una versión de mantenimiento comenzará a implementarse en los entornos de producción el 27 de enero), para reducir el desorden de la interfaz de usuario y optimizar el rendimiento, se producirán algunos cambios en el comportamiento de sincronización, lo que dará como resultado que aparezcan menos grupos en las versiones de. AEM Se eliminarán dos categorías de grupos de:

1. AEM Grupos con el sufijo `GROUP_NAME_SUFFIX`. Estos grupos no aparecen en Adobe Developer Console AEM, pero sí en la pantalla Administración de grupos de informes, como se muestra a continuación. AEM En el improbable caso de que la aplicación haga referencia a estos grupos, asegúrese de hacer referencia a grupos de usuarios de Adobe Admin Console sin ese sufijo en su lugar.

   ![Grupos eliminados 1](/help/security/assets/removed-groups-1.png)

1. AEM grupos de productos asociados con perfiles de producto de Adobe Admin Console no relacionados con el entorno específico. Esto puede incluir perfiles de producto que son:

   * relacionados con otros productos de Adobe
   * AEM relacionado con otros programas de la
   * AEM AEM relacionado con otros entornos de en el mismo programa de
   * relacionado con Cloud Manager (por ejemplo, `Business Owner - Cloud Service`)

   Por ejemplo, en la imagen siguiente, hay muchas filas con el patrón `AEM Administrators-<suffix>` o `AEM Users-<suffix>` donde el sufijo no está relacionado con el entorno actual.

   ![Grupos eliminados 2](/help/security/assets/removed-groups-2.png)

Puede comprobar qué sufijo está relacionado con el entorno actual seleccionando Administrar **Acceso - Perfiles de autor** (o **Perfiles de Publish**) en el menú de acción del entorno en Cloud Manager.

![Comprobar sufijos](/help/security/assets/suffix-check.png)

Navegará a Adobe Admin Console, como se muestra en la captura de pantalla siguiente. Tenga en cuenta que `<suffix>` puede ser un conjunto aleatorio de caracteres o más bien el nivel y los identificadores de programa y entorno (por ejemplo, `author - Program 12345 - Environment 45678`).

![Sufijos en el Admin Console](/help/security/assets/admin-console-profile-suffixes.png)

AEM AEM AEM En el improbable caso de que la aplicación haga referencia a un grupo que ya no aparecerá en la aplicación, asegúrese de usar en su lugar i) un perfil de producto de la instancia correcta de la aplicación o ii) un grupo de usuarios de Adobe Admin Console, en su lugar, un perfil de producto de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la.

