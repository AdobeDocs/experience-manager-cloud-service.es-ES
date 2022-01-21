---
title: Descargar recursos
description: Descargar recursos desde [!DNL Adobe Experience Manager Assets] y habilite o deshabilite la funcionalidad de descarga.
contentOwner: VG
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 797f0e6585666196acf7972f93d936fc54359c4a
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 3%

---

# Descargar recursos desde [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puede descargar recursos, incluidas representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados están agrupados en un archivo ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

Los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel no se pueden descargar.

Puede descargar recursos de Experience Manager mediante los métodos siguientes:

<!-- * [Link Share](#link-share-download) -->

* [interfaz de usuario del Experience Manager](#download-assets)
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Descargar recursos mediante [!DNL Experience Manager] interfaz {#download-assets}

El servicio de descarga asincrónica ofrece un marco para la descarga sin problemas de recursos de gran tamaño. La descarga archiva más de 100 GB en divisiones de tamaño en múltiples archivos zip con un tamaño máximo de 100 GB cada uno. Se pueden descargar individualmente. Los archivos más pequeños se descargan desde la interfaz de usuario en tiempo real. [!DNL Experience Manager] no archiva descargas de recursos individuales en las que se descarga el archivo original. Esta funcionalidad permite descargas más rápidas.

De forma predeterminada, [!DNL Experience Manager] déclencheur una notificación una vez completado el flujo de trabajo de descarga. La notificación de descarga aparece en la sección  [[!DNL Experience Manager] Bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

![Notificación de bandeja de entrada](assets/inbox-notification-for-large-downloads.png)

<!--
The large files are downloaded asynchronously and [!DNL Experience Manager] notifies of the completion via notifications in the Inbox. See [understand [!DNL Experience Manager] Inbox](/help/sites-cloud/authoring/getting-started/inbox.md).

![Download notification](assets/download-notification.png)

*Figure: Download notification via [!DNL Experience Manager] Inbox.*

Asynchronous downloads are triggered in either of the following case:

* If there are more than 10 assets or more than 100 MB to be downloaded.
* If the download takes more than 30 seconds to prepare.
-->


<!-- Go live is on 27th Jan 2022
### Enable email notifications for large downloads {#enable-emails-for-large-downloads}

Asynchronous downloads are triggered in any of the following cases:

* If there are more than ten assets 
* If the download size is more than 100 MB
* If the download takes more than 30 seconds to prepare

While the asynchronous download runs at the backend, the user can continue to explore and work further in Experience Manager. An out-of-the-box mechanism is required to notify the user upon completion of the download process. To achieve this objective, the administrators can configure email service by setting up an SMTP server. See [configure Mail Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#sending-email).

Once the email service is configured, the administrators and users can enable email notifications from the Experience Manager interface. 

To enable email notifications:

1. Log in to [!DNL Experience Manager Assets].
1. Click the user icon from the upper-right corner and then click **[!UICONTROL My Preferences]**. The User Preferences window opens.
1. Select the **[!UICONTROL Asset Download email notifications]** check box and click **[!UICONTROL Accept]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)

-->

Para descargar recursos, siga estos pasos:

1. En [!DNL Experience Manager] interfaz de usuario, haga clic en **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. Vaya a los recursos que desee descargar. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.

   ![Opciones disponibles al descargar recursos de [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. En el cuadro de diálogo de descarga, seleccione las opciones de descarga que desee.

   | Opción Descargar | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir cada recurso que descargue, incluidos los recursos de carpetas secundarias anidadas en la carpeta principal del recurso, en una carpeta del equipo local. Cuando esta opción esté *not* seleccione, de forma predeterminada, la jerarquía de carpetas se ignora y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Seleccione esta opción para enviar una notificación por correo electrónico (que contenga un vínculo a la descarga) a otro usuario. El usuario destinatario debe ser miembro de `dam-users` grupo. Las plantillas de correos electrónicos estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que personalice durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recursos]** | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representaciones]** | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado desde [!DNL Experience Manager]. Se crea y descarga un archivo zip con las representaciones de Recorte inteligente en el equipo local. |
   | **[!UICONTROL Representaciones dinámicas]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Al seleccionar esta opción, también puede seleccionar las representaciones que desea crear dinámicamente seleccionando una de las opciones del [Ajuste preestablecido de imagen](/help/assets/dynamic-media/image-presets.md) lista. <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como invertir la imagen. La opción solo está disponible si tiene [!DNL Dynamic Media] activada. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]**.

   Si la notificación por correo electrónico está habilitada para las descargas masivas, en la bandeja de entrada aparecerá un correo electrónico que contiene una dirección URL de descarga de la carpeta zip archivada. Haga clic en el vínculo de descarga del correo electrónico para descargar la carpeta zip.

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   También puede ver la notificación en su [!DNL Experience Manager] Bandeja de entrada.

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Descargar recursos compartidos mediante el uso compartido de vínculos {#link-share-download}

<!--
>[!NOTE]
>
>This functionality is available in the Experience Manager prerelease channel.
-->

El uso compartido de recursos mediante un vínculo es una forma cómoda de ponerlo a disposición de los interesados sin que tengan que iniciar sesión primero en [!DNL Assets]. Consulte [Vincular funcionalidad compartida](/help/assets/share-assets.md#sharelink).

Cuando los usuarios descargan recursos de vínculos compartidos, [!DNL Assets] utiliza un servicio asíncrono que ofrece descargas más rápidas e ininterrumpidas. Los recursos que se van a descargar se ponen en cola en segundo plano en una bandeja de entrada en archivos ZIP de tamaño de archivo manejable. Para descargas muy grandes, la descarga se divide en archivos de 100 GB de tamaño.

La bandeja de entrada muestra el estado de procesamiento de cada archivo. Una vez completado el procesamiento, puede descargar los archivos de la bandeja de entrada.

![Descargar bandeja de entrada](assets/download-inbox.png)

## Habilitar el servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado de [!DNL Experience Manager] permite a los usuarios autenticados emitir solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos. La preparación de la descarga puede tener implicaciones de rendimiento o incluso puede sobrecargar el servidor y la red. Para mitigar los riesgos potenciales de tipo DoS causados por esta función, `AssetDownloadServlet` El componente OSGi está deshabilitado para las instancias de publicación. Si no necesita la función de descarga en las instancias de autor, deshabilite el servlet en el autor.

Para permitir la descarga de recursos de su DAM, por ejemplo, al usar algo como Asset Share Commons u otra implementación similar a un portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda configurar el tamaño de descarga permisible lo más bajo posible sin afectar a los requisitos de descarga diarios. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombres dirigida al modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. En la carpeta de configuración, cree un nuevo archivo de tipo `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellenar `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente: Establece un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El siguiente ejemplo configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar el servlet de descarga de recursos {#disable-asset-download-servlet}

Si no necesita la funcionalidad de descarga, deshabilite el servlet para evitar riesgos similares a DoS. La variable `Asset Download Servlet` se puede deshabilitar en una [!DNL Experience Manager] crear y publicar instancias actualizando la configuración de Dispatcher para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede deshabilitar manualmente a través de la consola OSGi directamente.

1. Para bloquear las solicitudes de descarga de recursos a través de la configuración de Dispatcher, edite la `dispatcher.any` y agregue una regla nueva al [sección de filtro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Sugerencias y limitaciones {#tips-limitations}

* Si descarga una carpeta vacía, [!DNL Experience Manager] transmite un mensaje de éxito sobre la creación de un archivo ZIP, pero no se crea el archivo.

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos DRM](drm.md)
>* [Descargar recursos mediante la aplicación de escritorio de Experience Manager en Win o Mac Desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Descargar recursos mediante el vínculo de recursos de Adobe desde las aplicaciones de Adobe Creative Cloud compatibles](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

