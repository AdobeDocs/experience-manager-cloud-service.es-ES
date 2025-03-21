---
title: Administrar [!DNL Adobe Stock] recursos en [!DNL Assets].
description: Busque, recupere, conceda licencias y administre  [!DNL Adobe Stock] recursos dentro de [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: Vishabh Gupta
feature: Adobe Stock
role: Admin, User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 5%

---

# Usar [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

El servicio [!DNL Adobe Stock] proporciona a diseñadores y empresas acceso a millones de fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, depurados y libres de derechos para todos sus proyectos creativos.

[!DNL Adobe Stock] para la oferta empresarial, de forma predeterminada, incluye derechos de uso compartido en toda la organización. Una vez que un usuario de la organización ha concedido una licencia a un recurso, otros usuarios de la organización pueden identificar, descargar y utilizar este recurso sin tener que volver a obtener la licencia. Una vez que su organización ha concedido una licencia a un recurso, el derecho a utilizarlo es perpetuo.

Las organizaciones pueden integrar su plan empresarial [!DNL Adobe Stock] con [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén ampliamente disponibles para sus proyectos creativos y de marketing, con las potentes capacidades de administración de recursos de [!DNL Experience Manager]. Los usuarios de [!DNL Experience Manager] pueden buscar, obtener una vista previa y obtener una licencia rápidamente de los recursos de Adobe Stock guardados en [!DNL Experience Manager], sin salir de la interfaz de [!DNL Experience Manager].

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] ofrece a los usuarios la capacidad de buscar, obtener una vista previa, guardar y conceder licencias a [!DNL Adobe Stock] recursos directamente desde [!DNL Experience Manager].

**Requisitos previos**

La integración requiere lo siguiente:

* Se está ejecutando [!DNL Experience Manager Assets] como instancia de [!DNL Cloud Service]
* Un [plan de empresa [!DNL Adobe Stock] 2}](https://stockenterprise.adobe.com/)
* Un usuario con permisos en Admin Console para acceder al perfil de producto predeterminado de Stock
* Un usuario con permisos de acceso de desarrollador para crear la integración en Adobe Developer Console

Un plan de [!DNL Adobe Stock] de empresa,

* Proporciona derechos de producto para [!DNL Adobe Stock] (existencias conectadas a Experience Manager)
* Créditos comprados en [!DNL Adobe Admin Console] por su asignación de acciones
* Habilita la autenticación de cuenta de servicio (JWT) en [!DNL Adobe Developer Console] para sus derechos de stock
* Habilita la administración de créditos y licencias globalmente desde [!DNL Adobe Admin Console]

Dentro del derecho, existe un perfil de producto predeterminado para [!DNL Adobe Stock] en [!DNL Admin Console]. Se pueden crear varios perfiles, que determinan quién puede obtener la licencia de los recursos de Stock. Un usuario que tenga acceso directo al perfil del producto puede acceder a [https://stock.adobe.com/](https://stock.adobe.com/) y obtener la licencia de los recursos de Stock. Mientras que hay otro método para utilizar el acceso de desarrollador para crear una integración (API). Esta integración autentica la comunicación entre [!DNL Experience Manager Assets] y [!DNL Adobe Stock].

>[!NOTE]
>
>La autenticación de la cuenta de servicio de Stock (JWT) viene con el derecho de Stock de la empresa.
>
>La integración no admite la autenticación Oauth para el derecho de Enterprise Stock.


<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->

## Pasos para integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integration-steps}

Para integrar [!DNL Experience Manager] y [!DNL Adobe Stock], realice los siguientes pasos en la secuencia indicada:

1. [Obtener un certificado público](#public-certificate)

   En [!DNL Experience Manager], cree una cuenta de IMS y genere un certificado público (clave pública).

1. [Crear conexión de cuenta de servicio (JWT)](#createnewintegration)

   En [!DNL Adobe Developer Console], cree un proyecto para su organización [!DNL Adobe Stock]. En el proyecto, configure una API con la clave pública para crear una conexión de cuenta de servicio (JWT). Obtenga las credenciales de la cuenta de servicio y la información de carga útil JWT.

1. [Configuración de la cuenta IMS](#create-ims-account-configuration)

   En [!DNL Experience Manager], configure la cuenta de IMS mediante las credenciales de la cuenta de servicio y la carga útil JWT.

1. [Configurar servicio en la nube](#configure-the-cloud-service)

   En [!DNL Experience Manager], configure un servicio en la nube [!DNL Adobe Stock] con la cuenta de IMS.


### Creación de una configuración de IMS {#create-an-ims-configuration}

La configuración de IMS autentica la instancia de autor [!DNL Experience Manager Assets] con el derecho [!DNL Adobe Stock].

La configuración de IMS incluye dos pasos:

* [Obtener un certificado público](#public-certificate)
* [Configuración de la cuenta IMS](#create-ims-account-configuration)

### Obtener un certificado público {#public-certificate}

La clave pública (certificado) autentica el perfil del producto en Adobe Developer Console.

1. Inicie sesión en la instancia de nube [!DNL Experience Manager Assets].

1. En el panel **[!UICONTROL Herramientas]**, vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de Adobe IMS]**.

1. En la página Configuraciones de IMS de Adobe, haga clic en **[!UICONTROL Crear]**. Se abre la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]**.

1. En la ficha **[!UICONTROL Certificado]**, seleccione **[!UICONTROL Adobe Stock]** de la lista desplegable **[!UICONTROL Solución de nube]**.

1. Puede crear un certificado o reutilizar un certificado existente para la configuración.

   Para crear un certificado, marque la casilla **[!UICONTROL Crear nuevo certificado]** y especifique un **alias** para la clave pública. El alias sirve como nombre de la clave pública.

1. Haga clic en **[!UICONTROL Crear certificado]**. A continuación, haga clic en **[!UICONTROL Aceptar]** para generar la clave pública.

1. Haga clic en el icono **[!UICONTROL Descargar clave pública]** y guarde el archivo de clave pública (.crt) en el equipo. La clave pública se utiliza más adelante para configurar la API del inquilino de Brand Portal y generar credenciales de cuenta de servicio en Adobe Developer Console.

   Haga clic en **[!UICONTROL Siguiente]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. En la pestaña **Account**, se crea la cuenta de Adobe IMS, que requiere las credenciales de la cuenta de servicio.

   Abra una ficha nueva y [cree una conexión de cuenta de servicio (JWT) en Adobe Developer Console](#createnewintegration).

### Crear una conexión de cuenta de servicio (JWT) {#createnewintegration}

En Adobe Developer Console, los proyectos y las API se configuran en el nivel de organización. Al configurar una API, se crea una conexión de cuenta de servicio (JWT). Existen dos métodos para configurar la API: generar un par de claves (claves pública y privada) o cargar una clave pública. En este ejemplo, las credenciales de la cuenta de servicio se generan cargando la clave pública.

Para generar las credenciales de la cuenta de servicio y la carga útil JWT:

1. Inicie sesión en Adobe Developer Console con privilegios de administrador del sistema. La dirección URL predeterminada es [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Asegúrese de haber seleccionado la organización IMS correcta (asignación de existencias) en la lista desplegable (organización).

1. Haga clic en **[!UICONTROL Crear nuevo proyecto]**. Se crea un proyecto en blanco con un nombre generado por el sistema para su organización.

   Haga clic en **[!UICONTROL Editar proyecto]**. Actualice **[!UICONTROL Título del proyecto]** y **[!UICONTROL Descripción]**, y haga clic en **[!UICONTROL Guardar]**.

1. En la ficha **[!UICONTROL Información general del proyecto]**, haga clic en **[!UICONTROL Agregar API]**.

1. En la ventana **[!UICONTROL Agregar una API]**, seleccione **[!UICONTROL Adobe Stock]**. Haga clic en **[!UICONTROL Siguiente]**.

1. En la ventana **[!UICONTROL Configurar API]**, seleccione la autenticación **[!UICONTROL Cuenta de servicio (JWT)]**. Haga clic en **[!UICONTROL Siguiente]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Haga clic en **[!UICONTROL Cargar la clave pública]**. Haga clic en **[!UICONTROL Seleccionar un archivo]** y cargue la clave pública (archivo .crt) que descargó en la sección [obtener certificado público](#public-certificate). Haga clic en **[!UICONTROL Siguiente]**.

1. Compruebe la clave pública y haga clic en **[!UICONTROL Siguiente]**.

1. Seleccione el perfil de producto predeterminado **[!UICONTROL Adobe Stock]** y haga clic en **[!UICONTROL Guardar la API configurada]**.

1. Una vez configurada la API, se le redirigirá a la página de información general de la API. En el panel de navegación izquierdo bajo **[!UICONTROL Credenciales]**, haga clic en la opción **[!UICONTROL Cuenta de servicio (JWT)]**. Aquí puede ver las credenciales y realizar acciones como generar tokens JWT, copiar detalles de credenciales y recuperar secretos de cliente.

1. En la ficha **[!UICONTROL Credenciales de cliente]**, copie el **[!UICONTROL ID de cliente]**.

   Haga clic en **[!UICONTROL Recuperar secreto de cliente]** y copie el **[!UICONTROL secreto de cliente]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Vaya a la pestaña **[!UICONTROL Generar JWT]** y copie la información de **[!UICONTROL carga JWT]**.

Ahora puede usar el ID de cliente (clave de API), el secreto de cliente y la carga útil JWT para [configurar la cuenta de IMS](#create-ims-account-configuration) en [!DNL Experience Manager Assets].

### Configuración de la cuenta IMS {#create-ims-account-configuration}

Debe tener las credenciales de [certificado](#public-certificate) y [cuenta de servicio (JWT)](#createnewintegration) para configurar la cuenta de IMS.

Para configurar la cuenta de IMS:

1. Abra la configuración de IMS y vaya a la ficha **[!UICONTROL Cuenta]**. Mantuvo la página abierta mientras [obtenía el certificado público](#public-certificate).

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En el campo **[!UICONTROL Servidor de autorización]**, escriba la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Introduzca el ID de cliente en el campo **[!UICONTROL clave de API]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL Carga útil]** (carga útil JWT) que ha copiado al [crear la conexión de cuenta de servicio (JWT)](#createnewintegration).

1. Haga clic en **[!UICONTROL Crear]**. Se crea una configuración de cuenta de IMS.

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. Seleccione la configuración de la cuenta de IMS y haga clic en **[!UICONTROL Comprobar estado]**.

   Haga clic en **[!UICONTROL Comprobar]** en el cuadro de diálogo. Si la configuración se realiza correctamente, aparecerá un mensaje que indica que el *Token se ha recuperado correctamente*.

   ![comprobación de estado](assets/aem-stock-healthcheck.png)


### Configurar servicio en la nube {#configure-the-cloud-service}

Para configurar el servicio en la nube [!DNL Adobe Stock]:

1. En la interfaz de usuario de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. En la página [!DNL Adobe Stock Configurations], haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración de la nube.

   Seleccione la configuración de IMS que creó al [configurar la cuenta de IMS](#create-ims-account-configuration).

   Seleccione la configuración regional en la lista desplegable.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   Su instancia de autor de [!DNL Experience Manager Assets] ahora está integrada con [!DNL Adobe Stock]. Puede crear varias configuraciones de [!DNL Adobe Stock] (por ejemplo, configuraciones basadas en la configuración regional). Ahora puede obtener acceso, buscar y obtener una licencia de los recursos de [!DNL Adobe Stock] desde la interfaz de usuario de [!DNL Experience Manager].

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >En esta fase de integración, solamente los administradores pueden acceder a los recursos de [!DNL Adobe Stock], buscar recursos de Stock (mediante omnisearch) y obtener una licencia de los recursos de [!DNL Adobe Stock].
   >
   >Los administradores pueden agregar más usuarios o grupos al servicio en la nube [!DNL Adobe Stock] y dar permisos a estos usuarios que no son administradores en [!DNL Experience Manager] para que tengan acceso a la configuración de Stock.

1. Para agregar usuarios o grupos, seleccione la configuración de nube [!DNL Adobe Stock] y haga clic en **[!UICONTROL Propiedades]**.

1. Busque y añada los usuarios o grupos a los que ha asignado permisos para acceder a la configuración de Adobe Stock. Consulte [asignar permisos al grupo de usuarios](#assign-permissions-to-group).


## Asignar permisos al grupo de usuarios {#assign-permissions-to-group}

Los administradores pueden crear grupos de usuarios y conceder permisos a determinados usuarios o grupos para acceder al servicio en la nube [!DNL Adobe Stock].

A continuación se indican los permisos necesarios para que un usuario busque y conceda licencias a recursos de Adobe Stock:

* Configurar la ruta: `/conf/global/settings/stock`
* Privilegios: `jcr:read`
* Tipo de permiso: `Allow`

Puede crear un grupo de usuarios o asignar permisos a un grupo de usuarios existente. Los permisos se pueden asignar desde la interfaz [!DNL Experience Manager Assets] o desde la consola [!DNL User Admin].

**Para proporcionar acceso a un grupo de usuarios desde [!DNL Experience Manager]:**

1. En la interfaz de usuario de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Grupos]**. Crear un grupo de usuarios para [!DNL Adobe Stock].

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Permisos]**.

1. Busque el grupo de usuarios en el panel izquierdo y agregue la nueva **[!UICONTROL Entrada de control de acceso (ACE)]** para Adobe Stock.

   * Configurar la ruta: `/conf/global/settings/stock`
   * Privilegios: `jcr:read`
   * Tipo de permiso: `Allow`

   Haga clic en **[!UICONTROL Agregar]**.

   ![permisos de usuario](assets/aem-stock-user-permissions.png)

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**. Seleccione la configuración de nube [!DNL Adobe Stock] y haga clic en **[!UICONTROL Propiedades]**.

1. Agregue el grupo de usuarios creado a la configuración [!DNL Adobe Stock]. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![asignar-usuario](assets/aem-stock-adduser.png)

**Para proporcionar acceso a un usuario desde [!DNL User Admin Console]:**

1. Abra el Admin Console de usuario [!DNL Experience Manager]. La URL predeterminada es `http://localhost:4502/userdamin`.

1. En el panel izquierdo, busque el usuario al escribir `user_id` o `name`. Haga doble clic para abrir las propiedades del usuario.

1. Vaya a la pestaña **[!UICONTROL Permisos]** y permita los permisos de `read` para la configuración de nube de [!DNL Adobe Stock]: `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Si no se permite la configuración en la nube, el usuario solo podrá obtener acceso a **[!UICONTROL Assets]** en la interfaz [!DNL Experience Manager].
   >
   >Para permitir el acceso a los recursos [!UICONTROL Assets] y [!DNL Adobe Stock], asegúrese de que la configuración de nube esté permitida para el usuario.

1. Haga clic en **[!UICONTROL Guardar]** para actualizar los permisos.

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. Agregue el usuario o el grupo a la configuración de nube [!DNL Adobe Stock].


## Acceso a recursos de Adobe Stock {#access-stock-assets}

Un usuario no administrador que tenga permisos para la configuración de nube de [!DNL Adobe Stock] puede buscar y obtener una licencia de los recursos de [!DNL Adobe Stock] desde la interfaz de [!DNL Experience Manager].

El usuario debe realizar un paso adicional para activar la configuración de nube de [!DNL Adobe Stock] antes de acceder a los recursos de [!DNL Adobe Stock]. Es una actividad única. Si al usuario se le asignan permisos en varias configuraciones de nube de [!DNL Adobe Stock], puede seleccionar la configuración que desee en **[!UICONTROL Preferencias de usuario]**.

Para activar la configuración de nube [!DNL Adobe Stock]:

1. Inicie sesión en [!DNL Experience Manager].

1. Haga clic en el icono de usuario en la esquina superior derecha y, a continuación, haga clic en **[!UICONTROL Mis preferencias]**. Se abre la ventana **[!UICONTROL Preferencias de usuario]**.

1. Seleccione la **[!UICONTROL Configuración de Stock]** que desee en la lista desplegable y haga clic en **[!UICONTROL Aceptar]** para activar la configuración.

   ![preferencias de usuario](assets/aem-stock-preferences.png)

1. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Adobe Stock]**. Ahora puede ver, buscar y obtener licencia de [!DNL Adobe Stock] recursos.

En la tabla siguiente se explica cómo funcionan los permisos de usuario al obtener acceso a los recursos de [!DNL Adobe Stock]:

| Usuario | Grupo | Permisos | Aceptar configuración de Stock en Preferencias de usuario | Acceso a Assets | Acceso a Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| administrador | N/D | Todos | N/D | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global/settings/stock/cloud-config | Sí | Sí | Sí |
| test-doc1 | Usuario DAM | /conf/global/settings/stock/cloud-config | No | Error: Error al cargar los datos | No |
| test-doc1 | Usuario DAM | **permitir**: /conf/global/settings/stock **denegar**: /cloud-config | La configuración de Stock no es visible | Sí | No |

## Usar y administrar [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones pueden permitir que sus usuarios trabajen con [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]. Desde la interfaz de usuario de [!DNL Experience Manager], los usuarios pueden buscar [!DNL Adobe Stock] recursos y obtener la licencia de los recursos necesarios.

Una vez que un recurso de [!DNL Adobe Stock] tiene licencia en [!DNL Experience Manager], se puede usar y administrar como un recurso típico. En [!DNL Experience Manager], los usuarios pueden buscar y obtener una vista previa de los recursos; copiar y publicar los recursos; compartir los recursos en [!DNL Brand Portal]; acceder a los recursos y utilizarlos mediante la aplicación de escritorio de [!DNL Experience Manager], etc.

![Busque [!DNL Adobe Stock] recursos y filtre los resultados de su [!DNL Adobe Experience Manager] espacio de trabajo](assets/adobe-stock-search-results-workspace.png)

**A.** Busque recursos similares a los recursos cuyo identificador [!DNL Adobe Stock] se ha proporcionado. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recurso **D.** más admitidos. Abra o contraiga la licencia del panel de filtros **E.** y guarde el recurso seleccionado en [!DNL Experience Manager] **F.** Guarde el recurso en [!DNL Experience Manager] con la marca de agua **G.** Explore los recursos del sitio web [!DNL Adobe Stock] que sean similares al recurso seleccionado **H.** Vea los recursos seleccionados en el sitio web [!DNL Adobe Stock]I.**Número de recursos seleccionados de los resultados de la búsqueda** J.**Cambiar entre la vista de tarjeta y la vista de lista**

### Buscar recursos {#find-assets}

Los usuarios de [!DNL Experience Manager] pueden buscar recursos en [!DNL Experience Manager] y [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no está limitada a [!DNL Adobe Stock], se muestran los resultados de búsqueda de [!DNL Experience Manager] y [!DNL Adobe Stock].

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Assets]** > **[!UICONTROL Buscar Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en buscar ![buscar](assets/do-not-localize/search_icon.png).

También puede empezar a escribir `Location: Adobe Stock` en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] ofrece capacidades de filtrado avanzadas en los recursos buscados, lo que permite a los usuarios centrarse rápidamente en los recursos necesarios mediante filtros, como tipos de recursos admitidos, orientación de la imagen y estado con licencia.

>[!NOTE]
>
>Assets buscado desde [!DNL Adobe Stock] se muestra en [!DNL Experience Manager]. [!DNL Adobe Stock] recursos se recuperan y almacenan en el repositorio [!DNL Experience Manager] solo después de que un usuario [guarde un recurso](/help/assets/aem-assets-adobe-stock.md#saveassets) o [conceda licencias y guarde un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Las Assets que ya están almacenadas en [!DNL Experience Manager] se muestran y resaltan para facilitar la referencia y el acceso. Además, los recursos [!DNL Stock] se guardan con algunos metadatos adicionales para indicar el origen como [!DNL Stock].

![Filtros de búsqueda en [!DNL Experience Manager] y [!DNL Adobe Stock] recursos resaltados en los resultados de búsqueda](assets/aem-search-filters2.jpg)

### Guarde y vea los recursos necesarios {#saveassets}

Seleccione un recurso que desee guardar en [!DNL Experience Manager]. Haga clic en [!UICONTROL Guardar] en la barra de herramientas de la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de Distintivo con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden conceder licencias a [!DNL Adobe Stock] recursos mediante la cuota de su plan de empresa [!DNL Adobe Stock]. Al obtener la licencia de un recurso, este se guarda sin marca de agua y está disponible para buscarlo y utilizarlo en [!DNL Experience Manager Assets].

![Diálogo para autorizar y guardar [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden obtener acceso a los metadatos y obtener una vista previa de ellos, incluidas las propiedades de metadatos de [!DNL Adobe Stock] para los recursos guardados en [!DNL Experience Manager], y agregar **[!UICONTROL referencias de licencia]** para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre [!DNL Experience Manager] y el sitio web [!DNL Adobe Stock].

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Ver y acceder a metadatos y referencias de licencia de recursos guardados](assets/metadata_properties.jpg)


## Limitaciones conocidas {#known-limitations}

* **La funcionalidad para restringir las licencias de los usuarios no funciona correctamente**: Todos los usuarios que tengan `read` permisos para la configuración de existencias pueden buscar y obtener licencias de los recursos [!DNL Adobe Stock].

* **Los usuarios que no son administradores tienen que activar manualmente la configuración en la nube de [!DNL Adobe Stock]**: en la ventana **[!UICONTROL Preferencias de usuario]**, la **[!UICONTROL Configuración de stock]** muestra la configuración en la nube de [!DNL Adobe Stock] como habilitada, pero no funciona para un usuario que no es administrador. El usuario debe hacer clic en el botón **[!UICONTROL Aceptar]** para activar la configuración de Stock. Si no se da este paso, el sistema mostrará un mensaje de error al acceder a **[!UICONTROL Assets]**.

* **No se muestra la advertencia de imagen editorial**: al autorizar una imagen, los usuarios no pueden comprobar si una imagen es de uso editorial solamente. Para evitar un posible uso incorrecto, los administradores pueden desactivar el acceso a los recursos editoriales desde Admin Console.

* **Se muestra un tipo de licencia incorrecto**: Es posible que se muestre un tipo de licencia incorrecto en [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en el sitio web de [!DNL Adobe Stock] para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no están sincronizados**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en [!DNL Experience Manager] pero no en el sitio web [!DNL Adobe Stock]. Del mismo modo, si el usuario actualiza los campos de referencia del sitio web [!DNL Adobe Stock], las actualizaciones no se sincronizan en [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el uso de recursos de Adobe Stock con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Ayuda del plan empresarial de Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Preguntas frecuentes sobre Adobe Stock](https://helpx.adobe.com/stock/faq.html)
