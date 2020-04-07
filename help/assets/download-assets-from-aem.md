---
title: Descarga de recursos de AEM
description: Obtenga información sobre cómo descargar recursos de AEM y activar o desactivar la funcionalidad de descarga.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# Descarga de recursos de AEM {#download-assets-from-aem}

Puede descargar recursos, incluidas las representaciones estáticas y dinámicas. Los recursos descargados se incluyen en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 recursos totales por trabajo de exportación.

>[!NOTE]
>
>Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que activen la descarga de recursos.

Para descargar recursos, navegue hasta un recurso, selecciónelo y toque o haga clic en el icono **[!UICONTROL Descargar]** de la barra de herramientas. En el cuadro de diálogo resultante, especifique las opciones de descarga.

No se pueden descargar los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel.

![Opciones disponibles al descargar recursos de Recursos](assets/asset_download_dialog.png)AEM *Figura: Opciones disponibles al descargar recursos de Recursos AEM*

Las siguientes son las opciones de exportación y descarga. Las representaciones dinámicas son exclusivas de Dynamic Media y permiten generar representaciones sobre la marcha además del recurso seleccionado; esta opción solo está disponible si tiene Dynamic Media activado.

| Opciones de exportación o descarga | Descripciones |
|---|---|
| [!UICONTROL Recursos] | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación. |
| [!UICONTROL Representaciones] | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
| [!UICONTROL Representaciones dinámicas] | Una representación dinámica genera otras representaciones sobre la marcha. Cuando selecciona esta opción, también selecciona las representaciones que desea crear dinámicamente seleccionando una de las listas de ajustes preestablecidos de imagen. Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen (por ejemplo, para invertir la imagen) |
| [!UICONTROL Crear una carpeta independiente para cada recurso] | Seleccione esta opción para conservar la jerarquía de carpetas al descargar recursos. De forma predeterminada, la jerarquía de carpetas se ignora y todos los recursos se descargan en una carpeta del sistema local. |

La opción Representaciones está disponible si el recurso tiene representaciones. La opción de subrecursos está disponible si el recurso incluye subrecursos.

Cuando selecciona una carpeta para descargar, se descarga la jerarquía completa de recursos bajo la carpeta. Para incluir cada recurso que descargue (incluidos los recursos de las carpetas secundarias anidadas en la carpeta principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado de AEM permite a los usuarios autenticados emitir solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos visibles para ellos que pueden sobrecargar el servidor y la red. Para mitigar los posibles riesgos de DoS causados por esta función, el componente `AssetDownloadServlet` OSGi está deshabilitado de forma predeterminada para las instancias de publicación.

Para permitir la descarga de recursos de su DAM, por ejemplo, cuando se utiliza algo como Asset Share Commons u otra implementación similar al portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda que el tamaño de descarga permitido sea lo más bajo posible sin afectar a los requisitos de descarga diaria. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombre que destinatario el modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. En la carpeta config, cree un nuevo archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Define un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El ejemplo siguiente configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede desactivar en instancias de AEM Publish actualizando la configuración del despachante para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede desactivar manualmente directamente mediante la consola OSGi.

1. Para bloquear las solicitudes de descarga de recursos mediante una configuración de distribuidor, edite la `dispatcher.any` configuración y agregue una nueva regla a la sección [de](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter)filtros.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos DRM](drm.md)
>* [Descargar recursos con la aplicación de escritorio AEM en Windows o Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Descargar recursos mediante Adobe Assets Link desde las aplicaciones compatibles de Adobe Creative Cloud](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html)


<!-- FULL ARTICLE ARCHIVE IS BELOW 

You can download assets including static and dynamic renditions. Alternatively, you can send emails with links to assets directly from AEM Assets. Downloaded assets are bundled in a ZIP file. The compressed ZIP file has a maximum file size of 1 GB for the export job. You are allowed a maximum of 500 total assets per export job.

>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.

To download assets, navigate to an asset, select the asset, and tap/click the **[!UICONTROL Download]** icon from the toolbar. In the resulting dialog, specify your download options.

The asset types Image Sets, Spin Sets, Mixed Media Sets, and Carousel Sets cannot be downloaded.

![Available options when downloading assets from AEM Assets](assets/asset_download_dialog.png)
*Figure: Available options when downloading assets from AEM Assets*

The following are the Export/Download options. Dynamic renditions are unique to Dynamic Media and let you generate renditions on-the-fly in addition to the asset you selected - that option is only available if you have Dynamic Media enabled.

|Export or download options|Descriptions|
|---|---|
| [!UICONTROL Assets]| Select this to download the asset in its original form without any renditions.|
| [!UICONTROL Renditions] |A rendition is the binary representation of an asset. Assets have a primary representation - that of the uploaded file. They can have any number of representations. <br> With this option, you can select the renditions you want downloaded. The renditions available depend on the asset you select.|
| [!UICONTROL Dynamic Renditions] |A dynamic rendition generates other renditions on-the-fly. When you select this option, you also select the renditions you want to create dynamically by selecting from the image presets list. In addition, you can select the size and unit of measurement, format, color space, resolution, and any image modifiers (for example to invert the image)|
| [!UICONTROL Email] |An email notification is sent to the user. Standard emails templates are available at the following locations:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul> Templates that you customize during deployment should be present at these locations: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>You can store tenant-specific custom templates at these locations:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`</li></ul>|
| [!UICONTROL Create separate folder for each asset] |Select this to preserve the folder hierarchy while downloading assets. By default, the folder hierarchy is ignored and all assets are downloaded in one folder in your local system.|

The option renditions option is available if the asset has any renditions. The subassets option is available if the asset includes subassets.

When you select a folder to download, the complete asset hierarchy under the folder is downloaded. To include each asset you download (including assets in child folders nested under the parent folder) in an individual folder, select **[!UICONTROL Create separate folder for each asset]**.

## Enable asset download servlet {#enable-asset-download-servlet}

The default servlet in AEM allows authenticated users to issue arbitrarily-large, concurrent download requests for creating ZIP files of assets visible to them that can overload the server and the network. To mitigate potential DoS risks caused by this feature, `AssetDownloadServlet` OSGi component is disabled by default for publish instances.

To allow downloading assets from your DAM, say when using something like Asset Share Commons or other portal-like implementation, manually enable the servlet via an OSGi configuration. Adobe recommends setting the permissible download size as low as possible without affecting the day-to-day download requirements. A high value may impact performance.

1. Create a folder with a naming convention that targets the publish runmode, that is, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. In the config folder, create a new file of type `nt:file` named `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Populate `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` with the following. Sets a maximum size (in bytes) for the download as value of `asset.download.prezip.maxcontentsize`. The below sample configures the maximum size of the ZIP download to not exceed 100 kB.

   ```
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Disable asset download servlet {#disable-asset-download-servlet}

The `Asset Download Servlet` can be disabled on an AEM Publish instances by updating the dispatcher configuration to block any asset download requests. The servlet can also be manually disabled via the OSGi console directly.

1. To block asset download requests via a dispatcher configuration edit the `dispatcher.any` configuration and add a new rule to the [filter section](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#defining-a-filter).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Download DRM protected assets](drm.md)
>* [Download assets using AEM desktop app on Win or Mac desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Download assets using Adobe Assets Link from within the supported Adobe Creative Cloud apps](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)


-->