---
title: ¿Cómo se configuran las fuentes de datos?
description: La integración de datos de Experience Manager Forms le permite configurar y conectarse a fuentes de datos diferentes. Aprenda a configurar los servicios web RESTful, los servicios web basados en SOAP y los servicios OData como fuentes de datos y utilícelos para crear modelos de datos de formulario.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: b6c654f5456e1a7778b453837f04cbed32a82a77
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 0%

---

# Configuración de fuentes de datos {#configure-data-sources}

![Integración de datos](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] La integración de datos permite configurar y conectar a fuentes de datos diferentes. Los siguientes tipos son compatibles de serie. Sin embargo, con poca personalización, también puede integrar otras fuentes de datos.

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* Servicios web RESTful
* Servicios web basados en SOAP
* Servicios OData

La integración de datos es compatible con los tipos de autenticación OAuth2.0, Autenticación básica y API Key de serie, y permite implementar autenticación personalizada para acceder a servicios web. Mientras que los servicios RESTful, SOAP y OData están configurados en [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> y conector para [!DNL Experience Manager] el perfil de usuario está configurado en [!DNL Experience Manager] consola web.

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] no admite la base de datos relacional.

<!-- ## Configure relational database {#configure-relational-database}

You can configure relational databases using [!DNL Experience Manager] Web Console Configuration. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
1. Look for **[!UICONTROL Apache Sling Connection Pooled DataSource]** configuration. Tap to open the configuration in edit mode.
1. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Name of the data source
    * Data source service property that stores the data source name
    * Java class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver

   >[!NOTE]
   >
   >Ensure that you encrypt sensitive information like passwords before configuring the data source. To encrypt:
   >
   >    
   >    
   >    1. Go to https://'[server]:[port]'/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.
   >    
   >    
   >    
   >The encrypted text appears in the Protected Text field that you can specify in the configuration.

1. Enable **[!UICONTROL Test on Borrow]** or **[!UICONTROL Test on Return]** to specify that the objects are validated before being borrowed or returned from and to the pool, respectively.
1. Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:

    * SELECT 1 (MySQL and MS SQL) 
    * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration. -->

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

## Configuración de la carpeta para configuraciones de servicios en la nube {#cloud-folder}

La configuración de la carpeta de servicios de nube es necesaria para configurar los servicios de nube para los servicios RESTful, SOAP y OData.

Todas las configuraciones de servicios en la nube en [!DNL Experience Manager] se consolidan en la variable `/conf` carpeta [!DNL Experience Manager] repositorio. De forma predeterminada, la variable `conf` La carpeta contiene el `global` carpeta donde puede crear configuraciones de servicios en la nube. Sin embargo, debe habilitarlo manualmente para las configuraciones de nube. También puede crear carpetas adicionales en `conf` para crear y organizar configuraciones de servicios en la nube.

Para configurar la carpeta para las configuraciones del servicio en la nube:

1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   * Consulte la [Explorador de configuración](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) documentación para obtener más información.
1. Haga lo siguiente para habilitar la carpeta global para configuraciones de nube o omita este paso para crear y configurar otra carpeta para configuraciones de servicios de nube.

   1. En el **[!UICONTROL Explorador de configuración]**, seleccione `global` carpeta y toque **[!UICONTROL Propiedades]**.

   1. En el **[!UICONTROL Propiedades de configuración]** cuadro de diálogo, habilitar **[!UICONTROL Configuraciones de nube]**.

   1. Toque **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. En el **[!UICONTROL Explorador de configuración]**, toque **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración]** , especifique un título para la carpeta y habilite **[!UICONTROL Configuraciones de nube]**.
1. Toque **[!UICONTROL Crear]** para crear la carpeta habilitada para las configuraciones del servicio en la nube.

## Configuración de los servicios web de RESTful {#configure-restful-web-services}

