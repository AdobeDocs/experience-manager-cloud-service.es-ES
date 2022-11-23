---
title: Consideraciones importantes sobre la herramienta de asignación de usuarios
description: Consideraciones importantes sobre la herramienta de asignación de usuarios
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 18047b129a9a347cbf6edcdc07dc6570fca26d3b
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Consideraciones importantes sobre la herramienta de asignación de usuarios {#important-considerations}


## Casos excepcionales {#exceptional-cases}

Se registrarán los siguientes casos específicos:

1. Si un usuario no tiene ninguna dirección de correo electrónico en la `profile/email` campo de *jcr* nodo en el que se migrará el usuario o grupo en cuestión, pero no se asignará.  Este será el caso incluso si la dirección de correo electrónico se utiliza como nombre de usuario para iniciar sesión.

1. Si no se encuentra un correo electrónico determinado en el sistema Identity Management System de Adobe (IMS) para el ID de organización utilizado (o si el ID de IMS no se puede recuperar por otro motivo), el usuario o grupo en cuestión se migrará, pero no se asignará.

1. Si el usuario está deshabilitado actualmente, se trata igual que si no estuviera deshabilitado. Se asignará, migrará como de costumbre y permanecerá deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen AEM el usuario o grupo en cuestión no se migrará.

1. Si se migra un usuario sin que primero se asigne mediante Asignación de usuarios, en el sistema de nube de destino no podrá iniciar sesión con su ID de IMS.  Es posible que puedan iniciar sesión utilizando el método AEM tradicional, pero tenga en cuenta que esto no es normalmente lo que se desea o se espera.

## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** está configurado, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece toda la configuración, incluidos los permisos, en la instancia de Cloud Service de destino y es verdadero para un usuario administrador añadido al grupo **administradores** grupo. El usuario administrador deberá agregarse de nuevo al **administradores** grupo para recuperar el token de acceso para CTT.

* Se recomienda eliminar cualquier usuario existente de la instancia de Cloud Service AEM destino antes de ejecutar CTT con asignación de usuarios. Esto sirve para evitar conflictos entre los usuarios que migran de la instancia de AEM de origen a la instancia de AEM de destino. Se producirán conflictos durante la ingesta si el mismo usuario existe en la instancia de AEM de origen y en la instancia de AEM de destino.

* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transferirán, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido al que están asociados.

* Si la instancia de AEM Cloud Service de destino tiene un usuario con un nombre de usuario diferente pero la misma dirección de correo electrónico que uno de los usuarios de la instancia de AEM de origen y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y el usuario de AEM de origen no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

* Si dos usuarios de la instancia de AEM de origen tienen la misma dirección de correo electrónico y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y uno de los usuarios de origen AEM no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

### Siguientes pasos {#whats-next}

Una vez que conozca las consideraciones importantes y los casos excepcionales, ya estará listo para usar la herramienta. Consulte [Uso de la herramienta de asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) para obtener más información.
