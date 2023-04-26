---
title: Uso de la herramienta de asignación de usuarios (heredada)
description: Uso de la herramienta de asignación de usuarios (heredada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: 154c3eb3dbee07e830f489212777540a18c952b3
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 3%

---

# Uso de la herramienta de asignación de usuarios (heredada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de esta herramienta. Para obtener más información sobre la versión más reciente, consulte [Asignación de usuarios y migración principal](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un Secreto de cliente y un Token de acceso o portador.

## Configuración de la herramienta de asignación de usuarios {#setting-up-user-mapping}

**Requisito previo:** La asignación de usuarios requiere que cada usuario que se asigne a su ID de IMS tenga una dirección de correo electrónico en su perfil en AEM y en IMS.  Tenga en cuenta que, aunque el usuario utilice una dirección de correo electrónico como ID de usuario para iniciar sesión, la asignación no funcionará para ese usuario a menos que la dirección de correo electrónico también esté en el perfil y también en IMS.

Siga los pasos a continuación para configurar esto:

1. Vaya a [Consola de Adobe Developer](https://console.adobe.io) usar su Adobe ID.
1. Cree un nuevo proyecto o abra un proyecto existente.
1. Añadir una API: haga clic en **Agregar a proyecto** y seleccione **API**
1. Seleccione la API de administración de usuarios.  Debe tener permisos de administrador del sistema para que esta opción esté disponible.
1. Cree una credencial JWT.
1. Genere un par de claves o Cargue una clave pública (rsa no es buena).  Hay un botón, **Generación de un par de claves pública/privada**, que lo hará por usted.  Asegúrese de guardar las claves pública y privada.
1. Vaya a la API de administración de usuarios.
1. Genere un token de acceso (o token al portador) pegando el contenido de su clave privada en el cuadro de texto y haciendo clic en **Generar token**.
1. Guarde toda esta información, como **ID de cliente**, **Secreto del cliente**, **ID de cuenta técnica**, **Correo electrónico de la cuenta técnica**, **ID de organización** y **Token de acceso** de forma segura.

## Acceso a la interfaz de usuario para la herramienta de asignación de usuarios {#user-interface}

La herramienta de asignación de usuarios está integrada en la herramienta de transferencia de contenido. Puede descargar la herramienta de transferencia de contenido desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Para obtener más información sobre la versión más reciente, consulte la [Notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Haga clic en **Asignación de usuarios** tarjeta.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Haga clic en **Crear configuración de asignación de usuarios**.

   >[!NOTE]
   >Si omite este paso, la asignación de usuarios y grupos se omitirá durante la fase de Extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Rellene los campos de **Configuración de la API de administración de usuarios**, tal como se describe a continuación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID de organización**: Introduzca el ID de organización de Adobe Identity Management System (IMS) para la organización a la que se están migrando los usuarios.

      >[!NOTE]
      >Para obtener el ID de organización, inicie sesión en la [Admin Console](https://adminconsole.adobe.com/) y elija su organización (en el área superior derecha) si pertenece a más de una. El ID de organización estará en la dirección URL de esa página, con el formato siguiente: `xx@AdobeOrg`, donde xx es el ID de organización de IMS.  De forma alternativa, puede encontrar el ID de organización en la variable [Consola de Adobe Developer](https://console.adobe.io) página donde se genera el token de acceso.

   * **ID de cliente**: Introduzca el ID de cliente que guardó en el paso Configuración.

   * **Token de acceso**: Introduzca el token de acceso que guardó en el paso Configuración.

      >[!NOTE]
      >El token de acceso caduca cada 24 horas y es necesario crear uno nuevo. Para crear un nuevo token, vuelva a [Consola de Adobe Developer](https://console.adobe.io), elija el proyecto, haga clic en **API de administración de usuarios** y pegue la misma clave privada en el cuadro.

1. Después de rellenar los campos, haga clic en **Configuración de prueba** para probar la conexión con el servicio de API de administración de usuarios. Si la conexión se realiza correctamente, podrá hacer clic en **Guardar** para guardar la configuración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Después de guardar la configuración, seleccione la configuración y haga clic en **Iniciar asignación de usuarios**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Haga clic en **Inicio** del cuadro de diálogo para iniciar el proceso de asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Muestra el **Estado** como **EJECUCIÓN**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una vez finalizada la asignación de usuarios, haga clic en **Resultados** para ver el resumen.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

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

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Haga clic en el **Iniciar asignación de usuarios** para reanudar desde donde lo dejó.

   >[!NOTE]
   >Asegúrese de que, antes de reiniciar, el token de acceso sigue siendo válido o se ha actualizado.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Haga clic en **Inicio** del cuadro de diálogo para reanudar el proceso de Asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Una vez que se complete el proceso de asignación de usuarios, podrá ver la variable **Estado** como **FINALIZADO** para esa configuración específica.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
