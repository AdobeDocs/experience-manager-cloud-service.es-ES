---
title: Aprobación de recursos para Content Hub
description: Obtenga información sobre cómo aprobar recursos en Assets as a Cloud Service para que estén disponibles en Content Hub.
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: 59f97fc6ded4274c27400f56b50b4a3329cc471a
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 11%

---

# Aprobación de recursos para Content Hub {#approve-assets-content-hub}

![Aprobar recursos para Content Hub](assets/content-hub-approve-assets.png)

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Los responsables de marca y los especialistas en marketing mantienen un control estricto sobre los recursos de marca. Solo la versión aprobada y más reciente del recurso está disponible para su uso en Content Hub, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

Puede aprobar recursos con AEM Assets as a Cloud Service para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente para la administración de recursos.

## Antes de empezar {#pre-requisites}

Antes de empezar, debería tener:

* Acceso a AEM Assets as a Cloud Service

* Permisos de escritura para editar metadatos de recursos a fin de poder editar el campo **[!UICONTROL Estado]** disponible en [propiedades de recursos](/help/assets/manage-organize-assets-view.md##manage-asset-status) para un recurso.

## Aprobación de recursos para Content Hub{#approve-assets-for-content-hub}

Los recursos marcados como `approved` en Assets as a Cloud Service están disponibles automáticamente en Content Hub.

>[!NOTE]
>
>Assets as a Cloud Service y Content Hub deben utilizar la misma organización para que los recursos se muestren en Content Hub.

Para establecer el estado del recurso como `approved` mediante la vista de Assets en AEM as a Cloud Service:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]** en la barra de herramientas.

1. En la ficha **[!UICONTROL Básico]**, seleccione el estado del recurso como `approved` en la lista desplegable **[!UICONTROL Estado]**.
1. Haga clic en **[!UICONTROL Guardar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3433172)

Si necesita aprobar recursos con la vista de administrador, consulte [Aprobar recursos con la vista de administrador](/help/assets/approve-assets.md#approve-assets).

## Aprobación masiva de recursos para Content Hub mediante la vista de Assets {#bulk-approve-assets-content-hub}

Aprobación masiva de recursos mediante la vista de Assets para AEM Assets de as a Cloud Service. Todos los recursos, aprobados de forma masiva, estarán disponibles en Content Hub.

Para aprobar recursos de forma masiva dentro de una carpeta en la vista Assets:

1. Seleccione los recursos y haga clic en **[!UICONTROL Edición masiva de metadatos]**.

1. Seleccione **[!UICONTROL Aprobado]** en el campo **[!UICONTROL Estado]** disponible en la sección [!UICONTROL Propiedades] del panel derecho.

1. Haga clic en **[!UICONTROL Guardar]**.

## Definir destino de aprobación {#set-approval-target}

La vista de Assets le permite publicar recursos aprobados en Dynamic Media con capacidades de OpenAPI, Content Hub o ambas en función del valor establecido en el campo **Destino de aprobación** disponible en la página Detalles del recurso.

Para establecer el objetivo de aprobación:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]** en la barra de herramientas.

1. En la ficha **[!UICONTROL Básico]**, seleccione el estado del recurso en la lista desplegable **[!UICONTROL Estado]**. Los valores posibles incluyen Aprobado, Rechazado y Sin estado (predeterminado).

