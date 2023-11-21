---
title: Configuración del Cloud Service de Dynamic Media
description: Obtenga información sobre cómo configurar Dynamic Media en Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '3794'
ht-degree: 3%

---

# Acerca de la configuración del Cloud Service Dynamic Media {#configuring-dynamic-media}

Si utiliza Adobe Experience Manager para diferentes entornos, como desarrollo, ensayo y producción en directo, configure los Cloud Service de Dynamic Media para cada uno de esos entornos.

Consulte también [Configuración de una cuenta de alias de empresa de Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md)

## Diagrama de arquitectura de Dynamic Media {#architecture-diagram-of-dynamic-media}

En el siguiente diagrama de arquitectura se describe cómo funciona Dynamic Media.

Con la nueva arquitectura, Experience Manager es responsable de los recursos de origen principales y se sincroniza con Dynamic Media para el procesamiento y la publicación de recursos:

1. Cuando el recurso de origen principal se carga en Adobe Experience Manager as a Cloud Service, se replica en Dynamic Media. En este punto, Dynamic Media gestiona todo el procesamiento de recursos y la generación de representaciones, como la codificación de vídeo y las variantes dinámicas de una imagen.
1. Una vez generadas las representaciones, Experience Manager as a Cloud Service puede acceder y previsualizar de forma segura las representaciones remotas de Dynamic Media (no se envían binarios de vuelta a la instancia as a Cloud Service del Experience Manager).
1. Una vez que el contenido está listo para publicar y aprobar, déclencheur al servicio Dynamic Media para que inserte contenido en los servidores de entrega y almacene en caché el contenido en la CDN (red de entrega de contenido).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>La siguiente lista de funciones requiere que utilice la CDN predeterminada que está incluida con Adobe Experience Manager - Dynamic Media. Estas funciones no admiten ninguna otra CDN personalizada.
>
>* [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md)
>* [Invalidación de caché](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Protección de vínculos interactivos](/help/assets/dynamic-media/hotlink-protection.md)
>* [Entrega de contenido HTTP/2](/help/assets/dynamic-media/http2faq.md)
>* Redireccionamiento de URL en el nivel de CDN
>* Akamai ChinaCDN (para una entrega óptima en China)

<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## Creación de una configuración de Dynamic Media en Cloud Service {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. En Experience Manager as a Cloud Service, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. A la izquierda de la consola, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Cloud Service > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** (no seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**). A continuación seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración de Dynamic Media]** , introduzca el título, la dirección de correo electrónico y la contraseña de la cuenta de Dynamic Media del administrador de la empresa de la cuenta de Dynamic Media y, a continuación, seleccione su región. Esta información se proporciona por Adobe en el correo electrónico de aprovisionamiento. Póngase en contacto con Asistencia al cliente de Adobe si no recibió este correo electrónico.
1. Seleccionar **[!UICONTROL Conectar con Dynamic Media]**.
1. En el **[!UICONTROL Cambiar contraseña]** , en el **[!UICONTROL Nueva contraseña]** , introduzca una nueva contraseña de 8 a 25 caracteres. La contraseña debe contener al menos una de las siguientes opciones:

   * Letra mayúscula
   * Letra minúscula
   * Número
   * Carácter especial: `# $ & . - _ : { }`

   El **[!UICONTROL Contraseña actual]** El campo se rellena previamente de forma intencionada y se oculta de la interacción.

   Si es necesario, puede revisar la ortografía de una contraseña que haya escrito o vuelto a escribir seleccionando el icono ojo de contraseña para revelar la contraseña. Vuelva a seleccionar el icono para ocultar la contraseña.

