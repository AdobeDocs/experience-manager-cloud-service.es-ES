---
title: Aprobar recursos en Experience Manager
description: Obtenga información sobre cómo aprobar recursos en  [!DNL Experience Manager].
role: User
exl-id: fe61a0f1-94d3-409a-acb9-195979668c25
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 7%

---

# Aprobar recursos en [!DNL Experience Manager]

Los responsables de marca y los especialistas en marketing mantienen un control estricto sobre los recursos de marca. Solo está disponible la versión aprobada y más reciente del recurso para su uso, lo que garantiza la coherencia de marca en todos los canales y aplicaciones.

Puede aprobar recursos en AEM Assets para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente para administrarlos.

## Antes de empezar {#pre-requisites}

Debe tener acceso al as a Cloud Service de AEM Assets y permisos para editar la propiedad **[!UICONTROL Estado de revisión]** de un recurso.

## Configuración

Debe realizar una actualización única del esquema de metadatos aplicable en la vista de administrador para poder aprobar un recurso. Puede omitir esta configuración para la vista de Assets. Siga estos pasos para configurar el esquema de metadatos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Seleccione el esquema de metadatos aplicable y haga clic en **[!UICONTROL Editar]**. <br>El **[!UICONTROL Editor de formularios de esquemas de metadatos]** se abre con la ficha **[!UICONTROL Básico]** resaltada.
1. Desplácese hacia abajo y haga clic en **[!UICONTROL Estado de revisión]**.
1. Haga clic en la ficha **[!UICONTROL Reglas]** en el panel derecho.
1. Desmarque **[!UICONTROL Deshabilitar edición]**.
Si necesita ver la propiedad a la que está asignado el campo **[!UICONTROL Estado de revisión]**, vaya a la pestaña **[!UICONTROL Configuración]** y vea el valor `./jcr:content/metadata/dam:status` en el campo **[!UICONTROL Asignar a propiedad]**.
1. Arrastre y suelte un campo **[!UICONTROL Dropdown]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** a _Destino de aprobación_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:activationTarget_.
   1. Agregue las opciones con `contenthub` y `delivery` como valores de opción.

   >[!NOTE]
   >
   >Al seleccionar el objetivo de aprobación como Content Hub mediante la vista de Assets, los recursos están disponibles en Content Hub para los usuarios que forman parte de la misma organización. Al seleccionar el objetivo de aprobación como Envío, los recursos están disponibles para todos los usuarios.

1. Haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Si los recursos o carpetas tienen un esquema predeterminado diferente, asegúrese de realizar esta actualización en ese esquema en particular.

## Aprobación de recursos {#approve-assets}

Para aprobar recursos en [!DNL Experience Manager Admin view], siga estos pasos:

1. Seleccione los recursos y haga clic en **[!UICONTROL Propiedades]** en el panel superior.
1. En la ficha **[!UICONTROL Básico]**, desplácese hacia abajo hasta **[!UICONTROL Estado de revisión]**.
1. Cambiar el estado de revisión a **[!UICONTROL Aprobado]**.
   ![imagen](/help/assets/assets/approve-old-ui.png)
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Del mismo modo, puede aprobar recursos con la [nueva vista de Assets](/help/assets/manage-organize-assets-view.md).

## Aprobar recursos de forma masiva {#bulk-approve-assets}

Optimice su flujo de trabajo aprobando rápidamente varios recursos a la vez. Puede aprobar recursos de forma masiva para acelerar el proceso de aprobación, lo que ahorra tiempo y mejora la productividad.
<br>Siga estos pasos para aprobar recursos en bloque en [!DNL Experience Manager Admin view]:

