---
title: Introducción a la herramienta de transferencia de contenido
description: Introducción a la herramienta de transferencia de contenido
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 1dfef0f1157ead7f1240e9a41794436197136daa
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 9%

---

# Introducción a la herramienta de transferencia de contenido {#getting-started-content-transfer-tool}


## Disponibilidad {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Descargar"
>abstract="La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la última versión."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="Notas de la versión"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribución de software"

La herramienta de transferencia de contenido se puede descargar como archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en la instancia de Adobe Experience Manager (AEM) de origen. Asegúrese de descargar la última versión. Para obtener más información sobre la versión más reciente, consulte [Notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=es).

>[!NOTE]
>Descargue Content Transfer Tool desde el portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html).

## Conectividad del entorno de origen {#source-environment-connectivity}

>[!NOTE]
>
>También puede producirse un error de conexión si se ha eliminado un conjunto de migración de Cloud Acceleration Manager.

La instancia de AEM de origen puede estar ejecutándose detrás de un cortafuegos en el que solo puede llegar a ciertos hosts que se han añadido a una Lista de permitidos. Para ejecutar correctamente una extracción, es necesario tener acceso a los siguientes extremos desde la instancia que se está ejecutando AEM:

* El servicio de almacenamiento del blob de Azure: `casstorageprod.blob.core.windows.net`
* El extremo de E/S de asignación de usuario: `usermanagement.adobe.io`

>[!NOTE]
>Si la extracción falla debido al siguiente error : &quot;javax.net.ssl.SSLHandsysException: sun.security.validator.ValidatorException: Error al crear la ruta PKIX: sun.security.provider.certpath.SunCertPathBuilderException: no se puede encontrar una ruta de certificación válida para el destino solicitado&quot;, esto se puede resolver importando el certificado de CA correspondiente.

### Habilitar el registro SSL {#enable-ssl-logging}

A veces es difícil comprender los problemas de conexión SSL/TLS. Para solucionar problemas de conexión durante un proceso de extracción, puede habilitar el registro SSL a través de la consola del sistema del entorno de AEM de origen siguiendo estos pasos:

