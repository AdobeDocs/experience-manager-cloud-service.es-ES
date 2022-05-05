---
title: Configuración de IMS que usar al integrar con Adobe Analytics
description: Obtenga información sobre la configuración de IMS para su uso al integrar con Adobe Analytics
exl-id: 12bd1573-373a-4001-be71-c8f155ef6896
source-git-commit: 0030b0f6f17dd66229f681e9c513786de4fe10a2
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# Configuración de IMS que usar al integrar con Adobe Analytics {#ims-configuration-for-integration-with-adobe-analytics}

La integración de Adobe Experience Manager as a Cloud Service (AEMaaCS) con Adobe Analytics a través de la API de Analytics Standard requiere la configuración de Adobe IMS (Identity Management System). La configuración se realiza con la consola de Adobe Developer.

>[!NOTE]
>
>La compatibilidad con la API de Adobe Analytics Standard 2.0 es nueva en AEMaaCS 2022.2.0. Esta versión de la API admite la autenticación IMS.
>
>La selección de la API se basa en el método de autenticación utilizado para la integración de AEM/Analytics.
>
>También puede obtenerse más información en [Migración a las API 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## Requisitos previos {#prerequisites}

Antes de iniciar este procedimiento:

* [Compatibilidad con Adobe](https://helpx.adobe.com/es/contact/enterprise-support.ec.html) debe aprovisionar su cuenta para:

   * Consola Adobe
   * Adobe Developer Console
   * Adobe Analytics y
   * Adobe IMS (sistema Identity Management)

* El administrador del sistema de su organización debe utilizar el Admin Console para agregar los desarrolladores necesarios de su organización a los perfiles de producto relevantes.

   * Esto proporciona a los desarrolladores específicos permisos para habilitar integraciones mediante la consola de Adobe Developer.
   * Para obtener más información, consulte [Administrar desarrolladores](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## Configuración de IMS: generación de una clave pública {#configuring-ims-generating-a-public-key}

El primer paso de la configuración es crear una configuración de IMS en AEM y generar la clave pública.

1. En AEM, abra el **Herramientas** para abrir el Navegador.
1. En el **Seguridad** sección seleccionar **Configuraciones de IMS de Adobe**.
1. Select **Crear** para abrir el **Configuración de cuenta técnica de Adobe IMS**.
1. Uso de la lista desplegable debajo de **Configuración de nube**, seleccione **Adobe Analytics**.
1. Activar **Crear nuevo certificado** e introduzca un nuevo alias.
1. Confirme con **Crear certificado**.

   ![Crear certificado](assets/integrate-analytics-ims-01.png)

1. Select **Descargar** (o **Descargar clave pública**) para descargar el archivo en la unidad local, de modo que esté listo para usar cuando [configuración de IMS para la integración de Adobe Analytics con AEM](#configuring-ims-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >Mantenga esta configuración abierta, será necesaria de nuevo cuando [Finalización de la configuración de IMS en AEM](#completing-the-ims-configuration-in-aem).

   ![Descargar certificado](assets/integrate-analytics-ims-02.png)

## Configuración de IMS para la integración de Adobe Analytics con AEM {#configuring-ims-adobe-analytics-integration-with-aem}

Con la consola de desarrollador de Adobe, debe crear un proyecto (integración) con Adobe Analytics (para AEM uso) y, a continuación, asignar los privilegios necesarios.

### Creación del proyecto {#creating-the-project}

Abra Adobe Developer Console para crear un proyecto con Adobe Analytics que AEM:

1. Abra Adobe Developer Console para proyectos:

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. Se mostrarán todos los proyectos que tenga. Select **Crear nuevo proyecto** - la ubicación y el uso dependerán de:

   * Si todavía no tiene ningún proyecto, **Crear nuevo proyecto** estará en el centro, abajo.
      ![Crear nuevo proyecto: primer proyecto](assets/integration-analytics-ims-02.png)
   * Si ya tiene proyectos existentes, estos se enumerarán y **Crear nuevo proyecto** estará en la parte superior derecha.
      ![Crear nuevo proyecto: varios proyectos](assets/integration-analytics-ims-03.png)


1. Select **Agregar a proyecto** seguido de **API**:

   ![Introducción a su nuevo proyecto](assets/integration-analytics-ims-10.png)

1. Select **Adobe Analytics**, luego **Siguiente**:

   >[!NOTE]
   >
   >Si está suscrito a Adobe Analytics, pero no lo ve en la lista, debe comprobar la variable [Requisitos previos](#prerequisites).

   ![Añadir una API](assets/integration-analytics-ims-12.png)

1. Select **Cuenta de servicio (JWT)** como tipo de autenticación, continúe con **Siguiente**:

   ![Seleccionar tipo de autenticación](assets/integration-analytics-ims-12a.png)

1. **Cargar la clave pública** y, cuando se complete, continúe con **Siguiente**:

   ![Cargar la clave pública](assets/integration-analytics-ims-13.png)

1. Revise las credenciales y continúe con **Siguiente**:

   ![Revisar credenciales](assets/integration-analytics-ims-15.png)

1. Seleccione los perfiles de producto necesarios y continúe con **Guardar la API configurada**:

   ![Seleccionar perfiles de producto necesarios](assets/integration-analytics-ims-16.png)

1. La configuración se confirmará.

### Asignación de privilegios a la integración {#assigning-privileges-to-the-integration}

Ahora debe asignar los privilegios necesarios a la integración:

1. Abra el Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. Vaya a **Productos** (barra de herramientas superior) y, a continuación, seleccione **Adobe Analytics: &lt;*your-tenant-id*>** (del panel izquierdo).
1. Select **Perfiles de producto** y, a continuación, el espacio de trabajo necesario de la lista presentada. Por ejemplo, Espacio de trabajo predeterminado.
1. Select **Credenciales de API**, luego la configuración de integración requerida.
1. Select **Editor** como el **Función del producto**; en lugar de **Observador**.

## Detalles almacenados para el proyecto de integración de Adobe Developer Console {#details-stored-for-the-ims-integration-project}

Desde la consola para desarrolladores de Adobe: Proyectos, puede ver una lista de todos sus proyectos de integración:

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

Seleccione una entrada de proyecto específica para mostrar más detalles sobre la configuración. Entre estas características se incluyen:

* Información general del proyecto
* Perspectivas
* Credenciales
   * Cuenta de servicio (JWT)
      * Detalles de la credencial
      * Generar JWT
* API
   * Por ejemplo, Adobe Analytics

En algunos de estos casos, deberá completar la integración de Adobe Analytics en AEM según IMS.

## Finalización de la configuración de IMS en AEM {#completing-the-ims-configuration-in-aem}

Al volver a AEM puede completar la configuración de IMS añadiendo los valores necesarios desde la integración de IMS para Analytics:

1. Vuelva a la [Configuración de IMS abierta en AEM](#configuring-ims-generating-a-public-key).
1. Seleccione **Siguiente**.

1. Aquí puede usar la variable [detalles de la configuración del proyecto en la consola de Adobe Developer](#details-stored-for-the-ims-integration-project):

   * **Título**: El texto.
   * **Servidor de autorización**: Copie/pegue esto desde el `aud` línea del **Carga útil** a continuación, p. ej. `https://ims-na1.adobelogin.com` en el ejemplo siguiente
   * **Clave de API**: Copie esto desde el **Credenciales** de la sección [Información general del proyecto](#details-stored-for-the-ims-integration-project)
   * **Secreto del cliente**: Genere esto en el [Pestaña Secreto del cliente de la sección Cuenta de servicio (JWT)](#details-stored-for-the-ims-integration-project)y copie
   * **Carga útil**: Copie esto desde el [Ficha Generar JWT de la sección Cuenta de servicio (JWT)](#details-stored-for-the-ims-integration-project)

   ![AEM detalles de configuración de IMS](assets/integrate-analytics-ims-10.png)

1. Confirme con **Crear**.

1. La configuración de Adobe Analytics se mostrará en la consola AEM.

   ![Configuración de IMS](assets/integrate-analytics-ims-11.png)

## Confirmación de la configuración de IMS {#confirming-the-ims-configuration}

Para confirmar que la configuración funciona según lo esperado:

1. Abra:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   Por ejemplo:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. Seleccione la configuración.
1. Select **Comprobar estado** en la barra de herramientas, seguido de **Marque**.

   ![Configuración de IMS - Comprobar estado](assets/integrate-analytics-ims-12.png)

1. Si se realiza correctamente, verá un mensaje de confirmación.

## Completar la integración con Adobe Analytics {#complete-the-integration-with-adobe-analytics}

Ahora puede utilizar esta configuración de IMS para completar la [integración con Adobe Analytics](/help/sites-cloud/integrating/integrating-adobe-analytics.md).

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank this will be generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that will be sent to Adobe Analytics. 
-->
