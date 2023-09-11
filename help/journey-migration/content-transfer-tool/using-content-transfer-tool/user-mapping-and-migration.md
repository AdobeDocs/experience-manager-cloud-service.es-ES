---
title: Asignación de usuarios y migración de principales
description: AEM Información general sobre la asignación de usuarios y la migración de principales en as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 2fdfb65543fa2942e809aa5d379f4000e40bd517
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 9%

---

# Asignación de usuarios y migración de principales {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema de Adobe Experience Manager (AEM) existente a AEM as a Cloud Service. Los usuarios existentes deben asignarse a sus ID de IMS para evitar que se dupliquen en la instancia de creación de Cloud Service."

>[!NOTE]
>Para ver las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

Como parte del recorrido de transición a Adobe Experience Manager AEM () as a Cloud Service AEM AEM, los usuarios y grupos (o &quot;principales&quot;) deben migrarse de los sistemas de existentes a los as a Cloud Service de la. Esta tarea la realiza la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de Adobe ID para acceder al nivel de creación. Este proceso requiere el uso del [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Debido a este cambio, los usuarios existentes deben asignarse a sus ID de IMS para evitar la creación de usuarios duplicados en la instancia de autor del Cloud Service. AEM Dado que los grupos de los grupos tradicionales son fundamentalmente diferentes de los grupos de IMS, los grupos no se asignan, pero los dos conjuntos de grupos deben reconciliarse una vez completada la migración.

## Detalles de migración principal {#principal-migration-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán al sistema de la nube todas las entidades de seguridad asociadas con el contenido que se está migrando.  AEM La herramienta de transferencia de contenido lo hace copiando todas las entidades de seguridad del sistema de fuentes de datos de origen durante el proceso de extracción.  A continuación, Ingesta de CAM selecciona y migra solo las entidades principales asociadas con el contenido que se está ingiriendo.

## Detalles de asignación de usuarios {#user-mapping-detail}

AEM Los usuarios de Adobe IMS se pueden asignar a los usuarios de Adobe IMS correspondientes con la misma dirección de correo electrónico.  Esta asignación se puede realizar automáticamente en CTT (durante el paso de extracción) y se puede controlar o no mediante un conmutador antes de iniciar la extracción. El usuario puede anular la configuración predeterminada de la opción al iniciar la extracción.

* Si el sistema de origen es una instancia de autor, la opción predeterminada para realizar la asignación es _el_, porque es el proceso recomendado.
* Si el sistema de origen es una instancia de publicación, la opción predeterminada para realizar la asignación es _desactivado_, ya que los usuarios no se migran ni se utilizan normalmente en instancias de publicación; o si se utilizan, se suele utilizar un sistema de autenticación diferente (es decir, no IMS) para ellos.

Independientemente de si los usuarios están asignados durante la extracción o no, estos, junto con los grupos, se migran al sistema en la nube durante la ingesta si están asociados con el contenido que se está migrando.

## Consideraciones importantes a la hora de asignar y migrar usuarios {#important-considerations}

### Casos excepcionales {#exceptional-cases}

Se registran los siguientes casos específicos:

1. Si un usuario no tiene dirección de correo electrónico en la `profile/email` campo de su *jcr* , el usuario o grupo en cuestión puede migrarse, pero no está asignado. Este escenario se da incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.
2. Si el usuario está deshabilitado, se trata igual que otros usuarios; se asigna y migra con normalidad y permanece deshabilitado en la instancia de nube.
3. AEM Si existe un principal con el mismo nombre (rep:principalName) tanto en la instancia de origen como en la instancia de AEM Cloud Service de destino, el principal en cuestión no se migra y el principal existente anteriormente en el sistema de la nube permanece sin cambios.
4. Si un usuario se migra sin que se le asigne mediante Asignación de usuarios, en el sistema de la nube de destino el usuario no podrá iniciar sesión con su ID de IMS. O bien, si su dirección de correo electrónico no coincide con la dirección de correo electrónico utilizada para iniciar sesión en IMS, en el sistema de la nube de Target tampoco podrán iniciar sesión con su ID de IMS. AEM Es posible que puedan iniciar sesión utilizando el método de inicio de sesión tradicional (inicio de sesión local), pero este método no suele ser el deseado o esperado.

## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** Cuando se establece, los usuarios ya transferidos en la instancia de Cloud Service se eliminan junto con todo el repositorio existente; se crea un nuevo repositorio en el que se ingiere contenido. Este proceso también restablece todos los ajustes, incluidos los permisos, en la instancia del Cloud Service de destino y es verdadero para un usuario administrador añadido a **administradores** grupo. El usuario administrador debe volver a agregarse al **administradores** para recuperar el token de acceso para la ingesta de CTT/CAM.
* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transfieren. Esta regla es verdadera incluso si los usuarios y grupos han cambiado en el sistema de origen. El motivo es que los usuarios y grupos solo se migran junto con el contenido con el que están asociados.
* Si la instancia de AEM Cloud Service AEM de destino tiene un usuario con un nombre de usuario diferente pero con la misma dirección de correo electrónico que uno de los usuarios de la instancia de origen, y la asignación de usuarios está habilitada, los registros registran un mensaje de error. AEM Además, el usuario de origen no se transfiere, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.
* Consulte [Migración de grupos de usuarios cerrados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) por consideraciones adicionales para las entidades de seguridad utilizadas en una directiva de grupo de usuarios cerrado (CUG).

## Resumen final e informe {#final-report}

Una vez que la extracción y la ingesta se han completado correctamente, se genera un informe con los detalles de migración principales. Consulte [Validación de la migración de entidades principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) para obtener más información.
