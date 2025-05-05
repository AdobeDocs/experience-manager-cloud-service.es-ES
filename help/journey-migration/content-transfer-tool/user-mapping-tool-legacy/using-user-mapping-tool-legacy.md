---
title: Uso de la herramienta de asignación de usuarios (heredada)
description: Uso de la herramienta de asignación de usuarios (heredada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
feature: Migration
role: Admin
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---


# Uso de la herramienta de asignación de usuarios (heredada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de la herramienta. Para obtener más información sobre la versión más reciente, consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un secreto de cliente y un token de acceso o portador.

## Configuración de la herramienta de asignación de usuarios {#setting-up-user-mapping}

AEM **Requisito previo:** La asignación de usuarios requiere que cada usuario que se asigne a su ID de IMS tenga una dirección de correo electrónico en su perfil en y en IMS. Incluso si el usuario utiliza una dirección de correo electrónico como ID de usuario para iniciar sesión, la asignación no funciona para ese usuario a menos que la dirección de correo electrónico también esté en el perfil y también en IMS.

Siga los pasos a continuación para configurar esto:

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console/) con su Adobe ID.
1. Cree un proyecto o abra uno existente.
1. Agregar una API: haga clic en **Agregar al proyecto** y seleccione **API**
1. Elija la API de administración de usuarios. Debe tener permisos de administrador del sistema para que esta opción esté disponible.
1. Cree una credencial JWT.
1. Genere un par de claves o cargue una clave pública (rsa no sirve). Hay un botón **Generar un par de claves pública y privada** que crea este par de claves automáticamente. Asegúrese de guardar las claves pública y privada.
1. Vaya a la API de administración de usuarios.
1. Genere un token de acceso (o token de portador) pegando el contenido de su clave privada en el cuadro de texto y haciendo clic en **Generar token**.
1. Guarde toda esta información, como **ID de cliente**, **Secreto de cliente**, **ID de cuenta técnica**, **correo electrónico de cuenta técnica**, **ID de organización** y **token de acceso**, de forma segura.

## Acceso a la interfaz de usuario para la herramienta de asignación de usuarios {#user-interface}

La herramienta de asignación de usuarios está integrada en la herramienta de transferencia de contenido. Puede descargar la herramienta de transferencia de contenido desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Para obtener más información sobre la versión más reciente, consulte [Notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleccione Adobe Experience Manager y vaya a herramientas > **Operaciones** > **Migración de contenido**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Haga clic en la tarjeta **Asignación de usuarios**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Haga clic en **Crear configuración de asignación de usuarios**.

   >[!NOTE]
   >Si omite este paso, la asignación de usuarios y grupos se omitirá durante la fase de extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Rellene los campos en **Configuración de la API de administración de usuarios**, tal como se describe a continuación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **Org ID**: escriba el identificador de organización de Adobe Identity Management System (IMS) para la organización a la que se están migrando los usuarios.

     >[!NOTE]
     >Para obtener el identificador de organización, inicia sesión en [Admin Console](https://adminconsole.adobe.com/) y elige tu organización (en el área superior derecha) si perteneces a más de uno. El identificador de organización se encuentra en la dirección URL de esa página, con formato como `xx@AdobeOrg`, donde xx es el identificador de organización de IMS. También puede encontrar el identificador de organización en la página [Adobe Developer Console](https://developer.adobe.com/console/), donde genera el token de acceso.

   * **ID de cliente**: escriba el ID de cliente que guardó desde el paso de instalación.

   * **Token de acceso**: escriba el token de acceso que guardó desde el paso de instalación.

     >[!NOTE]
     >El token de acceso caduca cada 24 horas y se debe crear uno nuevo. Para crear un token, vuelve a [Adobe Developer Console](https://developer.adobe.com/console/), elige tu proyecto, haz clic en **API de administración de usuarios** y pega la misma clave privada en el cuadro.

1. Después de rellenar los campos, haga clic en **Probar configuración** para probar la conexión con el servicio de API de administración de usuarios. Si la conexión se ha realizado correctamente, puede hacer clic en **Guardar** para guardar la configuración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Después de guardar la configuración, seleccione la configuración y haga clic en **Iniciar asignación de usuarios**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Haga clic en **Iniciar** en el cuadro de diálogo para iniciar el proceso de asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Muestra **Status** como **RUNNING**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una vez completada la asignación de usuarios, haga clic en **Resultados** para ver el resumen.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* Una vez finalizada la asignación de usuarios, puede volver a la página Migración de contenido con la ruta de exploración. La tarjeta Asignación de usuarios muestra el estado y la marca de tiempo. Haga clic en **Transferencia de contenido** para poder crear un conjunto de migración y ejecutar la extracción. Consulte [Ejecución de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=es#running-tool) para obtener más información.

### Reanudación del proceso de asignación de usuarios {#resume-user-mapping-process}

Si el proceso de asignación de usuarios se detiene debido a cualquiera de las siguientes razones:

* El usuario seleccionó la opción **Detener asignación de usuarios**.
* El token de acceso caducó durante el proceso.
* O por alguna otra razón.

  >[!NOTE]
  >El progreso se guarda desde donde se detuvo el proceso.

Siga los pasos a continuación para reanudar el proceso de asignación de usuarios:

1. Haga clic en **Ver registro** para revisar el registro de asignación de usuarios y comprobar el progreso guardado.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Vuelva a hacer clic en el botón **Iniciar asignación de usuarios** para reanudarlo desde donde lo dejó.

   >[!NOTE]
   >Asegúrese de que el token de acceso sigue siendo válido o se ha actualizado antes de reiniciar.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Haga clic en **Iniciar** en el cuadro de diálogo para reanudar el proceso de asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Una vez completado el proceso de asignación de usuarios, puede ver el **estado** como **FINALIZADO** para esa configuración específica.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
