---
title: Configuración del Cloud Service de Dynamic Media
description: Obtenga información sobre cómo configurar Dynamic Media en Adobe Experience Manager as a Cloud Service.
contentOwner: Rick Brough
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '3795'
ht-degree: 3%

---

# Acerca de la configuración del Cloud Service de Dynamic Media {#configuring-dynamic-media}

Si utiliza Adobe Experience Manager para diferentes entornos, como desarrollo, ensayo y producción en directo, configure los Cloud Services de Dynamic Media para cada uno de esos entornos.

Consulte también [Configurar una cuenta de alias de empresa de Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md)

## Diagrama de arquitectura de Dynamic Media {#architecture-diagram-of-dynamic-media}

En el diagrama de arquitectura siguiente se describe cómo funciona Dynamic Media.

Con la nueva arquitectura, Experience Manager es responsable de los recursos de origen principales y se sincroniza con Dynamic Media para el procesamiento y la publicación de recursos:

1. Cuando el recurso de origen principal se carga en Adobe Experience Manager as a Cloud Service, se replica en Dynamic Media. En este punto, Dynamic Media gestiona todo el procesamiento de recursos y la generación de representaciones, como la codificación de vídeo y las variantes dinámicas de una imagen.
1. Una vez generadas las representaciones, el Experience Manager as a Cloud Service puede acceder y previsualizar de forma segura las representaciones remotas de Dynamic Media (no se envían binarios a la instancia as a Cloud Service del Experience Manager).
1. Una vez que el contenido está listo para publicarse y aprobarse, se déclencheur al servicio de Dynamic Media para enviar contenido a los servidores de entrega y almacenar en caché el contenido en la CDN (red de entrega de contenido).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>La siguiente lista de funciones requiere que utilice la CDN predeterminada incluida con Adobe Experience Manager - Dynamic Media. Ninguna otra CDN personalizada es compatible con estas funciones.
>
>* [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md)
>* [Invalidación de caché](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [Protección de Hotlink](/help/assets/dynamic-media/hotlink-protection.md)
>* [Entrega de contenido HTTP/2](/help/assets/dynamic-media/http2faq.md)
>* Redireccionamiento de URL a nivel de CDN
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

## Crear una configuración de Dynamic Media en Cloud Services {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. En as a Cloud Service de Experience Manager, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. En la parte izquierda de la consola, seleccione el icono Herramientas y vaya a **[!UICONTROL Cloud Services > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]** (no seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**). A continuación, seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración de Dynamic Media]** , introduzca el título, la dirección de correo electrónico de la cuenta de Dynamic Media y la contraseña del administrador de la empresa de la cuenta de Dynamic Media y, a continuación, seleccione su región. Esta información se proporciona por Adobe en el correo electrónico de aprovisionamiento. Póngase en contacto con el servicio de atención al cliente de Adobe si no ha recibido este correo electrónico.
1. Select **[!UICONTROL Conectarse a Dynamic Media]**.
1. En el **[!UICONTROL Cambiar contraseña]** en el **[!UICONTROL Nueva contraseña]** , introduzca una nueva contraseña que consta de 8-25 caracteres. La contraseña debe contener al menos una de las siguientes opciones:

   * Letra mayúscula
   * Letra minúscula
   * Número
   * Carácter especial: `# $ & . - _ : { }`

   La variable **[!UICONTROL Contraseña actual]** se rellena intencionalmente y se oculta de la interacción.

   Si es necesario, puede revisar la ortografía de una contraseña que ha escrito o que ha vuelto a escribir seleccionando el icono de ojo de contraseña para mostrar la contraseña. Vuelva a seleccionar el icono para ocultar la contraseña.

1. En el **[!UICONTROL Repetir contraseña]** , vuelva a escribir la nueva contraseña y, a continuación, seleccione **[!UICONTROL Listo]**.

   La nueva contraseña se guarda al seleccionar **[!UICONTROL Guardar]** en la esquina superior derecha del **[!UICONTROL Crear configuración de Dynamic Media]** página.

   Si ha seleccionado **[!UICONTROL Cancelar]** en el **[!UICONTROL Cambiar contraseña]** , debe introducir una contraseña nueva cuando guarde la configuración de Dynamic Media recién creada.

   Consulte también [Cambiar la contraseña a Dynamic Media](#change-dm-password).

1. Cuando la conexión se realiza correctamente, puede establecer lo siguiente:

   | Propiedad | Descripción |
   |---|---|
   | Compañía | Nombre de la cuenta de Dynamic Media.<br>**Importante**: Solo se admite una configuración de Dynamic Media en Cloud Services en una instancia de Experience Manager; no agregue más de una configuración. Varias configuraciones de Dynamic Media en una instancia de Experience Manager son _not_ compatible o recomendado por Adobe.<!-- CQDOC-19579 and CQDOC-19612 --><br>Consulte también [Configurar una cuenta de alias de empresa de Dynamic Media](/help/assets/dynamic-media/dm-alias-account.md). |
   | Ruta de carpeta raíz de la empresa | Ruta de la carpeta raíz de su empresa. |
   | Publicación de recursos | Puede elegir entre las tres opciones siguientes:<br>**[!UICONTROL Inmediatamente ]**: Cuando se cargan recursos, el sistema los incorpora y proporciona la URL o la Incrustar instantáneamente. No es necesario que el usuario intervenga para publicar recursos.<br>**[!UICONTROL Al activar]** : Debe publicar el recurso explícitamente primero antes de proporcionar un vínculo de URL/incrustación.<br>**[!UICONTROL Publicación selectiva ]**- Los recursos se publican automáticamente solo para vista previa segura. También pueden publicarse explícitamente en el Experience Manager as a Cloud Service sin publicarse en DMS7 para su envío en el dominio público. En el futuro, esta opción pretende publicar recursos en un Experience Manager as a Cloud Service y publicar recursos en Dynamic Media, mutuamente excluyentes entre sí. Es decir, puede publicar recursos en DMS7 para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en un Experience Manager as a Cloud Service para la vista previa; esos mismos recursos no se publican en DMS7 para su envío en el dominio público. |
   | Servidor de previsualización segura | Permite especificar la ruta URL del servidor de vista previa de representaciones seguras. Es decir, una vez generadas las representaciones, el Experience Manager as a Cloud Service puede acceder y previsualizar de forma segura las representaciones remotas de Dynamic Media (no se devuelven binarios a la instancia as a Cloud Service del Experience Manager).<br>A menos que tenga una disposición especial para utilizar el servidor de su propia empresa o un servidor especial, Adobe recomienda que deje esta configuración como se ha especificado. |
   | Sincronizar todo el contenido | Seleccionado de forma predeterminada. Anule la selección de esta opción si desea incluir o excluir selectivamente recursos de la sincronización con Dynamic Media. Al anular la selección de esta opción, puede elegir entre los dos modos de sincronización de Dynamic Media siguientes:<br>**[!UICONTROL Modo de sincronización de Dynamic Media]**<br>**[!UICONTROL Habilitar de forma predeterminada ]**- La configuración se aplica a todas las carpetas de forma predeterminada, a menos que marque una carpeta específicamente para la exclusión. <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL Deshabilitado de forma predeterminada]** - La configuración no se aplica a ninguna carpeta hasta que marque explícitamente una carpeta seleccionada para sincronizar con Dynamic Media.<br>Para marcar una carpeta seleccionada para sincronizar con Dynamic Media, seleccione una carpeta de recursos y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**. En el **[!UICONTROL Detalles]** en la **[!UICONTROL Modo de sincronización de Dynamic Media]** , elija entre las tres opciones siguientes. Cuando haya terminado, seleccione **[!UICONTROL Guardar]**. _Recuerde: estas tres opciones no están disponibles si ha seleccionado **Sincronizar todo el contenido**más temprano._ Consulte también [Trabajar con publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL Heredado ]**- No hay ningún valor de sincronización explícito en la carpeta. En su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o del modo predeterminado en la configuración de la nube. El estado detallado de heredado se muestra mediante una información del objeto.<br>**[!UICONTROL Habilitar para subcarpetas]** - Incluya todo en este subárbol para sincronizar con Dynamic Media. La configuración específica de la carpeta anula el modo predeterminado en la configuración de la nube.<br>**[!UICONTROL Deshabilitado para subcarpetas ]**- Excluya todo lo que se encuentra en este subárbol de la sincronización con Dynamic Media. |

   >[!NOTE]
   >
   >No se admite el control de versiones en Dynamic Media. Además, la activación retrasada solo se aplica si **[!UICONTROL Publicar recursos]** en la página Editar configuración de Dynamic Media está configurada como **[!UICONTROL Tras la activación]**. Y, a continuación, solo hasta la primera vez que se activa el recurso.
   >
   >
   >Una vez activado un recurso, las actualizaciones se publican inmediatamente en S7 Delivery.

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. Seleccione **[!UICONTROL Guardar]**. Se guarda la nueva contraseña y configuración de Dynamic Media. Si ha seleccionado **[!UICONTROL Cancelar]** en su lugar, no se actualiza la contraseña.
1. En el **[!UICONTROL Configuración de Dynamic Media]** cuadro de diálogo, seleccione **[!UICONTROL OK]** para iniciar la configuración.

   >[!IMPORTANT]
   >
   >Cuando la nueva configuración de Dynamic Media finaliza su configuración, recibe una notificación de estado en la bandeja de entrada del Experience Manager as a Cloud Service.
   >
   >Esta notificación de la bandeja de entrada le informa de si la configuración se ha realizado correctamente o no.
   > Consulte [Resolución de problemas de una nueva configuración de Dynamic Media](#troubleshoot-dm-config) y [Su bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) para obtener más información.

1. Para previsualizar de forma segura el contenido de Dynamic Media antes de publicarlo, el Experience Manager as a Cloud Service utiliza la validación basada en token y, por lo tanto, el Experience Manager Autor obtiene una vista previa del contenido de Dynamic Media de forma predeterminada. Sin embargo, puede *lista de permitidos* más direcciones IP para proporcionar a los usuarios acceso a la vista previa del contenido de forma segura. Para configurar esta acción en Experience Manager as a Cloud Service, consulte [Configuración de Dynamic Media Publish Setup para Image Server: ficha Seguridad](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

Ya ha finalizado con la configuración básica; está listo para usar Dynamic Media.

Si desea personalizar aún más la configuración, como habilitar los permisos de ACL (Access Control List), puede completar opcionalmente cualquiera de las tareas en [Configuración avanzada en Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### Resolución de problemas de una nueva configuración de Dynamic Media {#troubleshoot-dm-config}

Cuando finaliza la configuración de una nueva Dynamic Media, recibe una notificación de estado en la bandeja de entrada del Experience Manager as a Cloud Service. Esta notificación le informa de si la configuración se ha realizado correctamente o no, como se ve en las siguientes imágenes respectivas de la Bandeja de entrada.

![Experience Manager Bandeja de entrada correcta](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Fallo en la bandeja de entrada del Experience Manager](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

Consulte también [Su bandeja de entrada](/help/sites-cloud/authoring/getting-started/inbox.md).

**Para solucionar problemas de una nueva configuración de Dynamic Media:**

1. Cerca de la esquina superior derecha de la página as a Cloud Service del Experience Manager, seleccione el icono de campana y, a continuación, seleccione **[!UICONTROL Ver todo]**.
1. En la página Bandeja de entrada, seleccione la notificación de éxito para leer una descripción general del estado y los registros de la configuración.

   Si la configuración falla, seleccione la notificación de error similar a la siguiente captura de pantalla.

   ![Error en la configuración de Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. En el **[!UICONTROL DMSETUP]** revise los detalles de configuración que describen el error. En particular, tome nota de cualquier mensaje de error o código de error. Póngase en contacto con el servicio de asistencia al cliente de Adobe para obtener esta información.

   ![Página de configuración de Dynamic Media](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### Cambiar la contraseña a Dynamic Media {#change-dm-password}

La caducidad de la contraseña en Dynamic Media se establece en 100 años a partir de la fecha actual del sistema.

La contraseña debe contener al menos una de las siguientes opciones:

* Letra mayúscula
* Letra minúscula
* Número
* Carácter especial: `# $ & . - _ : { }`

Si es necesario, puede revisar la ortografía de una contraseña que ha escrito o que ha vuelto a escribir seleccionando el icono de ojo de contraseña para mostrar la contraseña. Vuelva a seleccionar el icono para ocultar la contraseña.

La contraseña modificada se guarda al seleccionar **[!UICONTROL Guardar]** en la esquina superior derecha del **[!UICONTROL Editar configuración de Dynamic Media]** página.

1. En as a Cloud Service de Experience Manager, seleccione el logotipo as a Cloud Service de Experience Manager para acceder a la consola de navegación global.
1. En la parte izquierda de la consola, seleccione el icono Herramientas y vaya a **[!UICONTROL Cloud Services > Configuración de Dynamic Media]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]**. No seleccione el icono de carpeta a la izquierda de **[!UICONTROL global]**. A continuación, seleccione **[!UICONTROL Editar]**.
1. En el **[!UICONTROL Editar configuración de Dynamic Media]** directamente debajo de la **[!UICONTROL Contraseña]** campo, seleccione **[!UICONTROL Cambiar contraseña]**.
1. En el **[!UICONTROL Cambiar contraseña]** haga lo siguiente:

   * En el **[!UICONTROL Nueva contraseña]** , introduzca una contraseña nueva.

      La variable **[!UICONTROL Contraseña actual]** se rellena intencionalmente y se oculta de la interacción.

   * En el **[!UICONTROL Repetir contraseña]** , vuelva a escribir la nueva contraseña y, a continuación, seleccione **[!UICONTROL Listo]**.

1. En la esquina superior derecha de la variable **[!UICONTROL Editar configuración de Dynamic Media]** página, seleccione **[!UICONTROL Guardar]** y, a continuación, seleccione **[!UICONTROL OK]**.

## (Opcional) Configuración avanzada en Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Para personalizar aún más la configuración y configuración de Dynamic Media o optimizar su rendimiento, puede realizar una o más de las siguientes acciones: _opcional_ tareas:

* [(Opcional) Habilite permisos ACL en Dynamic Media](#optional-enable-acl)
* [(Opcional) Configuración de Dynamic Media](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [(Opcional) Ajuste el rendimiento de Dynamic Media](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### (Opcional) Habilite los permisos de la Lista de control de acceso en Dynamic Media {#optional-enable-acl}

Cuando ejecuta Dynamic Media en AEM, actualmente se reenvía `/is/image` solicitudes para el servicio de imágenes de vista previa segura sin comprobar los permisos de ACL (Access Control List) en PlatformServerServlet. Sin embargo, puede _enable_ Permisos ACL. Al hacerlo, se reenvía el `/is/image` solicitudes. Si un usuario no está autorizado a acceder al recurso, se muestra el error &quot;403 - Prohibido&quot;.

**Para habilitar permisos ACL en Dynamic Media:**

1. En el Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Una nueva pestaña del navegador se abre para **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]** página.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hasta el nombre _Adobe CQ Scene7 Platform Server_.

1. A la derecha del nombre, seleccione el icono de lápiz (**[!UICONTROL Editar los valores de configuración]**).

1. En el **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** seleccione la casilla de verificación para las dos configuraciones siguientes:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - Cuando está habilitado, esta configuración almacena en caché los resultados de permisos durante dos minutos (predeterminado) para guardarlos.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` : Cuando está activado, esta configuración valida el acceso de un usuario mientras obtiene una vista previa de los recursos mediante Dynamic Media Image Server.

   ![Habilitar la configuración de la lista de control de acceso en el modo Dynamic Media - Scene7](/help/assets/dynamic-media/assets/acl.png)

1. Cerca de la esquina inferior derecha de la página, seleccione **[!UICONTROL Guardar]**.

### (Opcional) Configuración de Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

Utilice la interfaz de usuario de Dynamic Media Classic para cambiar la configuración de Dynamic Media.

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

Las tareas de configuración y configuración incluyen lo siguiente:

* [Configuración de Dynamic Media Publish Setup para Image Server](#publishing-setup-for-image-server)
* [Configuración general de Dynamic Media](#configuring-application-general-settings)
* [Configuración de la gestión de color](#configuring-color-management)
* [Editar tipos MIME para formatos admitidos](#editing-mime-types-for-supported-formats)
* [Añadir tipos MIME para formatos no compatibles](#adding-mime-types-for-unsupported-formats)

<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### Configuración de Dynamic Media Publish Setup para Image Server {#publishing-setup-for-image-server}

La página Configuración de publicación de Dynamic Media establece una configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o aplicaciones.

Consulte [Configuración de Dynamic Media Publish Setup para Image Server](/help/assets/dynamic-media/dm-publish-settings.md).

#### Configuración general de Dynamic Media {#configuring-application-general-settings}

Configuración de Dynamic Media **[!UICONTROL Nombre del servidor de publicación]** La URL y el **[!UICONTROL Nombre del servidor de origen]** URL. También puede especificar **[!UICONTROL Cargar a la aplicación]** configuración y **[!UICONTROL Opciones de carga predeterminadas]** todo en función de su caso de uso particular.

Consulte [Configuración general de Dynamic Media](/help/assets/dynamic-media/dm-general-settings.md).

#### Configuración de la gestión de color {#configuring-color-management}

La gestión de color de Dynamic Media le permite colorear los recursos correctos. Con la corrección de color, los recursos ingestados conservan su espacio de color (RGB, CMYK, Gris) y su perfil de color incrustado. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color de destino mediante la salida CMYK, RGB o Gris.

Consulte [Configurar ajustes preestablecidos de imagen](/help/assets/dynamic-media/managing-image-presets.md).

Para configurar las propiedades de color predeterminadas para habilitar la corrección de color al solicitar imágenes:

1. Abra el [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)y, a continuación, inicie sesión en la cuenta con las credenciales proporcionadas durante el aprovisionamiento.
1. Vaya a **[!UICONTROL Configuración > Configuración de la aplicación]**.
1. Expanda el área **[!UICONTROL Ajustes de publicación]** y seleccione **[!UICONTROL Servidor de imágenes]**. Configure **[!UICONTROL Publicar contexto]** en **[!UICONTROL Servicio de imágenes]** cuando establezca los valores predeterminados para las instancias de publicación.
1. Desplácese hasta la propiedad que debe cambiar, por ejemplo, una propiedad de la variable **[!UICONTROL Atributos de gestión de color]** .
Puede establecer las siguientes propiedades de corrección de color:

   | Propiedad | Descripción |
   |---|---|
   | Espacio de color predeterminado CMYK | Nombre del perfil de color CMYK predeterminado. |
   | Espacio de color predeterminado de escala de grises | Nombre del perfil de color gris predeterminado. |
   | Espacio de color predeterminado del RGB | Nombre del perfil de color del RGB predeterminado. |
   | Interpretación de conversión de color | Especifica la interpretación. Los valores aceptables son: **[!UICONTROL perceptual]**, **[!UICONTROL colométrico relativo]**, **[!UICONTROL saturación]**, **[!UICONTROL colométrico absoluto]**. Recomendaciones de Adobe **[!UICONTROL relativo]** como predeterminado. |

1. Seleccione **[!UICONTROL Guardar]**.

Por ejemplo, puede establecer el **[!UICONTROL espacio de color predeterminado RGB]** en *sRGB* y el **[!UICONTROL espacio de color predeterminado CMYK]** en *WebCoated*.

Al hacerlo, se haría lo siguiente:

* Habilita la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes de RGB que no tienen un perfil de color están en la variable *sRGB* espacio de color.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *WebCoated* espacio de color.
* Representaciones dinámicas que devuelven la salida del RGB, las devuelven en la variable *sRGB* espacio de color.
* Representaciones dinámicas que devuelven la salida CMYK y la devuelven en la variable *WebCoated* espacio de color.

#### Editar tipos MIME para formatos admitidos {#editing-mime-types-for-supported-formats}

Puede definir qué tipos de recursos procesa Dynamic Media y personalizar los parámetros avanzados de procesamiento de recursos. Por ejemplo, puede especificar parámetros de procesamiento de recursos para hacer lo siguiente:

* Convierta una Adobe PDF en un recurso de catálogo electrónico.
* Convierta un documento de Adobe Photoshop (.PSD) en un recurso de plantilla de banner para su personalización.
* Rasterizar un archivo Adobe Illustrator (.AI) o un archivo de PostScript® Encapsulado de Adobe Photoshop (.EPS).
* [Perfiles de vídeo](/help/assets/dynamic-media/video-profiles.md) y [Perfiles de imagen](/help/assets/dynamic-media/image-profiles.md) se puede utilizar para definir el procesamiento de vídeos e imágenes, respectivamente.

Consulte [Cargar recursos](/help/assets/add-assets.md).

**Para editar tipos MIME para formatos compatibles:**

1. Inicie sesión en su Experience Manager as a Cloud Service como administrador del producto.
1. En Experience Manager as a Cloud Service , seleccione el logotipo as a Cloud Service del Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL General > CRXDE Lite]**.

   Si no tiene acceso al CRXDE Lite, consulte [Uso del CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. En el carril izquierdo, vaya a lo siguiente:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. En la carpeta mimeTypes , seleccione un tipo MIME.
1. En el lado derecho de la página CRXDE Lite, en la parte inferior:

   * Toque dos veces el botón **[!UICONTROL enabled]** campo . De forma predeterminada, todos los tipos de MIME de recursos están habilitados (se establece en **[!UICONTROL true]**), lo que significa que los recursos se sincronizan con Dynamic Media para su procesamiento. Si desea excluir este tipo MIME de recurso para que no se procese, cambie esta configuración a **[!UICONTROL false]**.

   * Pulsar dos veces **[!UICONTROL jobParam]** para abrir el campo de texto asociado. Consulte [Tipos MIME admitidos](/help/assets/file-format-support.md) para obtener una lista de los valores de parámetro de procesamiento permitidos que puede utilizar para un tipo MIME determinado.

1. Realice una de las siguientes acciones:
   * Repita los pasos del 3 al 4 para editar más tipos MIME.
   * En la barra de menús de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

1. En la esquina superior izquierda de la página, seleccione **[!UICONTROL CRXDE Lite]** para volver al Experience Manager as a Cloud Service.

#### Añadir tipos MIME para formatos no compatibles {#adding-mime-types-for-unsupported-formats}

Puede añadir tipos MIME personalizados para formatos no compatibles en Experience Manager Assets. Para asegurarse de que el Experience Manager no elimina ningún nodo nuevo que agregue al CRXDE Lite, mueva el tipo MIME antes de `image_`. Asegúrese también de que su valor habilitado esté establecido en **[!UICONTROL false]**.

**Para añadir tipos MIME para formatos no compatibles:**

1. Inicie sesión en su Experience Manager as a Cloud Service como administrador del producto.
1. Desde el Experience Manager as a Cloud Service, vaya a **[!UICONTROL Herramientas > Operaciones > Consola web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Una nueva pestaña del navegador se abre para **[!UICONTROL Configuración de la consola web de Adobe Experience Manager]** página.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. En la página, desplácese hacia abajo hasta el nombre *Servicio MIME de tipo de recurso de Adobe CQ Scene7* como se muestra en la siguiente captura de pantalla. A la derecha del nombre, pulse la opción **[!UICONTROL Editar los valores de configuración]** (icono de lápiz).

   ![Editar los valores de configuración](assets/2019-08-02_16-44-56.png)

1. En el **Servicio de tipo MIME de Adobe CQ Scene7 Asset** seleccione cualquier icono de signo más &lt;+>. La ubicación en la tabla donde se selecciona el signo más para añadir el nuevo tipo MIME es trivial.

   ![Servicio de tipo mime de Adobe CQ Scene7 Asset Mime](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` en el campo de texto vacío que acaba de añadir.

   La variable `DWG=image/vnd.dwg` El tipo MIME es solo para fines de ejemplo. El tipo MIME que agregue aquí puede ser cualquier otro formato no admitido.

   ![Adición de un tipo de mime DWG](assets/2019-08-02_16-36-36.png)

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   En este punto, puede cerrar la ficha del explorador que tiene la página de configuración de la consola web de Adobe Experience Manager abierta.

1. Vuelva a la ficha del explorador que tiene la consola as a Cloud Service del Experience Manager abierta.
1. Desde el Experience Manager as a Cloud Service, vaya a **[!UICONTROL Herramientas > General > CRXDE Lite]**.

   Si no tiene acceso al CRXDE Lite, consulte [Uso del CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![Herramientas > General > CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. En el carril izquierdo, vaya a lo siguiente:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arrastre el tipo MIME `image_vnd.dwg` y suéltelo directamente encima `image_` en el árbol como se ve en la siguiente captura de pantalla.

   ![Edición de un archivo DWG en un CRXDE Lite](assets/crxdelite_cqdoc-14627.png)

1. Con el tipo MIME `image_vnd.dwg` aún seleccionado, en la **[!UICONTROL Propiedades]** en la **[!UICONTROL enabled]** dentro de **[!UICONTROL Valor]** , toque dos veces el valor. La variable **[!UICONTROL Valor]** se abre la lista desplegable.
1. Tipo `false` en el campo (o seleccione **[!UICONTROL false]** en la lista desplegable).

   ![Edición de tipos de mime en el CRXDE Lite](assets/2019-08-02_16-60-30.png)

1. Cerca de la esquina superior izquierda de la página CRXDE Lite, seleccione **[!UICONTROL Guardar todo]**.

### (Opcional) Ajuste el rendimiento de Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para conservar Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> cuando se ejecuta sin problemas, Adobe recomienda los siguientes consejos de ajuste del rendimiento/escalabilidad de la sincronización:

* [Actualizar los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo](#update-job-para).
* [Actualizar los subprocesos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo)](#update-granite-workflow-queue-worker-threads-video)
* [Actualizar los subprocesos de trabajo predefinidos de la cola de flujo de trabajo transitorio de Granite (imágenes y recursos que no sean de vídeo)](#update-granite-transient-workflow-queue-worker-threads-images).
* [Actualizar las conexiones de carga máximas al servidor de Dynamic Media Classic (Scene7)](#update-max-s7-upload-connections).

#### Actualizar los parámetros de trabajo predefinidos para el procesamiento de diferentes formatos de archivo {#update-job-para}

Puede ajustar los parámetros de trabajo para un procesamiento más rápido al cargar archivos. Por ejemplo, si carga archivos de PSD, pero no desea procesarlos como plantillas, puede establecer la extracción de capas en false (desactivado). En tal caso, el parámetro de trabajo ajustado aparece de la siguiente manera: `process=None&createTemplate=false`.

Si desea activar la creación de plantillas, utilice los siguientes parámetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe recomienda utilizar los siguientes parámetros de trabajo &quot;ajustados&quot; para archivos de PDF, PostScript® y PSD:

| Tipo de archivo | Parámetros de trabajo recomendados |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para actualizar cualquiera de estos parámetros, consulte [Edición de tipos MIME para formatos compatibles](#editing-mime-types-for-supported-formats).

Consulte también [Adición de tipos MIME para formatos no admitidos](#adding-mime-types-for-unsupported-formats).

#### Actualizar los subprocesos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo) {#update-granite-workflow-queue-worker-threads-video}

La cola Granite Workflow se utiliza para flujos de trabajo no transitorios. En Dynamic Media, se utilizaba para procesar vídeos con la variable **[!UICONTROL Codificar vídeo de Dynamic Media]** flujo de trabajo.

>[!NOTE]
>
>Debe iniciar sesión en el Experience Manager as a Cloud Service como administrador del producto para completar esta tarea.

Si no tiene acceso a OSGi, consulte [Configuración de OSGi](/help/implementing/developing/components/overview.md#osgi-configuration).

**Para actualizar los subprocesos de trabajo predefinidos de la cola de flujo de trabajo de Granite (recursos de vídeo):**

1. Vaya a `https://<server>/system/console/configMgr` y busque **Cola: Cola de flujo de trabajo de Granite**.

   >[!NOTE]
   >
   >Es necesario buscar texto en lugar de una dirección URL directa porque el OSGi PID se genera dinámicamente.

1. En el **[!UICONTROL Trabajos paralelos máximos]** , cambie el número al valor deseado.

   De forma predeterminada, el número máximo de trabajos paralelos depende del número de núcleos de CPU disponibles. Por ejemplo, en un servidor de 4 núcleos, asigna dos subprocesos de trabajo. (Un valor entre 0,0 y 1,0 se basa en la relación o cualquier número bueno que uno asigna al número de subprocesos de trabajo).

   Para la mayoría de los casos de uso, la configuración predeterminada de 0,5 es suficiente.

   ![Configuración de una cola de procesamiento de trabajos](assets/chlimage_1-1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualizar los subprocesos de trabajo de cola de flujo de trabajo transitorio predefinidos de Granite {#update-granite-transient-workflow-queue-worker-threads-images}

La cola Flujo de trabajo de tránsito de Granite se utiliza para la variable **[!UICONTROL Recurso de actualización DAM]** flujo de trabajo. En Dynamic Media, se utiliza para la ingesta y el procesamiento de recursos de imagen y que no sean de vídeo.

>[!NOTE]
>
>Debe iniciar sesión en el Experience Manager as a Cloud Service como administrador del producto para completar esta tarea.

**Para actualizar los subprocesos de trabajo de la cola de Granite Transient Workflow predefinidos:**

1. Vaya a la **Configuración de la consola web de Adobe Experience Manager** at `http://<host>:<port>/system/console/configMgr`
1. Buscar **Cola: Cola de flujo de trabajo transitorio de Granite**.

   >[!NOTE]
   >
   >Es necesario buscar texto en lugar de una dirección URL directa porque el OSGi PID se genera dinámicamente.

1. En el **[!UICONTROL Trabajos paralelos máximos]** , cambie el número al valor deseado.

   Puede aumentar **[!UICONTROL Trabajos paralelos máximos]** para admitir correctamente la carga pesada de archivos en Dynamic Media. El valor exacto depende de la capacidad del hardware. En algunos casos, como una migración inicial o una carga masiva única, puede utilizar un valor grande. No obstante, tenga en cuenta que el uso de un valor grande (por ejemplo, dos veces el número de núcleos) puede tener efectos negativos en otras actividades simultáneas. Como tal, pruebe y ajuste el valor en función de su caso de uso particular.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![imagen_1](assets/chlimage_1.jpeg)

1. Seleccione **[!UICONTROL Guardar]**.

#### Actualizar las conexiones de carga máximas al servidor de Dynamic Media Classic (Scene7) {#update-max-s7-upload-connections}

La configuración de conexión de carga de Dynamic Media Classic (Scene7) sincroniza los recursos de Experience Manager con los servidores de Dynamic Media Classic.

>[!NOTE]
>
>Debe iniciar sesión en el Experience Manager as a Cloud Service como administrador del producto para completar esta tarea.

**Para actualizar las conexiones de carga máximas al servidor de Dynamic Media Classic (Scene7):**

1. Navegue hasta `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. En el **[!UICONTROL Número de conexiones]** o **[!UICONTROL Tiempo de espera de trabajo activo]** o ambos, cambie el número como desee.

   La variable **[!UICONTROL Número de conexiones]** controla el número máximo de conexiones HTTP permitidas para que el Experience Manager cargue Dynamic Media. Normalmente, el valor predefinido de diez conexiones es suficiente.

   La variable **[!UICONTROL Tiempo de espera de trabajo activo]** determina el tiempo de espera para que los recursos de Dynamic Media cargados se publiquen en el servidor de entrega. Este valor es de 2100 segundos o 35 minutos de forma predeterminada.

   Para la mayoría de los casos de uso, el ajuste de 2100 es suficiente.

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
