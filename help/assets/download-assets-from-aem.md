---
title: Descarga de recursos
description: Descargue recursos de [!DNL Adobe Experience Manager Assets] y habilite o deshabilite la funcionalidad de descarga.
contentOwner: Vishabh Gupta
feature: Asset Management
role: User
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 5%

---

# Descargar recursos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

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
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/download-assets-from-aem.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Puede descargar recursos, incluidas representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados están agrupados en un archivo ZIP. <!-- The compressed ZIP file has a maximum file size of 1 GB for the export job. A maximum of 500 total assets per export job are allowed. -->

<!--
>[!NOTE]
>
>Recipients of emails must be members of the `dam-users` group to access the ZIP download link in the email message. To be able to download the assets, the members must have permissions to launch workflows that trigger downloading of assets.
-->

No se pueden descargar los siguientes tipos de recursos: conjuntos de imágenes, conjuntos de giros, conjuntos de medios mixtos y conjuntos de carrusel.

Puede descargar recursos desde Experience Manager mediante los métodos siguientes:

<!-- * [Link Share](#link-share-download) -->

* [Interfaz de usuario de Experience Manager](#download-assets)
* [Uso compartido de recursos Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=es)
* [aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es#download-assets)

## Descargar recursos mediante la interfaz [!DNL Experience Manager] {#download-assets}

Experience Manager optimiza la experiencia de descarga en función de la cantidad y el tamaño del recurso. Los archivos más pequeños se descargan de la interfaz de usuario en tiempo real. [!DNL Experience Manager] descarga directamente solicitudes de recursos individuales para el archivo original en lugar de incluir recursos individuales en un archivo ZIP para permitir descargas más rápidas. Experience Manager admite descargas grandes con solicitudes asincrónicas. Las solicitudes de descarga superiores a 100 GB se dividen en varios archivos ZIP con un tamaño máximo de 100 MB cada uno.

De manera predeterminada, [!DNL Experience Manager] almacena en déclencheur una notificación en la [[!DNL Experience Manager] Bandeja de entrada](/help/sites-cloud/authoring/inbox.md) al generar un archivo de descarga.

![Notificación de bandeja de entrada](assets/inbox-notification-for-large-downloads.png)


### Habilitar notificaciones por correo electrónico para descargas grandes {#enable-emails-for-large-downloads}

Las descargas asincrónicas se activan en cualquiera de los siguientes casos:

* Si hay más de diez recursos
* Si el tamaño de la descarga es superior a 100 MB
* Si la descarga tarda más de 30 segundos en prepararse

Mientras que la descarga asincrónica se ejecuta en el servidor, el usuario puede seguir explorando y trabajando en Experience Manager. Además de las notificaciones de la bandeja de entrada de Experience Manager, Experience Manager puede enviar correos electrónicos para notificar al usuario una vez completado el proceso de descarga. Para habilitar esta función, los administradores pueden configurar el servicio de correo electrónico al [configurar una conexión de servidor SMTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=es#sending-email).

Una vez configurado el servicio de correo electrónico, los administradores y usuarios pueden activar las notificaciones por correo electrónico desde la interfaz de Experience Manager.

Para habilitar las notificaciones por correo electrónico:

1. Inicie sesión en [!DNL Experience Manager Assets].
1. Haga clic en el icono de usuario en la esquina superior derecha y, a continuación, haga clic en **[!UICONTROL Mis preferencias]** para abrir la ventana Preferencias de usuario.
1. Seleccione la casilla de verificación **[!UICONTROL Notificaciones por correo electrónico de descarga de recursos]** y haga clic en **[!UICONTROL Aceptar]**.

   ![enable-email-notifications-for-large-downloads](/help/assets/assets/enable-email-for-large-downloads.png)


Para descargar recursos, siga estos pasos:

1. En la interfaz de usuario de [!DNL Experience Manager], haga clic en **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Desplácese hasta los recursos que desee descargar. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.

   ![Opciones disponibles al descargar recursos de [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

1. En el cuadro de diálogo de descarga, seleccione las opciones de descarga que desee.

   | Opción Descargar | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para crear una carpeta para cada recurso que contenga todas las representaciones descargadas para el recurso. Si no se selecciona, cada recurso (y sus representaciones si se seleccionan para su descarga) se encuentra en la carpeta principal del archivo generado. |
   | **[!UICONTROL Correo electrónico]** | Seleccione esta opción para enviar una notificación por correo electrónico (que contenga un vínculo a la descarga) a otro usuario. El usuario destinatario debe ser miembro del grupo `dam-users`. Las plantillas de correo electrónico estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que personaliza durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recurso(s)]** | Seleccione esta opción para descargar el recurso en su forma original.<br>La opción subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representación(es)]** | Una representación es la representación binaria de un recurso. Assets tiene una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desea descargar. Las representaciones disponibles dependen del recurso seleccionado. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado dentro de [!DNL Experience Manager]. Se crea un archivo zip con las representaciones de recorte inteligente y se descarga en el equipo local. |
   | **[!UICONTROL Representación(es) dinámica(es)]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Cuando selecciona esta opción, también selecciona las representaciones que desea crear dinámicamente seleccionando de la lista [Ajuste preestablecido de imagen](/help/assets/dynamic-media/image-presets.md). <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como la inversión de la imagen. La opción solo está disponible si tiene habilitado [!DNL Dynamic Media]. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]**.

   Si la notificación por correo electrónico está habilitada para descargas grandes, aparecerá en la bandeja de entrada un mensaje de correo electrónico con la URL de descarga de la carpeta zip archivada. Haga clic en el vínculo de descarga del correo electrónico para descargar el archivo zip.

   ![email-notifications-for-large-downloads](/help/assets/assets/email-for-large-notification.png)

   También puede ver la notificación en la Bandeja de entrada [!DNL Experience Manager].

   ![inbox-notifications-for-large-downloads](/help/assets/assets/inbox-notification-for-large-downloads.png)

## Descargar recursos compartidos mediante el uso compartido de vínculos {#link-share-download}

Compartir recursos mediante un vínculo es una forma cómoda de ponerlos a disposición de las personas interesadas sin que tengan que iniciar sesión en [!DNL Assets]. Ver [funcionalidad de vínculos compartidos](/help/assets/share-assets.md#sharelink).

Cuando los usuarios descargan recursos desde vínculos compartidos, [!DNL Assets] utiliza un servicio asincrónico que ofrece descargas más rápidas e ininterrumpidas. Los recursos que se van a descargar se colocan en segundo plano en una bandeja de entrada en archivos ZIP de tamaño de archivo manejable. Para descargas mayores, la descarga se divide en archivos de 100 GB.

La [!UICONTROL Bandeja de entrada de descarga] muestra el estado de procesamiento de cada archivo. Una vez completado el procesamiento, puede descargar los archivos desde la bandeja de entrada.

![Descargar bandeja de entrada](assets/link-sharing-download-inbox.png)

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado en [!DNL Experience Manager] permite que los usuarios autenticados emitan solicitudes de descarga simultáneas y arbitrariamente grandes para crear archivos ZIP de recursos. La preparación de la descarga puede tener implicaciones de rendimiento o incluso puede sobrecargar el servidor y la red. Para mitigar estos riesgos potenciales de tipo DoS causados por esta característica, el componente OSGi `AssetDownloadServlet` está deshabilitado para las instancias de publicación. Si no necesita la función de descarga en instancias de autor, deshabilite el servlet en Author.

Para permitir la descarga de recursos desde su DAM, por ejemplo, cuando utilice algo como Asset Share Commons u otra implementación similar a un portal, habilite manualmente el servlet a través de una configuración OSGi. Adobe recomienda configurar el tamaño de descarga permitido lo más bajo posible sin afectar a los requisitos de descarga diarios. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombres que se dirija al modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. En la carpeta de configuración, cree un archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Establece un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El siguiente ejemplo configura el tamaño máximo de la descarga ZIP para que no supere los 100 KB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

Si no necesita la funcionalidad de descarga, deshabilite el servlet para evitar riesgos similares al DoS. `Asset Download Servlet` se puede deshabilitar en las instancias de autor y publicación de [!DNL Experience Manager] al actualizar la configuración de Dispatcher para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede deshabilitar manualmente a través de la consola OSGi directamente.

1. Para bloquear solicitudes de descarga de recursos a través de una configuración de Dispatcher, edite la configuración de `dispatcher.any` y agregue una nueva regla a la [sección de filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

## Representación OnTime u OffTime {#on-off-time-rendition}

Para habilitar el servicio `OnOffTimeAssetAccessFilter`, debe crear una configuración OSGi. Este servicio permite bloquear el acceso a representaciones y metadatos, además del propio recurso en función de la configuración de tiempo de activación/desactivación. La configuración de OSGi debe ser para `com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter`. Complete los siguientes pasos:

1. En el código de su proyecto en Git, cree un archivo de configuración en `/apps/system/config/com.day.cq.dam.core.impl.servlet.OnOffTimeAssetAccessFilter.cfg.json`. El archivo debe contener `{}` como contenido, lo que significa una configuración OSGi vacía para el componente OSGi correspondiente. Esta acción habilita el servicio.
1. Implemente su código, incluida esta nueva configuración, mediante [!DNL Cloud Manager].
1. Una vez implementados, se puede acceder a las representaciones y los metadatos según la configuración de tiempo de activación y desactivación de los recursos. Si la fecha u hora actual es anterior a la hora de activación o posterior a la hora de inactividad, se muestra un mensaje de error.
Para obtener más información sobre cómo agregar una configuración OSGi vacía, consulte esta [guía](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=es).

## Sugerencias y limitaciones {#tips-limitations}

* Si descarga una carpeta vacía, [!DNL Experience Manager] transmite un mensaje de éxito acerca de la creación de un archivo ZIP, pero el archivo no se crea.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos por DRM](drm.md)
>* [Descargar recursos mediante la aplicación de escritorio de Experience Manager en Windows o Mac Desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es)
>* [Descargue recursos mediante Adobe Assets Link desde las aplicaciones de Adobe Creative Cloud admitidas](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html)
