---
title: Uso de la herramienta de asignación de usuarios
description: Uso de la herramienta de asignación de usuarios
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 4%

---

# Uso de la herramienta de asignación de usuarios {#using-user-mapping-tool}

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un Secreto de cliente y un Token de acceso o portador.

## Configuración de la herramienta de asignación de usuarios {#setting-up-user-mapping}

Siga los pasos a continuación para configurar esto:

1. Vaya a [Adobe Developer Console](https://console.adobe.io) usar su Adobe ID.
1. Cree un nuevo proyecto o abra un proyecto existente.
1. Añadir una API: haga clic en **Agregar a proyecto** y seleccione **API**
1. Seleccione la API de administración de usuarios.  Es posible que necesite obtener permisos para tener esta opción.
1. Cree una credencial JWT.
1. Genere un par de claves o Cargue una clave pública (rsa no es buena).  Hay un botón, **Generación de un par de claves pública/privada**, que lo hará por usted.  Asegúrese de guardar las claves pública y privada.
1. Vaya a la API de administración de usuarios.
1. Genere un token de acceso (o token al portador) pegando el contenido de su clave privada en el cuadro de texto y haciendo clic en **Generar token**.
1. Guarde toda esta información, como **ID de cliente**, **Secreto del cliente**, **ID de cuenta técnica**, **Correo electrónico de la cuenta técnica**, **ID de organización** y **Token de acceso** de forma segura.

## Acceso a la interfaz de usuario para la herramienta de asignación de usuarios {#user-interface}

La herramienta de asignación de usuarios está integrada en la herramienta de transferencia de contenido. Puede descargar la herramienta de transferencia de contenido desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Para obtener más información sobre la versión más reciente, consulte la [Notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Haga clic en **Asignación de usuarios** tarjeta.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Haga clic en **Crear configuración de asignación de usuarios**.

   >[!NOTE]
   >Si omite este paso, la asignación de usuarios y grupos se omitirá durante la fase de Extracción.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Rellene los campos de **Configuración de la API de administración de usuarios**, tal como se describe a continuación.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID de organización**: Introduzca el ID de organización de Adobe Identity Management System (IMS) para la organización a la que se están migrando los usuarios.

      >[!NOTE]
      >Para obtener el ID de organización, inicie sesión en la [Admin Console](https://adminconsole.adobe.com/) y elija su organización (en el área superior derecha) si pertenece a más de una. El ID de organización estará en la dirección URL de esa página, con el formato siguiente: `xx@AdobeOrg`, donde xx es el ID de organización de IMS.  De forma alternativa, puede encontrar el ID de organización en la variable [Adobe Developer Console](https://console.adobe.io) página donde se genera el token de acceso.

   * **ID de cliente**: Introduzca el ID de cliente que guardó en el paso Configuración.

   * **Token de acceso**: Introduzca el token de acceso que guardó en el paso Configuración.

      >[!NOTE]
      >El token de acceso caduca cada 24 horas y es necesario crear uno nuevo. Para crear un nuevo token, vuelva a [Adobe Developer Console](https://console.adobe.io), elija el proyecto, haga clic en **API de administración de usuarios** y pegue la misma clave privada en el cuadro.

1. Después de rellenar los campos, haga clic en **Configuración de prueba** para probar la conexión con el servicio de API de administración de usuarios. Si la conexión se realiza correctamente, podrá hacer clic en **Guardar** para guardar la configuración.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Después de guardar la configuración, seleccione la configuración y haga clic en **Iniciar asignación de usuarios**.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Haga clic en **Inicio** del cuadro de diálogo para iniciar el proceso de asignación de usuarios.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Muestra el **Estado** como **EJECUCIÓN**.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una vez finalizada la asignación de usuarios, haga clic en **Resultados** para ver el resumen.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Una vez finalizada la asignación de usuarios, puede volver a la página Migración de contenido mediante la ruta. La tarjeta Asignación de usuarios muestra el estado y la marca de tiempo. Haga clic en **Transferencia de contenido** para crear un conjunto de migración para ejecutar la extracción. Consulte [Ejecución de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) para obtener más información.


### Reanudación del proceso de asignación de usuarios {#resume-user-mapping-process}

Si el proceso de asignación de usuarios se detiene por cualquiera de los siguientes motivos:

* El usuario seleccionado **Detener la asignación de usuarios**
* el token de acceso expiró durante el proceso o,
* alguna otra razón

   >[!NOTE]
   >El progreso se guarda desde donde se detuvo el proceso.

Siga los pasos a continuación para reanudar el proceso de asignación de usuarios:

1. Haga clic en **Ver registro** para revisar el registro de asignación de usuarios para comprobar el progreso guardado.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Haga clic en el **Iniciar asignación de usuarios** para reanudar desde donde lo dejó.

   >[!NOTE]
   >Asegúrese de que, antes de reiniciar, el token de acceso sigue siendo válido o se ha actualizado.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Haga clic en **Inicio** del cuadro de diálogo para reanudar el proceso de Asignación de usuarios.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Una vez que se complete el proceso de asignación de usuarios, podrá ver la variable **Estado** como **FINALIZADO** para esa configuración específica.

   ![image](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
