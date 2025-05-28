---
title: Introducción a la herramienta de transferencia de contenido
description: Obtenga información sobre cómo empezar a utilizar la herramienta de transferencia de contenido
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: 0c76419b5efa6d45cf4db51990633fea3b489063
workflow-type: tm+mt
source-wordcount: '1654'
ht-degree: 14%

---


# Introducción a la herramienta de transferencia de contenido {#getting-started-content-transfer-tool}


## Disponibilidad {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="Descargar"
>abstract="La herramienta de transferencia de contenido se puede descargar como un archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la última versión."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=es" text="Notas de la versión"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Portal de distribución de software"

La herramienta de transferencia de contenido se puede descargar como un archivo zip desde el portal de distribución de software. Puede instalar el paquete mediante [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en la instancia de origen de Adobe Experience Manager (AEM). Asegúrese de descargar la versión más reciente. Para obtener más información sobre la versión más reciente, consulte [Notas de la versión](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=es).

Solo se admite la versión 2.0.0 y posteriores, y es aconsejable utilizar la versión más reciente.

>[!NOTE]
>Descargue Content Transfer Tool desde el portal de [distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html).

## Conectividad del entorno de Source {#source-environment-connectivity}

>[!NOTE]
>
>También puede producirse un error de conexión si se ha eliminado un conjunto de migración de Cloud Acceleration Manager.

Es posible que la instancia de AEM de origen se esté ejecutando detrás de un cortafuegos donde solo puede llegar a ciertos hosts que se han añadido a una Lista de permitidos. Para ejecutar correctamente una extracción, es necesario poder acceder a los siguientes extremos desde la instancia que ejecuta AEM:

* El servicio de almacenamiento del blob de Azure: `casstorageprod.blob.core.windows.net`

>[!NOTE]
>Si la extracción falla debido al siguiente error : &quot;javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: Error al crear la ruta PKIX: sun.security.provider.certpath.SunCertPathBuilderException: no se puede encontrar la ruta de certificación válida al destino solicitado&quot;, esto se puede resolver importando el certificado de CA correspondiente.

### Habilitar registro SSL {#enable-ssl-logging}

A veces, es difícil comprender los problemas de conexión SSL/TLS. Para solucionar problemas de conexión durante un proceso de extracción, puede habilitar el registro SSL a través de la consola del sistema del entorno de AEM de origen siguiendo estos pasos:

1. Vaya a la consola web de Adobe Experience Manager en la instancia de origen, en **Herramientas > Operaciones > Consola web** o directamente a la dirección URL en *https://serveraddress:serverport/system/console/configMgr*
1. Buscar **Configuración del servicio de extracción de herramienta de transferencia de contenido**
1. Utilice el botón del icono de lápiz para editar sus valores de configuración
1. Habilite la opción **Habilitar el registro ssl para la extracción** y, a continuación, presione **Guardar**:

   ![imagen](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>Este indicador solo sirve para depurar problemas SSL. Asegúrese de que el indicador esté deshabilitado antes de ejecutar la extracción, ya que puede requerir una gran cantidad de espacio en disco. Esto podría llenar la capacidad de la unidad y provocar el fallo del proceso de extracción.

## Ejecución de la herramienta de transferencia de contenido {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="Ejecución de la herramienta de transferencia de contenido"
>abstract="Obtenga información acerca de cómo utilizar la herramienta de transferencia de contenido para migrar el contenido a AEM as a Cloud Service (autor/publicación)."
>additional-url="https://video.tv.adobe.com/v/327076/?quality=12&learn=on&captions=spa" text=" Consulte la demostración"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=es#migration" text="Tutorial: uso de la herramienta de transferencia de contenido"

La siguiente sección se aplica a la nueva versión de la herramienta de transferencia de contenido. Siga esta sección para aprender a utilizar la herramienta de transferencia de contenido para migrar contenido a AEM as a Cloud Service:

### Fase de configuración de la extracción {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="Fase de configuración de la extracción"
>abstract="Obtenga información sobre cómo crear y administrar un conjunto de migración y cómo copiar la clave de extracción."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=es#migration" text="Tutorial: uso de la herramienta de transferencia de contenido"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. Inicie sesión en Cloud Acceleration Manager (CAM) y haga clic en el proyecto CAM que había creado anteriormente para evaluar su preparación para pasar a AEM as a Cloud Service. Si no ha creado ningún proyecto CAM, consulte Creación y gestión de un proyecto en CAM.

1. Haga clic en la tarjeta **Transferencia de contenido** para abrir la vista Lista de conjuntos de migración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. Cree un conjunto de migración haciendo clic en **Crear conjunto de migración**.

   >[!NOTE]
   >
   >Se puede crear un máximo de 10 conjuntos de migración, incluidos conjuntos caducados, por proyecto en Cloud Acceleration Manager.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   Se muestra el siguiente cuadro de diálogo. Tenga en cuenta que un conjunto de migración caducará después de un período prolongado de inactividad. Después de mostrar advertencias en la tarjeta de proyecto y en las filas de la tabla de trabajos de migración durante un período de tiempo, el conjunto de migración caducará y sus datos dejarán de estar disponibles. Revise [Expiración del conjunto de migración](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) para obtener detalles.

   Durante la creación del conjunto de migración, puede elegir la región geográfica en la que se almacenarán los datos de migración temporales.  Se recomienda elegir la región más cercana al entorno de nube de Target para garantizar un rendimiento óptimo durante las ingestas.  La región no se puede cambiar después de crear el conjunto de migración; para utilizar una región diferente, deberá crear un nuevo conjunto de migración.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >El nombre debe seguir las mismas convenciones de un nodo AEM, por lo que no puede contener ninguno de estos caracteres: &grave;. / : [ ] | * &lt; > ^ ? { } % # &quot;ni ningún símbolo o emojis inusual.

1. Ahora debería ver la lista de migración en la vista de lista. Seleccione el símbolo de tres puntos (**...**) para abrir la lista desplegable y seleccione **Copiar clave de extracción**. Necesita esta clave durante la fase de extracción. Copie esta clave de extracción.

   >[!NOTE]
   >
   >La clave de extracción permite que el entorno de AEM de origen se conecte de forma segura al conjunto de migración. Trate esta clave con el mismo cuidado con el que haría con una contraseña y no la comparta nunca por un medio no seguro, como el correo electrónico.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### Rellenado del conjunto de migración {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Rellenar un conjunto de migración"
>abstract="Después de crear un conjunto de migración, debe rellenarse con el contenido de la instancia de origen que debe moverse al entorno de AEM as a Cloud Service. Para ello, la herramienta de transferencia de contenido debe instalarse en la instancia de origen."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=es" text="Extracción de contenido"

Para rellenar el conjunto de migración que ha creado en Cloud Acceleration Manager, instale la versión más reciente de la herramienta de transferencia de contenido en la instancia de origen de Adobe Experience Manager (AEM). Para obtener información sobre cómo rellenar el conjunto de migración, siga esta sección.

1. Después de instalar la versión más reciente de la herramienta de transferencia de contenido en la instancia de Adobe Experience Manager de origen, vaya a **Operaciones - Migración de contenido**

1. Haga clic en **Crear conjunto de migración**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. Pegue la clave de extracción que copió de CAM anteriormente en el campo de entrada de la clave de extracción del formulario **Crear conjunto de migración**. Después de hacer esto, los campos Nombre del conjunto de migración y Nombre del proyecto de Cloud Acceleration Manager (CAM) se rellenan automáticamente. Deben coincidir con el nombre del conjunto de migración de CAM y el nombre del proyecto de CAM que ha creado. Ahora puede añadir rutas de contenido. Después de agregar las rutas de contenido, guarde el conjunto de migración. Puede ejecutar la extracción con cualquiera de las versiones incluidas o excluidas.

   >[!NOTE]
   >
   >Asegúrese de que la clave de extracción sea válida y no esté cerca de su caducidad. Puede obtener esta información en el cuadro de diálogo **Crear conjunto de migración** después de pegar la clave de extracción. Si se produce un error de conexión, consulte [Conectividad del entorno de Source](#source-environment-connectivity) para obtener más información.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/createMigrationSet.png)

1. A continuación, seleccione los siguientes parámetros para crear un conjunto de migración:

   1. **Incluir versión**: seleccione según sea necesario. Cuando se incluyen versiones, la ruta `/var/audit` se incluye automáticamente para migrar eventos de auditoría.

      ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/includeVersion.png)

      >[!NOTE]
      >Si tiene intención de incluir versiones como parte de un conjunto de migración y está realizando recargas con `wipe=false`, debe deshabilitar la depuración de versiones debido a una limitación actual en la herramienta de transferencia de contenido. Si prefiere mantener habilitada la depuración de versiones y realiza recargas en un conjunto de migración, debe realizar la ingesta como `wipe=true`.

      >[!NOTE]
      >A partir de la versión de CTT (3.0.24), se han incluido nuevas funciones en la herramienta de transferencia de contenido, lo que mejora el proceso de incluir y excluir rutas. Anteriormente, las rutas debían seleccionarse una por una, lo que resultaba tedioso y laborioso. Ahora, los usuarios pueden incluir rutas directamente desde la interfaz de usuario o cargar un archivo CSV según sus preferencias.  El archivo CSV debe tener una ruta por línea y sin comas.

   1. **Rutas que se incluirán**: use el explorador de rutas para seleccionar las rutas que deben migrarse. El selector de rutas acepta entradas escribiendo o seleccionando. Los usuarios solo pueden seleccionar una opción para incluir las rutas: desde la interfaz de usuario de o cargando un archivo CSV.

      >[!IMPORTANT]
      >Las siguientes rutas están restringidas al crear un conjunto de migración:
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (se permite seleccionar algunas `/etc` rutas en CTT)

      ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/includeAndExcludePath.png)

      1. Solo se permite la selección de rutas y debe haber al menos una ruta. Si no se selecciona ninguna ruta, se producirá un error del servidor.

         ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ServerError.png)

      1. Al usar la **opción de carga CSV**, el archivo CSV debe contener rutas de acceso válidas.

         ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validCsvUpload.png)

      1. Para volver al selector de rutas, los usuarios deben actualizar la página y volver a empezar.

      1. Si se encuentran **rutas de acceso no válidas** en el archivo CSV cargado, aparecerá un cuadro de diálogo independiente con las rutas de acceso no válidas.

         ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/invalidPathsInCsv.png)

      1. Los usuarios deben corregir el archivo CSV y cargarlo de nuevo o actualizar la interfaz de usuario para seleccionar rutas a través del selector de rutas.

   1. **Rutas que se excluirán**: Una nueva característica permite a los usuarios excluir rutas específicas si no desean que se incluyan. Por ejemplo, si la ruta de la sección de inclusión es /content/dam, los usuarios ahora pueden excluir rutas como /content/dam/catalogs.

      ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/excludePathHighlighted.png)

