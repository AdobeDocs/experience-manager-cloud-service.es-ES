---
title: Uso de la herramienta de asignación de usuarios
description: Uso de la herramienta de asignación de usuarios
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 3%

---


# Uso de la herramienta de asignación de usuarios {#using-user-mapping-tool}

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un Secreto de cliente y un Token de acceso o portador.

## Configuración de la herramienta de asignación de usuarios {#setting-up-user-mapping}

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

## Acceso a la interfaz de usuario para la herramienta de asignación de usuarios {#user-interface}

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
