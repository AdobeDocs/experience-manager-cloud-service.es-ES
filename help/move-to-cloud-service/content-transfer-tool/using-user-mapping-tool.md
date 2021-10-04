---
title: Uso de la herramienta de asignación de usuarios
description: Uso de la herramienta de asignación de usuarios
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: b290b402fe58d449dd85e9eaaef5b75e61ac1a74
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 1%

---

# Uso de la herramienta de asignación de usuarios {#user-mapping-tool}

## Información general {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Herramienta de asignación de usuarios"
>abstract="La herramienta de transferencia de contenido le ayuda a mover usuarios y grupos de su sistema AEM existente a AEM como Cloud Service. Los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de creación del Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Consideraciones importantes sobre el uso de la herramienta de asignación de usuarios"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Uso de la herramienta de asignación de usuarios"

Como parte del recorrido de transición a Adobe Experience Manager (AEM) como Cloud Service, debe mover usuarios y grupos del sistema de AEM existente a AEM como Cloud Service. Esto lo hace la herramienta de transferencia de contenido.

Un cambio importante en AEM como Cloud Service es el uso completamente integrado de los ID de Adobe para acceder al nivel de creación.  Esto requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS) que proporciona el inicio de sesión único en todas las aplicaciones de nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Debido a este cambio, los usuarios y grupos existentes deben asignarse a sus ID de IMS para evitar usuarios y grupos duplicados en la instancia de creación del Cloud Service.

### Herramienta de asignación de usuarios {#mapping-tool}

La herramienta de transferencia de contenido (sin asignación de usuarios) migrará todos los usuarios y grupos asociados con el contenido que se migra. La herramienta de asignación de usuarios forma parte de la herramienta de transferencia de contenido y su único propósito es modificar los usuarios y grupos de modo que IMS los reconozca correctamente, la funcionalidad de inicio de sesión único que AEM como Cloud Service. Una vez realizadas estas modificaciones, la herramienta de transferencia de contenido migra los usuarios y grupos del contenido especificado de la forma habitual.

## Consideraciones importantes {#important-considerations}

### Casos excepcionales {#exceptional-cases}

Se registrarán los siguientes casos específicos:

1. Si un usuario no tiene dirección de correo electrónico en el campo `profile/email` de su nodo *jcr*, se migrará el usuario o grupo en cuestión, pero no se asignará.

1. Si no se encuentra un correo electrónico determinado en el sistema Identity Management System de Adobe (IMS) para el ID de organización utilizado (o si el ID de IMS no se puede recuperar por otro motivo), el usuario o grupo en cuestión se migrará, pero no se asignará.

1. Si el usuario está deshabilitado actualmente, se trata igual que si no estuviera deshabilitado. Se asignará, migrará como de costumbre y permanecerá deshabilitado en la instancia de nube.

1. Si existe un usuario en la instancia de Cloud Service de AEM de destino con el mismo nombre de usuario (rep:principalName) que uno de los usuarios de la instancia de AEM de origen, no se migrará el usuario o grupo en cuestión.

### Consideraciones adicionales {#additional-considerations}

* Si la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta** está establecida, los usuarios ya transferidos en la instancia de Cloud Service se eliminarán junto con todo el repositorio existente y se creará un nuevo repositorio para introducir contenido en. Esto también restablece toda la configuración, incluidos los permisos de la instancia de Cloud Service de destino, y es verdadero para un usuario administrador agregado al grupo **administradores**. El usuario administrador deberá agregarse de nuevo al grupo **administradores** para recuperar el token de acceso para CTT.

* Se recomienda eliminar cualquier usuario existente de la instancia de Cloud Service AEM destino antes de ejecutar CTT con asignación de usuarios. Esto sirve para evitar conflictos entre los usuarios que migran de la instancia de AEM de origen a la instancia de AEM de destino. Se producirán conflictos durante la ingesta si el mismo usuario existe en la instancia de AEM de origen y en la instancia de AEM de destino.

* Cuando se realizan recargas de contenido, si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, los usuarios y grupos asociados con ese contenido tampoco se transferirán, aunque los usuarios y grupos hayan cambiado mientras tanto. Esto se debe a que los usuarios y grupos se migran junto con el contenido al que están asociados.

