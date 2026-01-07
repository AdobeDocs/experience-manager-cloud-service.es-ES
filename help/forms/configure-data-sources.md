---
title: Configuración de las fuentes de datos?
description: Aprenda a configurar los servicios web RESTful, los servicios web basados en SOAP y los servicios OData como fuentes de datos para un modelo de datos de formulario (FDM).
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: f913871da16b44d7a465e0fa00608835524ba7e3
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 94%

---


# Configuración de las fuentes de datos {#configure-data-sources}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

![Integración de datos](do-not-localize/data-integeration.png)

La integración de datos de [!DNL Experience Manager Forms] le permite configurar y conectarse a fuentes de datos diferentes. Los siguientes tipos son compatibles de forma predeterminada:

* Bases de datos relacionales: MySQL, [!DNL Microsoft® SQL Server], [!DNL IBM® DB2®], postgreSQL, Azure SQL y [!DNL Oracle RDBMS]
* Servicios web RESTful
* Servicios web basados en SOAP
* Servicios OData (versión 4.0)
* Microsoft® Dynamics
* SalesForce
* Microsoft® Azure Blob Storage

La integración de datos es compatible con los tipos de autenticación OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica y clave de la API predeterminados, y permite implementar la autenticación personalizada para acceder a servicios web. Mientras que los servicios RESTful, basados en SOAP y OData están configurados en [!DNL Experience Manager] as a Cloud Service, JDBC para bases de datos relacionales y conector para el perfil de usuario de [!DNL Experience Manager] están configurados en la consola web de [!DNL Experience Manager].

## Configuración de la base de datos relacional {#configure-relational-database}

### Requisitos previos

Antes de configurar bases de datos relacionales mediante la configuración de la consola web de [!DNL Experience Manager], es obligatorio lo siguiente:

