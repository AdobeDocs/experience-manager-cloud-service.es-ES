---
title: Configuración de la interfaz de usuario de Content Hub
description: Configuración de la interfaz de usuario de Content Hub
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 5%

---

# Configuración de la interfaz de usuario de Content Hub {#configure-content-hub-user-interface}

<!-- ![Download assets](assets/download-asset.jpg) -->
![Configuración de recursos en Content Hub](assets/configure-assets.png)

Experience Manager Assets permite a los administradores configurar las opciones disponibles en la interfaz de usuario de Content Hub. En función de las opciones de configuración seleccionadas por los administradores, los usuarios de Content Hub pueden ver los campos en Content Hub. Las opciones de configuración incluyen:

* Filtros disponibles para los usuarios al buscar recursos.

* Detalles o propiedades del recurso disponibles para cada recurso.

* Campos de metadatos disponibles para los usuarios al añadir recursos a Content Hub.

* Campos de metadatos de recursos que están disponibles para la búsqueda en Content Hub.

* Contenido de marca que debe mostrar para su organización.

* Cualquier vínculo personalizado que necesite incluir en Content Hub, además de los recursos, las colecciones y las perspectivas.

## Requisitos previos {#prerequisites-configuration-ui}

[Administradores de Content Hub](/help/assets/deploy-content-hub.md#step-3-onboard-content-hub-administrator) Puede establecer las opciones de configuración para otros usuarios de su organización.

## Acceso a las opciones de configuración en Content Hub {#access-configuration-options-content-hub}

Para acceder a las opciones de configuración de Content Hub:

1. Haga clic en el icono de usuario en el panel derecho.

1. En el **[!UICONTROL Configuración del producto]** , seleccione **[!UICONTROL Configuraciones]**.

   ![Acceso a las opciones de configuración en Content Hub](assets/access-content-hub-configuration-ui.png)

## Administrar las opciones de configuración en Content Hub {#manage-configuration-options}

Administre las siguientes opciones de configuración para los usuarios:

* [Importar](#configure-import-options-content-hub)

* [Filtros](#configure-filters-content-hub)

* [Detalles del recurso](#configure-asset-details-content-hub)

* [Búsqueda](#configure-metadata-search-content-hub)

* [Personalización de marca](#configure-branding-content-hub)

* [Vínculos personalizados](#configure-custom-links-content-hub)

### Importar {#configure-import-options-content-hub}

Puede configurar los campos de metadatos que se muestran a los usuarios al cargar o importar recursos en el portal de Content Hub como, por ejemplo, Nombre de campaña, Palabras clave, Canales, Periodo de tiempo, Región, etc. Para ello, ejecute los siguientes pasos:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Importar]**.

1. Clic **[!UICONTROL Añadir metadatos]**.

1. Especifique una etiqueta para la propiedad, asígnela a una propiedad mediante el **[!UICONTROL Metadatos]** y seleccione el tipo de entrada para los nuevos metadatos del recurso.

1. Haga clic en **[!UICONTROL Campo obligatorio]** active esta opción para que el nuevo campo de metadatos sea obligatorio para especificar usuarios mientras cargan nuevos recursos.

1. Clic **[!UICONTROL Confirmar]**. Los nuevos metadatos se muestran en la lista de las propiedades de recursos existentes.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios.

Igualmente, puede hacer clic en ![Icono Editar](assets/do-not-localize/edit_icon.svg), disponible junto a cada propiedad disponible, para editar las etiquetas, haga que estos campos sean obligatorios o no obligatorios para los usuarios al cargar recursos mediante **[!UICONTROL Campo obligatorio]** o haga clic en el icono Eliminar para eliminar cualquier propiedad de metadatos.

Haga clic en **[!UICONTROL Aprobación automática]** alterne si necesita que todos los recursos que agregue al repositorio de Experience Manager Assets se aprueben automáticamente para que estén disponibles en Content Hub inmediatamente. De lo contrario, los autores o administradores de DAM deben aprobar manualmente los recursos para que estén disponibles en Content Hub. De forma predeterminada, la opción está desactivada.

Clic **[!UICONTROL Guardar]** después de realizar todas las modificaciones para aplicar los cambios.

![Detalles de carga de IU de configuración en Content Hub](assets/configuration-ui-upload-details.png)

Los metadatos activados en la interfaz de usuario de configuración se muestran en la página de carga de recursos:

![Carga de metadatos en Content Hub](assets/configuration-ui-add-assets.png)

### Filtros {#configure-filters-content-hub}

Content Hub permite a los administradores configurar filtros que se muestran al buscar recursos. Siga estos pasos para agregar un nuevo filtro:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Filtros]**.

1. Clic **[!UICONTROL Añadir filtros]**.

1. Especifique una etiqueta para el filtro y asígnelo a una propiedad mediante la variable **[!UICONTROL Metadatos]** y seleccione el tipo de entrada para el nuevo filtro.
1. Clic **[!UICONTROL Confirmar]**. El nuevo filtro se muestra en la lista de los filtros existentes.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios de modo que el nuevo filtro se muestre en la página Buscar al filtrar los recursos.

   >[!NOTE]
   >
   >El nuevo filtro se muestra en la página Buscar solo si hay al menos un recurso en el repositorio que coincida con los criterios de filtro.

Igualmente, puede hacer clic en ![Icono Editar](assets/do-not-localize/edit_icon.svg), disponible junto a cada filtro disponible, para editar las etiquetas o haga clic en el icono eliminar para eliminar cualquier filtro existente. Clic **[!UICONTROL Guardar]** después de realizar todas las modificaciones para aplicar los cambios.

![Filtros de IU de configuración en Content Hub](assets/configuration-ui-filters.png)

Los filtros activados en la interfaz de usuario de configuración se muestran en la página Buscar:

![Buscar en Content Hub](assets/filters-for-search.png)


### Detalles del recurso {#configure-asset-details-content-hub}

También puede configurar las propiedades del recurso que se muestran para cada recurso, como el nombre de archivo, el título, el formato, el tamaño, etc. Para ello, ejecute los siguientes pasos:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Detalles del recurso]**.

1. Clic **[!UICONTROL Añadir metadatos]**.

1. Especifique una etiqueta para la propiedad, asígnela a una propiedad mediante el **[!UICONTROL Metadatos]** y seleccione el tipo de entrada para los nuevos metadatos del recurso.
1. Clic **[!UICONTROL Confirmar]**. Los nuevos metadatos se muestran en la lista de las propiedades de recursos existentes.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios de modo que la nueva propiedad se muestre en la página detalles del recurso.

Igualmente, puede hacer clic en ![Icono Editar](assets/do-not-localize/edit_icon.svg), disponible junto a cada propiedad disponible, para editar las etiquetas o hacer clic en el icono Eliminar para eliminar cualquier detalle de recurso existente. Clic **[!UICONTROL Guardar]** después de realizar todas las modificaciones para aplicar los cambios.

![Detalles del recurso de la IU de configuración en Content Hub](assets/configuration-ui-asset-details.png)

Las propiedades activadas en la interfaz de usuario de configuración se muestran en la página Detalles del recurso:

![Propiedades del recurso en Content Hub](assets/config-ui-asset-properties.png)

### Búsqueda {#configure-metadata-search-content-hub}

Los administradores pueden definir los campos de metadatos que se buscan cuando un usuario especifica criterios de búsqueda en Content Hub. Ejecute los siguientes pasos:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Añadir metadatos]**.

1. Especifique el campo de metadatos y haga clic en **[!UICONTROL Confirmar]**.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios de modo que la nueva propiedad de metadatos se muestre en la lista de campos de metadatos.

Igualmente, puede hacer clic en ![Icono Editar](assets/do-not-localize/edit_icon.svg), disponible junto a cada propiedad de metadatos disponible, para editar la propiedad o haga clic en el icono Eliminar para eliminar cualquier propiedad existente. Clic **[!UICONTROL Guardar]** después de realizar todas las modificaciones para aplicar los cambios.

![Búsqueda de IU de configuración en Content Hub](assets/configuration-ui-metadata-search.png)


### Personalización de marca {#configure-branding-content-hub}

Los administradores también pueden personalizar el título y el texto del cuerpo en el banner del portal de Content Hub, según sus requisitos de marca. Para ello, ejecute los siguientes pasos:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Marca]**.

1. Especificar texto en **[!UICONTROL Texto del título del titular]** y **[!UICONTROL Texto del cuerpo en el titular]** campos.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios.

![Personalización de la IU de configuración en Content Hub](assets/configuration-ui-branding.png)

Las actualizaciones de marca habilitadas en la interfaz de usuario de configuración se muestran en el banner del portal de Content Hub:

![Personalización de la IU de configuración en Content Hub](assets/configuration-ui-branding-updates.png)

### Vínculos personalizados {#configure-custom-links-content-hub}

También puede agregar pestañas personalizadas además de las estándar **[!UICONTROL Todos los Assets]**, **[!UICONTROL Colecciones]**, y **[!UICONTROL Insights]** en el portal de Content Hub, justo debajo del titular. Para ello, ejecute los siguientes pasos:

1. En el [Configuraciones](#access-configuration-options-content-hub) interfaz de usuario, haga clic en **[!UICONTROL Vínculos personalizados]**.

1. Clic **[!UICONTROL Añadir vínculo]**.

1. Especificar texto en **[!UICONTROL Etiqueta]** y **[!UICONTROL URL]** campos. La etiqueta que defina se mostrará como una pestaña y, al hacer clic en la etiqueta, navegará a la dirección URL definida en la **[!UICONTROL URL]** field.

1. Clic **[!UICONTROL Confirmar]**.

1. Clic **[!UICONTROL Guardar]** para aplicar los cambios.

Igualmente, puede hacer clic en ![Icono Editar](assets/do-not-localize/edit_icon.svg), disponible junto a cada URL, para editar los vínculos o haga clic en el icono Eliminar para eliminar cualquier URL existente. Clic **[!UICONTROL Guardar]** después de realizar todas las modificaciones para aplicar los cambios.

![Vínculos personalizados de la IU de configuración en Content Hub](assets/configuration-ui-custom-links.png)

El vínculo personalizado se muestra como una nueva pestaña junto a la pestaña Información en la página de inicio de Content Hub.

![Fichas de vínculos personalizados de la IU de configuración en Content Hub](assets/configuration-ui-custom-link-tab.png)


