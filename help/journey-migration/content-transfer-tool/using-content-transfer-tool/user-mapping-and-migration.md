---
title: Asignación de usuarios y migración de principales
description: Información general sobre la asignación de usuarios y la migración principal
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 22%

---

# Asignación de usuarios y migración de principales {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema AEM existente a AEM as a Cloud Service. Los usuarios existentes deben asignarse a sus ID de IMS para evitar que se dupliquen en la instancia de autor del Cloud Service."

>[!NOTE]
>Para las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM as a Cloud Service. Esto lo hace la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de Adobe ID para acceder al nivel de creación. Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar los usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en Adobe Identity Management System (IMS) que proporciona el inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). Debido a este cambio, los usuarios existentes deben asignarse a sus ID de IMS para evitar usuarios duplicados en la instancia de autor del Cloud Service. Dado que los grupos de AEM tradicionales son fundamentalmente diferentes de los grupos de IMS, los grupos no están asignados, pero los dos grupos deben conciliarse una vez completada la migración.

## Asignación de usuarios y detalles de migración {#user-mapping-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán todos los usuarios asociados con el contenido que se está migrando. Esta asignación se realiza automáticamente y si se realiza se puede controlar mediante un interruptor antes de que se inicie la extracción. El usuario puede anular la configuración predeterminada de la opción al iniciar la extracción.

* Si el sistema de origen es una instancia de autor, la opción predeterminada para realizar la asignación es _en_, ya que este es el proceso recomendado.
* Si el sistema de origen es una instancia de publicación, de forma predeterminada la opción para realizar la asignación es _off_, ya que los usuarios no se migran normalmente ni se utilizan en instancias de publicación.

## Consideraciones importantes al asignar y migrar usuarios {#important-considerations}


### Casos excepcionales {#exceptional-cases}

Se registran los siguientes casos específicos:

1. Si un usuario no tiene ninguna dirección de correo electrónico en la `profile/email` campo de *jcr* el usuario o grupo en cuestión se puede migrar, pero no se asignará. Este es el caso incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si el usuario está deshabilitado, se trata igual que si no estuviera deshabilitado. Se asigna y migra con normalidad, y permanece deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de AEM de origen, el usuario o grupo en cuestión no se migrará.

1. Si se migra un usuario sin que primero se asigne a través de la Asignación de usuarios, o si su dirección de correo electrónico no coincide con la dirección de correo electrónico usada para iniciar sesión en IMS, en el sistema de la nube de destino no podrán iniciar sesión con su ID de IMS. Es posible que puedan iniciar sesión utilizando el método AEM tradicional, pero tenga en cuenta que esto no es normalmente lo que se desea o se espera.


## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** está configurado, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino y es verdadero para un usuario administrador añadido al grupo **administradores** grupo. El usuario administrador debe agregarse de nuevo al **administradores** grupo para recuperar el token de acceso para CTT.
* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transfieren, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido al que están asociados.
* Si la instancia de AEM Cloud Service de destino tiene un usuario con un nombre de usuario diferente pero la misma dirección de correo electrónico que uno de los usuarios de la instancia de AEM de origen y la Asignación de usuarios está habilitada, se escribe un mensaje de error en los registros y el usuario de AEM de origen no se transfiere, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.