El servicio web RESTful se puede describir mediante [Especificaciones de Swagger](https://swagger.io/specification/) en formato JSON o YAML en un [!DNL Swagger] archivo de definición. Para configurar el servicio web RESTful en [!DNL Experience Manager] as a Cloud Service, asegúrese de que dispone de la variable [!DNL Swagger] en el sistema de archivos o en la URL donde se aloja el archivo.

Haga lo siguiente para configurar los servicios RESTful:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio RESTful]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio RESTful:

   * Seleccione URL o archivo en la [!UICONTROL Fuente de Swagger] y, en consecuencia, especifique la variable [!DNL Swagger URL] a[!DNL  Swagger] archivo de definición o cargue el [!DNL Swagger] del sistema de archivos local.
   * En función de la variable[!DNL  Swagger] Entrada de origen, los siguientes campos están rellenados previamente con valores:

      * Esquema: Los protocolos de transferencia utilizados por la API de REST. El número de tipos de esquema que se muestran en la lista desplegable depende de los esquemas definidos en la [!DNL Swagger] fuente.
      * Host: El nombre de dominio o la dirección IP del host que sirve la API de REST. Es un campo obligatorio.
      * Ruta base: El prefijo URL de todas las rutas de API. Es un campo opcional.\
         Si es necesario, edite los valores rellenados previamente para estos campos.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica, Clave de API o Autenticación personalizada) para acceder al servicio RESTful y proporcione los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL Clave de API]** como tipo de autenticación, especifique el valor de la clave de API. La clave de API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en el **[!UICONTROL Ubicación]** lista desplegable y especifique el nombre del encabezado o el parámetro de consulta en la **[!UICONTROL Nombre del parámetro]** en consecuencia.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio RESTful.

### Modelo de datos de formulario Configuración del cliente HTTP para optimizar el rendimiento {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] modelo de datos de formulario al integrarse con los servicios web RESTful, ya que el origen de datos incluye configuraciones de cliente HTTP para la optimización del rendimiento.
Realice los siguientes pasos para configurar el cliente HTTP del modelo de datos de formulario:

1. Iniciar sesión en [!DNL Experience Manager Forms] Instancia de autor como administrador y vaya a [!DNL Experience Manager] paquetes de la consola web. La dirección URL predeterminada es [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Toque **[!UICONTROL Configuración del cliente HTTP del modelo de datos de formulario para el origen de datos REST]**.

1. En el [!UICONTROL Configuración del cliente HTTP del modelo de datos de formulario para el origen de datos REST] diálogo:

   * Especifique el número máximo de conexiones permitidas entre el modelo de datos de formulario y los servicios web RESTful en la variable **[!UICONTROL Límite de conexión en total]** campo . El valor predeterminado es 20 conexiones.

   * Especifique el número máximo de conexiones permitidas para cada ruta en la variable **[!UICONTROL Límite de conexión por ruta]** campo . El valor predeterminado es 2 conexiones.

   * Especifique la duración, durante la cual se mantiene activa una conexión HTTP persistente, en la variable **[!UICONTROL Mantener viva]** campo . El valor predeterminado es de 15 segundos.

   * Especifique la duración para la que [!DNL Experience Manager Forms] espera a que una conexión se establezca, en la variable **[!UICONTROL Tiempo de espera de la conexión]** campo . El valor predeterminado es de 10 segundos.

   * Especifique el período de tiempo máximo para la inactividad entre dos paquetes de datos en la variable **[!UICONTROL Tiempo de espera de socket]** campo . El valor predeterminado es de 30 segundos.


## Configuración de servicios web SOAP {#configure-soap-web-services}

Los servicios web basados en SOAP se describen utilizando [Especificaciones del lenguaje de descripción de servicios web (WSDL)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] no admiten el modelo WSDL de estilo RPC.

Para configurar el servicio web basado en SOAP en [!DNL Experience Manager] as a Cloud Service, asegúrese de que tiene la URL WSDL para el servicio web y haga lo siguiente:

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](configure-data-sources.md#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio web SOAP]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique lo siguiente para el servicio web SOAP:

   * URL de WSDL para el servicio web.
   * Punto final de servicio. Especifique un valor en este campo para anular el extremo de servicio mencionado en WSDL.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica o Autenticación personalizada) para acceder al servicio SOAP y proporcione los detalles para la autenticación.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio web SOAP.