* [Habilitar las redes avanzadas mediante la API de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=es), ya que los puertos están deshabilitados de forma predeterminada.
* [Añadir dependencias de controladores JDBC en Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=es#mysql-driver-dependencies).


### Pasos para configurar una base de datos relacional

Puede configurar bases de datos relacionales mediante la configuración de la consola web de [!DNL Experience Manager]. Haga lo siguiente:

**Paso 1: clonar el repositorio Git de AEM as a Cloud Service**

1. Abra la línea de comandos y seleccione un directorio para almacenar el repositorio de AEM as a Cloud Service, como `/cloud-service-repository/`.

2. Ejecute el siguiente comando para clonar el repositorio:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **¿Dónde se encuentra esta información?**

   Para obtener instrucciones paso a paso sobre cómo localizar estos detalles, consulte el artículo de Adobe Experience League “[Acceder a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git)”.

   Cuando el comando se complete correctamente, verá que se ha creado una nueva carpeta en su directorio local. Esta carpeta recibe el nombre de su aplicación.

**Paso 2: Vaya a la carpeta de configuración**

1. Abra la carpeta del repositorio en un editor.

1. Vaya al siguiente directorio de su `<application folder>` donde se debe colocar la configuración OSGi para el grupo JDBC:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Paso 3: Crear el archivo de configuración de la conexión MySQL**

1. Cree el archivo:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-mysql.cfg.json
   ```

1. Añada las siguientes líneas de código:

```json
{
  "jdbc.driver.class": "com.mysql.cj.jdbc.Driver",
  "jdbc.connection.uri": "jdbc:mysql://<hostname>:<port>/<database>?useSSL=false",
  "jdbc.username": "<your-db-username>",
  "jdbc.password": "<your-db-password>",
  "datasource.name": "<application folder>-mysql",
  "datasource.svc.prop.name": "<application folder>-mysql"
}
```

> 
>
> Reemplace marcadores de posición como `<application folder>`, `<hostname>`, `<database>`, `<your-db-username>` y `<your-db-password>` con valores reales.

**Paso 4: confirmar y enviar los cambios**

Abra el terminal y ejecute los siguientes comandos:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Paso 5: Implementar los cambios a través de la canalización de Cloud Manager**

1. Inicie sesión en **AEM Cloud Manager**.
1. Vaya al proyecto y ejecute la canalización para implementar los cambios.

>[!NOTE]
>
> Consulte las [Conexiones SQL con el conjunto de fuentes de datos JDBC](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=es) para obtener información más detallada.

<!--
1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
2. Locate **[!UICONTROL Day Commons JDBC Connections Pools]** configuration. Select to open the configuration in edit mode.

   ![JDBC Connector Pool](/help/forms/assets/jdbc_connector.png)

3. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Java&trade; class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver
    * Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:
      * SELECT 1 (MySQL and MS&reg; SQL) 
      * SELECT 1 from dual (Oracle)
    * Name of the data source

   Sample strings for configuring a relational database:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```


    
4. Select **[!UICONTROL Save]** to save the configuration.

Now, you can use the configured relational database with your Form Data Model (FDM). 

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## Configurar carpetas para configuraciones de servicios en la nube {#cloud-folder}

La configuración de la carpeta de servicios en la nube es necesaria para configurar los servicios en la nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube en [!DNL Experience Manager] se consolidan en la carpeta `/conf`, en el repositorio [!DNL Experience Manager]. De forma predeterminada, la carpeta `conf` contiene la carpeta `global`, donde puede crear configuraciones de servicios en la nube. Con todo, debe habilitarlo manualmente para las configuraciones en la nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicios en la nube.

Para configurar la carpeta para las configuraciones de servicios en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   * Consulte la documentación del [Explorador de configuración](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=es) para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube u omita este paso para crear y configurar otra carpeta para configuraciones de servicios en la nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione la carpeta `global` y **[!UICONTROL Propiedades]**.

   1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

   1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Seleccione **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.

## Configurar servicios web de RESTful {#configure-restful-web-services}

Los servicios web RESTful se pueden describir con las [especificaciones de Swagger](https://swagger.io/specification/v2/) en formato JSON o YAML en un archivo de definición de [!DNL Swagger] o un punto final de servicio.

>[!NOTE]
> Para configurar el servicio web RESTful en [!DNL Experience Manager] as a Cloud Service, asegúrese de que dispone del archivo [!DNL Swagger] ([versión 2.0 de Swagger](https://swagger.io/specification/v2/)) o [!DNL Swagger] ([versión 3.0 de Swagger](https://swagger.io/specification/v3/)) en su sistema de archivos o la URL donde se hospeda el archivo.

### Configure los servicios RESTful para la versión 2.0 de la especificación de API abierta {#configure-restful-services-open-api-2.0}

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione la URL o archivo en la lista desplegable [!UICONTROL Fuente de Swagger] y, en consecuencia, especifique el [!DNL Swagger URL] para el archivo de definición [!DNL &#x200B; Swagger] o cargue el archivo [!DNL Swagger] de su sistema de archivos local.
   * En función de la entrada de fuente de [!DNL &#x200B; Swagger], los siguientes campos aparecen ya cumplimentados con valores:

      * Esquema: Los protocolos de transferencia utilizados por el API de REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en la fuente de [!DNL Swagger].
      * Host: El nombre de dominio o la dirección IP del host que sirve el API de REST. Es un campo obligatorio.
      * Ruta base: El prefijo URL de todas las rutas de API. Es un campo opcional.\
        Si es necesario, edite los valores rellenados previamente para estos campos.

   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica, clave de la API o autenticación personalizada) para acceder al servicio RESTful y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

### Configurar servicios RESTful para la versión 3.0 de la especificación de API abierta {#configure-restful-services-open-api-3.0}

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione la URL o archivo en la lista desplegable [!UICONTROL Fuente de Swagger] y, en consecuencia, especifique la [!DNL Swagger 3.0 URL] para el archivo de definición [!DNL &#x200B; Swagger] o cargue el archivo [!DNL Swagger] de su sistema de archivos local.
   * En función de la entrada de origen de [!DNL &#x200B; Swagger], se muestra la información de conexión con el servidor de destino.
   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica, clave de la API o autenticación personalizada) para acceder al servicio RESTful y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

Algunas de las operaciones no admitidas por los servicios de la especificación de API abierta versión 3.0 son las siguientes:

* Rellamadas
* Uno de/cualquiera de
* Referencia remota
* Vínculos
* Diferentes cuerpos de solicitud para diferentes tipos de MIME para una sola operación

Consulte [Especificación de OpenAPI 3.0](https://swagger.io/specification/v3/) para obtener información detallada.

### Configuración de servicios RESTful mediante el punto final de servicio {#configure-restful-services-service-endpoint}

<span class="preview"> La capacidad de punto final de servicio está en el programa para primeros usuarios y solo se aplica a los componentes principales. Puede enviar un correo electrónico a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa para primeros usuarios y solicitar acceso a esta funcionalidad. </span>

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL asistente Crear configuración de origen de datos]**. 

1. Especifique un nombre y, opcionalmente, un título para la configuración. Seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.

1. En la página siguiente, seleccione **[!UICONTROL Punto final de servicio]** de la **[!UICONTROL lista desplegable Servicio RESTful]**.

   ![Punto final de servicio](/help/forms/assets/select-service-endpoint.png)

1. Especifique la **[!UICONTROL URL de punto final de servicio]**.

   >[!NOTE]
   > De forma predeterminada, el tipo de método es POST.
1. Seleccione el tipo de contenido que prefiera de la lista desplegable. Los tipos de contenido son datos de formulario de varias partes, JSON y con codificación de URL (par clave-valor).
1. Ahora puede seleccionar cualquiera de los tipos de autenticación, como OAuth 2.0, autenticación básica, clave API o autenticación personalizada, en la lista desplegable.
   ![Tipo de autenticación de punto final de servicio](/help/forms/assets/service-endpoint-authtype.png)
1. Haga clic en Crear.

### Configuración del cliente HTTP del modelo de datos de formulario (FDM) para optimizar el rendimiento {#fdm-http-client-configuration}

Modelo de datos del formulario [!DNL Experience Manager Forms] al integrarse con los servicios web RESTful, ya que la fuente de datos incluye configuraciones de cliente HTTP para la optimización del rendimiento.

Establezca las siguientes propiedades de la configuración **[!UICONTROL Configuración del cliente HTTP del modelo de datos de formulario para fuente de datos de REST]** para especificar la expresión regular:

* Utilice la propiedad `http.connection.max.per.route` para establecer el número máximo de conexiones permitidas entre el modelo de datos de formulario (FDM) y los servicios web RESTful. El valor predeterminado es 20 conexiones.

* Utilice la propiedad `http.connection.max` para especificar el número máximo de conexiones permitidas para cada ruta. El valor predeterminado es 40 conexiones.

* Utilice la propiedad `http.connection.keep.alive.duration` para especificar la duración durante la cual se mantiene activa una conexión HTTP persistente. El valor predeterminado es 15 segundos.

* Utilice la propiedad `http.connection.timeout` para especificar la duración, durante la cual el servidor [!DNL Experience Manager Forms] espera a que se establezca una conexión. El valor predeterminado es 10 segundos.

* Utilice la propiedad `http.socket.timeout` para especificar el período máximo de inactividad entre dos paquetes de datos. El valor predeterminado es 30 segundos.

El siguiente archivo JSON muestra un ejemplo:


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. Seleccione **[!UICONTROL Configuración del cliente HTTP del modelo de datos de formulario para fuente de datos de REST]**.

1. En el diálogo [!UICONTROL Configuración del cliente HTTP del modelo de datos de formulario para fuente de datos de REST]:

   * Especifique el número máximo de conexiones permitidas entre el modelo de datos de formulario (FDM) y los servicios web RESTful en el campo **[!UICONTROL Límite de conexión en total]**. El valor predeterminado es 20 conexiones.

   * Especifique el número máximo de conexiones permitidas para cada ruta en el campo **[!UICONTROL Límite de conexión por ruta]**. El valor predeterminado son dos conexiones.

   * Especifique la duración, durante la cual se mantiene activa una conexión HTTP persistente, en el campo **[!UICONTROL Mantener activa]**. El valor predeterminado es 15 segundos.

   * Especifique la duración durante la que el servidor [!DNL Experience Manager Forms] espera a que se establezca una conexión, en el campo **[!UICONTROL Tiempo de espera de conexión]**. El valor predeterminado es 10 segundos.

   * Especifique el período de tiempo máximo de inactividad entre dos paquetes de datos en el campo **[!UICONTROL Tiempo de espera de la toma]**. El valor predeterminado es 30 segundos.

## Configurar servicios web SOAP {#configure-soap-web-services}

Los servicios web basados en SOAP se describen utilizando [Especificaciones del lenguaje de descripción de servicios web (WSDL)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] no admite el modelo WSDL de estilo RPC.

Para configurar el servicio web basado en SOAP en [!DNL Experience Manager] as a Cloud Service, asegúrese de que cuenta con la URL de WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear las fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio web SOAP]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL de WSDL para el servicio web.
   * Punto final de servicio. Especifique un valor en este campo para anular el punto final de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación (ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica o autenticación personalizada) para acceder al servicio SOAP y facilitar los detalles correspondientes para la autenticación.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio web SOAP.

### Habilitar el uso de instrucciones de importación en el WSDL de los servicios web SOAP {#enable-import-statements}

Puede especificar una expresión regular que sirva como filtro para las URL absolutas permitidas como instrucciones de importación en el WSDL de los servicios web SOAP. De forma predeterminada, no hay ningún valor en este campo. Como resultado, [!DNL Experience Manager] bloquea todas las instrucciones de importación disponibles en WSDL. Si especifica `.*` como el valor de este campo, [!DNL Experience Manager] permite todas las instrucciones de importación.

Establezca la propiedad `importAllowlistPattern` de la configuración **[!UICONTROL Lista de permitidos de importación de servicios web SOAP del modelo de datos de formulario]** configuración para especificar la expresión regular. El siguiente archivo JSON muestra un ejemplo:

```json
{
  "importAllowlistPattern": ".*"
}
```

Para establecer los valores de una configuración, [Generar configuraciones OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implemente la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) a su instancia de Cloud Service.

## Configurar servicios OData {#config-odata}

Un servicio OData se identifica mediante su URL raíz de servicio. Para configurar un servicio OData en [!DNL Experience Manager] as a Cloud Service, asegúrese de que tiene una URL raíz de servicio para el servicio y haga lo siguiente:

>[!NOTE]
>
> El modelo de datos de formulario (FDM) es compatible con la [versión 4 de OData](https://www.odata.org/documentation/).
>Para obtener una guía paso a paso sobre la configuración de [!DNL Microsoft®® Dynamics 365], en línea o de forma local, consulte [[!DNL Microsoft® Dynamics] Configuración de OData](ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Seleccione para elegir la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Seleccione **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y seleccionar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL raíz del servicio para configurar el servicio OData.
   * Seleccione el tipo de autenticación (ninguna, OAuth2.0,([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales de cliente](https://oauth.net/2/grant-types/client-credentials/)), autenticación básica, clave de la API o autenticación personalizada) para acceder al servicio OData y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   >[!NOTE]
   >
   >Debe seleccionar el tipo de autenticación OAuth 2.0 con el que conectarse a los servicios de [!DNL Microsoft®® Dynamics] que utilizan el punto final OData como raíz de servicio.

1. Seleccione **[!UICONTROL Crear]** para crear la configuración de nube para el servicio OData.

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Pasos siguientes {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un modelo de datos de formulario (FDM) o, si ya ha creado uno sin fuente de datos, puede asociarlo a la fuente de datos que acaba de configurar. Consulte [Crear un modelo de datos de formulario](create-form-data-models.md) para obtener más información.

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->