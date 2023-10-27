---
title: Distribuir y compartir recursos, carpetas y colecciones
description: Distribuya sus recursos digitales mediante métodos como compartir como vínculo, descargar y a través de [!DNL Brand Portal], [!DNL desktop app], y [!DNL Asset Link].
contentOwner: Vishabh Gupta
feature: Asset Management, Collaboration, Asset Distribution
role: User, Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 177021106fc67e67a8cd6645a6684185331dd6f4
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 5%

---

# Uso compartido y distribución de recursos administrados en [!DNL Experience Manager] {#share-assets-from-aem}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/link-sharing.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Experience Manager Assets] permite compartir recursos, carpetas y colecciones con miembros de la organización y entidades externas, incluidos socios y proveedores. Utilice los siguientes métodos para compartir recursos de [!DNL Experience Manager Assets] as a [!DNL Cloud Service]:

* [Compartir como vínculo](#sharelink)
* [Descarga de recursos](/help/assets/download-assets-from-aem.md) y comparta por separado.
* Compartir usando [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=es).
* Compartir usando [[!DNL Adobe Asset Link]](https://www.adobe.com/es/creativecloud/business/enterprise/adobe-asset-link.html).
* Compartir usando [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## Compartir recursos como un vínculo {#sharelink}

Compartir recursos a través de un vínculo es una forma cómoda de poner los recursos a disposición de terceros externos, especialistas en marketing y otros [!DNL Experience Manager] usuarios. La funcionalidad permite a los usuarios anónimos acceder y descargar los recursos compartidos con ellos. Al descargar recursos desde un vínculo compartido, [!DNL Experience Manager Assets] utiliza un servicio asincrónico que ofrece una descarga más rápida e ininterrumpida. Los recursos que se van a descargar se colocan en segundo plano en archivos ZIP de un tamaño de archivo manejable. Para las descargas grandes, la descarga está agrupada en varios archivos de 100 GB por tamaño de archivo.

<!--
Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. 
-->

>[!NOTE]
>
>* Necesita el permiso Editar ACL en la carpeta o el recurso que desea compartir como vínculo.
>* [Habilitar correos electrónicos salientes](/help/implementing/developing/introduction/development-guidelines.md#sending-email) antes de compartir un vínculo con los usuarios.

Existen dos formas de compartir los recursos mediante la funcionalidad de uso compartido de vínculos:

1. Generar un vínculo compartido, [copie y comparta el vínculo del recurso](#copy-and-share-assets-link) con otros usuarios. El tiempo de caducidad predeterminado del vínculo es de un día. No se puede cambiar la hora de caducidad al compartir el vínculo copiado con otros usuarios.

1. Generar un vínculo compartido y [compartir el vínculo del recurso por correo electrónico](#share-assets-link-through-email). En este caso, puede modificar los valores predeterminados, como la fecha y la hora de caducidad, y permitir la descarga de los recursos originales y sus representaciones. Puede enviar correos electrónicos a varios usuarios añadiendo sus direcciones de correo electrónico.

   ![Cuadro de diálogo Compartir vínculos](assets/link-sharing-dialog.png)

### Copiar y compartir el vínculo del recurso{#copy-and-share-asset-link}

Para compartir recursos como una URL pública:

1. Iniciar sesión en [!DNL Experience Manager Assets] y vaya a **[!UICONTROL Archivos]**.
1. Seleccione los recursos o la carpeta que contienen los recursos. En la barra de herramientas, haga clic en **[!UICONTROL Compartir vínculo]**.
1. El **[!UICONTROL Vínculos compartidos]** aparece un cuadro de diálogo que contiene un vínculo de recurso generado automáticamente en **[!UICONTROL Compartir vínculo]** field.
1. Copie el vínculo del recurso y compártalo con los usuarios.

### Compartir vínculo de recurso mediante notificación por correo electrónico {#share-assets-link-through-email}

Para compartir recursos por correo electrónico:

1. Seleccione los recursos o la carpeta que contienen los recursos. En la barra de herramientas, haga clic en **[!UICONTROL Compartir vínculo]**.
1. El **[!UICONTROL Vínculos compartidos]** aparece un cuadro de diálogo que contiene un vínculo de recurso generado automáticamente en **[!UICONTROL Compartir vínculo]** field.

   * En el cuadro Dirección de correo electrónico, escriba el ID de correo electrónico del usuario con el que desea compartir el vínculo. Puede compartir el vínculo con varios usuarios. Si el usuario es miembro de su organización, seleccione su ID de correo electrónico de entre las sugerencias que aparecen en la lista desplegable. Si el usuario es externo, escriba el ID de correo electrónico completo y pulse **[!UICONTROL Entrar]**; el ID de correo electrónico se añade a la lista de usuarios.

   * En el **[!UICONTROL Asunto]** , escriba un asunto para especificar el propósito de los recursos compartidos.
   * En el **[!UICONTROL Mensaje]** , escriba un mensaje si es necesario.
   * En el **[!UICONTROL Caducidad]** , utilice el selector de fechas para especificar una fecha y hora de caducidad para el vínculo.
   * Habilite la **[!UICONTROL Permitir la descarga del archivo original]** para permitir que los destinatarios descarguen la representación original.

1. Clic **[!UICONTROL Compartir]**. Un mensaje confirma que el vínculo se comparte con los usuarios. Los usuarios reciben un correo electrónico con el vínculo compartido.

   ![Correo electrónico de uso compartido de vínculos](assets/link-sharing-email-notification.png)

### Descarga de recursos mediante el vínculo de recursos

Cualquier usuario que tenga acceso al vínculo de recursos compartidos puede descargar los recursos agrupados en una carpeta zip. El proceso de descarga es el mismo, tanto si un usuario accede al vínculo de recurso copiado como si utiliza el vínculo de recurso compartido a través del correo electrónico.

* Haga clic en el vínculo del recurso o pegue la dirección URL en el explorador. El [!UICONTROL Vínculos compartidos] se abre la interfaz, en la que puede cambiar al [!UICONTROL Vista de tarjeta] o [!UICONTROL Vista de lista].

* En el [!UICONTROL Vista de tarjeta], puede situar el ratón sobre el recurso compartido o la carpeta de recursos compartidos para seleccionarlos o colocarlos en la cola de descarga.

* De forma predeterminada, la interfaz de usuario muestra **[!UICONTROL Descargar bandeja de entrada]** opción. Refleja la lista de todos los recursos o carpetas compartidos que se ponen en cola para su descarga junto con su estado.

* Al seleccionar los recursos o la carpeta, aparece un **[!UICONTROL Descarga de cola]** opción aparece en la pantalla. Haga clic en **[!UICONTROL Descarga de cola]** para iniciar el proceso de descarga.

  ![Descarga de cola](assets/queue-download.png)

* Mientras prepara el archivo de descarga, haga clic en el icono **[!UICONTROL Descargar bandeja de entrada]** para ver el estado de la descarga. Para descargas grandes, haga clic en **[!UICONTROL Actualizar]** para actualizar el estado.

  ![Descargar bandeja de entrada](assets/link-sharing-download-inbox.png)

* Una vez completado el procesamiento, haga clic en **[!UICONTROL Descargar]** para descargar el archivo zip.

<!--
You can also copy the auto-generated link and share it with the users. The default expiration time for the link is one day.
-->

>[!NOTE]
>
>Si un recurso compartido se mueve a una ubicación diferente, su vínculo deja de funcionar. Vuelva a crear el vínculo y vuelva a compartirlo con los usuarios.


<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

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

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

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
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Descargar recursos y compartirlos por separado {#download-and-share-assets}

Los usuarios pueden descargar los recursos necesarios y compartirlos fuera de [!DNL Experience Manager]. Para obtener más información, consulte [cómo buscar recursos](/help/assets/search-assets.md), [cómo descargar recursos](/help/assets/download-assets-from-aem.md), y [cómo descargar colecciones](manage-collections.md#download-a-collection)

## Comparta recursos con profesionales creativos {#share-with-creatives}

Los especialistas en marketing y los usuarios de la línea de negocios pueden compartir fácilmente recursos aprobados con sus profesionales creativos mediante,

* **aplicación de escritorio de Experience Manager**: la aplicación funciona en Windows y Mac. Consulte [información general de aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=es). Para saber cómo cualquier usuario de escritorio autorizado puede acceder fácilmente a los recursos compartidos, consulte [examinar, buscar y previsualizar recursos](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Los usuarios de escritorio pueden crear recursos y volver a compartirlos con sus homólogos que sean usuarios Experience Manager, por ejemplo, cargando nuevas imágenes. Consulte [cargar recursos mediante la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: los profesionales creativos pueden buscar y utilizar recursos directamente desde [!DNL Adobe InDesign], [!DNL Adobe Illustrator], y [!DNL Adobe Photoshop].

## Configuración del uso compartido de recursos {#configure-sharing}

Las distintas opciones para compartir los recursos requieren una configuración específica y tienen requisitos previos específicos.

### Configurar el uso compartido de vínculos de recursos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para generar la dirección URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Usuarios con privilegios de administrador o con permisos de lectura en `/var/dam/share` Las ubicaciones de pueden ver los vínculos compartidos con ellas. Compartir recursos a través de un vínculo es una forma cómoda de poner los recursos a disposición de terceros externos sin tener que iniciar sesión primero en [!DNL Assets].

>[!NOTE]
>
>Si desea compartir vínculos de la instancia de autor a entidades externas, asegúrese de exponer solo las siguientes URL para `GET` solicitudes. Bloquee otras direcciones URL para asegurarse de que la instancia de autor sea segura.
>
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`

<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Habilitar las acciones de escritorio para usarlas con la aplicación de escritorio {#desktop-actions}

Desde dentro de [!DNL Assets] interfaz de usuario en un explorador, puede explorar las ubicaciones de los recursos o retirarlos y abrirlos para editarlos en la aplicación de escritorio. Estas opciones se denominan acciones de escritorio y, para habilitarlas, consulte [habilitar acciones de escritorio en [!DNL Assets] interfaz web](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Habilitar las acciones de escritorio para usarlas como acceso directo al trabajar con la aplicación de escritorio](assets/enable_desktop_actions.png)

### Configuraciones para utilizar [!DNL Adobe Asset Link] {#configure-asset-link}

Adobe Asset Link optimiza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Se conecta [!DNL Adobe Experience Manager Assets] con [!DNL Creative Cloud] aplicaciones de escritorio [!DNL Adobe InDesign], [!DNL Adobe Photoshop], y [!DNL Adobe Illustrator]. El [!DNL Adobe Asset Link] El panel permite a los creativos acceder y modificar el contenido almacenado en [!DNL Assets] sin salir de las aplicaciones creativas con las que están más familiarizados.

Consulte [cómo configurar [!DNL Assets] para utilizarlo con [!DNL Adobe Asset Link]](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).

## Prácticas recomendadas y solución de problemas {#bestpractices}

* Es posible que las carpetas de recursos o las colecciones que contienen un espacio en blanco en su nombre no se compartan.
* Si los usuarios no pueden descargar los recursos compartidos, consulte con el administrador del Experience Manager cuáles son los límites de descarga. El valor predeterminado es 100 MB.
* Para que un usuario obtenga una vista previa de un vídeo compartido mediante el uso compartido de vínculos, el vídeo debe tener una representación de vídeo estática disponible en `/jcr:content/renditions` ubicación en el nodo del vídeo en el repositorio. La vista previa no depende de la disponibilidad de un [!DNL Dynamic Media] representación.
* Al descargar un recurso de vídeo mediante el uso compartido de vínculos, la variable [!DNL Dynamic Media] las representaciones no se incluyen en el archivo descargado.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
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