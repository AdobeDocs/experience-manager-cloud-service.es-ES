---
title: Configurar fuentes de datos
description: La integración de datos de Experience Manager Forms le permite configurar y conectarse a fuentes de datos diferentes. Aprenda a configurar los servicios web RESTful, los servicios web basados en SOAP y los servicios OData como fuentes de datos y a utilizarlos para crear modelos de datos de formulario.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: ac525d2500177229221a5d6f79d2a8feeefe3f06
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 91%

---

# Configurar fuentes de datos {#configure-data-sources}

![Integración de datos](do-not-localize/data-integeration.png)

La integración de datos de [!DNL Experience Manager Forms] le permite configurar y conectarse a fuentes de datos diferentes. Los siguientes tipos son compatibles de forma predeterminada:

* Bases de datos relacionales: MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2] y [!DNL Oracle RDBMS]
* Servicios web RESTful
* Servicios web basados en SOAP
* Servicios OData (versión 4.0)
* Microsoft® Dynamics
* SalesForce
* Microsoft® Azure Blob Storage

La integración de datos es compatible con OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica y Tipos de autenticación de clave de API predeterminados, y permite implementar la autenticación personalizada para acceder a servicios web. Mientras que los servicios RESTful, basados en SOAP y OData están configurados en [!DNL Experience Manager] as a Cloud Service, JDBC para bases de datos relacionales y conector para el perfil de usuario de [!DNL Experience Manager] están configurados en la consola web de [!DNL Experience Manager].

## Configuración de la base de datos relacional {#configure-relational-database}

### Requisitos previos