* Si la instancia de Cloud Service de AEM de destino tiene un usuario con un nombre de usuario diferente pero la misma dirección de correo electrónico que uno de los usuarios de la instancia de AEM de origen y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y el usuario de origen AEM no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.

* Si dos usuarios de la instancia de AEM de origen tienen la misma dirección de correo electrónico y la Asignación de usuarios está habilitada, se escribirá un mensaje de error en los registros y uno de los usuarios de origen AEM no se transferirá, ya que solo se permite un usuario con una dirección de correo electrónico determinada en el sistema de destino.


## Uso de la herramienta de asignación de usuarios {#using-user-mapping-tool}

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un Secreto de cliente y un Token de acceso o portador.

Siga los pasos a continuación para configurar esto:

1. Vaya a [Adobe Developer Console](https://console.adobe.io) con su Adobe ID.
1. Cree un nuevo proyecto o abra un proyecto existente.
1. Agregar una API: haga clic en **Agregar al proyecto** y seleccione **API**
1. Seleccione la API de administración de usuarios.  Es posible que necesite obtener permisos para tener esta opción.
1. Cree una credencial JWT.
1. Genere un par de claves o Cargue una clave pública (rsa no es buena).  Hay un botón, **Generate a public/private keypair**, que hará esto por usted.  Asegúrese de guardar las claves pública y privada.
1. Vaya a la API de administración de usuarios.
1. Genere un token de acceso (o token al portador) pegando el contenido de su clave privada en el cuadro de texto y haciendo clic en **Generate Token**.
1. Guarde toda esta información, como **Client ID**, **Client Secret**, **Technical Account ID**, **Technical Account Email**, **Org ID** y **Access Token** de forma segura.

## Interfaz de usuario {#user-interface}

La herramienta de asignación de usuarios está integrada en la herramienta de transferencia de contenido. Puede descargar la herramienta de transferencia de contenido desde [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html). Para obtener más información sobre la versión más reciente, consulte las [Notas de la versión actuales](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Asignación de usuarios**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing1.png)

1. Haga clic en **Crear configuración de asignación de usuarios**.

   >[!NOTE]
   >Si omite este paso, la asignación de usuarios y grupos se omitirá durante la fase de Extracción.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing2.png)

   Rellene los campos de **Configuración de la API de administración de usuarios** como se describe a continuación.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing3.png)

   * **ID de organización**: Introduzca el ID de organización de Adobe Identity Management System (IMS) para la organización a la que se están migrando los usuarios.

      >[!NOTE]
      >Para obtener el ID de organización, inicie sesión en el [Admin Console](https://adminconsole.adobe.com/) y seleccione su organización (en el área superior derecha) si pertenece a más de uno. El ID de organización estará en la dirección URL de esa página, con el formato `xx@AdobeOrg`, donde xx es el ID de organización de IMS.  También puede encontrar el identificador de organización en la página [Consola de desarrollador de Adobe](https://console.adobe.io) donde genera el token de acceso.

   * **ID** de cliente: Introduzca el ID de cliente que guardó en el paso Configuración.

   * **Token** de acceso: Introduzca el token de acceso que guardó en el paso Configuración.

      >[!NOTE]
      >El token de acceso caduca cada 24 horas y es necesario crear uno nuevo. Para crear un token nuevo, vuelva a [Adobe Developer Console](https://console.adobe.io), elija el proyecto, haga clic en **User Management API** y pegue la misma clave privada en el cuadro.

1. Después de rellenar los campos, haga clic en **Probar configuración** para probar la conexión con el servicio de API de administración de usuarios. Si la conexión se realiza correctamente, podrá hacer clic en **Guardar** para guardar la configuración.

1. Después de guardar la configuración, seleccione la configuración y haga clic en **Iniciar asignación de usuarios**.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Una vez finalizada la asignación de usuarios, haga clic en **Results** para ver el resumen.

   ![image](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >Una vez finalizada la asignación de usuarios, puede volver a la página Migración de contenido mediante la ruta. La tarjeta Asignación de usuarios muestra el estado y la marca de tiempo. Haga clic en **Content Transfer** para crear un conjunto de migración para ejecutar la extracción. Consulte [Ejecución de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) para obtener más información.
