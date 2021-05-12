---
title: Descargar recursos
description: Descargue recursos de [!DNL Adobe Experience Manager Assets] y habilite o deshabilite la funcionalidad de descarga.
contentOwner: AG
feature: Administración de activos
role: Business Practitioner
exl-id: f68b03ba-4ca1-4092-b257-16727fb12e13
translation-type: tm+mt
source-git-commit: a14d5ec69889ef3d89e595cd837f182c499d0ebc
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 4%

---

# Descargar recursos de [!DNL Adobe Experience Manager] {#download-assets-from-aem}

Puede descargar recursos, incluidas representaciones estáticas y dinámicas. También puede enviar correos electrónicos con vínculos a recursos directamente desde [!DNL Adobe Experience Manager Assets]. Los recursos descargados están agrupados en un archivo ZIP. El archivo ZIP comprimido tiene un tamaño máximo de 1 GB para el trabajo de exportación. Se permite un máximo de 500 activos totales por trabajo de exportación.

>[!NOTE]
>
>Los destinatarios de los correos electrónicos deben ser miembros del grupo `dam-users` para acceder al vínculo de descarga ZIP en el mensaje de correo electrónico. Para poder descargar los recursos, los miembros deben tener permisos para iniciar flujos de trabajo que permitan la descarga de recursos.

Los tipos de recurso Conjuntos de imágenes, Conjuntos de giros, Conjuntos de medios mixtos y Conjuntos de carrusel no se pueden descargar.

Puede descargar recursos de Experience Manager mediante los métodos siguientes:

* [interfaz de usuario del Experience Manager](#download-in-aem)
* Interfaz de usuario de Asset Link Share
* [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
* [Aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#download-assets)

## Descargar recursos mediante la interfaz [!DNL Experience Manager] {#download-in-aem}

El servicio de descarga asincrónica ofrece un marco para la descarga sin problemas de recursos de gran tamaño. Los archivos más pequeños se descargan desde la interfaz de usuario en tiempo real. Los archivos grandes se descargan de forma asíncrona y se informa a los usuarios de la finalización mediante notificaciones del Experience Manager en la Bandeja de entrada. Consulte [explicación de la bandeja de entrada del Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html).

![Descargar notificación](assets/download-notification.png)

*Figura: Descargue la notificación a través de la  [!DNL Experience Manager] Bandeja de entrada.*

Las descargas asincrónicas se activan en cualquiera de los casos siguientes:

* Si hay más de 10 recursos o más de 100 MB que descargar.
* Si la descarga tarda más de 30 segundos en prepararse.

Para descargar recursos, siga estos pasos:

1. En la interfaz de usuario [!DNL Experience Manager], haga clic en **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Vaya a los recursos que desee descargar. Seleccione la carpeta o seleccione uno o varios recursos de la carpeta. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.

   ![Opciones disponibles al descargar recursos de  [!DNL Experience Manager Assets]](/help/assets/assets/asset-download1.png)

   *Figura: Opciones del cuadro de diálogo Descargar.*

1. En el cuadro de diálogo Descargar, seleccione las opciones de descarga que desee.

   | Opción Descargar | Descripción |
   |---|---|
   | **[!UICONTROL Crear una carpeta independiente para cada recurso]** | Seleccione esta opción para incluir cada recurso que descargue, incluidos los recursos de carpetas secundarias anidadas en la carpeta principal del recurso, en una carpeta del equipo local. Cuando esta opción está *not* seleccionada, de forma predeterminada, la jerarquía de carpetas se ignora y todos los recursos se descargan en una carpeta del equipo local. |
   | **[!UICONTROL Correo electrónico]** | Seleccione esta opción para que se envíe una notificación por correo electrónico al destinatario. Las plantillas de correos electrónicos estándar están disponibles en las siguientes ubicaciones:<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> Las plantillas que personalice durante la implementación están disponibles en las siguientes ubicaciones: <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>Puede almacenar plantillas personalizadas específicas del inquilino en las siguientes ubicaciones:<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Recursos]** | Seleccione esta opción para descargar el recurso en su formulario original sin ninguna representación.<br>La opción de subrecursos está disponible si el recurso original tiene subrecursos. |
   | **[!UICONTROL Representaciones]** | Una representación es la representación binaria de un recurso. Los recursos tienen una representación principal: la del archivo cargado. Pueden tener cualquier número de representaciones. <br> Con esta opción, puede seleccionar las representaciones que desee descargar. Las representaciones disponibles dependen del recurso seleccionado. |
   | **[!UICONTROL Recortes inteligentes]** | Seleccione esta opción para descargar todas las representaciones de recorte inteligente del recurso seleccionado desde [!DNL Experience Manager]. Se crea y descarga un archivo zip con las representaciones de Recorte inteligente en el equipo local. |
   | **[!UICONTROL Representaciones dinámicas]** | Seleccione esta opción para generar una serie de representaciones alternativas en tiempo real. Al seleccionar esta opción, también puede seleccionar las representaciones que desea crear dinámicamente seleccionando una de las [Ajustes preestablecidos de imagen](/help/assets/dynamic-media/image-presets.md). <br>Además, puede seleccionar el tamaño y la unidad de medida, el formato, el espacio de color, la resolución y cualquier modificador de imagen opcional, como invertir la imagen. La opción solo está disponible si tiene [!DNL Dynamic Media] habilitado. |

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Descargar]**.

## Habilitar el servlet de descarga de recursos {#enable-asset-download-servlet}

El servlet predeterminado en [!DNL Experience Manager] permite que los usuarios autenticados emitan solicitudes de descarga concurrentes de gran tamaño arbitrario para crear archivos ZIP de recursos. La preparación de la descarga puede tener implicaciones de rendimiento o incluso puede sobrecargar el servidor y la red. Para mitigar los posibles riesgos de tipo DoS causados por esta función, el componente OSGi `AssetDownloadServlet` está deshabilitado para las instancias de publicación. Si no necesita la función de descarga en las instancias de autor, deshabilite el servlet en el autor.

Para permitir la descarga de recursos de su DAM, por ejemplo, al usar algo como Asset Share Commons u otra implementación similar a un portal, habilite manualmente el servlet mediante una configuración OSGi. Adobe recomienda configurar el tamaño de descarga permisible lo más bajo posible sin afectar a los requisitos de descarga diarios. Un valor alto puede afectar al rendimiento.

1. Cree una carpeta con una convención de nombres dirigida al modo de ejecución de publicación, es decir, `config.publish`:

   `/apps/<your-app-name>/config.publish`

1. En la carpeta de configuración, cree un nuevo archivo de tipo `nt:file` denominado `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`.
1. Rellene `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` con lo siguiente: Establece un tamaño máximo (en bytes) para la descarga como valor de `asset.download.prezip.maxcontentsize`. El siguiente ejemplo configura el tamaño máximo de la descarga ZIP para que no supere los 100 kB.

   ```java
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## Deshabilitar servlet de descarga de recursos {#disable-asset-download-servlet}

Si no necesita la funcionalidad de descarga, deshabilite el servlet para evitar riesgos similares a DoS. El `Asset Download Servlet` se puede deshabilitar en una [!DNL Experience Manager] instancia de autor y publicación actualizando la configuración del despachante para bloquear cualquier solicitud de descarga de recursos. El servlet también se puede deshabilitar manualmente a través de la consola OSGi directamente.

1. Para bloquear las solicitudes de descarga de recursos a través de una configuración de Dispatcher, edite la configuración `dispatcher.any` y añada una nueva regla a la sección [filter](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring).

   `/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

>[!MORELIKETHIS]
>
>* [Descargar recursos protegidos DRM](drm.md)
>* [Descargar recursos mediante la aplicación de escritorio de Experience Manager en Win o Mac local](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=es)
>* [Descargar recursos mediante el vínculo de recursos de Adobe desde las aplicaciones de Adobe Creative Cloud compatibles](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)

