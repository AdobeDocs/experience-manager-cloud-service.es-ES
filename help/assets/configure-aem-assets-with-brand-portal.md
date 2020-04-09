---
title: Configuración del servicio de nube de AEM Assets con Brand Portal
description: Configure el servicio en la nube de AEM Assets con Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 9d37fdae4445d0ccbdd6f800fc3ad4cbeec971fe

---


# Configuración de AEM Assets con Brand Portal {#configure-aem-assets-with-brand-portal}

Los recursos de Adobe Experience Manager (AEM) se configuran con Brand Portal a través de Adobe I/O, que proporciona un distintivo IMS para la autorización del inquilino de Brand Portal.

## Requisitos previos {#prerequisites}

Para configurar Recursos AEM con Brand Portal, es necesario lo siguiente:

* Una instancia de nube de Recursos AEM en ejecución.
* URL del inquilino de Brand Portal.
* Un usuario con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.

**Póngase en contacto con la asistencia** para obtener más consultas.

## Create configuration {#create-new-configuration}

Puede crear una nueva configuración en Adobe I/O para configurar la instancia de nube de AEM Assets con Brand Portal.

Realice los siguientes pasos en la secuencia indicada:
1. [Obtener certificado público](#public-certificate)
1. [Creación de la integración de Adobe I/O](#createnewintegration)
1. [Crear configuración de cuenta IMS](#create-ims-account-configuration)
1. [Configurar servicio de nube](#configure-the-cloud-service)
1. [Configuración de prueba](#test-configuration)

### Crear configuración de IMS {#create-ims-configuration}

La configuración de IMS autentica el inquilino de Brand Portal con la instancia de creación de AEM Assets.

La configuración de IMS incluye dos pasos:

* [Obtener certificado público](#public-certificate)
* [Crear configuración de cuenta IMS](#create-ims-account-configuration)

### Obtener certificado público {#public-certificate}

El certificado público le permite autenticar su perfil en Adobe I/O.

1. Inicie sesión en la instancia de nube de AEM Assets

1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a **[!UICONTROL Seguridad]** >> Configuraciones de **[!UICONTROL Adobe IMS]**.

   ![Interfaz de usuario de configuración de cuenta de Adobe IMS](assets/ims-configuration1.png)

1. Se abre la página Configuraciones de IMS de Adobe.

   Haga clic en **[!UICONTROL Crear]**.

   Esto le llevará a la página de configuración **[!UICONTROL de la cuenta técnica de]** Adobe IMS.

1. De forma predeterminada, se abre la ficha **Certificado** .

   En **Cloud Solution**, seleccione **[!UICONTROL Adobe Brand Portal]**.

1. Marque la casilla de verificación **[!UICONTROL Crear nuevo certificado]** y especifique un **alias** para el certificado. El alias sirve como nombre del cuadro de diálogo.

1. Haga clic en **[!UICONTROL Crear certificado]**. Aparece un cuadro de diálogo. Haga clic en **[!UICONTROL Aceptar]** para generar el certificado público.

   ![Crear certificado](assets/ims-config2.png)

1. Haga clic en **[!UICONTROL Descargar clave]** pública y guarde el archivo de certificado *AEM-Adobe-IMS.crt* en el equipo. El archivo de certificado se utiliza para [crear la integración](#createnewintegration)de Adobe I/O.

   ![Descargar certificado](assets/ims-config3.png)

1. Haga clic en **[!UICONTROL Siguiente]**. 

   En la ficha **Cuenta** , cree la cuenta de Adobe IMS, pero para ello necesitará los detalles de integración. Mantenga esta página abierta por ahora.

   Abra una pestaña nueva y [cree la integración](#createnewintegration) de Adobe I/O para obtener los detalles de integración de las configuraciones de cuenta de IMS.

### Creación de la integración de Adobe I/O {#createnewintegration}

La integración de Adobe I/O genera la clave de API, el secreto del cliente y la carga útil (JWT), que es necesaria para configurar las configuraciones de cuenta de IMS.

1. Inicie sesión en la consola de Adobe I/O con privilegios de administrador del sistema en la organización IMS del inquilino de Brand Portal.

   Dirección URL predeterminada: [https://console.adobe.io/](https://console.adobe.io/)

1. Haga clic en **[!UICONTROL Crear integración]**.

1. Seleccione **[!UICONTROL Acceso a una API]** y haga clic en **[!UICONTROL Continuar]**.

   ![Crear nueva integración](assets/create-new-integration1.png)

1. Se abre una nueva página de integración.

   Seleccione su organización en la lista desplegable.

   En **[!UICONTROL Experience Cloud]**, seleccione **[!UICONTROL AEM Brand Portal]** y haga clic en **[!UICONTROL Continuar]**.

   Si la opción de Brand Portal está deshabilitada para usted, asegúrese de que ha seleccionado la organización correcta en el cuadro desplegable situado encima de la opción Servicios **[!UICONTROL de]** Adobe. Si no conoce su organización, póngase en contacto con su administrador.

   ![Crear integración](assets/create-new-integration2.png)

1. Especifique un nombre y una descripción para la integración. Haga clic en **[!UICONTROL Seleccionar un archivo del equipo]** y cargue el `AEM-Adobe-IMS.crt` archivo descargado en la sección [Obtener certificados](#public-certificate) públicos.

1. Seleccione el perfil de su organización.

   O bien, seleccione el portal **[!UICONTROL de marca perfil]** Assets y haga clic en **[!UICONTROL Crear integración]**. Se crea la integración.

1. Haga clic en **[!UICONTROL Continuar para ver los detalles]** de la integración y vista de la información de integración.

   Copiar la clave de **[!UICONTROL API]**

   Haga clic en **[!UICONTROL Recuperar secreto]** de cliente y copie la clave Secreto de cliente.

   ![Clave de API, Secreto de cliente e información de carga útil de una integración](assets/create-new-integration3.png)

1. Vaya a la ficha **[!UICONTROL JWT]** y copie la carga útil **[!UICONTROL JWT]**.

   La clave de API, la clave secreta del cliente y la información de carga útil de JWT se utilizarán para crear la configuración de la cuenta de IMS.

### Crear configuración de cuenta IMS {#create-ims-account-configuration}

Asegúrese de que ha realizado los siguientes pasos:

* [Obtener certificado público](#public-certificate)
* [Creación de la integración de Adobe I/O](#createnewintegration)

**Pasos para crear la configuración de cuenta de IMS:**

1. Abra la página Configuración de IMS, ficha **[!UICONTROL Cuentas]** . La página se ha mantenido abierta al final de la sección, [Obtención de un certificado](#public-certificate)público.

1. Especifique un **[!UICONTROL Título]** para la cuenta de IMS.

   En **[!UICONTROL Servidor]** de autorización, introduzca la dirección URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Pegue la clave de API, el secreto del cliente y la carga útil JWT que ha copiado al final de [Crear integración](#createnewintegration)de Adobe I/O.

   Haga clic en **[!UICONTROL Crear]**.

   Se crea la integración.

   ![Configuración de cuenta de IMS](assets/create-new-integration6.png)


1. Seleccione la configuración de IMS y haga clic en **[!UICONTROL Comprobar estado]**. Aparecerá un cuadro de diálogo.

   Haga clic en **[!UICONTROL Comprobar]**. Cuando la conexión se ha realizado correctamente, aparece el mensaje *Token recuperado correctamente* .

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Cree sólo una configuración IMS válida. No cree varias configuraciones de IMS.
>
> Asegúrese de que la configuración esté correcta. En caso de que la configuración no esté en buen estado, elimínela y cree una nueva configuración en buen estado.


### Configurar servicio de nube {#configure-the-cloud-service}

Siga estos pasos para crear la configuración del servicio en la nube de Brand Portal:

1. Inicie sesión en la instancia de nube de AEM Assets

1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a Servicios de **[!UICONTROL nube >> AEM Brand Portal]**.

   Se abre la página Configuraciones de Brand Portal.

1. Haga clic en **[!UICONTROL Crear]**.

1. Especifique un **[!UICONTROL Título]** para la configuración.

   Seleccione la configuración de IMS que ha creado en el paso, [cree la configuración](#create-ims-account-configuration)de la cuenta de IMS.

   En la URL **** del servicio, introduzca la URL del inquilino de Brand Portal.

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. Se crea la configuración de nube. La instancia de nube de AEM Assets ahora está configurada con el inquilino de Brand Portal.

### Test configuration {#test-configuration}

1. Inicie sesión en la instancia de nube de AEM Assets.

1. En el panel **Herramientas** ![Herramientas](assets/tools.png) , vaya a **[!UICONTROL Implementación]** > **[!UICONTROL Distribución]**.

   ![](assets/test-bpconfig1.png)

1. Se abre la página Distribución.

   Un agente de distribución de Brand Portal `bpdistributionagent0` se crea en **[!UICONTROL Publicar en Brand Portal]**.

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >De forma predeterminada, se crea un agente de distribución para un inquilino de Brand Portal.

1. Se abre la página del agente de distribución. De forma predeterminada, se abre la ficha **[!UICONTROL Estado]** , que rellena las colas de distribución.

   Un agente de distribución contiene dos colas:
   * Una cola de procesamiento para la distribución de recursos a Brand Portal.
   * Una cola de errores para los recursos en los que se ha producido un error en la distribución.
   ![](assets/test-bpconfig3.png)

1. Para comprobar la conexión entre AEM Assets y Brand Portal, haga clic en **[!UICONTROL Probar conexión]**.

   ![](assets/test-bpconfig4.png)

   Aparece un mensaje en la parte inferior de la página que indica que el paquete de prueba se ha entregado correctamente.

   >[!NOTE]
   >
   >Evite desactivar el agente de distribución, ya que puede provocar errores en la distribución de los recursos (que se ejecutan en la cola).


Una vez que Brand Portal se haya configurado correctamente con la instancia de nube de AEM Assets, podrá:

* [Publicación de recursos de AEM Assets en Brand Portal](publish-to-brand-portal.md)
* [Publicación de carpetas de AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicación de colecciones de AEM Assets en Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Además de lo anterior, también puede publicar esquemas de metadatos, ajustes preestablecidos de imagen, facetas de búsqueda y etiquetas de Recursos AEM en Brand Portal.

* [Publicación de ajustes preestablecidos, esquemas y facetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar etiquetas en Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte la documentación [de](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) Brand Portal para obtener más información.


## Registros de distribución {#distribution-logs}

Puede consultar los registros para obtener información detallada sobre las acciones realizadas en el agente de distribución.

Por ejemplo, hemos publicado un recurso de Recursos AEM en Brand Portal para comprobar la configuración.

1. Siga los pasos (paso 1 a 4) que se muestran en **[!UICONTROL Test Connection]** y vaya a la página del agente de distribución.

1. Haga clic en **[!UICONTROL Registros]** para vista de los registros de distribución. Aquí puede ver los registros de procesamiento y error.

   ![](assets/test-bpconfig5.png)

El agente de distribución genera los siguientes registros:

* INFORMACIÓN: Es un registro generado por el sistema que se activa en una configuración correcta que habilita el agente de distribución.
* DSTRQ1 (Solicitud 1): Se activa en la conexión de prueba.

Al publicar el recurso, se generan los siguientes registros de solicitud y respuesta:

**Solicitud** del agente de distribución:
* DSTRQ2 (Solicitud 2): Se activa la solicitud de publicación de recursos.
* DSTRQ3 (Solicitud 3): El sistema activa otra solicitud para publicar la carpeta en la que existe el recurso y replica la carpeta en Brand Portal.

**Respuesta** del agente de distribución:
* queue-bpdistributionagent0 (DSTRQ2): El recurso se publica en Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): El sistema replica la carpeta que contiene el recurso en Brand Portal.

En el ejemplo anterior, se activa una solicitud y una respuesta adicionales. El sistema no pudo encontrar la carpeta principal (denominada ruta de Añado) en Brand Portal porque el recurso se publicó por primera vez, por lo que activa una solicitud adicional para crear una carpeta principal con el mismo nombre en Brand Portal en la que se publica el recurso.

>[!NOTE]
>>Se genera una solicitud adicional en caso de que la carpeta principal no exista en Brand Portal (en el ejemplo anterior) o de que la carpeta principal se haya modificado en Recursos AEM.
>

## Información adicional {#additional-information}

Vaya a `/system/console/slingmetrics` para obtener estadísticas relacionadas con el contenido distribuido:

1. **Métricas de contador**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Métricas de tiempo**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