1. Haga clic en **Guardar** después de rellenar todos los campos en la pantalla de detalles de **Crear conjunto de migración**.

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### Determinación del tamaño del conjunto de migración {#migration-set-size}

Después de crear un conjunto de migración, es muy recomendable ejecutar una comprobación de tamaño en el conjunto antes de iniciar un proceso de extracción.
Al realizar una comprobación de tamaño en el conjunto de migración, puede:

* Determine si hay suficiente espacio en disco en el subdirectorio `crx-quickstart` para completar la extracción correctamente.
* Determine si el tamaño del conjunto de migración se encuentra dentro de los límites del producto admitido y evite las ingestas de contenido fallidas.

Siga los pasos a continuación para ejecutar una comprobación de tamaño:

1. Seleccione un conjunto de migración y haga clic en **Comprobar tamaño**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. Esto abre el cuadro de diálogo **Comprobar tamaño**.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/checkMigrationSetSize.png)

1. Haga clic en **Comprobar tamaño** para iniciar el proceso. Volverá a la vista de lista del conjunto de migración y verá un mensaje que indica que **Comprobar tamaño** se está ejecutando.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. Una vez completado el proceso **Comprobar tamaño**, el estado cambia a **FINALIZADO**. Seleccione el mismo conjunto de migración y haga clic en **Comprobar tamaño** para ver los resultados. A continuación se muestra un ejemplo de **Comprobar tamaño** resultados sin advertencias.

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/checkSizeAfterFinished.png)

1. Si los resultados de **Comprobar tamaño** indican que no hay suficiente espacio en disco o que el conjunto de migración supera los límites del producto, o ambos, se muestra un estado **ADVERTENCIA**.

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## Siguientes pasos {#whats-next}

Una vez que haya aprendido a crear un conjunto de migración, ya puede obtener información sobre los procesos de extracción e ingesta en la herramienta de transferencia de contenido. Antes de aprender estos procesos, debe revisar [Gestión de repositorios de contenido grandes](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para acelerar de manera significativa las fases de extracción e ingesta de la actividad de transferencia de contenido y mover contenido a AEM as a Cloud Service.
