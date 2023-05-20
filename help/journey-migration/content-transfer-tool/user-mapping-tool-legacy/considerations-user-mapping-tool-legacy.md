---
title: Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada)
description: Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada)
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# Consideraciones importantes sobre la herramienta de asignación de usuarios (heredada) {#important-considerations}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de la herramienta. Para obtener más información sobre la versión más reciente, consulte [Asignación de usuarios y migración de principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## Casos excepcionales {#exceptional-cases}

Se registrarán los siguientes casos específicos:

1. Si un usuario no tiene una dirección de correo electrónico en `profile/email` campo de su *jcr* nodo en el que se migrará el usuario o grupo en cuestión, pero no se asignará.  Este será el caso incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si no se encuentra un correo electrónico determinado en el sistema Identity Management System (IMS) de Adobe para el ID de organización utilizado (o si el ID de IMS no se puede recuperar por otro motivo), se migrará el usuario o grupo en cuestión, pero no se asignará.

1. Si el usuario está deshabilitado actualmente, se trata igual que si no lo estuviera. Se asignará y migrará con normalidad y permanecerá deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service AEM de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen, no se migrará el usuario o grupo en cuestión.

1. Si se migra un usuario sin que se asigne primero mediante Asignación de usuarios, no podrá iniciar sesión con su ID de IMS en el sistema de la nube de destino.  AEM Es posible que puedan iniciar sesión utilizando el método tradicional de, pero tenga en cuenta que esto no suele ser lo que se quiere o se espera.

## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** se ha configurado, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece todos los ajustes, incluidos los permisos, en la instancia del Cloud Service de destino y es verdadero para un usuario administrador añadido a **administradores** grupo. El usuario administrador tendrá que volver a agregarse al **administradores** para recuperar el token de acceso para CTT.

* Se recomienda quitar cualquier usuario existente del Cloud Service AEM de destino antes de ejecutar CTT con Asignación de usuarios. AEM AEM Esto sirve para evitar cualquier conflicto entre migrar a los usuarios de la instancia de origen de la instancia de la a la instancia de destino. AEM AEM Se producirán conflictos durante la ingesta si el mismo usuario existe en la instancia de origen de los recursos y en la instancia de destino de los recursos de la.

* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transferirán, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido con el que están asociados.

* Si la instancia de AEM Cloud Service AEM AEM de destino tiene un usuario con un nombre de usuario diferente pero con la misma dirección de correo electrónico que uno de los usuarios de la instancia de origen, y la asignación de usuarios está activada, se escribirá un mensaje de error en los registros y no se transferirá el usuario de origen, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

* AEM AEM Si dos usuarios de la instancia de origen tienen la misma dirección de correo electrónico y la Asignación de usuarios está activada, se escribe un mensaje de error en los registros y uno de los usuarios de origen no se transfiere, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

### Siguientes pasos {#whats-next}

Una vez que haya aprendido las consideraciones importantes y los casos excepcionales, ya está listo para usar la herramienta. Consulte [Uso de la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) para obtener más información.
