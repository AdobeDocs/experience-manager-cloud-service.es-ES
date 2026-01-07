---
Title: How to Connect AEM Adaptive Forms with Azure SQL Storage
Description: Learn how to configure an Azure SQL Database connection in AEM Forms and integrate it with your Adaptive Forms to store or retrieve data efficiently using JDBC.
Keywords: Azure SQL integration with AEM Forms, Connecting Adaptive Forms to Azure SQL Database, JDBC connection for Azure SQL in AEM Forms, Storing Adaptive Form data in Azure SQL
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: 40193d89f2a4ef864a564eb9932403531eaf1ff7
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 15%

---

# Conectar un formulario adaptable al almacenamiento SQL de Azure

Forms adaptable en Adobe Experience Manager (AEM) se puede integrar con bases de datos externas para almacenar o recuperar datos.
Este artículo describe cómo conectar un formulario adaptable a una base de datos SQL de Azure mediante JDBC a través de AEM as a Cloud Service.

> 
> 
> Esta guía se aplica a entornos AEM as a Cloud Service que no son de zona protegida con redes avanzadas habilitadas.

## Ventajas

La integración de Forms adaptable con Azure SQL ofrece varias ventajas:

* **Interacción de datos en tiempo real:** Permite la lectura y escritura en tiempo real de datos entre formularios y la base de datos de Azure.
* **Escalabilidad:** Azure SQL proporciona un rendimiento de base de datos escalable adecuado para aplicaciones de nivel empresarial.
* **Almacenamiento de datos centralizado:** Mantiene los envíos de formularios y los datos recuperados almacenados de forma segura en una ubicación central.
* **Cumplimiento de la seguridad:** Aprovecha las opciones integradas de red, firewall y cifrado de Azure para garantizar una comunicación segura.
* **Integración nativa de la nube:** Ideal para arquitecturas modernas y con prioridad en la nube que usan AEM as a Cloud Service.

## Requisitos previos

* Cree [Azure SQL Database](https://learn.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart?view=azuresql&tabs=azure-portal) y asegúrese de que la **conexión proxy** esté habilitada.

  >[!NOTE]
  >
  > Vaya a: `Azure Portal → SQL Server → Security → Networking → Connectivity` para habilitar la **conexión proxy**.

  ![Crear Azure Db](/help/forms/assets/create-azure-db.png)

* Habilite [red avanzada configurada con una IP de salida dedicada](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/dedicated-egress-ip-address) para la base de datos de Azure creada.

  >[!NOTE]
  >
  >    Después de habilitar la IP de salida dedicada. Vaya a `Azure Portal → SQL Server → Security → Networking → Public Access` y agregue la dirección IP de salida a las reglas del firewall.

  ![IP de salida](/help/forms/assets/cretae-azure-db-egress-ip.png)

* Configure el reenvío de puertos en el entorno de la nube con:
   * **portOrigin**: entre `30000–30999`
   * **portDest**: `1433` (puerto predeterminado para Azure SQL)
Por ejemplo: `portOrigin: 30433 → portDest: 1433`

     > 
     > 
     > Puede ponerse en contacto con el servicio de asistencia de Adobe Cloud Manager para configurar el reenvío de puertos.


## Pasos para conectar Forms adaptable a Azure SQL

**Paso 1: clonar el repositorio Git de AEM as a Cloud Service**

1. Abra la línea de comandos y seleccione un directorio para almacenar el repositorio de AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Ejecute el siguiente comando para clonar el repositorio:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **¿Dónde se encuentra esta información?**

   Para obtener instrucciones paso a paso sobre cómo localizar estos detalles, consulte el artículo de Adobe Experience League “[Acceder a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git)”.

   Cuando el comando se complete correctamente, verá que se ha creado una nueva carpeta en su directorio local. Esta carpeta recibe el nombre de su aplicación.

1. Abra la carpeta del repositorio en un editor.

**Paso2: Agregar JAR requeridos**

Incluya la [dependencia del controlador SQL](https://central.sonatype.com/artifact/com.microsoft.sqlserver/mssql-jdbc/12.8.0.jre11?smo=true) al proyecto de AEM a través del paquete `all`.:

>[!NOTE]
>
> Para incluir la dependencia SQL en su proyecto, consulte la sección [Dependencias del controlador SQL](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool#mysql-driver-dependencies).

**Paso 3: Agregar Configuración JDBC**

1. Vaya al siguiente directorio de su `<application folder>` donde se debe colocar la configuración OSGi para el grupo JDBC:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Paso 4: crear el archivo de configuración de Azure SQL Connection**

1. Cree el archivo:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-sql.cfg.json
   ```

1. Añada las siguientes líneas de código:

   ```json
   {
   "datasource.name": "azuredbshr",
   "jdbc.driver.class": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
   "jdbc.username": "<azureuser>",
   "jdbc.connection.uri": "jdbc:sqlserver://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30433;database=testdb;user=<azureuser>;password=<azurepassword>;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;",
   "jdbc.password": "******",
   "jdbc.validation.query": "SELECT 1"
       }
   ```

   > 
   >
   > Reemplace `jdbc.username` con el nombre de usuario de Azure real y `jdbc.password` con la contraseña segura real.

**Paso 5: confirmar y enviar los cambios**

Abra el terminal y ejecute los siguientes comandos:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Paso 6: Implementar los cambios a través de la canalización de Cloud Manager**

1. Inicie sesión en **AEM Cloud Manager**.
1. Vaya al proyecto y ejecute la canalización para implementar los cambios.

**Paso 7: Crear un modelo de datos de formulario (FDM)**

Una vez completada la configuración de AEM y Azure y implementados los cambios de código:

1. Vaya a la instancia de autor de AEM.
1. Vaya a **Herramientas** > **Forms** > **Integraciones de datos**.
1. Crear nuevo **modelo de datos de formulario**.
1. En la pestaña **Fuentes de datos**, seleccione la configuración JDBC creada.
1. Haga clic en **[!UICONTROL Crear]** y verifique la conexión.

![Crear modelo de datos de formulario](/help/forms/assets/create-azure-sql-fdm.png)

**Paso 8: usar el FDM creado en un formulario adaptable**

1. Abra un formulario adaptable en modo de edición.
1. Seleccione el FDM creado en el paso anterior como modelo de datos.
1. Use [enlaces de datos para conectar campos de formulario con la fuente de datos SQL de Azure](/help/forms/work-with-form-data-model.md#add-data-model-objects-and-services) y configurar la acción de envío.

## Prácticas recomendadas

* Use **secret management** para evitar contraseñas de codificación en los archivos de configuración.
* Gire con regularidad las credenciales de la base de datos y actualice la configuración de forma segura.
* Monitorice los registros de conectividad JDBC para detectar errores y latencia.
* Siga las prácticas recomendadas de Azure para proteger las bases de datos SQL y las configuraciones de firewall.
* Evite utilizar cuentas de base de datos con privilegios elevados para acceder a formularios.

## Artículos relacionados

{{af-submit-action}}