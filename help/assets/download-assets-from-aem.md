---
title: Descargar recursos
description: Descargue recursos [!DNL Adobe Experience Manager Assets] desde y habilite o deshabilite la funcionalidad de descarga.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b1586cd9d6b3e9da115bff802d840a72d1207e4a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 4%

---


# Download assets from [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puede descargar recursos, incluidas las representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados se incluyen en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 recursos totales por trabajo de exportación.

>[!NOTE]
>
>Destinatarios de correos electrónicos deben ser miembros del `dam-users` grupo para acceder al vínculo de descarga ZIP del mensaje de correo electrónico. Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que activen la descarga de recursos.

No se pueden descargar los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel.

Puede descargar recursos de Experience Manager mediante los siguientes métodos:

* [interfaz de usuario de Experience Manager](#download-in-aem)
* Interfaz de usuario de uso compartido de vínculos de recursos
* [Uso compartido de recursos comunes](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Descargar recursos mediante AEM interfaz {#download-in-aem}

El servicio de descarga asincrónico proporciona un marco para la descarga sin problemas de recursos de gran tamaño. Los archivos más pequeños se descargan de la interfaz de usuario en tiempo real. Los archivos de gran tamaño se descargan de forma asíncrona y se informa a los usuarios de la finalización mediante notificaciones de Experience Manager en la Bandeja de entrada. Consulte [Descripción de la bandeja de entrada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html)del Experience Manager.

![Descargar notificación](assets/download-notification.png)

*Figura: Descargue la notificación a través de la [!DNL Experience Manager] Bandeja de entrada.*

Las descargas asincrónicas se activan en cualquiera de los casos siguientes:

* Si hay más de 10 recursos o más de 100 MB para descargar.
* Si la descarga tarda más de 30 segundos en prepararse.

Para descargar recursos, siga estos pasos:

1. En [!DNL Experience Manager] la interfaz de usuario, haga clic en **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. Vaya a los recursos que desee descargar. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.

   ![Opciones disponibles al descargar recursos de [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Figura: Opciones del cuadro de diálogo Descargar.*

1. En el cuadro de diálogo Descargar, seleccione las opciones de descarga que desee.

   | Opción de descarga | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir cada recurso que descargue, incluidos los recursos de carpetas secundarias anidados en la carpeta principal del recurso, en una carpeta del equipo local. Cuando esta opción *no está* seleccionada, de forma predeterminada se ignora la jerarquía de carpetas y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Seleccione esta opción para que se envíe una notificación por correo electrónico al destinatario. Las plantillas de correo electrónico estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que se personalizan durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recursos]** | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representaciones]** | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado desde dentro [!DNL Experience Manager]. Se crea un archivo zip con las representaciones de recorte inteligente y se descarga en el equipo local. |
   | **[!UICONTROL Representaciones dinámicas]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Al seleccionar esta opción, también puede seleccionar las representaciones que desea crear dinámicamente seleccionando una de las que aparecen en la lista Ajuste preestablecido [de](/help/assets/dynamic-media/image-presets.md) imagen. <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como invertir la imagen. La opción solo está disponible si se ha [!DNL Dynamic Media] activado. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]**.

## Habilitar servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado de [!DNL Experience Manager] permite a los usuarios autenticados emitir solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos. La preparación de la descarga puede tener implicaciones de rendimiento o incluso puede sobrecargar el servidor y la red. Para mitigar los riesgos potenciales de tipo DoS causados por esta función, el componente `AssetDownloadServlet` OSGi está desactivado para las instancias de publicación.

Para permitir la descarga de recursos de su DAM, por ejemplo, cuando se utiliza algo como Asset Share Commons u otra implementación similar al portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda que el tamaño de descarga permitido sea lo más bajo posible sin afectar a los requisitos de descarga diaria. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombre que destinatario el modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. En la carpeta config, cree un nuevo archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente. Define un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El ejemplo siguiente configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

El `Asset Download Servlet` se puede deshabilitar en instancias de [!DNL Experience Manager] publicación actualizando la configuración del despachante para bloquear las solicitudes de descarga de recursos. El servlet también se puede desactivar manualmente directamente mediante la consola OSGi.

1. Para bloquear las solicitudes de descarga de recursos mediante una configuración de distribuidor, edite la `dispatcher.any` configuración y agregue una nueva regla a la sección [de](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring)filtros.

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos DRM](drm.md)
>* [Descargar recursos mediante la aplicación de escritorio Experience Manager en el escritorio de Windows o Mac](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)
>* [Descargar recursos mediante el vínculo Recursos de Adobe desde las aplicaciones de Adobe Creative Cloud admitidas](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