Antes de configurar bases de datos relacionales mediante la configuración de la consola web de [!DNL Experience Manager], es obligatorio lo siguiente:
* [Habilitar redes avanzadas mediante la API de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=es), ya que los puertos están desactivados de forma predeterminada.
* [Añadir dependencias de controladores JDBC en Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=es#mysql-driver-dependencies).


### Pasos para configurar una base de datos relacional

Puede configurar bases de datos relacionales mediante la configuración de la consola web de [!DNL Experience Manager]. Haga lo siguiente:

1. Vaya a la consola web de [!DNL Experience Manager] en `https://server:host/system/console/configMgr`.
1. Localice la configuración de **[!UICONTROL Grupos de conexiones JDBC de Day Commons]**. Pulse para abrir la configuración en modo de edición.

   ![Grupo de conectores JDBC](/help/forms/assets/jdbc_connector.png)

1. En el cuadro de diálogo de configuración, especifique los detalles de la base de datos que desea configurar, como por ejemplo, los siguientes:

   * Nombre de clase Java™ para el controlador JDBC
   * URI de conexión JDBC
   * Nombre de usuario y contraseña para establecer conexión con el controlador JDBC
   * Especifique una consulta SQL SELECT en el campo **[!UICONTROL Consulta de validación]** para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. En función de la base de datos, especifique una de las siguientes opciones:
      * SELECT 1 (MySQL y MS SQL)
      * SELECT 1 desde dual (Oracle)
   * Nombre de la fuente de datos

   Cadenas de muestra para configurar una base de datos relacional:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Consulte [Conexiones SQL con el conjunto de fuentes de datos JDBC](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=es) para obtener información más detallada.

1. Pulse **[!UICONTROL Guardar]** para guardar la configuración.

Ahora puede utilizar la base de datos relacional configurada con el modelo de datos de formulario.

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## Configurar carpetas para configuraciones de servicios en la nube {#cloud-folder}

La configuración de la carpeta de servicios en la nube es necesaria para configurar los servicios en la nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube en [!DNL Experience Manager] se consolidan en la carpeta `/conf`, en el repositorio [!DNL Experience Manager]. De forma predeterminada, la carpeta `conf` contiene la carpeta `global`, donde puede crear configuraciones de servicios en la nube. Con todo, debe habilitarlo manualmente para las configuraciones en la nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicios en la nube.

Para configurar la carpeta para las configuraciones de servicios en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   * Consulte la documentación del [Explorador de configuración](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html?lang=es) para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube u omita este paso para crear y configurar otra carpeta para configuraciones de servicios en la nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione la carpeta `global` y pulse **[!UICONTROL Propiedades]**.

   1. En el cuadro de diálogo **[!UICONTROL Propiedades de configuración]**, habilite **[!UICONTROL Configuraciones de nube]**.

   1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Pulse **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.

## Configurar servicios web de RESTful {#configure-restful-web-services}

El servicio web RESTful se puede describir con las [especificaciones de Swagger](https://swagger.io/specification/v2/) en formato JSON o YAML en un archivo de definición [!DNL Swagger]. Para configurar el servicio web RESTful en [!DNL Experience Manager] as a Cloud Service, asegúrese de que dispone del archivo [!DNL Swagger] ([versión 2.0 de Swagger](https://swagger.io/specification/v2/)) o [!DNL Swagger] ([versión 3.0 de Swagger](https://swagger.io/specification/v3/)) en su sistema de archivos o la URL donde se hospeda el archivo.

### Configuración de servicios RESTful para la especificación de API abierta versión 2.0 {#configure-restful-services-open-api-2.0}

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Pulse **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione la URL o archivo en la lista desplegable [!UICONTROL Fuente de Swagger] y, en consecuencia, especifique la [!DNL Swagger URL] al archivo de definición [!DNL  Swagger] o cargue el archivo [!DNL Swagger] de su sistema de archivos local.
   * En función de la entrada de fuente de [!DNL  Swagger], los siguientes campos aparecen ya cumplimentados con valores:

      * Esquema: Los protocolos de transferencia utilizados por el API de REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en la fuente de [!DNL Swagger].
      * Host: El nombre de dominio o la dirección IP del host que sirve el API de REST. Es un campo obligatorio.
      * Ruta base: El prefijo URL de todas las rutas de API. Es un campo opcional.\
         Si es necesario, edite los valores rellenados previamente para estos campos.
   * Seleccione el tipo de autenticación — Ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica, Clave de API o Autenticación personalizada: para acceder al servicio RESTful y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Pulse **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

### Configuración de servicios RESTful para la especificación de API abierta versión 3.0 {#configure-restful-services-open-api-3.0}

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Pulse **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** en la lista desplegable **[!UICONTROL Tipo de servicio]**; opcionalmente puede examinar y seleccionar una imagen de miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione la URL o archivo en la lista desplegable [!UICONTROL Fuente de Swagger] y, en consecuencia, especifique la [!DNL Swagger 3.0 URL] al archivo de definición [!DNL  Swagger] o cargue el archivo [!DNL Swagger] de su sistema de archivos local.
   * En función de la entrada de origen de [!DNL  Swagger], se muestra la información de conexión con el servidor de destino.
   * Seleccione el tipo de autenticación — Ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica, Clave de API o Autenticación personalizada: para acceder al servicio RESTful y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Pulse **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

Algunas de las operaciones no admitidas por los servicios de la especificación de API abierta versión 3.0 son las siguientes:
* Rellamadas
* uno de/cualquiera de
* Referencia remota
* Vínculos
* Diferentes cuerpos de solicitud para diferentes tipos de MIME para una sola operación

Puede consultar [Especificación de API abierta 3.0 ](https://swagger.io/specification/v3/) para obtener información detallada.

### Configuración del cliente HTTP del modelo de datos del formulario para optimizar el rendimiento {#fdm-http-client-configuration}

Modelo de datos del formulario [!DNL Experience Manager Forms] al integrarse con los servicios web RESTful, ya que la fuente de datos incluye configuraciones de cliente HTTP para la optimización del rendimiento.

Establezca las siguientes propiedades de la configuración **[!UICONTROL Configuración del cliente HTTP del modelo de datos del formulario para fuente de datos de REST]** para especificar la expresión regular:

* Utilice la propiedad `http.connection.max.per.route` para establecer el número máximo de conexiones permitidas entre el modelo de datos de formulario y los servicios web RESTful. El valor predeterminado es 20 conexiones.

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

1. Pulse **[!UICONTROL Configuración del cliente HTTP del modelo de datos del formulario para fuente de datos de REST]**.

1. En el diálogo [!UICONTROL Configuración del cliente HTTP del modelo de datos del formulario para fuente de datos de REST]:

   * Especifique el número máximo de conexiones permitidas entre el modelo de datos de formulario y los servicios web RESTful en el campo **[!UICONTROL Límite de conexión en total]**. El valor predeterminado es 20 conexiones.

   * Especifique el número máximo de conexiones permitidas para cada ruta en el campo **[!UICONTROL Límite de conexión por ruta]**. El valor predeterminado son dos conexiones.

   * Especifique la duración, durante la cual se mantiene activa una conexión HTTP persistente, en el campo **[!UICONTROL Mantener activa]**. El valor predeterminado es 15 segundos.

   * Especifique la duración durante la que el servidor [!DNL Experience Manager Forms] espera a que se establezca una conexión, en el campo **[!UICONTROL Suspensión de la conexión]**. El valor predeterminado es 10 segundos.

   * Especifique el período de tiempo máximo de inactividad entre dos paquetes de datos en el campo **[!UICONTROL Suspensión de la toma]**. El valor predeterminado es 30 segundos.

## Configurar servicios web SOAP {#configure-soap-web-services}

Los servicios web basados en SOAP se describen utilizando [Especificaciones del lenguaje de descripción de servicios web (WSDL)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] no son compatibles con el modelo WSDL de estilo RPC.

Para configurar el servicio web basado en SOAP en [!DNL Experience Manager] as a Cloud Service, asegúrese de que cuenta con la URL de WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Pulse **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio web SOAP]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y pulsar **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL de WSDL para el servicio web.
   * Punto final de servicio. Especifique un valor en este campo para anular el punto final de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación — Ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica o Autenticación personalizada: para acceder al servicio SOAP y facilitar los detalles correspondientes para la autenticación.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Pulse **[!UICONTROL Crear]** para crear la configuración de nube para el servicio web SOAP.

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
> El modelo de datos de formulario es compatible con la [versión 4 de OData](https://www.odata.org/documentation/).
>Para obtener una guía paso a paso sobre la configuración de [!DNL Microsoft® Dynamics 365], en línea o de forma local, consulte [[!DNL Microsoft® Dynamics] Configuración de OData](ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configurar carpetas para configuraciones de servicios en la nube](#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Pulse **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente de configuración para crear fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** en la lista desplegable **[!UICONTROL Tipo de servicio]**. También puede examinar y seleccionar una imagen en miniatura para la configuración y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL raíz del servicio para configurar el servicio OData.
   * Seleccione el tipo de autenticación — Ninguna, OAuth2.0([Código de autorización](https://oauth.net/2/grant-types/authorization-code/), [Credenciales del cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticación básica, Clave de API o Autenticación personalizada: para acceder al servicio OData y facilitar los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL clave de la API]** como tipo de autenticación, especifique el valor de la clave de la API. La clave de la API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en la lista desplegable **[!UICONTROL Ubicación]** y especifique el nombre del encabezado o el parámetro de consulta en el campo **[!UICONTROL Nombre del parámetro]**.

   >[!NOTE]
   Debe seleccionar el tipo de autenticación OAuth 2.0 con el que conectarse a los servicios de [!DNL Microsoft® Dynamics] que utilizan el punto final OData como raíz de servicio.

1. Pulse **[!UICONTROL Crear]** para crear la configuración de nube para el servicio OData.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Pasos siguientes {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un modelo de datos de formulario o, si ya ha creado uno sin una fuente de datos, puede asociarlo a las que acaba de configurar. Consulte [Crear un modelo de datos de formulario](create-form-data-models.md) para obtener más información.
