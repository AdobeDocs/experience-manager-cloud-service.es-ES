---
title: Asignación de usuarios y migración de principales
description: Información general sobre asignación de usuarios y migración de principales
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 25bfcd521e9bbc54bff3b87d17cdeb0f99a68511
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 21%

---

# Asignación de usuarios y migración de principales {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema AEM existente a AEM as a Cloud Service. Los usuarios existentes deben asignarse a sus ID de IMS para evitar que se dupliquen en la instancia de creación de Cloud Service."

>[!NOTE]
>Para ver las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM as a Cloud Service. Esto lo hace la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de Adobe ID para acceder al nivel de creación. Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar los usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en Adobe Identity Management System (IMS) que proporciona el inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). Debido a este cambio, los usuarios existentes deben asignarse a sus ID de IMS para evitar usuarios duplicados en la instancia de autor del Cloud Service. AEM Dado que los grupos de los grupos tradicionales son fundamentalmente diferentes de los grupos de IMS, los grupos no se asignan, pero los dos conjuntos de grupos deben reconciliarse una vez completada la migración.

## Asignación de usuarios y detalles de migración {#user-mapping-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán todos los usuarios asociados con el contenido que se está migrando. Esta asignación se realiza automáticamente y se puede controlar mediante un conmutador antes de iniciar la extracción. El usuario puede anular la configuración predeterminada de la opción al iniciar la extracción.

* Si el sistema de origen es una instancia de autor, la opción predeterminada para realizar la asignación es _el_, ya que este es el proceso recomendado.
* Si el sistema de origen es una instancia de publicación, la opción predeterminada para realizar la asignación es _desactivado_, ya que los usuarios no se migran ni utilizan normalmente en instancias de publicación.

## Consideraciones importantes a la hora de asignar y migrar usuarios {#important-considerations}


### Casos excepcionales {#exceptional-cases}

Se registran los siguientes casos específicos:

1. Si un usuario no tiene una dirección de correo electrónico en `profile/email` campo de su *jcr* el usuario o grupo en cuestión puede migrarse, pero no asignarse. Este es el caso incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si el usuario está deshabilitado, se trata igual que si no lo estuviera. Se asigna y migra con normalidad y permanece deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service AEM de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen, no se migrará el usuario o grupo en cuestión.

1. Si se migra un usuario sin asignarlo primero mediante Asignación de usuarios, o si su dirección de correo electrónico no coincide con la utilizada para iniciar sesión en IMS, no podrá iniciar sesión con su ID de IMS en el sistema de la nube de destino. AEM Es posible que puedan iniciar sesión utilizando el método tradicional de, pero tenga en cuenta que esto no suele ser lo que se quiere o se espera.


## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** se ha configurado, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece todos los ajustes, incluidos los permisos, en la instancia del Cloud Service de destino y es verdadero para un usuario administrador añadido a **administradores** grupo. El usuario administrador debe volver a agregarse al **administradores** para recuperar el token de acceso para CTT.
* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transfieren, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido con el que están asociados.
* Si la instancia de AEM Cloud Service AEM AEM de destino tiene un usuario con un nombre de usuario diferente pero con la misma dirección de correo electrónico que uno de los usuarios de la instancia de origen, y la asignación de usuarios está activada, se escribe un mensaje de error en los registros y no se transfiere el usuario de origen, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

## Resumen final e informe {#final-report}

Una vez que la extracción y la ingesta se han completado correctamente, se genera un informe con los detalles de migración principales. Consulte [Validación de la migración de entidades principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) para obtener más información.
