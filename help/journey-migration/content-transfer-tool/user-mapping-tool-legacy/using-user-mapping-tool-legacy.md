---
title: Uso de la herramienta de asignación de usuarios (heredada)
description: Uso de la herramienta de asignación de usuarios (heredada)
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 3%

---

# Uso de la herramienta de asignación de usuarios (heredada) {#using-user-mapping-tool}

>[!INFO]
>
>Esta documentación hace referencia a una versión obsoleta de la herramienta. Para obtener más información sobre la versión más reciente, consulte [Asignación de usuarios y migración de principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

La herramienta de asignación de usuarios utiliza una API que le permite buscar usuarios de Adobe Identity Management System (IMS) por correo electrónico y devolver sus ID de IMS. Esta API requiere que el usuario cree un ID de cliente para su organización, un secreto de cliente y un token de acceso o portador.

## Configuración de la herramienta de asignación de usuarios {#setting-up-user-mapping}

**Requisito previo:** AEM La asignación de usuarios requiere que cada usuario asignado a su ID de IMS tenga una dirección de correo electrónico en su perfil en, y en IMS.  Tenga en cuenta que incluso si el usuario utiliza una dirección de correo electrónico como ID de usuario para iniciar sesión, la asignación no funcionará para ese usuario a menos que la dirección de correo electrónico también esté en el perfil y también en IMS.

Siga los pasos a continuación para configurar esto:

1. Vaya a [Consola de Adobe Developer](https://console.adobe.io) con su Adobe ID.
1. Cree un nuevo proyecto o abra uno existente.
1. Añadir una API: haga clic en **Agregar al proyecto** y seleccione **API**
1. Elija la API de administración de usuarios.  Debe tener permisos de administrador del sistema para que esta opción esté disponible.
1. Cree una credencial JWT.
1. Genere un par de claves o cargue una clave pública (rsa no sirve).  Hay un botón, **Generar un par de claves pública y privada**, que hará esto por usted.  Asegúrese de guardar las claves pública y privada.
1. Vaya a la API de administración de usuarios.
1. Genere un token de acceso (o token de portador) pegando el contenido de la clave privada en el cuadro de texto y haciendo clic en **Generar token**.
1. Guarde toda esta información, como **ID de cliente**, **Secreto del cliente**, **ID de cuenta técnica**, **Correo electrónico de cuenta técnica**, **ID de organización**, y **Token de acceso** de forma segura.

## Acceso a la interfaz de usuario para la herramienta de asignación de usuarios {#user-interface}

La herramienta de asignación de usuarios está integrada en la herramienta de transferencia de contenido. Puede descargar la herramienta de transferencia de contenido desde [Portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html). Para obtener más información sobre la versión más reciente, consulte la [Notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. Seleccione Adobe Experience Manager y vaya a las herramientas -> **Operaciones** -> **Migración de contenido**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. Haga clic en **Asignación de usuarios** Tarjeta de.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. Haga clic en **Crear configuración de asignación de usuarios**.

   >[!NOTE]
   >Si omite este paso, la asignación de usuarios y grupos se omitirá durante la fase de extracción.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   Rellene los campos en **Configuración de API de User Management**, como se describe a continuación.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **ID de organización**: introduzca el ID de organización de Adobe Identity Management System (IMS) para la organización a la que se están migrando los usuarios.

     >[!NOTE]
     >Para obtener el ID de organización de, inicie sesión en [Admin Console](https://adminconsole.adobe.com/) y elija su organización (en el área superior derecha) si pertenece a más de una. El ID de organización se encuentra en la dirección URL de esa página, con el formato siguiente `xx@AdobeOrg`, donde xx es el ID de organización de IMS.  También puede encontrar el ID de organización en la variable [Consola de Adobe Developer](https://console.adobe.io) página donde se genera el token de acceso.

   * **ID de cliente**: introduzca el ID de cliente que guardó desde el paso de instalación.

   * **Token de acceso**: introduzca el token de acceso que guardó desde el paso Configuración.

     >[!NOTE]
     >El token de acceso caduca cada 24 horas y es necesario crear uno nuevo. Para crear un nuevo token, vuelva a [Consola de Adobe Developer](https://console.adobe.io), elija el proyecto y haga clic en **API de administración de usuarios** y pegue la misma clave privada en el cuadro.

1. Después de rellenar los campos, haga clic en **Probar configuración** para probar la conexión al servicio de API de administración de usuarios. Si la conexión se ha realizado correctamente, puede hacer clic en **Guardar** para guardar la configuración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. Después de guardar la configuración, seleccione la configuración y haga clic en **Iniciar asignación de usuarios**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. Haga clic en **Inicio** en el cuadro de diálogo para iniciar el proceso Asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Muestra el **Estado** as **EN EJECUCIÓN**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. Una vez finalizada la asignación de usuarios, haga clic en **Resultados** para ver el resumen.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* Una vez finalizada la asignación de usuarios, puede volver a la página Migración de contenido con la ruta de exploración. La tarjeta Asignación de usuarios muestra el estado y la marca de tiempo. Haga clic en **Transferencia de contenido** para crear un conjunto de migración para ejecutar la extracción. Consulte [Ejecución de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) para obtener más información.

### Reanudación del proceso de asignación de usuarios {#resume-user-mapping-process}

Si el proceso de asignación de usuarios se detiene debido a cualquiera de las siguientes razones:

* El usuario seleccionado **Detener asignación de usuarios**
* el token de acceso caducó durante el proceso o,
* alguna otra razón

  >[!NOTE]
  >El progreso se guarda desde donde se detuvo el proceso.

Siga los pasos a continuación para reanudar el proceso de asignación de usuarios:

1. Clic **Ver registro** para revisar el registro de asignación de usuarios y comprobar el progreso guardado.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. Clic **Iniciar asignación de usuarios** para reanudar desde donde lo dejó.

   >[!NOTE]
   >Asegúrese de que el token de acceso sigue siendo válido o se ha actualizado antes de reiniciar.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. Clic **Inicio** en el cuadro de diálogo para reanudar el proceso Asignación de usuarios.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   Una vez completado el proceso de asignación de usuarios, puede ver el **Estado** as **FINALIZADO** para esa configuración específica.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
