---
title: Administrar recursos de vídeo
description: Cargar, previsualizar, anotar y publicar recursos de vídeo en  [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management, Publishing, Collaboration, Video
role: User
exl-id: 91edce4a-dfa0-4eca-aba7-d41ac907b81e
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '4983'
ht-degree: 6%

---

# Administrar recursos de vídeo {#manage-video-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-video-assets.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

El formato de vídeo es una parte esencial de los recursos digitales de una organización. [!DNL Adobe Experience Manager] ofrece ofertas y características consolidadas para administrar todo el ciclo de vida de los recursos de vídeo después de su creación.

Obtenga información sobre cómo administrar y editar los recursos de vídeo en [!DNL Adobe Experience Manager Assets]. La codificación y transcodificación de vídeo, por ejemplo, la transcodificación FFmpeg, es posible mediante Perfiles de procesamiento y mediante la integración de [!DNL Dynamic Media]. Sin la licencia [!DNL Dynamic Media], [!DNL Experience Manager] proporciona compatibilidad básica con los vídeos, como la transcodificación mediante FFmpeg, la extracción de miniaturas de vista previa para los formatos de archivo admitidos y la vista previa en la interfaz de usuario para los formatos compatibles con la reproducción directa en el explorador.

## Carga y previsualización de recursos de vídeo {#upload-and-preview-video-assets}

Puede cargar y previsualizar recursos de vídeo de formato compatible en [!DNL Experience Manager Assets].
<!-- It generates previews for video assets with the extension MP4. -->

### Cargar recursos de vídeo

Para cargar un recurso de vídeo, siga estos pasos:

1. En la carpeta o subcarpetas de recursos digitales, vaya a la ubicación donde debe agregar el recurso.
1. Haga clic en **[!UICONTROL Crear]** en la barra de herramientas y elija **[!UICONTROL Archivos]**. <br>También puede arrastrar un archivo a la interfaz de usuario.
Más información sobre [cargar recursos](manage-digital-assets.md#uploading-assets) en [!DNL Experience Manager Assets].

<!-- 1. To preview a video in the card view, click the **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) option on the video asset. You can pause or play video in the card view only. The [!UICONTROL Play] and [!UICONTROL Pause] options are not available in the list view.
1. To preview the video in the asset details page, select **[!UICONTROL Edit]** on the card. The video plays in the native video player of the browser. You can play, pause, control the volume, and zoom the video to full screen. -->

### Previsualización de recursos de vídeo

Puede obtener una vista previa de los vídeos de las representaciones compatibles en la interfaz de usuario de [!DNL Assets]. Para obtener una vista previa de un recurso de vídeo, siga estos pasos:

1. Cargue un recurso de vídeo de un formato compatible en [!DNL Experience Manager Assets]. Más información sobre los [formatos de vídeo compatibles](file-format-support.md#video-formats). <br>Una vez cargado, el recurso de vídeo se procesa y se genera una vista previa de la representación.
1. Haga clic en el recurso y seleccione ![opción de detalles](assets/do-not-localize/details_icon.svg) **[!UICONTROL Detalles]** en la barra de herramientas superior. El recurso de vídeo se abre en el visor de vídeo.
1. Haz clic en el icono ![opción de reproducción](assets/do-not-localize/play.png) de la miniatura de vídeo. <br>Puede reproducir, pausar, controlar el volumen y ampliar el vídeo a pantalla completa.

Para los recursos de vídeo existentes en [!DNL Experience Manager Assets], debe **[!UICONTROL reprocesar]** los recursos de [!DNL Experience Manager] para habilitar la característica de vista previa de vídeo. Aprenda a [reprocesar recursos digitales](reprocessing.md) en [!DNL Experience Manager].

### Limitaciones de la previsualización de vídeo

* Los archivos MXF no muestran previsualizaciones de vídeo aunque se haya generado la representación.
* Los archivos WebM no generan representaciones de previsualización, ya que los exploradores web los pueden reproducir de forma nativa.

## Publicar recursos de vídeo {#publish-video-assets}

Después de la publicación, puede incluir los recursos de vídeo en una página web como una URL o incrustar directamente los recursos. Para obtener más información, consulte [publicar [!DNL Dynamic Media] recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Publicación de vídeos en YouTube {#publishing-videos-to-youtube}

Puede publicar recursos de vídeo administrados en Experience Manager Assets directamente en un canal de YouTube que haya creado anteriormente.

Para publicar recursos de vídeo en YouTube, puede etiquetar recursos de vídeo en Experience Manager Assets con etiquetas. Estas etiquetas se asocian a un canal de YouTube. Si la etiqueta de un recurso de vídeo coincide con la de un canal de YouTube, el vídeo se publica en YouTube. La publicación en YouTube se produce junto con la publicación normal del vídeo, siempre y cuando se utilice una etiqueta asociada.

YouTube realiza su propia codificación. De este modo, el archivo de vídeo original que se cargó en Experience Manager se publica en YouTube, en lugar de en cualquier representación de vídeo que haya creado la codificación de Dynamic Media. Aunque no es necesario procesar vídeos mediante Dynamic Media, se espera que lo hagan en caso de que se necesite un ajuste preestablecido de visualizador para la reproducción.

Cuando evita el perfil de procesamiento de vídeo y publica directamente en YouTube, simplemente significa que el recurso de vídeo en Experience Manager Asset no obtiene una miniatura visible. También significa que los vídeos no codificados no funcionan con ninguno de los tipos de recursos de Dynamic Media.

La publicación de recursos de vídeo en servidores de YouTube implica completar las siguientes tareas para garantizar la verificación segura y protegida servidor a servidor con YouTube:

1. [Configuración de Google Cloud](#configuring-google-cloud-settings)
1. [Crear un canal de YouTube](#creating-a-youtube-channel)
1. [Añadir etiquetas para publicar](#adding-tags-for-publishing)
1. [Configuración de YouTube en Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatice la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicación de vídeos en el canal de YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Compruebe el vídeo publicado en YouTube](/help/assets/dynamic-media/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vinculación de URL de YouTube a la aplicación web](#linking-youtube-urls-to-your-web-application)

También puede [cancelar la publicación de vídeos para quitarlos de YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Configuración de Google Cloud {#configuring-google-cloud-settings}

Para publicar en YouTube, necesita una cuenta de Google. Si tiene una cuenta de GMAIL, entonces ya tiene una cuenta de Google; si no tiene una cuenta de Google, puede crear fácilmente una. Necesita la cuenta de porque necesita credenciales para publicar recursos de vídeo en YouTube. <!-- hidden March 3 2022 If you have an account already created, then skip this task and proceed directly to [Create a YouTube channel](#creating-a-youtube-channel). -->

La cuenta utilizada con Google Cloud y la cuenta de Google utilizada para YouTube no tienen por qué ser la misma.

Google cambia periódicamente su interfaz de usuario. Como tal, los pasos para publicar vídeos en YouTube pueden variar ligeramente de lo que se documenta a continuación. Esta advertencia también se aplica a YouTube cuando intenta comprobar si se han cargado vídeos en él.

>[!NOTE]
>
>Los siguientes pasos eran precisos en el momento de escribir este artículo. Sin embargo, Google actualiza periódicamente sus páginas web en la nube sin previo aviso. De este modo, es posible que algunas opciones de configuración tengan nombres ligeramente diferentes en la interfaz de usuario de Google del nombre utilizado en los pasos.

**Para establecer la configuración de Google Cloud:**

1. Cree una cuenta de Google.

   Si ya tiene una cuenta de Google, puede pasar al siguiente paso.

1. Vaya a [https://cloud.google.com/](https://cloud.google.com/).
1. En la página **[!UICONTROL Google Cloud]**, cerca de la esquina superior derecha, seleccione **[!UICONTROL Consola]**.

   Si es necesario, **[!UICONTROL inicia sesión]** con las credenciales de tu cuenta de Google para ver la opción **[!UICONTROL Consola]**.

1. En la página **[!UICONTROL Panel]**, a la derecha de **[!UICONTROL Google Cloud Platform]**, seleccione la lista desplegable **[!UICONTROL Proyecto]** para abrir el cuadro de diálogo **[!UICONTROL Seleccionar un proyecto]**.
1. En el cuadro de diálogo **[!UICONTROL Seleccionar un proyecto]**, seleccione **[!UICONTROL Nuevo proyecto]**.
1. En el cuadro de diálogo **[!UICONTROL Nuevo proyecto]**, en el campo **[!UICONTROL Nombre del proyecto]**, escriba el nombre del nuevo proyecto.

   El ID del proyecto se basa en el nombre del proyecto. Como tal, elija el nombre del proyecto con cuidado; no se puede cambiar después de crearlo. Además, debe volver a introducir el mismo ID de proyecto al configurar YouTube en Experience Manager más adelante. Por lo tanto, anótelo.

1. Seleccione **[!UICONTROL Crear]**.

1. Realice una de las siguientes acciones:

   * En el panel del proyecto, en la tarjeta **[!UICONTROL Introducción]**, seleccione **[!UICONTROL Explorar y habilitar API]**.
   * En el panel del proyecto, en la tarjeta **[!UICONTROL API]**, seleccione **[!UICONTROL Ir a la descripción general de las API]**.

1. Cerca de la parte superior central de la página **[!UICONTROL API y servicios]**, seleccione **[!UICONTROL HABILITAR API Y SERVICIOS]**.<!-- NEXT STEP BELOW IS STEP 10 -->
1. En la página **[!UICONTROL Biblioteca de API]**, en el lado izquierdo, bajo **[!UICONTROL Categoría]**, seleccione **[!UICONTROL YouTube]**. En el lado derecho de la página, seleccione **[!UICONTROL YouTube]**.
1. En la página **[!UICONTROL YouTube]**, seleccione **[!UICONTROL API de datos de YouTube v3]**.
1. En la página **[!UICONTROL API de datos de YouTube v3]**, seleccione **[!UICONTROL ADMINISTRAR]**.

   ![6_5_googleaccount-apis-manage](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-manage.png)

1. Para utilizar la API, necesita credenciales. Si es necesario, en el lado izquierdo de la página **[!UICONTROL API y servicios]**, seleccione **[!UICONTROL Credenciales]**.
1. En la página **[!UICONTROL Credenciales]**, cerca de la parte superior, seleccione **[!UICONTROL CREAR CREDENCIALES]** y luego seleccione **[!UICONTROL ID de cliente de OAuth]**.
1. En la página **[!UICONTROL Crear ID de cliente de OAuth]**, en la lista desplegable **[!UICONTROL Tipo de aplicación]**, seleccione **[!UICONTROL Aplicación web]**.

   ![6_5_googleaccount-apis-applicationType](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-applicationtype.png)

1. Realice una de las siguientes acciones:

   * En el campo **[!UICONTROL Nombre]**, escriba un nombre único para su cliente de OAuth 2.0.
   * Utilice el nombre predeterminado que Google ya proporcionó en el campo **[!UICONTROL Nombre]**.

1. Bajo el encabezado **[!UICONTROL Orígenes autorizados de JavaScript]**, seleccione **[!UICONTROL AGREGAR URI]**.

   ![6_5_googleaccount-apis-nameauthorization](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-nameauthorizations.png)

1. En el campo de texto **[!UICONTROL URIs]**, escriba la siguiente ruta, sustituyendo su propio dominio y número de puerto en la ruta, luego presione **[!UICONTROL Entrar]** para agregar la ruta a la lista:

   `https://<servername.domain>:<port_number>`

   Por ejemplo, `https://1a2b3c.mycompany.com:4321`

   >[!NOTE]
   >
   >El ejemplo de ruta de URI anterior es hipotético y solo con fines explicativos.

1. En el encabezado **[!UICONTROL URI de redireccionamiento autorizados]**, seleccione AGREGAR URI.
1. En el campo de texto **[!UICONTROL URIs]**, escriba la siguiente ruta, sustituyendo su propio dominio y número de puerto en la ruta, luego presione **[!UICONTROL Entrar]** para agregar la ruta a la lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por ejemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   >[!NOTE]
   >
   >El ejemplo de ruta de URI anterior es hipotético y solo con fines explicativos.

1. Cerca de la parte inferior de la página **[!UICONTROL Crear ID de cliente de OAuth]**, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Cliente de OAuth creado]**, haga lo siguiente:

   * (Opcional) Copie los valores de los campos **[!UICONTROL Su ID de cliente]** y **[!UICONTROL Secreto de cliente]**, y guarde los cambios.
   * Seleccione **[!UICONTROL DESCARGAR JSON]** y, a continuación, guarde el archivo JSON.

   Necesita este archivo JSON descargado cuando configure YouTube en Adobe Experience Manager más adelante.

   ![6_5_googleaccount-apis-oauthclientcreated](/help/assets/dynamic-media/assets/6_5_googleaccount-apis-oauthclientcreated.png)

1. En el cuadro de diálogo **[!UICONTROL Cliente de OAuth creado]**, seleccione **[!UICONTROL Aceptar]**.
1. Cierre la sesión de su cuenta de Google. Ahora cree un canal de YouTube.

### Crear un canal de YouTube {#creating-a-youtube-channel}

La publicación de vídeos en YouTube requiere que tenga uno o más canales. Si ya has creado un canal de YouTube, puedes omitir esta tarea y ir a [Agregar etiquetas para publicar](/help/assets/dynamic-media/video.md#adding-tags-for-publishing).

>[!CAUTION]
>
>Asegúrese de que ya ha configurado uno o más canales en YouTube *antes de* que agregue canales en Configuración de YouTube en Experience Manager (consulte [Configurar YouTube en Experience Manager](#setting-up-youtube-in-aem) a continuación). Si no puede configurar el canal, no se le avisará de que no hay canales. Sin embargo, la verificación mediante Google se sigue produciendo cuando se añade un canal, pero no existe la opción de elegir el canal al que se envía el vídeo.

**Para crear un canal de YouTube:**

1. Vaya a [https://www.youtube.com](https://www.youtube.com/) e inicie sesión con las credenciales de su cuenta de Google.
1. En la esquina superior derecha de la página de YouTube, selecciona la imagen de perfil (también puede aparecer como una letra dentro de un círculo de color sólido) y, a continuación, selecciona **[!UICONTROL Configuración de YouTube]** (icono de engranaje redondo).
1. En la página Información general, en el encabezado Características adicionales, seleccione **[!UICONTROL Ver todos mis canales o crear un canal]**.
1. En la página Canales, seleccione **[!UICONTROL Crear un canal nuevo]**.
1. En la página Cuenta de marca, en el campo Nombre de cuenta de marca, escribe un nombre de empresa o cualquier otro nombre de canal que elijas donde deseas publicar tus recursos de vídeo y, a continuación, selecciona **[!UICONTROL Crear]**.

   Recuerde el nombre que introduce aquí; debe introducirlo de nuevo cuando tenga que configurar YouTube en Experience Manager.

1. (Opcional) Si es necesario, agregue más canales.

   Ahora puede añadir etiquetas para la publicación.

### Añadir etiquetas para publicar {#adding-tags-for-publishing}

Para publicar en los vídeos en YouTube, Experience Manager asocia las etiquetas a uno o varios canales de YouTube. Para agregar etiquetas para la publicación, consulte [Administrar etiquetas](/help/sites-cloud/authoring/sites-console/tags.md).

O bien, si deseas usar las etiquetas predeterminadas en Experience Manager, puedes omitir esta tarea y ir a [Configurar YouTube en Experience Manager](#setting-up-youtube-in-aem).

>[!NOTE]
>
>Una vez configurado Cloud Service, no se requiere ninguna otra configuración para habilitar el agente de replicación de publicación de YouTube en este momento. El motivo es que se habilitó cuando se guardó la configuración de Cloud Service.

<!-- ### Enabling the YouTube Publish replication agent {#enabling-the-youtube-publish-replication-agent}

After you enable the YouTube Publish replication agent, if you want to test the connection to the Google Cloud account, select **[!UICONTROL Test Connection]**. A browser tab displays the connection results. If you have added YouTube Channels, then a listing of those is displayed as part of the test.

1. In the upper-left corner of Experience Manager, select the Experience Manager logo, then in the left rail, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]** > **[!UICONTROL Agents on Author]**.
1. On the Agents of Author page, select **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, select **[!UICONTROL Edit]**.
1. Select the **[!UICONTROL Enabled]** checkbox to turn on the replication agent.
1. Select **[!UICONTROL OK]**. -->

### Configuración de YouTube en Experience Manager {#setting-up-youtube-in-aem}

A partir de Experience Manager 6.4, se introdujo un nuevo método de interfaz de usuario táctil para configurar la publicación de YouTube en Experience Manager. En función de la instancia instalada de Experience Manager que esté utilizando, realice una de las siguientes acciones:

* Para configurar YouTube en Experience Manager anterior a la versión 6.4, consulte [Configuración de YouTube en Experience Manager anterior a la versión 6.4](/help/assets/dynamic-media/video.md#setting-up-youtube-in-aem-before).
* Para configurar YouTube en Experience Manager 6.4 o posterior, consulte [Configurar YouTube en Experience Manager 6.4 y posterior](#setting-up-youtube-in-aem-and-later).

#### Configuración de YouTube en Experience Manager 6.4 y posterior {#setting-up-youtube-in-aem-and-later}

1. Asegúrese de iniciar sesión en la instancia de Dynamic Media como administrador.
1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager y, a continuación, en el carril izquierdo, vaya a **[!UICONTROL Herramientas]**(icono de martillo) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de publicación de YouTube]**.
1. Seleccione **[!UICONTROL global]** (no lo seleccione).

1. Cerca de la esquina superior derecha de la página global, seleccione **[!UICONTROL Crear]**.
1. En la página Crear configuración de YouTube, en Configuración de plataforma de Google Cloud, en el campo **[!UICONTROL Nombre de aplicación]**, introduzca el ID de proyecto de Google.

   Especificó el ID del proyecto al establecer inicialmente la configuración de Google Cloud anteriormente.
Deje abierta la página Crear configuración de YouTube; volverá a ella en un momento.

   ![6_5_youtubepublish-createyoutubeconfiguration](/help/assets/dynamic-media/assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Con un editor de texto sin formato, abra el archivo JSON que descargó y guardó anteriormente en la tarea [Configuración de Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings).
1. Seleccione y copie todo el texto JSON.
1. Vuelva al cuadro de diálogo Configuración de cuenta de YouTube. En el campo **[!UICONTROL Configuración JSON]**, pegue el texto JSON.
1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

   Ahora configure los canales de YouTube en Experience Manager.

1. Seleccione **[!UICONTROL Agregar canal]**.
1. En el campo Nombre de canal, escriba el nombre del canal que creó en la tarea **[!UICONTROL Agregar uno o más canales a YouTube]** anteriormente.

   Si lo desea, puede añadir una descripción.

1. Seleccione **[!UICONTROL Añadir]**.
1. Se muestra la verificación de YouTube/Google. Si aún no ha iniciado sesión en la cuenta de Google Cloud, omita este paso.

   * Introduzca el nombre de usuario y la contraseña de Google asociados con el ID del proyecto de Google y el texto JSON anteriores.
   * Según el número de canales de su cuenta, verá dos o más elementos. Seleccione un canal. No seleccione la dirección de correo electrónico; no es un canal.
   * En la página siguiente, seleccione **[!UICONTROL Aceptar]** para permitir el acceso a este canal.

1. Seleccione **[!UICONTROL Permitir]**.

   Ahora configure etiquetas para la publicación.

1. **[!UICONTROL Configuración de etiquetas para la publicación]**: en la página Cloud Services > YouTube, seleccione el icono de lápiz para editar la lista de etiquetas que desea utilizar.
1. Para mostrar la lista de etiquetas disponibles en Experience Manager, seleccione el icono de lista desplegable (circunflejo invertido).
1. Para añadirlas, seleccione una o varias etiquetas.

   Para eliminar una etiqueta que hayas agregado, selecciona la etiqueta y selecciona **[!UICONTROL X]**.

1. Cuando termine de agregar las etiquetas que desea, seleccione **[!UICONTROL Guardar]**.

   Ahora puede publicar vídeos en su canal de YouTube.

#### Configuración de YouTube en Experience Manager anterior a 6.4 {#setting-up-youtube-in-aem-before}

1. Asegúrese de iniciar sesión en la instancia de Dynamic Media como administrador.

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager y, en el carril izquierdo, vaya a **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Implementación]** > **[!UICONTROL Cloud Services]**.
1. En el encabezado Servicios de terceros, en YouTube, seleccione **[!UICONTROL Configurar ahora]**.
1. En el cuadro de diálogo Crear configuración, introduzca un título (obligatorio) y un nombre (opcional) en los campos respectivos.
1. Seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Configuración de cuenta de YouTube, en el campo **[!UICONTROL Nombre de la aplicación]**, introduzca el ID del proyecto de Google.

   Especificó el identificador de proyecto al [establecer inicialmente la configuración de Google Cloud](/help/assets/dynamic-media/video.md#configuring-google-cloud-settings) antes.
Deje abierto el cuadro de diálogo Configuración de cuenta de YouTube; volverá a él en un momento.

1. Con un editor de texto sin formato, abra el archivo JSON que descargó y guardó anteriormente en la tarea Configuración de Google Cloud.
1. Seleccione y copie todo el texto JSON.
1. Vuelva al cuadro de diálogo Configuración de cuenta de YouTube. En el campo **[!UICONTROL Configuración JSON]**, pegue el texto JSON.
1. Seleccione **[!UICONTROL Aceptar]**.

   Ahora configure los canales de YouTube en Experience Manager.

1. A la derecha de **[!UICONTROL Canales disponibles]**, seleccione **+** (icono de signo más).
1. En el cuadro de diálogo Configuración de canal de YouTube, en el apartado Título, escriba el nombre del canal que creó en la tarea **[!UICONTROL Agregar uno o más canales a YouTube]** anteriormente.

   Si lo desea, puede añadir una descripción.

1. Seleccione **[!UICONTROL Aceptar]**.
1. Se muestra la verificación de YouTube/Google. Si aún no ha iniciado sesión en la cuenta de Google Cloud, omita este paso.

   * Introduzca el nombre de usuario y la contraseña de Google asociados con el ID del proyecto de Google y el texto JSON anteriores.
   * Según el número de canales de su cuenta, verá dos o más elementos. Seleccione un canal. No seleccione la dirección de correo electrónico; no es un canal.
   * En la página siguiente, seleccione **[!UICONTROL Aceptar]** para permitir el acceso a este canal.

1. Seleccione **[!UICONTROL Permitir]**.

   Ahora configure etiquetas para la publicación.

1. **[!UICONTROL Configuración de etiquetas para la publicación]**: en la página Cloud Services > YouTube, seleccione el icono de lápiz para editar la lista de etiquetas que desea utilizar.
1. Para mostrar la lista de etiquetas disponibles en Experience Manager, seleccione el icono de lista desplegable (circunflejo invertido).
1. Para añadirlas, seleccione una o varias etiquetas.

   Para eliminar una etiqueta que hayas agregado, selecciona la etiqueta y selecciona **X**.

1. Cuando termine de agregar las etiquetas que desee, seleccione **[!UICONTROL Aceptar]**.

   Ahora puede publicar vídeos en su canal de YouTube.

### (Opcional) Automatice la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Si lo desea, puede automatizar la configuración de las propiedades de YouTube al cargar los vídeos. Cree un perfil de procesamiento de metadatos en Experience Manager.

Para crear el perfil de procesamiento de metadatos, en primer lugar copiará valores de los campos **[!UICONTROL Etiqueta de campo]**, **[!UICONTROL Asignar a propiedad]** y **[!UICONTROL Opciones]**, todos se encuentran en Esquemas de metadatos para vídeo. A continuación, cree su perfil de procesamiento de metadatos de vídeo de YouTube agregándole esos valores.

**Para automatizar la configuración de las propiedades predeterminadas de YouTube para los vídeos cargados:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager y, en el carril izquierdo, vaya a **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Seleccione **[!UICONTROL default]**. (No añada una marca de verificación al cuadro de selección a la izquierda de &quot;predeterminado&quot;.)
1. En la página **[!UICONTROL default]**, marque la casilla a la izquierda de **[!UICONTROL video]** y luego seleccione **[!UICONTROL Editar]**.
1. En la página Editor de esquemas de metadatos, seleccione la ficha **[!UICONTROL Avanzado]**.
1. Bajo el encabezado Publicación de YouTube, seleccione **[!UICONTROL Categoría de YouTube]**.
1. En el lado derecho de la página, en la ficha **[!UICONTROL Configuración]**, haga lo siguiente:

   * En el campo de texto **[!UICONTROL Asignar a propiedad]**, seleccione y copie el valor.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

   * En **[!UICONTROL Opciones]**, seleccione y copie el valor predeterminado que desee usar (como Personas y blogs o Ciencia y tecnología).
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

1. En el encabezado Publicación de YouTube, seleccione **[!UICONTROL Privacidad de YouTube]**.
1. En el lado derecho de la página, en la ficha **[!UICONTROL Configuración]**, haga lo siguiente:

   * En el campo de texto **[!UICONTROL Asignar a propiedad]**, seleccione y copie el valor.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

   * En **[!UICONTROL Opciones]**, seleccione y copie el valor predeterminado que desee utilizar. Observe que las Opciones se agrupan en pares de dos. El campo inferior del par es el valor predeterminado que desea copiar, como público, no incluido en la lista o privado.
Pegue el valor copiado en el editor de texto abierto. Necesitará este valor más adelante cuando cree su perfil de procesamiento de metadatos. Deje abierto el editor de texto.

1. Cerca de la esquina superior derecha de la página Editor de esquemas de metadatos, seleccione **[!UICONTROL Cancelar]**.
1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager y, en el carril izquierdo, seleccione **[!UICONTROL Herramientas]** (icono de martillo) > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]**.

1. En la página Perfiles de metadatos, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo Agregar perfil de metadatos, en el campo de texto **[!UICONTROL Título del perfil]**, escriba el nombre `YouTube Video` y, a continuación, seleccione **[!UICONTROL Crear]**.
1. En la página Editor de perfiles de metadatos, seleccione la pestaña **[!UICONTROL Avanzar]**.
1. Agregue los valores de publicación de YouTube copiados al perfil haciendo lo siguiente:

   * En el lado derecho de la página, seleccione la pestaña **[!UICONTROL Generar formulario]**.
   * (Opcional) Arrastre el componente con la etiqueta **[!UICONTROL Encabezado de sección]** hacia la izquierda y suéltelo en el área de formulario.
   * (Opcional) Seleccione **[!UICONTROL Etiqueta de campo]** para seleccionar el componente.
   * (Opcional) En el lado derecho de la página, en la pestaña Configuración, en el campo de texto Etiqueta de campo, escriba `YouTube Publishing`.
   * Seleccione la pestaña **[!UICONTROL Generar formulario]**, luego arrastre el componente etiquetado **[!UICONTROL Texto de varios valores]** y suéltelo debajo del encabezado **[!UICONTROL Publicación de YouTube]** que ha creado.

   * Para seleccionar el componente, seleccione **[!UICONTROL Etiqueta de campo]**.
   * En el lado derecho de la página, en la pestaña Configuración, pegue los valores de publicación de YouTube (valor Etiqueta de campo y Asignar a valor de propiedad) que copió anteriormente, en sus respectivos campos del formulario. Pegue el valor Choices en el campo Default Value.

1. Agregue los valores de privacidad de YouTube copiados al perfil haciendo lo siguiente:

   * En el lado derecho de la página, seleccione la pestaña **[!UICONTROL Generar formulario]**.
   * (Opcional) Arrastre el componente con la etiqueta **[!UICONTROL Encabezado de sección]** hacia la izquierda y suéltelo en el área de formulario.
   * (Opcional) Seleccione **[!UICONTROL Etiqueta de campo]** para seleccionar el componente.
   * (Opcional) En el lado derecho de la página, en la pestaña Configuración, en el campo de texto Etiqueta de campo, escriba `YouTube Privacy`.
   * Seleccione la pestaña **[!UICONTROL Generar formulario]**, luego arrastre el componente etiquetado **[!UICONTROL Texto de varios valores]** y suéltelo debajo del encabezado **[!UICONTROL Privacidad de YouTube]** que ha creado.

   * Para seleccionar el componente, seleccione **[!UICONTROL Etiqueta de campo]**.
   * En el lado derecho de la página, en la pestaña Configuración, pegue los valores de publicación de YouTube (valor Etiqueta de campo y Asignar a valor de propiedad) que copió anteriormente, en sus respectivos campos del formulario. Pegue el valor Choices en el campo Default Value.

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.
1. Aplique el perfil de metadatos de publicación de YouTube a las carpetas en las que va a cargar los vídeos. Debe tener establecidos tanto el perfil de metadatos como el perfil de vídeo.

   Consulte [Perfiles de metadatos](/help/assets/metadata-profiles.md) y [Perfiles de vídeo](/help/assets/dynamic-media/video-profiles.md).

### Publicación de vídeos en el canal de YouTube {#publishing-videos-to-your-youtube-channel}

Ahora asocia las etiquetas que agregó anteriormente a los recursos de vídeo. Este proceso permite a Experience Manager saber qué recursos publicar en su canal de YouTube.

>[!NOTE]
>
>La publicación inmediata no se publica automáticamente en YouTube. Cuando se configura Dynamic Media, hay dos opciones de publicación entre las que elegir: **[!UICONTROL Inmediata]** o **[!UICONTROL Después de la activación]**.
>
>**[!UICONTROL Publicar inmediatamente]** significa que el recurso cargado (después de sincronizarlo con IPS) se publica automáticamente en el sistema de entrega. Aunque esto se aplica a Dynamic Media, no se aplica a YouTube. Para publicar en YouTube, debe publicar mediante Experience Manager Author.

>[!NOTE]
>
>Para publicar contenido desde YouTube, Experience Manager usa el flujo de trabajo **[!UICONTROL Publicar en YouTube]**, que le permite supervisar el progreso y ver cualquier información de error.
>
>Ver [Supervisión de la codificación de vídeo y progreso de publicación en YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obtener información de progreso más detallada, puede monitorizar el registro de YouTube en replicación. No obstante, tenga en cuenta que dicha monitorización requiere acceso de administrador.

**Para publicar vídeos en su canal de YouTube:**

1. En Experience Manager, vaya a un recurso de vídeo que desee publicar en el canal de YouTube.
1. Seleccione el recurso de vídeo (el conjunto de vídeos adaptable).
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. En la pestaña Básico, debajo del encabezado Metadatos, seleccione **[!UICONTROL Abrir cuadro de diálogo de selección]** a la derecha del campo Etiquetas.
1. En la página Seleccionar etiquetas, vaya a las etiquetas que desee utilizar y, a continuación, seleccione una o varias etiquetas.

   Recuerde que las etiquetas deben estar asociadas al canal de YouTube.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.
1. En la esquina superior derecha de la página de propiedades del vídeo, seleccione **[!UICONTROL Guardar y cerrar]**.
1. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**.

   Consulte también [Usar la administración de publicaciones con Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html#page-authoring).

   Si lo desea, puede comprobar el vídeo publicado en el canal de YouTube.

### (Opcional) Compruebe el vídeo publicado en YouTube {#optional-verifying-the-published-video-on-youtube}

Si lo desea, puede monitorizar el progreso de la publicación de YouTube (o cancelar la publicación).

Ver [Supervisión de la codificación de vídeo y progreso de publicación en YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Los tiempos de publicación pueden variar considerablemente según numerosos factores, entre los que se incluyen el formato del vídeo de origen principal, el tamaño del archivo y el tráfico de carga. El proceso de publicación puede tardar entre unos minutos y varias horas. Además, los formatos de mayor resolución se procesan mucho más lentamente. Por ejemplo, 720p y 1080p tardan más en aparecer que 480p.

Después de ocho horas, si sigue viendo un mensaje de estado que indica **[!UICONTROL Cargado (procesando, espere)]**, intente quitar el vídeo del sitio y cargarlo de nuevo.

### Vinculación de URL de YouTube a la aplicación web {#linking-youtube-urls-to-your-web-application}

Puede obtener una cadena de URL de YouTube generada por Dynamic Media después de publicar el vídeo. Al copiar la URL de YouTube, esta aterriza en el Portapapeles para que pueda pegarla según sea necesario en las páginas de su sitio web o aplicación.

>[!NOTE]
>
>La URL de YouTube no estará disponible para copiar hasta que haya publicado el recurso de vídeo en YouTube.

Para vincular URL de YouTube a la aplicación web:

1. Vaya al recurso de vídeo *YouTube publicado* cuya URL desee copiar y selecciónelo.

   Recuerde que las direcciones URL de YouTube solo están disponibles para copiar *después de* de haber *publicado* los recursos de vídeo por primera vez en YouTube.

1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Avanzadas]**.
1. En el encabezado Publicación de YouTube, en la Lista de URL de YouTube, seleccione y copie el texto de la URL en el explorador web para previsualizar el recurso o añadirlo a la página de contenido web.

### Cancele la publicación de vídeos para poder eliminarlos de YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Cuando se cancela la publicación de un recurso de vídeo en Experience Manager, el vídeo se elimina de YouTube.

>[!CAUTION]
>
>Si elimina un vídeo directamente desde YouTube, Experience Manager no lo tendrá en cuenta y seguirá comportándose como si el vídeo se publicara en YouTube. Cancele siempre la publicación de un recurso de vídeo de YouTube mediante Experience Manager.

>[!NOTE]
>
>Para quitar contenido de YouTube, Experience Manager usa el flujo de trabajo **[!UICONTROL Cancelar la publicación de YouTube]**, que le permite supervisar el progreso y ver la información de errores.
>
>Ver [Supervisión de la codificación de vídeo y progreso de publicación en YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para cancelar la publicación de vídeos y quitarlos de YouTube:**

1. Desplácese hasta los recursos de vídeo cuya publicación desea cancelar del canal de YouTube.
1. En un modo de selección de recursos, seleccione uno o varios recursos de vídeo publicados.
1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Si es necesario, seleccione el icono de tres puntos (`. . .`) en la barra de herramientas para ver **[!UICONTROL Administrar publicación]**.
1. En la página Administrar publicación, seleccione **[!UICONTROL Cancelar publicación]**.
1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Siguiente]**.
1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Cancelar publicación]**.

## Monitorización de la codificación de vídeo y progreso de publicación en YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Al cargar un nuevo vídeo en una carpeta a la que se ha aplicado la codificación de vídeo o, publica el vídeo en YouTube y supervisa cómo avanza (o falla) la codificación de vídeo o la publicación en Youtube. El progreso real de publicación de YouTube solo está disponible a través de los registros. Sin embargo, tanto si falla como si tiene éxito, se enumera de otras formas que se describen en el siguiente procedimiento. Además, recibirá notificaciones por correo electrónico cuando se complete o interrumpa un flujo de trabajo de publicación de YouTube o una codificación de vídeo.

### Monitorización del progreso {#monitoring-progress}

Puede monitorizar el progreso, incluida la codificación fallida o la publicación en YouTube.

1. Vea el progreso de la codificación de vídeo en la carpeta de recursos:

   * En la vista de tarjeta, el progreso de codificación de vídeo se muestra en el recurso en porcentaje. Si hay un error, esta información también se muestra en el recurso.

   ![chlimage_1-429](/help/assets/dynamic-media/assets/chlimage_1-429.png)

   * En la vista de lista, el progreso de codificación de vídeo se muestra en la columna **[!UICONTROL Estado de procesamiento]**. Si hay un error, este mensaje se muestra en la misma columna.

   ![chlimage_1-430](/help/assets/dynamic-media/assets/chlimage_1-430.png)

   Esta columna no se muestra de forma predeterminada. Para habilitar la columna, selecciona **[!UICONTROL Ver configuración]** en el menú desplegable de vistas, agrega la columna **[!UICONTROL Estado de procesamiento]** y selecciona **[!UICONTROL Actualizar]**.

   ![chlimage_1-431](/help/assets/dynamic-media/assets/chlimage_1-431.png)

1. Vea el progreso en los detalles del recurso. Cuando seleccione un recurso, abra el menú desplegable y seleccione **[!UICONTROL Cronología]**. Para reducirlo a actividades de flujo de trabajo como codificación o publicación en YouTube, seleccione **[!UICONTROL Flujos de trabajo]**.

   ![chlimage_1-432](/help/assets/dynamic-media/assets/chlimage_1-432.png)

   Cualquier información del flujo de trabajo, como la codificación, se muestra en la cronología. Para la publicación en YouTube, la cronología del flujo de trabajo también incluye el nombre del canal de YouTube y la dirección URL del vídeo de YouTube. Además, verá cualquier notificación de error en la cronología del flujo de trabajo una vez completada la publicación.

   >[!NOTE]
   >
   >Podría tomar mucho tiempo que los mensajes de error/error finalmente se registren debido a varias configuraciones de flujo de trabajo en **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL tiempo de espera]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por ejemplo:
   >
   >* Configuración de cola de trabajos de Apache Sling
   >* Controlador de trabajos de proceso externo de flujo de trabajo de Adobe Granite
   >* Cola de tiempo de espera de Granite Workflow
   >
   >Puede ajustar las propiedades de **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL tiempo de espera]** en estas configuraciones.

1. Para los flujos de trabajo en curso, consulte Instancias de flujo de trabajo disponibles en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Instancias]**.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al menú **[!UICONTROL Herramientas]**.

   ![chlimage_1-433](/help/assets/dynamic-media/assets/chlimage_1-433.png)

   Seleccione la instancia y seleccione **[!UICONTROL Abrir historial]**.

   ![chlimage_1-434](/help/assets/dynamic-media/assets/chlimage_1-434.png)

   Desde el área Instancias de flujo de trabajo, también puede suspender, finalizar o cambiar el nombre de los flujos de trabajo. Consulte [Administrar flujos de trabajo](/help/sites-cloud/authoring/workflows/overview.md) para obtener más información.

1. Para los trabajos con errores, consulte Errores de flujo de trabajo disponibles en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Errores]**. El **[!UICONTROL error de flujo de trabajo]** muestra todas las actividades de flujo de trabajo con errores.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al menú **[!UICONTROL Herramientas]**.

   ![chlimage_1-435](/help/assets/dynamic-media/assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Podría tomar mucho tiempo que el mensaje de error finalmente se registre debido a varias configuraciones de flujo de trabajo en **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL tiempo de espera]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por ejemplo:
   >
   >* Configuración de cola de trabajos de Apache Sling
   >* Controlador de trabajos de proceso externo de flujo de trabajo de Adobe Granite
   >* Cola de tiempo de espera de Granite Workflow
   >
   >Puede ajustar las propiedades de **[!UICONTROL reintentos]**, **[!UICONTROL retraso de reintentos]** y **[!UICONTROL tiempo de espera]** en estas configuraciones.

1. Para ver los flujos de trabajo completados, consulte Archivo de flujo de trabajo, disponible en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Archivar]**. El **[!UICONTROL archivo de flujo de trabajo]** enumera todas las actividades de flujo de trabajo completadas.

   >[!NOTE]
   >
   >Necesita derechos administrativos para acceder al menú **[!UICONTROL Herramientas]**.

   ![chlimage_1-436](/help/assets/dynamic-media/assets/chlimage_1-436.png)

1. Recibirá notificaciones por correo electrónico sobre trabajos de flujo de trabajo anulados o fallidos. Un administrador puede configurar estas notificaciones por correo electrónico. Consulte [Configurar notificaciones por correo electrónico](#configuring-e-mail-notifications).

<!-- EMAIL NOT AVAILABLE IN SKYLINE

#### Configuring e-mail notifications {#configuring-e-mail-notifications}

>[!NOTE]
>
>You may need administrative rights to access the **[!UICONTROL Tools]** menu.

How you configure notification depends on whether you want notifications for YouTube publishing jobs.

* For encoding jobs, you can access the configuration page for all Experience Manager workflow email notifications at **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

For YouTube publishing jobs, do the following:

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. On the Workflow Models page, select **[!UICONTROL Publish to YouTube]**, then select **[!UICONTROL Edit]** on the toolbar.
1. Near the upper-right corner of the Publish to YouTube workflow page, select **[!UICONTROL Edit]**.
1. Hover the mouse pointer on the YouTube Upload component, then select once to display the inline toolbar.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. On the inline toolbar, select the Configuration icon (wrench). Select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. In the YouTube Upload Process - Step Properties dialog box, select the **[!UICONTROL Arguments]** tab.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. You can select or clear the following check boxes:

    * Publish Start
    * Publish Failure
    * Publish Completion - includes information on channels and URLs

   Clearing a check box means that you will not receive the specified email notification from the YouTube Publish workflow.

   >[!NOTE]
   >
   >These emails are specific to YouTube and are in addition to the generic workflow email notifications. As a result, you may receive two sets of email notification - the generic notification available in the **[!UICONTROL Day CQ Workflow Email Notification Service]** and one specific to YouTube depending on your configuration settings.

1. When you are finished, near the upper-right corner of the dialog box, select the **[!UICONTROL Done]** icon (check mark).
1. On the Publish to YouTube workflow page, near the upper-right corner, select **[!UICONTROL Sync]**.

-->

## Transcodificar mediante perfil de procesamiento {#transcode-video}

[!DNL Experience Manager] as a [!DNL Cloud Service] le permite realizar transcodificaciones básicas de archivos de vídeo MP4 mediante Perfiles de procesamiento. La funcionalidad no solo le permite cargar, sino también previsualizar y escalar un archivo de vídeo MP4.

![Crear perfil de procesamiento para la transcodificación de vídeo en [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Un perfil de procesamiento para la transcodificación de vídeo en [!DNL Experience Manager].*

Si solo se proporciona anchura o altura y se deja en blanco el otro campo, las representaciones mantienen la relación de aspecto. El códec de vídeo H.264 está disponible para transcodificar.

Para procesar recursos mediante un perfil de procesamiento, agregue un perfil a una carpeta. Ver [usar perfiles de procesamiento para procesar recursos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar recursos de vídeo {#annotate-video-assets}

Puede añadir anotaciones a recursos de vídeo. Al realizar anotaciones en vídeos, el reproductor realiza pausas para permitirle realizar anotaciones en un fotograma. Para obtener más información, consulte [administración de recursos de vídeo](manage-video-assets.md).

>[!NOTE]
>
>El formato de vídeo MXF aún no es compatible con anotaciones de recursos de vídeo.

1. En la consola [!DNL Assets], seleccione **[!UICONTROL Editar]** en la tarjeta de recursos para mostrar la página de detalles del recurso.
1. Para reproducir el vídeo, haz clic en **[!UICONTROL Vista previa]**.
1. Para anotar el vídeo, haz clic en **[!UICONTROL Anotar]**. Se añade una anotación en el momento (fotograma) concreto del vídeo. Al realizar anotaciones, puede dibujar en el lienzo e incluir un comentario con el dibujo. Los comentarios se guardan automáticamente. Para salir del asistente para anotaciones, haga clic en **[!UICONTROL Cerrar]**.
1. Busque un punto específico en el vídeo, establezca el tiempo en segundos en el campo de **texto** y haga clic en **Saltar**. Por ejemplo, para omitir los primeros 20 segundos de vídeo, introduzca 20 en el campo de texto.
1. Para verla en la cronología, haga clic en una anotación. Para eliminar la anotación de la cronología, haga clic en **[!UICONTROL Eliminar]**.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Sin la licencia [!DNL Dynamic Media], solo puede procesar archivos MP4 mediante perfiles de procesamiento.
* Al transcodificar archivos MP4 mediante perfiles de procesamiento, se aplican las siguientes directrices y limitaciones:

   * Los archivos ProRes de Apple solo pueden transcodificarse a una resolución máxima de 1080p.
   * Si el archivo de origen tiene una velocidad de bits >200 Mbps, solo puede transcodificar a una resolución máxima de 1080p.
   * Si la velocidad de fotogramas de origen >=60 fps, el tamaño máximo del archivo de origen que puede utilizar es,

      * 400 MB para transcodificación de 4k.
      * 800 MB para transcodificación a 1080p.
      * 8 GB para transcodificación a 720p.

   * El tamaño máximo de archivo que puede transcodificar a una resolución de 4k es de 2,55 GB de archivo MP4 con resolución de 4k, velocidad de bits de 12 Mbps y 23 fps.

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
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Documentación de vídeo de Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Más información sobre el uso, los tipos y la configuración de los perfiles de procesamiento](/help/assets/asset-microservices-configure-and-use.md).
