---
title: Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada)
description: Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada) {#important-considerations}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de la herramienta. Para obtener más información sobre la versión más reciente, consulte [Asignación de usuarios y migración de entidades de seguridad](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## Casos excepcionales {#exceptional-cases}

Se registran los siguientes casos específicos:

1. Si un usuario no tiene una dirección de correo electrónico en el campo `profile/email` de su nodo *jcr*, el usuario o grupo en cuestión se migra pero no se asigna. Este es el caso incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si no se encuentra un correo electrónico en el sistema Identity Management System (IMS) de Adobe para el ID de organización utilizado (o, si no se puede recuperar el ID de IMS), se migra el usuario o grupo, pero no se asigna.

1. Si el usuario está deshabilitado, se trata igual que si no lo estuviera. Se asigna y migra con normalidad, y permanece deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service AEM de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen, no se migra el usuario o grupo.

1. Si se migra un usuario sin que se asigne primero mediante Asignación de usuarios, en el sistema de la nube de destino no podrá iniciar sesión con su ID de IMS. AEM Es posible que puedan iniciar sesión utilizando el método de trabajo tradicional, pero este flujo de trabajo no suele ser el deseado o esperado.

## Consideraciones adicionales {#additional-considerations}

* Si se establece la configuración **Borrar el contenido existente en la instancia de Cloud antes de la ingesta**, se eliminarán los usuarios ya transferidos en la instancia de Cloud Service. También se elimina todo el repositorio existente y se crea un nuevo repositorio en el que se ingiere contenido. Esta acción también restablece toda la configuración, incluidos los permisos, en la instancia del Cloud Service de destino y es verdadera para un usuario administrador agregado al grupo **administrators**. El usuario administrador debe leerse en el grupo **administradores** para recuperar el token de acceso para CTT.

* El Adobe recomienda quitar cualquier usuario existente de la instancia de destino de Cloud Service AEM antes de ejecutar CTT con Asignación de usuarios. AEM AEM Esta acción es necesaria para evitar cualquier conflicto entre la migración de usuarios de la instancia de origen de los usuarios a la instancia de origen de los usuarios de la instancia de destino de los que se va a realizar la migración de la instancia de destino de los usuarios AEM AEM Pueden producirse conflictos durante la ingesta si el mismo usuario existe en la instancia de origen de los recursos y en la instancia de destino de los recursos de la.

* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transfieren. Esta regla se aplica incluso si los usuarios y grupos han cambiado mientras tanto. El motivo es que los usuarios y grupos se migran junto con el contenido con el que están asociados.

* Si AEM Cloud Service AEM tiene un usuario con un nombre de usuario diferente pero la misma dirección de correo electrónico que un usuario en la instancia de origen, y la asignación de usuarios está habilitada, se registra un mensaje de error. AEM Además, el usuario de origen no se transfiere, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

* AEM Si dos usuarios de la instancia de origen de la tienen la misma dirección de correo electrónico y la Asignación de usuarios está habilitada, se registra un mensaje de error. AEM Además, se transfiere uno de los usuarios de origen porque solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

### Siguientes pasos {#whats-next}

Una vez que haya aprendido las consideraciones importantes y los casos excepcionales, ya está listo para usar la herramienta. Consulte [Uso de la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) para obtener más información.
