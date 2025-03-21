---
title: Aprobación de recursos para Content Hub
description: Obtenga información sobre cómo aprobar recursos en Assets as a Cloud Service para que estén disponibles en Content Hub.
exl-id: fc849028-ab56-4388-b8d6-e36cac8f868f
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 20%

---

# Aprobación de recursos para Content Hub {#approve-assets-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

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
Assets as a Cloud Service y Content Hub deben utilizar la misma organización para que los recursos se muestren en Content Hub.

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

## Automatice la aprobación de los recursos recién ingeridos en la vista de administración {#automate-approval-newly-ingested-assets}

Después de cambiar de la vista de Assets a la vista de Administración, puede establecer la configuración de la carpeta para que todos los recursos nuevos agregados a la carpeta se aprueben automáticamente.

Puede cambiar entre las vistas Administración y Assets de las siguientes maneras:
![Información general de Mi Workspace](assets/assets-view.png)

Siga estos pasos para automatizar la aprobación de los recursos recién ingeridos en [!DNL Experience Manager Admin view]:

1. Cree una carpeta en el entorno de creación (https://author-pXXX-eYYY.adobeaemcloud.com). Reemplace _XXX_ con su ID de programa y _AAAA_ con el ID de entorno de Experience Manager.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]**.
1. Haga clic en **[!UICONTROL Crear]** en la parte superior derecha de la página.
1. Agregue un título de perfil y haga clic en **[!UICONTROL Crear]**. El perfil de metadatos se ha creado correctamente.
1. Seleccione el perfil de metadatos recién creado y haga clic en **[!UICONTROL Editar _(e)_]**. <br>El formulario **[!UICONTROL Editar perfil de metadatos]**se abre con la ficha **[!UICONTROL Básico]**resaltada.
1. Arrastre y suelte un **[!UICONTROL campo de texto de una sola línea]** desde la sección **[!UICONTROL Generar formulario]** a la derecha de la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** por _Assets aprobado_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:status_.
   1. Cambie el valor predeterminado a _aprobado_.

1. De forma similar al paso 6, arrastre un **[!UICONTROL campo de texto de una sola línea]** desde la sección **[!UICONTROL Generar formulario]** a la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en el panel **[!UICONTROL Configuración]**:
   1. Cambie **[!UICONTROL Etiqueta de campo]** a _Destino de activación_.
   1. Actualice el **[!UICONTROL mapa a la propiedad]** a _./jcr:content/metadata/dam:activationTarget_.
   1. Cambie el valor predeterminado a _contenthub_.

1. Haga clic en **[!UICONTROL Guardar]**.
1. En la página **[!UICONTROL Perfiles de metadatos]**, seleccione el perfil de metadatos recién creado.
1. Haga clic en **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** desde la barra de acciones superior.
1. Seleccione las carpetas que necesita aprobar y haga clic en **[!UICONTROL Aplicar]**.
   <br>: el permiso para toda la carpeta está establecido para su aprobación y todos los recursos cargados en esta carpeta se aprueban automáticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
Este método aprueba los recursos recién creados en la carpeta. Para los recursos existentes en la carpeta, debe seleccionarlos y aprobarlos manualmente.

## Administración de recursos cargados mediante Content Hub {#manage-assets-uploaded-using-content-hub}

[Los usuarios de Content Hub con derechos para agregar recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) pueden [agregar recursos a Content Hub](/help/assets/upload-brand-approved-assets.md) desde el sistema de archivos local o importar recursos desde fuentes de datos de OneDrive o Dropbox. Todos los recursos se muestran en el nivel superior en Content Hub, independientemente de la estructura de carpetas disponible en el sistema de archivos local o en las fuentes de datos de OneDrive y Dropbox, para mejorar las funciones de búsqueda.

La visualización de los recursos cargados mediante Content Hub depende de si ha [habilitado la opción de aprobación automática](/help/assets/configure-content-hub-ui-options.md#configure-import-options-content-hub):

* Si la opción **[!UICONTROL Aprobación automática]** está habilitada, los recursos que cargue mediante Content Hub estarán disponibles automáticamente.

* Si la opción **[!UICONTROL Aprobación automática]** está deshabilitada, los recursos que cargue mediante Content Hub no se mostrarán automáticamente. Los recursos están disponibles en la carpeta `hydrated-assets` de su entorno de Assets as a Cloud Service. Vaya a la carpeta y [edite en lotes](#bulk-approve-assets-content-hub) el estado de esos recursos a `Approved` para que se muestren en Content Hub.

![Proceso de aprobación de Content Hub](/help/assets/assets/content-hub-approval.png)
