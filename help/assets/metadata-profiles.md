---
title: Perfiles de metadatos
description: Obtenga información sobre los perfiles de metadatos para los recursos. Obtenga información sobre cómo crear un perfil de metadatos y aplicarlo a los recursos de carpeta.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: eef90c6a-b354-4342-8b97-21d067ae2979
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 21%

---

# Perfiles de metadatos {#metadata-profiles}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-config.html?lang=en) |
| AEM as a Cloud Service | Este artículo |

Un perfil de metadatos le permite aplicar metadatos predeterminados a los recursos de una carpeta. Cree un perfil de metadatos y aplíquelo a una carpeta. Cualquier recurso que cargue posteriormente en la carpeta heredará los metadatos predeterminados configurados en el perfil de metadatos.

Un concepto importante con respecto al uso de perfiles en Experience Manager Assets es que se asignan a carpetas. Dentro de un perfil hay ajustes en forma de perfiles de metadatos, junto con perfiles de vídeo o perfiles de imagen. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, el modo de asignar nombres a los archivos y carpetas, organizar las subcarpetas y administrar los archivos de estas carpetas tiene un impacto significativo en la forma en que un perfil procesa esos recursos.
Al utilizar estrategias de nomenclatura de archivos y carpetas coherentes y adecuadas, así como una buena práctica de metadatos, puede sacar el máximo partido a la colección de recursos digitales y asegurarse de que los archivos correctos se procesan mediante el perfil correcto.

## Añadir un perfil de metadatos {#adding-a-metadata-profile}

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]** y, a continuación, haga clic en **[!UICONTROL Crear]**.
1. Escriba un título para el perfil de metadatos, por ejemplo, Metadatos de muestra, y seleccione **[!UICONTROL Enviar]**. Se muestra el formulario de edición para el perfil de metadatos.
1. Haga clic en un componente y configure sus propiedades en la ficha **[!UICONTROL Configuración]**. Por ejemplo, haga clic en el componente **[!UICONTROL Description]** y edite sus propiedades.
Edite las siguientes propiedades para el componente **[!UICONTROL Description]**:

   * **[!UICONTROL Etiqueta de campo]** - El nombre para mostrar de la propiedad de metadatos. Solo es para la referencia del usuario.
   * **[!UICONTROL Asignar a propiedad]**: el valor de esta propiedad proporciona la ruta/nombre relativa al nodo de recurso donde se guarda en el repositorio. El valor siempre debe comenzar con `./` porque indica que la ruta de acceso está bajo el nodo del recurso.

     El valor que especifique para **[!UICONTROL Asignar a la propiedad]** se almacena como propiedad en el nodo de metadatos del recurso. Por ejemplo, si especifica `/jcr:content/metadata/dc:desc` como nombre de **[!UICONTROL Asignar a la propiedad]**, [!DNL Adobe Experience Manager Assets] almacena el valor `dc:desc` en el nodo de metadatos del recurso.

   * **[!UICONTROL Valor predeterminado]**: utilice esta propiedad para agregar un valor predeterminado para el componente de metadatos. Por ejemplo, si especifica &quot;Mi descripción&quot;, este valor se asigna a la propiedad `dc:desc` en el nodo de metadatos del recurso.

     >[!NOTE]
     >
     >Al agregar un valor predeterminado a una nueva propiedad de metadatos (que no existe en el nodo `/jcr:content/metadata`), no se muestra la propiedad y su valor en la página Propiedades del recurso de forma predeterminada. Para ver la nueva propiedad en la página [!UICONTROL Properties], modifique el formulario de esquema correspondiente.

1. (Opcional) Agregue más componentes a Editar formulario desde la pestaña **[!UICONTROL Generar formulario]** y configure sus propiedades en la pestaña **[!UICONTROL Configuración]**. Las siguientes propiedades están disponibles en la pestaña **[!UICONTROL Generar formulario]**:

| Componente | Propiedades |
|------------------|----------------------------------------------------|
| Encabezado de sección | Etiqueta de campo, Descripción |
| Texto de una sola línea | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Texto con varios valores | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Número | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Fecha | Etiqueta de campo, Asignar a propiedad, Valor predeterminado |
| Etiquetas estándar | Etiqueta de campo, Asignar a propiedad, Valor predeterminado, Descripción |

1. Haga clic en **[!UICONTROL Listo]**. El perfil de metadatos se agrega a la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

## Copiar un perfil de metadatos {#copying-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil de metadatos para hacer una copia del mismo.
1. Haga clic en **[!UICONTROL Copiar]** en la barra de herramientas.
1. En el diálogo **[!UICONTROL Copiar perfil de metadatos]**, escriba un título para la nueva copia del perfil de metadatos.
1. Haga clic en **[!UICONTROL Copiar]**. La copia del perfil de metadatos aparece en la lista de perfiles de la página **[!UICONTROL Perfiles de metadatos]**.

## Eliminación de un perfil de metadatos {#deleting-a-metadata-profile}

1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione un perfil para eliminar.
1. Haga clic en **[!UICONTROL Eliminar perfiles de metadatos]** en la barra de herramientas.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para confirmar la operación de eliminación. El perfil de metadatos se elimina de la lista.

## Aplicación de un perfil de metadatos a las carpetas {#applying-a-metadata-profile-to-folders}

