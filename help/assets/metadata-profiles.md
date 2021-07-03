---
title: Perfiles de metadatos
description: Obtenga información sobre los perfiles de metadatos de los recursos. Obtenga información sobre cómo crear un perfil de metadatos y aplicarlo a los recursos de carpetas.
contentOwner: AG
feature: Metadatos
role: User,Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 20%

---

# Perfiles de metadatos {#metadata-profiles}

Un perfil de metadatos permite aplicar metadatos predeterminados a los recursos de una carpeta. Crear un perfil de metadatos y aplicarlo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta heredará los metadatos predeterminados que haya configurado en el perfil de metadatos.

## Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Metadata Profiles]** y, a continuación, haga clic en **[!UICONTROL Create]**.
1. Introduzca un título para el perfil de metadatos, por ejemplo Metadatos de ejemplo, y pulse **[!UICONTROL Enviar]**. Se muestra Editar formulario para el perfil de metadatos.
1. Haga clic en un componente y configure sus propiedades en la pestaña **[!UICONTROL Settings]**. Por ejemplo, haga clic en el componente **[!UICONTROL Description]** y edite sus propiedades.
Edite las siguientes propiedades para el componente **[!UICONTROL Description]**:

   * **[!UICONTROL Etiqueta de campo]** : el nombre para mostrar de la propiedad de metadatos. Solo es para referencia del usuario.
   * **[!UICONTROL Asignar a propiedad]** : el valor de esta propiedad proporciona la ruta/nombre relativo al nodo de recurso donde se guarda en el repositorio. El valor siempre debe comenzar por `./` porque indica que la ruta está bajo el nodo del recurso.

      El valor que especifique para **[!UICONTROL Asignar a la propiedad]** se almacena como una propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica `/jcr:content/metadata/dc:desc` como nombre de  **[!UICONTROL Asignar a propiedad]**,  [!DNL Adobe Experience Manager Assets] almacena el valor  `dc:desc` en el nodo de metadatos del recurso.

   * **[!UICONTROL Valor predeterminado]** : utilice esta propiedad para añadir un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

      >[!NOTE]
      >
      >Al agregar un valor predeterminado a una nueva propiedad de metadatos (que no existe en el nodo `/jcr:content/metadata`), no se muestra la propiedad ni su valor en la página Propiedades del recurso de forma predeterminada. Para ver la nueva propiedad en la página [!UICONTROL Properties], modifique el formulario de esquema correspondiente.

1. (Opcional) Agregue más componentes a Editar formulario desde la pestaña **[!UICONTROL Generar formulario]** y configure sus propiedades en la pestaña **[!UICONTROL Configuración]**. Las siguientes propiedades están disponibles en la pestaña **[!UICONTROL Generar formulario]**:

| Componente | Propiedades |
|------------------|----------------------------------------------------|
| Sección de encabezado | Etiqueta de campo, descripción |
| Texto de una sola línea | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Texto con varios valores | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Número | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Fecha | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Etiquetas estándar | Etiqueta de campo, Asignar a propiedad, Valor predeterminado, Descripción |

1. Haga clic en **[!UICONTROL Listo]**. El perfil de metadatos se agrega a la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

## Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil de metadatos para realizar una copia de él.
1. Haga clic en **[!UICONTROL Copiar]** en la barra de herramientas.
1. En el cuadro de diálogo **[!UICONTROL Copiar perfil de metadatos]**, introduzca un título para la nueva copia del perfil de metadatos.
1. Haga clic en **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

## Eliminación de un perfil de metadatos {#deleting-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil que desee eliminar.
1. Haga clic en **[!UICONTROL Eliminar perfiles de metadatos]** en la barra de herramientas.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Delete]** para confirmar la operación de eliminación. El perfil de metadatos se elimina de la lista.

## Aplicar un perfil de metadatos a las carpetas {#applying-a-metadata-profile-to-folders}

