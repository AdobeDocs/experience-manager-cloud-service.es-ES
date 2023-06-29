---
title: Asignación de usuarios y migración de principales
description: Información general sobre asignación de usuarios y migración de principales
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 8%

---

# Asignación de usuarios y migración de principales {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema de Adobe Experience Manager AEM AEM () existente a los as a Cloud Service de la. Los usuarios existentes deben asignarse a sus ID de IMS para evitar que se dupliquen en la instancia de creación de Cloud Service."

>[!NOTE]
>Para ver las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager AEM () as a Cloud Service AEM AEM, debe mover usuarios y grupos de su sistema de existente a los de la red de usuarios de la red de trabajo de la red de trabajo de la red de trabajo de la red de la red de trabajo de la red de as a Cloud Service. Esta tarea la realiza la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de Adobe ID para acceder al nivel de creación. Este proceso requiere el uso del [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Debido a este cambio, los usuarios existentes deben asignarse a sus ID de IMS para evitar usuarios duplicados en la instancia de autor del Cloud Service. AEM Dado que los grupos de los grupos tradicionales son fundamentalmente diferentes de los grupos de IMS, los grupos no se asignan, pero los dos conjuntos de grupos deben reconciliarse una vez completada la migración.

## Detalles de migración de usuarios {#user-migration-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán al sistema en la nube todos los usuarios asociados con el contenido que se está migrando.

## Detalles de asignación de usuarios {#user-mapping-detail}

AEM Los usuarios de Adobe IMS se pueden asignar a los usuarios de Adobe IMS correspondientes con la misma dirección de correo electrónico.  Esta asignación se puede realizar automáticamente en CTT y se puede controlar mediante un conmutador antes de iniciar la extracción. El usuario puede anular la configuración predeterminada de la opción al iniciar la extracción.

* Si el sistema de origen es una instancia de autor, la opción predeterminada para realizar la asignación es _el_, porque es el proceso recomendado.
* Si el sistema de origen es una instancia de publicación, la opción predeterminada para realizar la asignación es _desactivado_, porque los usuarios no se migran ni utilizan normalmente en instancias de publicación.

## Consideraciones importantes a la hora de asignar y migrar usuarios {#important-considerations}


### Casos excepcionales {#exceptional-cases}

Se registran los siguientes casos específicos:

1. Si un usuario no tiene una dirección de correo electrónico en `profile/email` campo de su *jcr* , el usuario o grupo en cuestión puede migrarse, pero no está asignado. Este escenario se da incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si el usuario está deshabilitado, se trata igual que si no lo estuviera. Se asigna y migra con normalidad y permanece deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service AEM de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen, no se migra el usuario en cuestión.

1. Si un usuario se migra sin que se le asigne mediante Asignación de usuarios, en el sistema de la nube de destino no puede iniciar sesión con su ID de IMS. O bien, si su dirección de correo electrónico no coincide con la dirección de correo electrónico utilizada para iniciar sesión en IMS, en el sistema de la nube de Target tampoco pueden iniciar sesión con su ID de IMS. AEM Es posible que puedan iniciar sesión utilizando el método tradicional, pero este método no suele ser el deseado o esperado.


## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** Cuando se establece, los usuarios ya transferidos en la instancia de Cloud Service se eliminan junto con todo el repositorio existente. Además, se crea un nuevo repositorio en el que se ingiere contenido. Este proceso también restablece todos los ajustes, incluidos los permisos, en la instancia del Cloud Service de destino y es verdadero para un usuario administrador añadido a **administradores** grupo. El usuario administrador debe leerse en el **administradores** para recuperar el token de acceso para CTT.
* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transfieren. Esta regla se aplica incluso si los usuarios y grupos han cambiado mientras tanto. El motivo es que los usuarios y grupos se migran junto con el contenido con el que están asociados.
* Si la instancia de AEM Cloud Service AEM de destino tiene un usuario con un nombre de usuario diferente pero con la misma dirección de correo electrónico que uno de los usuarios de la instancia de origen, y la asignación de usuarios está habilitada, los registros registran un mensaje de error. AEM Además, el usuario de origen no se transfiere, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

## Resumen final e informe {#final-report}

Una vez que la extracción y la ingesta se han completado correctamente, se genera un informe con los detalles de migración principales. Consulte [Validación de la migración de entidades principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) para obtener más información.