1. Si selecciona **Aprobado** en el paso 2, seleccione un destino de aprobación. Los valores posibles incluyen Delivery y Content Hub.

   * **Delivery** es la opción predeterminada seleccionada en el menú desplegable y publica el recurso en [Dynamic Media con OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) y [Content Hub](/help/assets/product-overview.md), si ambos están habilitados para Experience Manager Assets.

   * Al seleccionar **Content Hub**, se publica el recurso en Content Hub. Content Hub solo se muestra como opción si está habilitado para Experience Manager Assets.

   * Si no selecciona una opción en la lista desplegable, la opción predeterminada habilitada para su entorno de AEM as a Cloud Service se aplica automáticamente al recurso.


   Para obtener más información sobre las opciones disponibles, consulte [Destino de aprobación predeterminado y destinos de publicación para recursos aprobados](#default-approval-target-options-publish-destinations).

   ![Estado de aprobación](/help/assets/assets/approval-status-delivery.png)

1. Especifique otras propiedades del recurso y haga clic en **[!UICONTROL Guardar]**.

Otros puntos que hay que tener en cuenta son:

* Si no usa el formulario de metadatos predeterminado y no puede ver el campo **[!UICONTROL Destino de aprobación]**, [edite el formulario de metadatos](/help/assets/metadata-assets-view.md#metadata-forms) para arrastrar el campo **[!UICONTROL Aprobación para]** desde los componentes disponibles hasta el formulario de metadatos y haga clic en **[!UICONTROL Guardar]**.

* Al seleccionar el destino de aprobación como `Content Hub` mediante la vista de Assets, los recursos se ponen a disposición de los usuarios de Content Hub que forman parte de la misma organización.

### Destinos de aprobación predeterminados y destinos de publicación para recursos aprobados {#default-approval-target-options-publish-destinations}

La siguiente tabla ilustra los requisitos previos para la visualización de la lista desplegable `Approval Target` y el objetivo de aprobación predeterminado en función de la habilitación de DM con OpenAPI y Content Hub en el entorno de AEM as a Cloud Service:

| Dynamic Media con OpenAPI | Content Hub | ¿Se muestra la lista desplegable Destino de aprobación? | Destino de aprobación predeterminado para recursos aprobados | Destino de publicación |
| --- | --- | --- | --- |---|
| Habilitado | Habilitado | Sí | Entrega | Dynamic Media con OpenAPI y Content Hub |
| No disponible | Habilitado | Sí | Content Hub | Content Hub |
| Habilitado | No disponible | Sí | Entrega | Dynamic Media con OpenAPI |
| No disponible | No disponible | No | N/D | N/D |

## Automatice la aprobación de los recursos recién ingeridos en la vista de administración {#automate-approval-newly-ingested-assets}

Después de cambiar de la vista de Assets a la vista de Administración, puede establecer la configuración de la carpeta para que todos los recursos nuevos agregados a la carpeta se aprueben automáticamente.

Puede cambiar entre las vistas Administración y Assets de las siguientes maneras:
![Información general de Mi Workspace](assets/assets-view.png)

Siga estos pasos para automatizar la aprobación de los recursos recién ingeridos en [!DNL Experience Manager Admin view]:

1. Cree una carpeta en el entorno de creación (https://author-pXXX-eYYY.adobeaemcloud.com). Reemplace _XXX_ con su ID de programa y _AAAA_ con el ID de entorno de Experience Manager.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]**.
1. Haga clic en **[!UICONTROL Crear]** en la parte superior derecha de la página.
1. Agregue un título de perfil y haga clic en **[!UICONTROL Crear]**. El perfil de metadatos se ha creado correctamente.
1. Seleccione el perfil de metadatos recién creado y haga clic en **[!UICONTROL Editar _(e)_]**. <br>El formulario **[!UICONTROL Editar perfil de metadatos]**&#x200B;se abre con la ficha **[!UICONTROL Básico]**&#x200B;resaltada.
1. Arrastre y suelte un **[!UICONTROL campo de texto de una sola línea]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** por _Assets aprobado_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam :status_.
   1. Cambie el valor predeterminado a _aprobado_.

1. De forma similar al paso 6, arrastre un **[!UICONTROL campo de texto de una sola línea]** desde la sección **[!UICONTROL Generar formulario]** a la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** a _Destino de activación_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam :activationTarget_.
   1. Cambie el valor predeterminado a _contenthub_.

1. Haga clic en **[!UICONTROL Guardar]**.
1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione el perfil de metadatos recién creado.
1. Haga clic en **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** desde la barra de acciones superior.
1. Seleccione las carpetas que necesita aprobar y haga clic en **[!UICONTROL Aplicar]**.
   <br>: el permiso para toda la carpeta está establecido para su aprobación y todos los recursos cargados en esta carpeta se aprueban automáticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Este método aprueba los recursos recién creados en la carpeta. Para los recursos existentes en la carpeta, debe seleccionarlos y aprobarlos manualmente.

## Administración de recursos cargados mediante Content Hub {#manage-assets-uploaded-using-content-hub}

[Los usuarios de Content Hub con derechos para agregar recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) pueden [agregar recursos a Content Hub](/help/assets/upload-brand-approved-assets.md) desde el sistema de archivos local o importar recursos desde fuentes de datos de OneDrive o Dropbox. Todos los recursos se muestran en el nivel superior en Content Hub, independientemente de la estructura de carpetas disponible en el sistema de archivos local o en las fuentes de datos de OneDrive y Dropbox, para mejorar las funciones de búsqueda.

La visualización de los recursos cargados mediante Content Hub depende de si ha [habilitado la opción de aprobación automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Si la opción **[!UICONTROL Aprobación automática]** está habilitada, los recursos que cargue mediante Content Hub estarán disponibles automáticamente.

* Si la opción **[!UICONTROL Aprobación automática]** está deshabilitada, los recursos que cargue mediante Content Hub no se mostrarán automáticamente. Los recursos están disponibles en la carpeta `hydrated-assets` de su entorno de Assets as a Cloud Service. Vaya a la carpeta y [edite en lotes](#bulk-approve-assets-content-hub) el estado de esos recursos a `Approved` para que se muestren en Content Hub.

![Proceso de aprobación de Content Hub](/help/assets/assets/content-hub-approval.png)

## Preguntas frecuentes {#faqs-content-hub-approved-assets}

### ¿Cuál es el propósito de aprobar recursos para AEM Assets Content Hub en Experience Manager as a Cloud Service? {#approving-assets-content-hub}

La aprobación de recursos garantiza que solo las versiones más recientes y aprobadas estén disponibles para su uso en AEM Assets Content Hub, manteniendo una estricta coherencia de marca en todos los canales y aplicaciones. Este proceso controlado optimiza la administración de recursos para los administradores de marca y los especialistas en marketing.

### ¿Cuáles son los requisitos previos necesarios para aprobar recursos para AEM Assets Content Hub?

Debe tener acceso a as a Cloud Service de AEM Assets y permisos de escritura para editar metadatos de recursos, específicamente el campo **Estado** en las propiedades del recurso.

### ¿Cómo se aprueba un solo recurso con la vista Assets en AEM as a Cloud Service para que esté disponible en AEM Assets Content Hub?

Seleccione el recurso, haga clic en **Detalles** en la barra de herramientas, vaya a la pestaña **Básico**, elija **Aprobado** en la lista desplegable **Estado** y haga clic en **Guardar**. El recurso está disponible en AEM Assets Content Hub.

### ¿Pueden aprobarse los recursos por lotes para AEM Assets Content Hub y, si es así, cómo?

Sí, los recursos se pueden aprobar por lotes. En la vista de Assets, seleccione varios recursos, haga clic en **Edición masiva de metadatos**, seleccione **Aprobado** en el campo **Estado** en Propiedades y haga clic en **Guardar**. Todos los recursos seleccionados están disponibles en Content Hub de AEM Assets.

### ¿Cómo funciona el proceso de aprobación de recursos en AEM Assets Content Hub? {#asset-approval-content-hub}

Si la opción Auto-approval está activada, los recursos cargados mediante AEM Assets Content Hub están disponibles automáticamente. Si está desactivado, los recursos cargados se colocan en la carpeta **hydroassets** de Assets as a Cloud Service y debe editar manualmente su estado en **Aprobado** para que se muestren en Content Hub.

### ¿Qué es el campo Destino de aprobación en la vista de AEM Assets y cómo afecta a la publicación de recursos?

El campo **Destino de aprobación** de la página Detalles del recurso le permite elegir dónde se publican los recursos aprobados. Las opciones incluyen **Envío** (publica en Dynamic Media con OpenAPI y Content Hub) o solo **Content Hub**. Si no se selecciona ninguna opción, se aplica la predeterminada para el entorno de as a Cloud Service de Assets. Consulte [Destinos de aprobación predeterminados y destinos de publicación para recursos aprobados](#default-approval-target-options-publish-destinations) para obtener más información.


### ¿Qué sucede si no ve el campo Destino de aprobación en la página AEM Assets: ver detalles del recurso?

Si falta el campo **Destino de aprobación** en la página de detalles del recurso de vista de Assets, debe editar el formulario de metadatos, arrastrar el campo **Aprobación para** desde los componentes disponibles hasta el formulario y hacer clic en **Guardar**. Esto le permite establecer objetivos de aprobación para los recursos.

### ¿Cómo se puede automatizar la aprobación de los recursos recién ingeridos en la vista de administración de AEM Assets?

Cree una carpeta en el entorno de creación, vaya a **Herramientas** > **Assets** > **Perfiles de metadatos**, y cree y edite un perfil de metadatos. Agregue un campo de texto de una sola línea, etiquete **Aprobado por Assets** y asígnelo a &#39;./jcr:content/metadata/dam:status&#39; y establezca su valor predeterminado en `approved`. Aplicar el perfil de metadatos a la carpeta. Esto aprueba automáticamente los nuevos recursos agregados a la carpeta.

### ¿Quién puede acceder a los recursos aprobados en AEM Assets Content Hub y qué controles existen?

Los recursos aprobados están disponibles para los usuarios que forman parte de la misma organización en AEM Assets Content Hub. Los estrictos controles garantizan que solo se pueda acceder a las versiones más recientes y aprobadas, lo que ayuda a mantener la coherencia y seguridad de la marca.
