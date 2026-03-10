---
title: Compartir Assets en  [!DNL the Content Hub]
description: Compartir Assets en  [!DNL the Content Hub]
role: User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# Uso compartido de recursos en Content Hub {#search-assets-as-a-link}

Cree un vínculo a los recursos seleccionados para compartirlos con otros fácilmente. Como usuario autorizado de [!DNL Content Hub], seleccione uno o más recursos disponibles en su entorno de [!DNL Content Hub], genere un vínculo y envíelo a otros usuarios privados o públicos.

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden crear un vínculo a los recursos seleccionados y compartirlo con otros usuarios.

## Compartir recursos {#share-assets}

Para compartir uno o más recursos con usuarios privados o públicos, ejecute los siguientes pasos:

1. Vaya a la página principal de [!DNL Content Hub], seleccione uno o varios recursos y haga clic en ![Compartir](/help/assets/assets/share.svg) **[!UICONTROL Compartir]** para mostrar un solo recurso seleccionado o una lista de varios recursos seleccionados en el cuadro de diálogo **[!UICONTROL Compartir recursos]**.

   También puede seleccionar y compartir recursos disponibles en ![colecciones](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL colecciones]**.

1. Vea un recurso o revise la lista de recursos disponibles en el cuadro de diálogo **[!UICONTROL Compartir recursos]**. Haga clic en ![anular la selección](/help/assets/assets/Close.svg) junto a un recurso para quitarlo de la lista.

1. Especifique un título y una descripción opcional que defina el conjunto de recursos seleccionados.

1. Seleccione **[!UICONTROL Período de caducidad]**.