1. En el **[!UICONTROL Repetir contraseña]** , vuelva a escribir la nueva contraseña y, a continuación, seleccione **[!UICONTROL Listo]**.

   La nueva contraseña se guarda al seleccionar **[!UICONTROL Guardar]** en la esquina superior derecha de la **[!UICONTROL Crear configuración de Dynamic Media]** página.

   Si ha seleccionado **[!UICONTROL Cancelar]** en el **[!UICONTROL Cambiar contraseña]** , aún debe introducir una nueva contraseña al guardar la configuración de Dynamic Media creada.

   Consulte también [Cambiar la contraseña a Dynamic Media](#change-dm-password).

1. Cuando la conexión se realiza correctamente, puede establecer lo siguiente:

   | Propiedad | Descripción |
   |---|---|
   | Compañía | El nombre de la cuenta de Dynamic Media.<br>**Importante**: solo se admite una configuración de Dynamic Media en Cloud Service en una instancia de Experience Manager; no agregue más de una configuración. Hay varias configuraciones de Dynamic Media en una instancia de Experience Manager _no_ compatible o recomendado por el Adobe.<!-- CQDOC-19579 and CQDOC-19612 --><br>Consulte también [Configuración de una cuenta de alias de empresa de Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md). |
   | Ruta de carpeta raíz de la empresa | Ruta de la carpeta raíz de su empresa. |
   | Publicación de recursos | Puede elegir entre las tres opciones siguientes:<br>**[!UICONTROL Inmediata ]**: Cuando se cargan recursos, el sistema los ingiere y proporciona la URL o la incrustación al instante. No es necesaria la intervención del usuario para publicar los recursos.<br>**[!UICONTROL En la activación]** : primero debe publicar explícitamente el recurso antes de proporcionar un vínculo URL/incrustado.<br>**[!UICONTROL Publicación selectiva ]**- Los recursos se publican automáticamente solo para previsualización segura. También se pueden publicar explícitamente en Experience Manager as a Cloud Service sin publicar en DMS7 para envío de dominio público. En el futuro, esta opción pretende publicar recursos en Experience Manager as a Cloud Service y publicarlos en Dynamic Media, mutuamente excluyentes entre sí. Es decir, puede publicar recursos en DMS7 para poder utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en el Experience Manager as a Cloud Service para la previsualización; esos mismos recursos no se publican en DMS7 para su envío en el dominio público. |
   | Servidor de previsualización segura | Permite especificar la ruta de URL del servidor de previsualización de representaciones seguras. Es decir, una vez generadas las representaciones, Experience Manager as a Cloud Service puede acceder y previsualizar de forma segura las representaciones remotas de Dynamic Media (no se envían binarios de vuelta a la instancia as a Cloud Service de Experience Manager).<br>A menos que tenga una disposición especial para utilizar el servidor de su propia compañía o un servidor especial, Adobe recomienda dejar esta configuración como se ha especificado. |
   | Sincronizar todo el contenido | Seleccionado de forma predeterminada. Anule la selección de esta opción si desea incluir o excluir recursos de forma selectiva de la sincronización con Dynamic Media. Al anular la selección de esta opción, puede elegir entre los dos modos de sincronización de Dynamic Media siguientes:<br>**[!UICONTROL Modo de sincronización de Dynamic Media]**<br>**[!UICONTROL Habilitar de forma predeterminada ]**: la configuración se aplica a todas las carpetas de forma predeterminada a menos que marque una carpeta específicamente para la exclusión. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Deshabilitado de forma predeterminada]** : la configuración no se aplicará a ninguna carpeta hasta que marque explícitamente una carpeta seleccionada para sincronizar con Dynamic Media.<br>Para marcar una carpeta seleccionada para sincronizar con Dynamic Media, seleccione una carpeta de recursos y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**. En el **[!UICONTROL Detalles]** , en la pestaña **[!UICONTROL Modo de sincronización de Dynamic Media]** , elija una de las tres opciones siguientes. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**. _Recuerde: estas tres opciones no están disponibles si ha seleccionado **Sincronizar todo el contenido**antes._ Consulte también [Trabajo con Publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Heredado ]**- No hay ningún valor de sincronización explícito en la carpeta. En su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o el modo predeterminado en la configuración de la nube. Estado detallado de los programas heredados mediante información sobre herramientas.<br>**[!UICONTROL Habilitar para subcarpetas]** : incluya todo en este subárbol para sincronizarlo con Dynamic Media. La configuración específica de la carpeta anula el modo predeterminado en la configuración de la nube.<br>**[!UICONTROL Deshabilitado para subcarpetas ]**- Excluya todo el contenido de este subárbol de la sincronización con Dynamic Media. |

   >[!NOTE]
   >
   >No se admite el control de versiones en Dynamic Media. Además, la activación retrasada solo se aplica si **[!UICONTROL Publicar recursos]** en la página Editar configuración de Dynamic Media se establece como **[!UICONTROL Tras la activación]**. Y, a continuación, solo hasta la primera vez que se activa el recurso.
   >
   >
   >Una vez activado un recurso, las actualizaciones se publican inmediatamente en la entrega de S7.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Seleccione **[!UICONTROL Guardar]**. Se guardarán la nueva contraseña y configuración de Dynamic Media. Si ha seleccionado **[!UICONTROL Cancelar]** en su lugar, no se actualiza la contraseña.