Al asignar un perfil de metadatos a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. La herencia se detiene cuando se aplica un perfil diferente a una subcarpeta. Solo puede asignar un perfil de metadatos a una carpeta. Por lo tanto, considere detenidamente la estructura de carpetas en la que carga, almacena, utiliza y archiva recursos.

Si ha asignado un perfil de metadatos diferente a una carpeta, el nuevo perfil anula el perfil anterior. Los recursos de carpeta existentes no cambian. El nuevo perfil se aplica a los recursos que se agregan a la carpeta después del cambio. Puede aplicar perfiles de metadatos a carpetas específicas o globalmente a todos los recursos.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario por el nombre del perfil que aparece en el nombre de la tarjeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente que haya cambiado posteriormente. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Aplicación de perfiles de metadatos a carpetas específicas {#applying-metadata-profiles-to-specific-folders}

Puede aplicar un perfil de metadatos a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de metadatos a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente que haya cambiado posteriormente. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Aplicación de perfiles de metadatos a carpetas desde la interfaz de usuario Perfiles {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Vaya a **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Seleccione el perfil de metadatos que desea aplicar a una o varias carpetas.
1. Haga clic en **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para recibir los recursos cargados recientemente y haga clic en **[!UICONTROL Listo]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicación de perfiles de metadatos a carpetas desde Propiedades {#applying-metadata-profiles-to-folders-from-properties}

1. En el carril izquierdo, haga clic en **[!UICONTROL Assets]** y vaya a la carpeta a la que desee aplicar un perfil de metadatos.
1. En la carpeta, haga clic o haga clic en la marca de verificación para seleccionarla y, a continuación, haga clic o haga clic en **Properties**.
1. Seleccione la pestaña **[!UICONTROL Metadata Profiles]** , seleccione el perfil en el menú desplegable y haga clic en **[!UICONTROL Save]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

### Aplicar un perfil de metadatos globalmente {#applying-a-metadata-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicarlo de forma global para que cualquier contenido cargado en [!DNL Experience Manager Assets] en cualquier carpeta tenga aplicado el perfil seleccionado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente que haya cambiado posteriormente. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Para aplicar un perfil de metadatos globalmente, realice una de las siguientes acciones:**

* Vaya a `https://<AEM server>/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`, aplique el perfil adecuado y haga clic en **Guardar**.

* Vaya al CRXDE Lite al nodo siguiente: `/content/dam/jcr:content`. Agregue la propiedad `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Haga clic en **Guardar todo**.

## Eliminación de perfiles de metadatos de carpetas {#removing-a-metadata-profile-from-folders}

Al quitar un perfil de metadatos de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanece intacto.

Puede quitar un perfil de metadatos de una carpeta desde el menú **Herramientas** o, si está en la carpeta, desde **Propiedades**. En esta sección se describe cómo quitar perfiles de metadatos de las carpetas de ambos modos.

### Eliminación de perfiles de metadatos de carpetas mediante la interfaz de usuario de Perfiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Haga clic en el logotipo de AEM y vaya a **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. Seleccione el perfil de metadatos que desea eliminar de una carpeta o varias carpetas.
1. Haga clic en **[!UICONTROL Quitar perfil de metadatos de las carpetas]** y seleccione la carpeta o carpetas que desee utilizar para quitar un perfil y haga clic en **[!UICONTROL Listo]**.

   Puede confirmar que el perfil de metadatos ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de metadatos de carpetas mediante Propiedades {#removing-metadata-profiles-from-folders-via-properties}

1. Haga clic en el logotipo de AEM y vaya a **[!UICONTROL Assets]** y, a continuación, a la carpeta desde la que desea eliminar un perfil de metadatos.
1. En la carpeta, haga clic en la marca de verificación para seleccionarla y, a continuación, haga clic en **[!UICONTROL Properties]**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de metadatos]**, seleccione **[!UICONTROL Ninguno]** en el menú desplegable y haga clic en **[!UICONTROL Guardar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.