1. Vaya a la consola web de Adobe Experience Manager en la instancia de origen, yendo a **Herramientas - Operaciones - Consola Web** o directamente a la dirección URL en *https://serveraddress:serverport/system/console/configMgr*
1. Buscar **Configuración del servicio de extracción de la herramienta de transferencia de contenido**
1. Utilice el botón de icono de lápiz para editar sus valores de configuración
1. Active la variable **Habilitar el registro ssl para la extracción** configuración y, a continuación, pulse **Guardar**:

   ![imagen](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## Ejecución de la herramienta de transferencia de contenido {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Ejecución de la herramienta de transferencia de contenido"
>abstract="Aprenda a utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación)."
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" Consulte Demostración"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial: uso de la herramienta de transferencia de contenido"

La siguiente sección se aplica a la nueva versión de la herramienta de transferencia de contenido. Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar contenido a AEM as a Cloud Service:

### Fase de configuración de extracción {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Fase de configuración de extracción"
>abstract="Obtenga información sobre cómo crear un conjunto de migración y copiar la clave de extracción."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="Tutorial: uso de la herramienta de transferencia de contenido"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. Inicie sesión en Cloud Acceleration Manager (CAM) y haga clic en el proyecto CAM que había creado anteriormente para evaluar su preparación para pasar a AEM as a Cloud Service. Si no ha creado ningún proyecto CAM, consulte Creación y administración de un proyecto en CAM.

1. Haga clic en el **Transferencia de contenido** tarjeta. Esto le llevará a la vista Lista de conjunto de migración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Cree un conjunto de migraciones haciendo clic en **Crear conjunto de migración**.

   >[!NOTE]
   >
   >Se puede crear un máximo de cinco conjuntos de migración por proyecto en Cloud Acceleration Manager.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. Ahora debería ver la lista de migración en la vista de lista. Haga clic en el símbolo de tres puntos (**...**) para abrir el menú desplegable y hacer clic en **Copiar clave de extracción**. Necesitará esta clave durante la fase de Extracción. Copie esta clave de Extracción.

   >[!NOTE]
   >
   >La clave de extracción permite que el entorno de AEM de origen se conecte de forma segura al conjunto de migración. Trate esta clave con el mismo cuidado que si usara una contraseña, y nunca la comparta en un medio no seguro como correo electrónico.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Rellenado del conjunto de migración {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Rellenar conjunto de migración&quot; abstract=&quot;Después de crear un conjunto de migración, debe rellenarse con el contenido de la instancia de origen que debe moverse al entorno as a Cloud Service AEM. Para ello, la herramienta de transferencia de contenido debe estar instalada en la instancia de origen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="Extracción de contenido"

Para rellenar el conjunto de migración creado en Cloud Acceleration Manager, debe instalar la última versión de la herramienta de transferencia de contenido en la instancia de Adobe Experience Manager (AEM) de origen. Siga esta sección para aprender a rellenar el conjunto de migración.

1. Después de instalar la última versión de la herramienta de transferencia de contenido en la instancia de Adobe Experience Manager de origen, vaya a **Operaciones: migración de contenido**

1. Haga clic en **Crear conjunto de migración**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Pegue la clave de extracción que se copió de CAM anteriormente en el campo de entrada de la clave de extracción de **Crear conjunto de migración** formulario. Una vez que lo haga, los campos Nombre del conjunto de migración y Nombre del proyecto de Cloud Acceleration Manager (CAM) se rellenarán automáticamente. Estas deberían coincidir con el nombre del conjunto de migración en CAM y con el nombre del proyecto CAM que ha creado. Ahora puede agregar rutas de contenido. Una vez que haya añadido rutas de contenido, podrá guardar el conjunto de migración. Puede ejecutar la extracción con versiones incluidas o excluidas.

   >[!NOTE]
   >
   >Asegúrese de que la clave de extracción sea válida y no esté cerca de su caducidad. Puede obtener esta información en la **Crear conjunto de migración** después de pegar la clave de extracción. Si se produce un error de conexión, consulte [Conectividad del entorno de origen](#source-environment-connectivity) para obtener más información.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. A continuación, seleccione los siguientes parámetros para crear un conjunto de migración:

   1. **Incluir versión**: seleccione la opción que desee. Cuando se incluyen versiones, la ruta `/var/audit` se incluye automáticamente para migrar eventos de auditoría.

      ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >Si tiene intención de incluir versiones como parte de un conjunto de migración y realiza complementos con `wipe=false`, debe desactivar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.


   1. **Rutas que se incluyen**: utilice el explorador para seleccionar las rutas que deben migrarse. El selector de rutas acepta entradas mediante escritura o selección.

      >[!IMPORTANT]
      >Las siguientes rutas están restringidas al crear un conjunto de migración:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (algunas `/etc` rutas permitidas para ser seleccionadas en CTT)


1. Haga clic en **Guardar** después de rellenar todos los campos en la variable **Crear conjunto de migración** pantalla de detalles.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Determinación del tamaño del conjunto de migración {#migration-set-size}

Después de crear un conjunto de migración, es muy recomendable ejecutar una comprobación de tamaño en el conjunto de migración antes de iniciar un proceso de Extracción.
Al ejecutar una comprobación de tamaño en el conjunto de migración, podrá:
* Determine si hay suficiente espacio en disco en la variable `crx-quickstart` para completar la extracción correctamente.
* Determine si el tamaño del conjunto de migración se encuentra dentro de los límites del producto admitidos y evite la ingesta fallida de contenido.

Siga los pasos a continuación para ejecutar una comprobación de tamaño:

1. Seleccione un conjunto de migración y haga clic en **Comprobar tamaño**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Esto abrirá las **Comprobar tamaño** diálogo.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. Haga clic en **Comprobar tamaño** para iniciar el proceso. A continuación, volverá a la vista de la lista de conjuntos de migración y verá un mensaje que indique que **Comprobar tamaño** se está ejecutando.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Una vez **Comprobar tamaño** se completa el proceso, el estado cambiará a **FINALIZADO**. Seleccione el mismo conjunto de migración y haga clic en **Comprobar tamaño** para ver los resultados. A continuación se muestra un ejemplo de **Comprobar tamaño** resultados sin advertencias.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. Si la variable **Comprobar tamaño** los resultados indican que no hay suficiente espacio en disco o que el conjunto de migración supera los límites del producto, **ADVERTENCIA** se muestra.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a crear un conjunto de migración, ya está listo para obtener información sobre los procesos de extracción e ingesta en la herramienta de transferencia de contenido. Antes de conocer estos procesos, debe revisar [Gestión de repositorios de contenido grandes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) para acelerar de forma significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y así mover el contenido a AEM as a Cloud Service.