1. Cree una carpeta en el entorno de creación (https://author-pXXX-eYYY.adobeaemcloud.com). Reemplace _XXX_ con su ID de programa y _AAAA_ con el ID de entorno de Experience Manager.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]**.
1. Haga clic en **[!UICONTROL Crear]** en la parte superior derecha de la página.
1. Agregue un título de perfil y haga clic en **[!UICONTROL Crear]**. El perfil de metadatos se ha creado correctamente.
1. Seleccione el perfil de metadatos recién creado y haga clic en **[!UICONTROL Editar _(e)_]**. <br>El formulario **[!UICONTROL Editar perfil de metadatos]**&#x200B;se abre con la ficha **[!UICONTROL Básico]**&#x200B;resaltada.
1. Arrastre y suelte un **[!UICONTROL campo de texto de una sola línea]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** por _Assets aprobado_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:status_.
   1. Cambie el valor predeterminado a _aprobado_.

1. Arrastre y suelte un campo **[!UICONTROL Dropdown]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** a _Destino de aprobación_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:activationTarget_.
   1. Agregue las opciones con `contenthub` y `delivery` como valores de opción.

   >[!NOTE]
   >
   >Al seleccionar el objetivo de aprobación como Content Hub mediante la vista de Assets, los recursos están disponibles en Content Hub para los usuarios que forman parte de la misma organización. Al seleccionar el objetivo de aprobación como Envío, los recursos están disponibles para todos los usuarios.
1. Haga clic en **[!UICONTROL Guardar]**.
1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione el perfil de metadatos recién creado.
1. Haga clic en **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** desde la barra de acciones superior.
1. Seleccione las carpetas que necesita aprobar y haga clic en **[!UICONTROL Aplicar]**.
   <br>: el permiso para toda la carpeta está establecido para su aprobación y todos los recursos cargados en esta carpeta se aprueban automáticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Este método aprueba los recursos recién creados en la carpeta. Para los recursos existentes en la carpeta, debe seleccionarlos y aprobarlos manualmente. <br> También puede usar la opción **[!UICONTROL Reprocesar]** para aplicar los cambios del perfil de metadatos a los recursos más antiguos.

Del mismo modo, para aprobar recursos de forma masiva dentro de una carpeta en la vista Assets:

1. Seleccione los recursos y haga clic en **[!UICONTROL Edición masiva de metadatos]**.

1. Seleccione **[!UICONTROL Aprobado]** en el campo **[!UICONTROL Estado]** disponible en la sección [!UICONTROL Propiedades] del panel derecho.

   Si selecciona el estado como `Approved` y si [Dynamic Media con capacidades OpenAPI](/help/assets/dynamic-media-open-apis-overview.md), [Content Hub](/help/assets/product-overview.md) o ambos están habilitados para su Experience Manager Assets, puede ver las opciones `Delivery` y `Content Hub` disponibles en el campo **[!UICONTROL Destino de aprobación]**.

   * Seleccione **[!UICONTROL Delivery]** para que los recursos estén disponibles tanto para Dynamic Media con las capacidades de OpenAPI como para Content Hub. Si no tiene Content Hub habilitado, al seleccionar esta opción los recursos estarán disponibles para Dynamic Media únicamente con funciones de OpenAPI.
   * Seleccione **[!UICONTROL Content Hub]** para que los recursos estén disponibles para Content Hub.

   ![Estado de aprobación](/help/assets/assets/approval-status-delivery.png)

   Si no usa el formulario de metadatos predeterminado y no puede ver el campo **[!UICONTROL Destino de aprobación]**, [edite el formulario de metadatos](/help/assets/metadata-assets-view.md#metadata-forms) para arrastrar el campo **[!UICONTROL Aprobación para]** desde los componentes disponibles hasta el formulario de metadatos y haga clic en **[!UICONTROL Guardar]**.

   >[!NOTE]
   >
   >Si selecciona el destino de aprobación como `Content Hub` mediante la vista de Assets dentro de una organización, los recursos estarán disponibles en Content Hub para los usuarios que formen parte de la misma organización.

1. Haga clic en **[!UICONTROL Guardar]**.

## Copiar la URL de envío para los recursos aprobados {#copy-delivery-url-approved-assets}

La URL de entrega de todos los recursos aprobados en el repositorio está disponible si tiene [!UICONTROL Dynamic Media con las capacidades de OpenAPI] habilitadas en la instancia de AEM as a Cloud Service.

Para copiar la URL de envío de un recurso aprobado dentro del repositorio:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]**.

1. Haga clic en el icono Dynamic Media disponible en el panel derecho.

1. Seleccione **[!UICONTROL Dynamic Media con OpenAPI]** disponible en el panel **[!UICONTROL Dynamic Media]**.

1. Haga clic en **[!UICONTROL Copiar URL]** para copiar la URL de envío del recurso.
   ![representaciones dinámicas](/help/assets/assets/dm-with-openapi-non-image-assets.png)

   >[!NOTE]
   >
   >La opción para copiar la URL de envío para los recursos aprobados solo está disponible en la vista de Assets.

Para obtener información sobre otras representaciones que se muestran en el panel Dynamic Media, consulte [Ver y descargar representaciones de Dynamic Media](/help/assets/renditions.md#view-download-dm-renditions).