1. En la lista desplegable **[!UICONTROL Quién puede acceder a]**, seleccione las opciones de acceso y haga clic en **[!UICONTROL Obtener vínculo]** para generar un vínculo que compartir con los usuarios seleccionados. Los usuarios privados deben iniciar sesión en el entorno [!DNL Content Hub] para tener acceso a la página de recursos compartidos. Mientras que los usuarios públicos, como invitados, pueden acceder a la página de recursos compartidos sin iniciar sesión en [!DNL Content Hub].

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![vínculo privado y público](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [Habilite el uso compartido de vínculos públicos desde la página de configuración](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing) para mostrar la opción **[!UICONTROL Vínculo público]** en el cuadro de diálogo **[!UICONTROL Compartir recursos]**.

## Compartir un recurso desde su página de vista previa {#share-asset-from-preview-page}

Ejecute los siguientes pasos para compartir un recurso mientras lo previsualiza:

1. Vaya a la página principal de [!DNL Content Hub] y haga clic en la miniatura del recurso para obtener una vista previa del recurso y mostrar las opciones de menú en el panel derecho del cuadro de diálogo.
1. Seleccione ![share](/help/assets/assets/share.svg) para mostrar el panel **[!UICONTROL Share]**.
   ![compartir recurso al previsualizarlo](/help/assets/assets/share-link-asset-preview.png)
1. Siga los pasos del 3 al 5 en la sección [Compartir recursos](#share-assets) para generar y compartir el vínculo de recursos (privados o públicos) desde este panel de **[!UICONTROL Compartir]**.

## Acceso a los recursos compartidos {#access-shared-assets}

Acceda a la página de recursos compartidos a través del vínculo y haga lo siguiente:

* Seleccione uno o más recursos y haga clic en ![descargar](/help/assets/assets/download-icon.svg) **[!UICONTROL Descargar]** para seleccionar las representaciones **[!UICONTROL Original]**, **[!UICONTROL Estática]** o ambas entre las opciones de descarga disponibles.
  ![](/help/assets/assets/download-shared-assets.png)
* Haga clic en la miniatura del recurso para ver sus metadatos.
* En la página de recursos compartidos ([a los que se accede mediante un vínculo privado](#share-assets)), haga clic en una miniatura de recurso y seleccione ![descargar](/help/assets/assets/download-icon.svg) para seleccionar y ver las representaciones dinámicas disponibles del recurso en el panel **[!UICONTROL Descargar]** antes de seleccionarlas y descargarlas.
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## Preguntas frecuentes {#faqs-share-assets-content-hub}

### ¿Qué significa compartir recursos en AEM Assets Content Hub?

Compartir recursos en AEM Assets Content Hub permite a los usuarios autorizados compartir fácilmente uno o varios recursos o colecciones completas con otros mediante la generación de un vínculo. Este vínculo se puede enviar a usuarios privados (que deben iniciar sesión) o públicos (que pueden acceder como invitados), lo que proporciona a los destinatarios acceso directo para ver y descargar los recursos seleccionados.

### ¿Cómo comparto recursos o colecciones con otros usuarios mediante AEM Assets Content Hub?

Para compartir recursos o colecciones en AEM Assets Content Hub, vaya a la página principal de Content Hub, seleccione uno o varios recursos (o vaya a la pestaña Colecciones para las colecciones) y haga clic en el icono Compartir. En el cuadro de diálogo Compartir, puede obtener una vista previa de los recursos, quitar los que sean necesarios, agregar un título y una descripción, seleccionar quién puede acceder al vínculo (privado o público), establecer un período de caducidad y, a continuación, hacer clic en Obtener vínculo para generar y copiar la dirección URL que se puede compartir. A continuación, el vínculo se puede enviar a los integrantes del equipo o a las partes interesadas.

### ¿Qué opciones de acceso están disponibles al compartir recursos en AEM Assets Content Hub y en qué se diferencian?

Content Hub permite elegir entre dos opciones de acceso para los vínculos compartidos: privado y público. Los vínculos privados requieren que los destinatarios inicien sesión en su entorno de Content Hub para ver y descargar recursos, lo que proporciona una mayor seguridad. Cualquier persona que tenga el vínculo puede acceder a los vínculos públicos sin necesidad de iniciar sesión. Cada tipo de vínculo viene con su propia configuración de caducidad, como de 24 horas a una semana para los vínculos públicos y fechas personalizadas para los vínculos privados.

### ¿Existe alguna configuración administrada por el administrador para poder generar vínculos públicos para los recursos en AEM Assets Content Hub?

Sí, los administradores pueden habilitar o deshabilitar la opción **Habilitar vínculo público** disponible en la pestaña **Colecciones y uso compartido** de la interfaz de usuario de configuración para administrar la generación de vínculos públicos para los recursos de AEM Assets Content Hub.

### ¿Puedo establecer fechas de caducidad para los vínculos de recursos compartidos en AEM Assets Content Hub y por qué es esto importante?

Sí, puede establecer fechas de caducidad para los vínculos compartidos públicos y privados en AEM Assets Content Hub. En el caso de los vínculos públicos, puede elegir entre ajustes preestablecidos de 24 horas hasta una semana, mientras que los vínculos privados le permiten seleccionar entre ajustes preestablecidos o establecer una fecha de caducidad personalizada. Las fechas de caducidad son importantes porque, una vez que caduca el vínculo, ya no se puede utilizar para acceder a los recursos o descargarlos, lo que ayuda a mantener la seguridad y el control del contenido.

### ¿Qué pueden hacer los destinatarios con el vínculo de recursos compartidos creado con AEM Assets Content Hub y hay opciones para descargar diferentes representaciones?

Los destinatarios que reciban un vínculo a un recurso compartido pueden abrirlo en su explorador para obtener una vista previa, seleccionar y descargar los recursos proporcionados. Si las representaciones de recursos están habilitadas en AEM Assets Content Hub, los destinatarios pueden elegir qué representaciones (como Original o Estático) desean descargar. Los recursos y las representaciones se descargan como un archivo zip, y los metadatos se pueden ver haciendo clic en la miniatura del recurso. El vínculo sigue funcionando hasta la fecha de caducidad establecida.




