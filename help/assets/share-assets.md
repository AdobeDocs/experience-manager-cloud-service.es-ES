---
title: Compartir recursos, carpetas y colecciones como vínculo
description: En este artículo se describe cómo compartir recursos, carpetas y colecciones dentro de Recursos Experience Manager como un hipervínculo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 3%

---


# Compartir y distribuir recursos administrados en Experience Manager {#share-assets-from-aem}

Recursos Adobe Experience Manager (AEM) permite compartir recursos, carpetas y colecciones con miembros de la organización y entidades externas, incluidos socios y proveedores. Utilice los siguientes métodos para compartir recursos de Recursos Experience Manager como Cloud Service:

* Compartir como vínculo.
* Descargue recursos y compártalos por separado.
* Compartir mediante AEM aplicación de escritorio.
* Compartir mediante Adobe Asset Link.
* (Próxima funcionalidad) Comparta con Brand Portal.

## Compartir recursos como un vínculo {#sharelink}

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la ubicación `/var/dam/share` pueden realizar la vista de los vínculos compartidos con ellos. El uso compartido de recursos a través de un vínculo es una manera práctica de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en AEM Assets en primer lugar.

>[!NOTE]
>
>* Necesita el permiso Editar ACL en la carpeta o el recurso que desea compartir como vínculo.
>* Antes de compartir un vínculo con los usuarios, asegúrese de que el servicio de correo de CQ de día está configurado. De lo contrario, se producirá un error.


1. En la interfaz de usuario de Recursos, seleccione el recurso que desea compartir como vínculo.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Vínculo compartido]**. Se crea automáticamente un vínculo de recurso en el campo **[!UICONTROL Vínculo compartido]**. Copie este vínculo y compártalo con los usuarios. El tiempo de caducidad predeterminado para el vínculo es un día.

   >[!NOTE]
   >
   >Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y vuelva a compartirlo con los usuarios.

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Descargar y compartir recursos {#download-and-share-assets}

Los usuarios pueden descargar los recursos necesarios y compartirlos fuera de [!DNL Experience Manager]. Para obtener más información, consulte [cómo buscar recursos](/help/assets/search-assets.md), [cómo descargar recursos](/help/assets/download-assets-from-aem.md) y [cómo descargar colecciones](manage-collections.md#download-a-collection)

## Comparta recursos con profesionales creativos {#share-with-creatives}

Los especialistas en marketing y los usuarios de la línea de negocios pueden compartir fácilmente los recursos aprobados con sus profesionales creativos mediante,

* **AEM aplicación** de escritorio: La aplicación funciona en Windows y Mac. Consulte [descripción general de la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). Para saber cómo cualquier usuario de escritorio autorizado puede acceder fácilmente a los recursos compartidos, consulte [exploración, búsqueda y previsualización de recursos](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Los usuarios de escritorio pueden crear recursos y compartirlos con sus homólogos que son usuarios AEM, por ejemplo, cargando imágenes nuevas. Consulte [carga de recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Vínculo** de recurso de Adobe: Los profesionales creativos pueden buscar y utilizar recursos directamente desde Adobe InDesign, Adobe Illustrator y Adobe Photoshop.

## Configuración del uso compartido de recursos {#configure-sharing}

Las diferentes opciones para compartir los recursos requieren una configuración específica y tienen requisitos previos específicos.

### Configurar el uso compartido de vínculos de recursos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la ubicación `/var/dam/share` pueden realizar la vista de los vínculos compartidos con ellos. El uso compartido de recursos a través de un vínculo es una manera práctica de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en AEM Assets en primer lugar.

>[!NOTE]
>
>Si desea compartir vínculos de la instancia de AEM Author con entidades externas, asegúrese de que solo muestra las siguientes URL para solicitudes `GET`. Bloquee otras direcciones URL para asegurarse de que la instancia de AEM Author es segura.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

### Configurar el tamaño máximo de datos {#maxdatasize}

Al descargar recursos del vínculo compartido mediante la función Compartir vínculos, AEM comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, a falta de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetas a compresión, lo que causa errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, puede configurar el tamaño máximo de los archivos descargados. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haga clic o pulse el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. Desde la consola web, localice la configuración de **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Abra la configuración en modo de edición y modifique el valor del parámetro **[!UICONTROL Tamaño máximo de contenido (sin comprimir)]**.
1. Guarde los cambios.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Habilitar acciones de escritorio para usar con la aplicación de escritorio {#desktop-actions}

Desde la interfaz de usuario de Recursos en un navegador, puede explorar las ubicaciones de los recursos o el cierre de compra y abrir el recurso para editarlo en la aplicación de escritorio. Estas opciones se denominan acciones de escritorio y para habilitarlas, consulte [habilitar acciones de escritorio en AEM interfaz Web](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Activar acciones de escritorio para usar como método abreviado al trabajar con una aplicación de escritorio](assets/enable_desktop_actions.png)

### Configuraciones para utilizar el vínculo de recursos de Adobe {#configure-asset-link}

Adobe Asset Link simplifica la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Conecta recursos de Adobe Experience Manager (AEM) con aplicaciones de escritorio de Creative Cloud como Adobe InDesign, Adobe Photoshop y Adobe Illustrator. El panel Vínculo de recursos de Adobe permite a los creativos acceder y modificar el contenido almacenado en AEM Assets sin tener que abandonar las aplicaciones creativas con las que están más familiarizados.

Consulte [cómo configurar AEM para usar con Adobe Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).

## Prácticas recomendadas y solución de problemas {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contengan un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, consulte con el administrador AEM cuáles son los [límites de descarga](#maxdatasize).

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!--
Add content or link about how to share using Brand Portal when it is available on Cloud Service.
-->