1. En el **[!UICONTROL Configuración de Dynamic Media]** , seleccione **[!UICONTROL OK]** para comenzar la configuración.

   >[!IMPORTANT]
   >
   >Cuando la nueva configuración de Dynamic Media finalice, recibirá una notificación de estado en la bandeja de entrada del Experience Manager as a Cloud Service.
   >
   >Esta notificación de la bandeja de entrada le informa si la configuración se ha realizado correctamente o no.
   > Consulte [Solución de problemas de una nueva configuración de Dynamic Media](#troubleshoot-dm-config) y [Su bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) para obtener más información.

1. Para previsualizar de forma segura el contenido de Dynamic Media antes de que se publique, Experience Manager as a Cloud Service utiliza la validación basada en tokens y, por lo tanto, Experience Manager Author previsualiza el contenido de Dynamic Media de forma predeterminada. Sin embargo, puede *lista de permitidos* Obtenga más direcciones IP para proporcionar a los usuarios acceso para previsualizar el contenido de forma segura. Para configurar esta acción en Experience Manager as a Cloud Service, consulte [Configuración del programa de instalación de publicación de Dynamic Media para el servidor de imágenes: pestaña Seguridad](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

Ya ha terminado la configuración básica; está listo para usar Dynamic Media.

Si desea personalizar aún más la configuración, como habilitar los permisos ACL (Lista de control de acceso), puede completar opcionalmente cualquiera de las tareas en [Configuración avanzada en Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Solución de problemas de una nueva configuración de Dynamic Media {#troubleshoot-dm-config}

Cuando una nueva configuración de Dynamic Media finalice, recibirá una notificación de estado en la bandeja de entrada del Experience Manager as a Cloud Service. Esta notificación le informa si la configuración se ha realizado correctamente o no, tal como se ve en las siguientes imágenes respectivas de la bandeja de entrada.

![Bandeja de entrada de Experience Manager correcta](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Error de bandeja de entrada Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Consulte también [Su bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

**Para solucionar problemas de una nueva configuración de Dynamic Media:**

1. Cerca de la esquina superior derecha de la página as a Cloud Service del Experience Manager, seleccione el icono de campana y, a continuación, seleccione **[!UICONTROL Ver todo]**.
1. En la página Bandeja de entrada, seleccione la notificación de éxito para leer una descripción general del estado y los registros de la configuración.

   Si la configuración falla, seleccione la notificación de error similar a la siguiente captura de pantalla.

   ![Error de configuración de Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. En el **[!UICONTROL DMSETUP]** , revise los detalles de configuración que describen el error. En particular, tome nota de cualquier mensaje de error o código de error. Póngase en contacto con Asistencia al cliente de Adobe con esta información.

   ![Página de configuración de Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Cambiar la contraseña a Dynamic Media {#change-dm-password}

La caducidad de la contraseña en Dynamic Media se establece en 100 años a partir de la fecha actual del sistema.

La contraseña debe contener al menos una de las siguientes opciones:

* Letra mayúscula
* Letra minúscula
* Número
* Carácter especial: `# $ & . - _ : { }`

Si es necesario, puede revisar la ortografía de una contraseña que haya escrito o vuelto a escribir seleccionando el icono ojo de contraseña para revelar la contraseña. Vuelva a seleccionar el icono para ocultar la contraseña.

La contraseña modificada se guarda al seleccionar **[!UICONTROL Guardar]** en la esquina superior derecha de la **[!UICONTROL Editar configuración de Dynamic Media]** página.

1. En Experience Manager as a Cloud Service, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. A la izquierda de la consola, seleccione el icono Herramientas y, a continuación, vaya a **[!UICONTROL Cloud Service > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]**. No seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**. A continuación, seleccione **[!UICONTROL Editar]**.
1. En el **[!UICONTROL Editar configuración de Dynamic Media]** , directamente debajo de la página **[!UICONTROL Contraseña]** , seleccione **[!UICONTROL Cambiar contraseña]**.
1. En el **[!UICONTROL Cambiar contraseña]** , haga lo siguiente:

   * En el **[!UICONTROL Nueva contraseña]** , introduzca una nueva contraseña.

     El **[!UICONTROL Contraseña actual]** El campo se rellena previamente de forma intencionada y se oculta de la interacción.

   * En el **[!UICONTROL Repetir contraseña]** , vuelva a escribir la nueva contraseña y, a continuación, seleccione **[!UICONTROL Listo]**.

1. En la esquina superior derecha de la **[!UICONTROL Editar configuración de Dynamic Media]** página, seleccione **[!UICONTROL Guardar]**, luego seleccione **[!UICONTROL OK]**.

## (Opcional) Configuración avanzada en Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Para personalizar aún más la configuración de Dynamic Media o optimizar su rendimiento, puede completar una o más de las siguientes acciones _opcional_ tareas:

* [(Opcional) Habilite los permisos de ACL en Dynamic Media](#optional-enable-acl)
* [(Opcional) Configuración de los ajustes de Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Opcional) Ajuste el rendimiento de Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Opcional) Habilite los permisos de la Lista de control de acceso en Dynamic Media {#optional-enable-acl}

Cuando ejecuta Dynamic Media AEM en el servidor de correo electrónico, actualmente se reenvía a través de la `/is/image` Solicitudes para obtener una vista previa segura del servicio de imágenes sin comprobar los permisos de ACL (Access Control List) en PlatformServerServlet. Sin embargo, puede _habilitar_ Permisos ACL. Al hacerlo, reenvía el `/is/image` solicitudes. Si un usuario no tiene autorización para acceder al recurso, se muestra el error 403 - Prohibido.

**Para habilitar los permisos de ACL en Dynamic Media:**

1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Se abre una nueva pestaña del explorador a la **[!UICONTROL Configuración de la consola web Adobe Experience Manager]** página.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hasta el nombre _Adobe CQ Scene7 PlatformServer_.

1. A la derecha del nombre, seleccione el icono de lápiz (**[!UICONTROL Editar los valores de configuración]**).

1. En el **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** , active la casilla de verificación de las dos opciones de configuración siguientes:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` : cuando está habilitada, esta configuración almacena en caché los resultados de los permisos durante dos minutos (predeterminado) para guardarlos.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` : cuando se habilita, esta configuración valida el acceso de un usuario mientras previsualiza los recursos mediante Dynamic Media Image Server.

   ![Habilitar la configuración de la Lista de control de acceso en Dynamic Media - Modo Scene7](/help/assets/dynamic-media/assets/acl.png)

1. Cerca de la esquina inferior derecha de la página, seleccione **[!UICONTROL Guardar]**.

### (Opcional) Configuración de los ajustes de Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilice la interfaz de usuario de Dynamic Media Classic para cambiar la configuración de Dynamic Media.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Las tareas de instalación y configuración incluyen las siguientes:

* [Configuración del programa de instalación de Dynamic Media Publish para el servidor de imágenes](#publishing-setup-for-image-server)
* [Configuración general de Dynamic Media](#configuring-application-general-settings)
* [Configurar la administración de color](#configuring-color-management)
* [Editar tipos MIME para formatos compatibles](#editing-mime-types-for-supported-formats)
* [Adición de tipos MIME para formatos no compatibles](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configuración del programa de instalación de Dynamic Media Publish para el servidor de imágenes {#publishing-setup-for-image-server}

La página Configuración de publicación de Dynamic Media establece la configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o las aplicaciones.

Consulte [Configuración del programa de instalación de Dynamic Media Publish para el servidor de imágenes](/help/assets/dynamic-media/dm-publish-settings.md).

#### Configuración general de Dynamic Media {#configuring-application-general-settings}

Configuración de Dynamic Media **[!UICONTROL Nombre del servidor de publicación]** La URL y **[!UICONTROL Servidor de origen]** URL. También puede especificar **[!UICONTROL Cargar en la aplicación]** configuración y **[!UICONTROL Opciones de carga predeterminadas]** todo en función de su caso de uso particular.

Consulte [Configuración general de Dynamic Media](/help/assets/dynamic-media/dm-general-settings.md).

#### Configurar la administración de color {#configuring-color-management}

La administración de color de Dynamic Media le permite corregir el color de los recursos. Con la corrección de color, los recursos ingeridos conservan su espacio de color (RGB, CMYK, gris) y su perfil de color incrustado. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color de destino mediante la salida CMYK, RGB o Gris.

Consulte [Configurar ajustes preestablecidos de imagen](/help/assets/dynamic-media/managing-image-presets.md).

Para configurar las propiedades de color predeterminadas para habilitar la corrección de color al solicitar imágenes:

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), e inicie sesión en su cuenta con las credenciales proporcionadas durante el aprovisionamiento.
1. Ir a **[!UICONTROL Configuración > Configuración de aplicación]**.
1. Expanda el área **[!UICONTROL Ajustes de publicación]** y seleccione **[!UICONTROL Servidor de imágenes]**. Configure **[!UICONTROL Publicar contexto]** en **[!UICONTROL Servicio de imágenes]** cuando establezca los valores predeterminados para las instancias de publicación.
1. Desplácese hasta la propiedad que debe cambiar; por ejemplo, una propiedad en **[!UICONTROL Atributos de gestión de color]** área.
Se pueden definir las siguientes propiedades de corrección de color:

   | Propiedad | Descripción |
   |---|---|
   | Espacio de color predeterminado CMYK | Nombre del perfil de color CMYK predeterminado. |
   | Espacio de color predeterminado de escala de grises | Nombre del perfil de color gris predeterminado. |
   | Espacio de color predeterminado del RGB | Nombre del perfil de color de RGB predeterminado. |
   | Interpretación de conversión de color | Especifica la intención de procesamiento. Los valores aceptables son: **[!UICONTROL perceptual]**, **[!UICONTROL colométrico relativo]**, **[!UICONTROL saturación]**, **[!UICONTROL colométrico absoluto]**. Adobe recomienda **[!UICONTROL relativo]** como valor predeterminado. |

1. Seleccione **[!UICONTROL Guardar]**.

Por ejemplo, puede establecer el **[!UICONTROL espacio de color predeterminado RGB]** en *sRGB* y el **[!UICONTROL espacio de color predeterminado CMYK]** en *WebCoated*.

Al hacerlo, se haría lo siguiente:

* Activa la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes de RGB que no tienen un perfil de color están en la *sRGB* espacio de color.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *WebCoated* espacio de color.
* Representaciones dinámicas que devuelven resultados de RGB, devuélvalos en el *sRGB* espacio de color.
* Representaciones dinámicas que devuelven salida CMYK, devuélvala en el *WebCoated* espacio de color.

#### Editar tipos MIME para formatos compatibles {#editing-mime-types-for-supported-formats}

Puede definir qué tipos de recursos procesa Dynamic Media y personalizar los parámetros avanzados de procesamiento de recursos. Por ejemplo, puede especificar parámetros de procesamiento de recursos para hacer lo siguiente:

* Convertir un Adobe PDF en un recurso de catálogo electrónico.
* Convierta un documento de Adobe Photoshop (.PSD) en un recurso de plantilla de banner para personalización.
* Rasterizar un archivo Adobe Illustrator (.AI) o un archivo de PostScript® encapsulado de Adobe Photoshop (.EPS).
* [Perfiles de vídeo](/help/assets/dynamic-media/video-profiles.md) y [Perfiles de imagen](/help/assets/dynamic-media/image-profiles.md) se puede utilizar para definir el procesamiento de vídeos e imágenes, respectivamente.

Consulte [Cargar recursos](/help/assets/add-assets.md).

**Para editar tipos MIME para formatos compatibles:**

1. Inicie sesión en el Experience Manager as a Cloud Service como administrador del producto.
1. En Experience Manager as a Cloud Service , seleccione el logotipo de Experience Manager as a Cloud Service para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL General > CRXDE Lite]**.

   Si no tiene acceso a CRXDE Lite, consulte [Uso del CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. En el carril izquierdo, vaya a lo siguiente:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. En la carpeta mimeTypes, seleccione un tipo MIME.
1. En el lado derecho de la página del CRXDE Lite, en la parte inferior:

   * Pulse dos veces el botón **[!UICONTROL activado]** field. De forma predeterminada, todos los tipos MIME de recursos están habilitados (establecidos en **[!UICONTROL true]**), lo que significa que los recursos se sincronizan con Dynamic Media para su procesamiento. Si desea excluir el procesamiento de este tipo MIME de recurso, cambie este ajuste a **[!UICONTROL false]**.

   * Pulsar dos veces **[!UICONTROL jobParam]** para abrir su campo de texto asociado. Consulte [Tipos MIME admitidos](/help/assets/file-format-support.md) para obtener una lista de valores de parámetros de procesamiento permitidos que puede utilizar para un tipo MIME determinado.

1. Realice una de las siguientes acciones:
   * Repita los pasos del 3 al 4 para editar más tipos MIME.
   * En la barra de menús de la página del CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

1. En la esquina superior izquierda de la página, seleccione **[!UICONTROL CRXDE Lite]** para volver a Experience Manager as a Cloud Service.

#### Adición de tipos MIME para formatos no compatibles {#adding-mime-types-for-unsupported-formats}

Puede agregar tipos MIME personalizados para formatos no compatibles en Experience Manager Assets. Para asegurarse de que el Experience Manager no elimina ningún nodo nuevo que agregue al CRXDE Lite, mueva el tipo MIME antes de que `image_`. Además, asegúrese de que su valor enabled está establecido en **[!UICONTROL false]**.

**Para agregar tipos MIME para formatos no compatibles:**

1. Inicie sesión en el Experience Manager as a Cloud Service como administrador del producto.
1. En Experience Manager as a Cloud Service, vaya a **[!UICONTROL Herramientas > Operaciones > Consola web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Se abre una nueva pestaña del explorador a la **[!UICONTROL Configuración de la consola web Adobe Experience Manager]** página.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hacia abajo hasta el nombre *Servicio MIME de tipo de recurso de Adobe CQ Scene7* como se muestra en la siguiente captura de pantalla. A la derecha del nombre, pulse la opción **[!UICONTROL Editar los valores de configuración]** (icono de lápiz).

   ![Editar los valores de configuración](assets/2019-08-02_16-44-56.png)

1. En el **Servicio MIME de tipo de recurso de Adobe CQ Scene7** , seleccione cualquier icono del signo más &lt;+>. La ubicación en la tabla donde selecciona el signo más para agregar el nuevo tipo MIME es trivial.

   ![Servicio de tipo MIME de recursos de Adobe CQ Scene7](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` en el campo de texto vacío que acaba de añadir.

   El `DWG=image/vnd.dwg` El tipo MIME solo es para fines de ejemplo. El tipo MIME que agregue aquí puede ser cualquier otro formato no compatible.

   ![Adición de tipo MIME DWG](assets/2019-08-02_16-36-36.png)

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   En este punto, puede cerrar la pestaña del explorador que tiene abierta la página Configuración de la consola web de Adobe Experience Manager.

1. Vuelva a la pestaña del explorador que tenga la consola as a Cloud Service del Experience Manager abierta.
1. En Experience Manager as a Cloud Service, vaya a **[!UICONTROL Herramientas > General > CRXDE Lite]**.

   Si no tiene acceso a CRXDE Lite, consulte [Uso del CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Herramientas > General > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. En el carril izquierdo, vaya a lo siguiente:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arrastre el tipo MIME `image_vnd.dwg` y suéltelo directamente encima `image_` en el árbol como se ve en la siguiente captura de pantalla.

   ![Edición de un archivo DWG en CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Con el tipo MIME `image_vnd.dwg` aún seleccionado, desde el **[!UICONTROL Propiedades]** , en la pestaña **[!UICONTROL activado]** fila, debajo de **[!UICONTROL Valor]** en el encabezado de la columna, pulse dos veces el valor. El **[!UICONTROL Valor]** se abre la lista desplegable.
1. Tipo `false` en el campo (o seleccione **[!UICONTROL false]** de la lista desplegable).

   ![Edición de tipos MIME en CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. Cerca de la esquina superior izquierda de la página de CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

### (Opcional) Ajuste el rendimiento de Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para conservar Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> con un funcionamiento sin problemas, Adobe recomienda las siguientes sugerencias de ajuste de rendimiento/escalabilidad de sincronización:

* [Actualizar los parámetros de trabajo predefinidos para procesar diferentes formatos de archivo](#update-job-para).
* [Actualizar los hilos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo)](#update-granite-workflow-queue-worker-threads-video)
* [Actualice los hilos de trabajo predefinidos de la cola de flujo de trabajo transitorio de Granite (imágenes y recursos que no sean de vídeo)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Actualización del número máximo de conexiones de carga al servidor de Dynamic Media Classic (Scene7)](#update-max-s7-upload-connections).

#### Actualizar los parámetros de trabajo predefinidos para procesar diferentes formatos de archivo {#update-job-para}

Puede ajustar los parámetros de trabajo para un procesamiento más rápido al cargar archivos. Por ejemplo, si carga archivos de PSD, pero no desea procesarlos como plantillas, puede establecer la extracción de capas en false (desactivado). En este caso, el parámetro de trabajo optimizado aparece de la siguiente manera: `process=None&createTemplate=false`.

Si desea activar la creación de plantillas, utilice los siguientes parámetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe recomienda utilizar los siguientes parámetros de trabajo &quot;optimizados&quot; para archivos de PDF, PostScript® y PSD:

| Tipo de archivo | Parámetros de trabajo recomendados |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para actualizar cualquiera de estos parámetros, consulte [Edición de tipos MIME para formatos compatibles](#editing-mime-types-for-supported-formats).

Consulte también [Adición de tipos MIME para formatos no compatibles](#adding-mime-types-for-unsupported-formats).

#### Actualizar los hilos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo) {#update-granite-workflow-queue-worker-threads-video}

La cola de flujo de trabajo de Granite se utiliza para flujos de trabajo no transitorios. En Dynamic Media, se utilizaba para procesar vídeo con **[!UICONTROL Codificar vídeo Dynamic Media]** flujo de trabajo.

>[!NOTE]
>
>Debe haber iniciado sesión en Experience Manager as a Cloud Service como administrador de productos para completar esta tarea.

Si no tiene acceso a OSGi, consulte [Configuración de OSGi](/help/implementing/developing/components/overview.md#osgi-configuration).

**Para actualizar los hilos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo):**

1. Vaya a `https://<server>/system/console/configMgr` y buscar **Cola: Cola de flujo de trabajo de Granite**.

   >[!NOTE]
   >
   >Es necesario realizar una búsqueda de texto en lugar de una dirección URL directa porque el PID de OSGi se genera dinámicamente.

1. En el **[!UICONTROL Máximo de trabajos paralelos]** , cambie el número al valor deseado.

   De forma predeterminada, el número máximo de trabajos paralelos depende del número de núcleos de CPU disponibles. Por ejemplo, en un servidor de 4 núcleos, asigna dos subprocesos de trabajo. (Un valor entre 0,0 y 1,0 se basa en la relación, o cualquier número mayor que uno asigna el número de subprocesos de trabajo.)

   Para la mayoría de los casos de uso, la configuración predeterminada de 0,5 es suficiente.

   ![Configuración de una cola de procesamiento de trabajos](assets/chlimage_1-1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualizar los hilos de trabajo predefinidos de la cola de flujo de trabajo transitorio de Granite {#update-granite-transient-workflow-queue-worker-threads-images}

La cola de flujo de trabajo de Granite Transit se utiliza para **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo. En Dynamic Media, se utiliza para la ingesta y el procesamiento de recursos de imagen y sin vídeo.

>[!NOTE]
>
>Debe haber iniciado sesión en Experience Manager as a Cloud Service como administrador de productos para completar esta tarea.

**Para actualizar los hilos de trabajo de cola de flujo de trabajo transitorio de Granite predefinidos:**

1. Vaya a **Configuración de la consola web Adobe Experience Manager** en `http://<host>:<port>/system/console/configMgr`
1. Buscar por **Cola: Cola de flujo de trabajo transitorio de Granite**.

   >[!NOTE]
   >
   >Es necesario realizar una búsqueda de texto en lugar de una dirección URL directa porque el PID de OSGi se genera dinámicamente.

1. En el **[!UICONTROL Máximo de trabajos paralelos]** , cambie el número al valor deseado.

   Puede aumentar **[!UICONTROL Máximo de trabajos paralelos]** para admitir adecuadamente una carga pesada de archivos en Dynamic Media. El valor exacto depende de la capacidad del hardware. En determinados casos, como una migración inicial o una carga masiva única, puede utilizar un valor elevado. Sin embargo, tenga en cuenta que el uso de un valor grande (como dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualización del número máximo de conexiones de carga al servidor de Dynamic Media Classic (Scene7) {#update-max-s7-upload-connections}

La configuración de conexión de carga de Dynamic Media Classic (Scene7) sincroniza los recursos del Experience Manager con los servidores de Dynamic Media Classic.

>[!NOTE]
>
>Debe haber iniciado sesión en Experience Manager as a Cloud Service como administrador de productos para completar esta tarea.

**Para actualizar el número máximo de conexiones de carga al servidor de Dynamic Media Classic (Scene7):**

1. Navegue hasta `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. En el **[!UICONTROL Número de conexiones]** o el campo **[!UICONTROL Tiempo de espera del trabajo activo]** , o ambos, cambie el número como desee.

   El **[!UICONTROL Número de conexiones]** Esta opción controla la cantidad máxima de conexiones HTTP permitidas para la carga de Experience Manager a Dynamic Media. Normalmente, el valor predefinido de diez conexiones es suficiente.

   El **[!UICONTROL Tiempo de espera del trabajo activo]** determina el tiempo de espera para que los recursos de Dynamic Media cargados se publiquen en el servidor de entrega. De forma predeterminada, este valor es 2100 segundos o 35 minutos.

   Para la mayoría de los casos de uso, el ajuste 2100 es suficiente.

   ![Servicio de carga de Adobe Scene7](assets/chlimage_1-2.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