### Habilitar el uso de instrucciones de importación en el WSDL de los servicios web SOAP {#enable-import-statements}

Puede especificar una expresión regular que sirva como filtro para las direcciones URL absolutas permitidas como instrucciones de importación en el WSDL de los servicios web SOAP. De forma predeterminada, no hay ningún valor en este campo. Como resultado, [!DNL Experience Manager] bloquea todas las instrucciones de importación disponibles en WSDL. Si especifica `.*` como el valor de este campo, [!DNL Experience Manager] permite todas las instrucciones de importación.

Configure las variables `importAllowlistPattern` propiedad de la variable **[!UICONTROL Lista de permitidos de importación de servicios web SOAP del Modelo de datos de formulario]** configuración para especificar la expresión regular. El siguiente archivo JSON muestra un ejemplo:

```json
{
  "importAllowlistPattern": ".*"
}
```

Para establecer los valores de una configuración, [Generación de configuraciones de OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)y [implementar la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) a su instancia de Cloud Service.

## Configuración de servicios OData {#config-odata}

Un servicio OData se identifica mediante su URL raíz de servicio. Para configurar un servicio OData en [!DNL Experience Manager] as a Cloud Service, asegúrese de que tiene una URL raíz de servicio para el servicio y haga lo siguiente:

>[!NOTE]
>
> El modelo de datos de formulario es compatible [OData versión 4](https://www.odata.org/documentation/).
>Para obtener una guía paso a paso sobre la configuración [!DNL Microsoft Dynamics 365], en línea o in situ, consulte [[!DNL Microsoft Dynamics] Configuración de OData](ms-dynamics-odata-configuration.md).

1. Vaya a **[!UICONTROL Herramientas > Cloud Services > Fuentes de datos]**. Pulse para seleccionar la carpeta en la que desea crear una configuración de nube.

   Consulte [Configuración de la carpeta para configuraciones de servicios en la nube](#cloud-folder) para obtener información sobre la creación y configuración de una carpeta para configuraciones de servicios en la nube.

1. Toque **[!UICONTROL Crear]** para abrir el **[!UICONTROL Asistente para la creación de la configuración de fuentes de datos]**. Especifique un nombre y, opcionalmente, un título para la configuración, seleccione **[!UICONTROL Servicio OData]** de la variable **[!UICONTROL Tipo de servicio]** lista desplegable, opcionalmente puede examinar y seleccionar una imagen en miniatura para la configuración, y pulsar **[!UICONTROL Siguiente]**.
1. Especifique los siguientes detalles para el servicio OData:

   * URL raíz del servicio para configurar el servicio OData.
   * Seleccione el tipo de autenticación (Ninguno, OAuth2.0, Autenticación básica, Clave de API o Autenticación personalizada) para acceder al servicio OData y proporcione los detalles correspondientes para la autenticación.

   Si selecciona **[!UICONTROL Clave de API]** como tipo de autenticación, especifique el valor de la clave de API. La clave de API se puede enviar como encabezado de solicitud o como parámetro de consulta. Seleccione una de estas opciones en el **[!UICONTROL Ubicación]** lista desplegable y especifique el nombre del encabezado o el parámetro de consulta en la **[!UICONTROL Nombre del parámetro]** en consecuencia.

   >[!NOTE]
   >
   >Debe seleccionar el tipo de autenticación de OAuth 2.0 con el que conectarse [!DNL Microsoft Dynamics] servicios que utilizan el extremo OData como raíz de servicio.

1. Toque **[!UICONTROL Crear]** para crear la configuración de nube para el servicio OData.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other’s identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Pasos siguientes {#next-steps}

Ha configurado las fuentes de datos. A continuación, puede crear un Modelo de datos de formulario o, si ya ha creado un Modelo de datos de formulario sin un origen de datos, puede asociarlo a los orígenes de datos que acaba de configurar. Consulte [Crear modelo de datos de formulario](create-form-data-models.md) para obtener más información.
