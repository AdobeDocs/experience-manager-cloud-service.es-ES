---
title: Consideraciones importantes sobre la herramienta de asignación de usuarios
description: Consideraciones importantes sobre la herramienta de asignación de usuarios
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---


# Consideraciones importantes sobre la herramienta de asignación de usuarios {#important-considerations}


## Casos excepcionales {#exceptional-cases}

Se registrarán los siguientes casos específicos:

1. Si un usuario no tiene dirección de correo electrónico en el campo `profile/email` de su nodo *jcr*, se migrará el usuario o grupo en cuestión, pero no se asignará.

1. Si no se encuentra un correo electrónico determinado en el sistema Identity Management System de Adobe (IMS) para el ID de organización utilizado (o si el ID de IMS no se puede recuperar por otro motivo), el usuario o grupo en cuestión se migrará, pero no se asignará.

1. Si el usuario está deshabilitado actualmente, se trata igual que si no estuviera deshabilitado. Se asignará, migrará como de costumbre y permanecerá deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de AEM Cloud Service de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de origen AEM el usuario o grupo en cuestión no se migrará.

## Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está establecida, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece toda la configuración, incluidos los permisos de la instancia de Cloud Service de destino, y es verdadero para un usuario administrador agregado al grupo **administradores**. El usuario administrador deberá agregarse de nuevo al grupo **administradores** para recuperar el token de acceso para CTT.

* Se recomienda eliminar cualquier usuario existente de la instancia de Cloud Service AEM destino antes de ejecutar CTT con asignación de usuarios. Esto sirve para evitar conflictos entre los usuarios que migran de la instancia de AEM de origen a la instancia de AEM de destino. Se producirán conflictos durante la ingesta si el mismo usuario existe en la instancia de AEM de origen y en la instancia de AEM de destino.

* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transferirán, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido al que están asociados.

* Si la instancia de AEM Cloud Service de destino tiene un usuario con un nombre de usuario diferente pero la misma dirección de correo electrónico que uno de los usuarios de la instancia de AEM de origen y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y el usuario de AEM de origen no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

* Si dos usuarios de la instancia de AEM de origen tienen la misma dirección de correo electrónico y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y uno de los usuarios de origen AEM no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.