Cuando se asigna un perfil de metadatos a una carpeta, las subcarpetas heredan automáticamente el perfil de su carpeta principal. La herencia se detiene cuando se aplica un perfil diferente a una subcarpeta. Solo puede asignar un perfil de metadatos a una carpeta. Por lo tanto, considere detenidamente la estructura de carpetas donde carga, almacena, utiliza y archiva los recursos.

Si asignó un perfil de metadatos diferente a una carpeta, el nuevo perfil anulará el perfil anterior. Los recursos de carpeta existentes anteriormente permanecen sin cambios. El nuevo perfil se aplica a los recursos que se agregan a la carpeta después del cambio. Puede aplicar perfiles de metadatos a carpetas específicas o globalmente a todos los recursos.

Las carpetas que tienen un perfil asignado se indican en la interfaz de usuario con el nombre del perfil que aparece en el nombre de la tarjeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente cambiado a posteriori. <!-- See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

### Aplicación de perfiles de metadatos a carpetas específicas {#applying-metadata-profiles-to-specific-folders}

Puede aplicar un perfil de metadatos a una carpeta desde el menú **[!UICONTROL Herramientas]** o si está en la carpeta, desde **[!UICONTROL Propiedades]**. En esta sección se describe cómo aplicar perfiles de metadatos a las carpetas de ambos modos.

Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de vídeo existente cambiado a posteriori. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

#### Aplicación de perfiles de metadatos a carpetas desde la interfaz de usuario Perfiles {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Vaya a **[!UICONTROL Herramientas > Assets > Perfiles de metadatos]**.
1. Seleccione el perfil de metadatos que desea aplicar a una o varias carpetas.
1. Haga clic en **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** y seleccione la carpeta o carpetas que desee usar para recibir los recursos cargados recientemente. A continuación, haga clic en **[!UICONTROL Listo]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

#### Aplicar perfiles de metadatos a carpetas desde Propiedades {#applying-metadata-profiles-to-folders-from-properties}

1. En el carril izquierdo, haga clic en **[!UICONTROL Assets]** y, a continuación, vaya a la carpeta a la que desee aplicar un perfil de metadatos.
1. En la carpeta, active la marca de verificación para seleccionarla y, a continuación, seleccione **Propiedades**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de metadatos]**, seleccione el perfil en el menú desplegable y haga clic en **[!UICONTROL Guardar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

### Aplicar un perfil de metadatos globalmente {#applying-a-metadata-profile-globally}

Además de aplicar un perfil a una carpeta, también puede aplicar uno de forma global para que cualquier contenido cargado en [!DNL Experience Manager Assets] en cualquier carpeta tenga aplicado el perfil seleccionado.

Puede volver a procesar los recursos en una carpeta que ya tenga un perfil de metadatos existente cambiado a posteriori. <!--See [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile). -->

**Para aplicar un perfil de metadatos globalmente, realice una de las siguientes acciones**

* Vaya a `https://[aem_server]/mnt/overlay/dam/gui/content/assets/v2/foldersharewizard.html/content/dam`, aplique el perfil adecuado y haga clic en **[!UICONTROL Guardar]**.

* Vaya a CRXDE Lite hasta el siguiente nodo: `/content/dam/jcr:content`. Agregue la propiedad `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>`. Haga clic en **Guardar todo**.

## Eliminación de perfiles de metadatos de carpetas {#removing-a-metadata-profile-from-folders}

Cuando se quita un perfil de metadatos de una carpeta, las subcarpetas heredan automáticamente la eliminación del perfil de su carpeta principal. Sin embargo, cualquier procesamiento de archivos que se haya producido dentro de las carpetas permanecerá intacto.

Puede quitar un perfil de metadatos de una carpeta desde el menú **Herramientas** o, si está en la carpeta, desde **Propiedades**. En esta sección se describe cómo quitar perfiles de metadatos de las carpetas de ambos modos.

### Eliminación de perfiles de metadatos de carpetas mediante la interfaz de usuario Perfiles {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Haga clic en el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas > Assets > Perfiles de metadatos]**.
1. Seleccione el perfil de metadatos que desea eliminar de una o varias carpetas.
1. Haga clic en **[!UICONTROL Quitar perfil de metadatos de las carpetas]**, seleccione la carpeta o carpetas que desee usar para quitar un perfil y haga clic en **[!UICONTROL Listo]**.

   Puede confirmar que el perfil de metadatos ya no se aplica a una carpeta porque el nombre ya no aparece debajo del nombre de la carpeta.

### Eliminación de perfiles de metadatos de carpetas mediante Propiedades {#removing-metadata-profiles-from-folders-via-properties}

1. Haga clic en el logotipo de Experience Manager, navegue por **[!UICONTROL Assets]** y, a continuación, vaya a la carpeta de la que desee quitar un perfil de metadatos.
1. En la carpeta, haga clic en la marca de verificación para seleccionarla y luego haga clic en **[!UICONTROL Propiedades]**.
1. Seleccione la pestaña **[!UICONTROL Perfiles de metadatos]**, seleccione **[!UICONTROL Ninguno]** en el menú desplegable y haga clic en **[!UICONTROL Guardar]**. Las carpetas que ya tienen un perfil asignado se indican mediante la visualización del nombre del perfil directamente debajo del nombre de la carpeta.

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
