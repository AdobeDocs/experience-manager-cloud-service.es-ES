---
title: Aprobar recursos en el Experience Manager
description: Obtenga información sobre cómo aprobar recursos en [!DNL Experience Manager].
role: User
source-git-commit: 540aa876ba7ea54b7ef4324634f6c5e220ad19d3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Aprobar recursos en [!DNL Experience Manager]

Los responsables de marca y los especialistas en marketing mantienen un control estricto sobre los recursos de marca. Solo está disponible la versión aprobada y más reciente del recurso para su uso, lo que garantiza la coherencia de la marca en todos los canales y aplicaciones.

Puede aprobar recursos en AEM Assets para optimizar la administración de recursos, lo que garantiza un proceso controlado y eficiente para administrarlos.

## Antes de empezar {#pre-requisites}

Debe tener acceso al as a Cloud Service de AEM Assets y permisos para editar el **[!UICONTROL Estado de revisión]** propiedad para un recurso.

## Configuración

Debe realizar una actualización única del esquema de metadatos aplicable en la vista de administrador para poder aprobar un recurso. Puede omitir esta configuración para la vista de Assets. Siga estos pasos para configurar el esquema de metadatos:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadatos]**.
1. Seleccione el esquema de metadatos aplicable y haga clic en **[!UICONTROL Editar]**. <br>El **[!UICONTROL Editor de formularios de esquemas de metadatos]** se abre con el **[!UICONTROL Básico]** pestaña resaltada.
1. Desplácese hacia abajo y haga clic **[!UICONTROL Estado de revisión]**.
1. Haga clic en **[!UICONTROL Reglas]** en el panel lateral derecho.
1. Desmarcar **[!UICONTROL Deshabilitar edición]** y haga clic en **[!UICONTROL Guardar]**.
Si necesita ver la propiedad que el **[!UICONTROL Estado de revisión]** el campo está asignado a, navegue hasta **[!UICONTROL Configuración]** y vea la pestaña `./jcr:content/metadata/dam:status` valor en **[!UICONTROL Asignar a la propiedad]** field.

>[!NOTE]
>
>Si los recursos o carpetas tienen un esquema predeterminado diferente, asegúrese de realizar esta actualización en ese esquema en particular.

## Aprobar recursos {#approve-assets}

Puede aprobar recursos en ambos [!DNL Experience Manager] y [!DNL Experience Manager Assets]. Para aprobar recursos en [!DNL Experience Manager], siga estos pasos:

1. Seleccione los recursos y haga clic en **[!UICONTROL Propiedades]** en el panel superior.
1. En el **[!UICONTROL Básico]** pestaña, desplazarse hacia abajo hasta **[!UICONTROL Estado de revisión]**.
1. Cambiar el estado de revisión a **[!UICONTROL Aprobado]**.
   ![imagen](/help/assets/assets/approve-old-ui.png)
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   >[!VIDEO](https://video.tv.adobe.com/v/3427430)

   Del mismo modo, puede aprobar recursos mediante el [nueva vista de Assets](/help/assets/manage-organize-assets-view.md).

## Aprobar recursos de forma masiva {#bulk-approve-assets}

Optimice su flujo de trabajo aprobando rápidamente varios recursos a la vez. Puede aprobar recursos de forma masiva para acelerar el proceso de aprobación, lo que ahorra tiempo y mejora la productividad.
<br>Siga estos pasos para aprobar recursos en bloque en [!DNL Experience Manager]:

1. Cree una carpeta en el entorno de creación (https://author-pXXX-eYYY.adobeaemcloud.com). Reemplazar _XXX_ con su ID de programa y _YYY_ con el ID de entorno del Experience Manager.
1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfiles de metadatos]**.
1. Clic **[!UICONTROL Crear]** en la parte superior derecha de la página.
1. Añada un título de perfil y haga clic en **[!UICONTROL Crear]**. El perfil de metadatos se ha creado correctamente.
1. Seleccione el perfil de metadatos recién creado y haga clic en **[!UICONTROL Editar _(e)_]**. <br>El **[!UICONTROL Editar perfil de metadatos]**El formulario se abre con la variable **[!UICONTROL Básico]**pestaña resaltada.
1. Arrastrar y soltar una **[!UICONTROL Campo de texto de línea única]** desde el **[!UICONTROL Generar formulario]** en el lado derecho a la sección Metadatos del formulario.
1. Haga clic en el campo recién agregado y, a continuación, realice las siguientes actualizaciones en la **[!UICONTROL Configuración]** panel:
   1. Cambie el **[!UICONTROL Etiqueta de campo]** hasta _Assets aprobado_.
   1. Actualice el **[!UICONTROL Asignar a la propiedad]** hasta _./jcr:content/metadata/dam:status_.
   1. Cambie el valor predeterminado a _aprobado_.

1. Haga clic en **[!UICONTROL Guardar]**.
1. En el **[!UICONTROL Perfiles de metadatos]** , seleccione el perfil de metadatos recién creado.
1. Clic **[!UICONTROL Aplicar perfil de metadatos a las carpetas]** de la barra de acciones superior.
1. Seleccione las carpetas que debe aprobar y haga clic en **[!UICONTROL Aplicar]**.
   <br> El permiso para toda la carpeta se establece para su aprobación y todos los recursos cargados en esta carpeta se aprueban automáticamente.

   >[!VIDEO](https://video.tv.adobe.com/v/3427431)

>[!NOTE]
> 
>Este método aprueba los recursos recién creados en la carpeta. Para los recursos existentes en la carpeta, debe seleccionarlos y aprobarlos manualmente. <br> Como alternativa, puede utilizar la variable **[!UICONTROL Reprocesar]** para aplicar los cambios del perfil de metadatos a los recursos más antiguos.

Del mismo modo, para aprobar recursos de forma masiva dentro de una carpeta en la vista Assets:

1. Seleccione los recursos y haga clic en **[!UICONTROL Edición masiva de metadatos]**.

1. Seleccionar **[!UICONTROL Aprobado]** en el **[!UICONTROL Estado]** disponible en el campo [!UICONTROL Propiedades] en el panel derecho.

1. Haga clic en **[!UICONTROL Guardar]**.

## Copiar la URL de envío para los recursos aprobados {#copy-delivery-url-approved-assets}

La URL de entrega de todos los recursos aprobados del repositorio está disponible si tiene [!UICONTROL Dynamic Media con funciones de OpenAPI] habilitado en la instancia de AEM as a Cloud Service.

Para copiar la URL de envío de un recurso aprobado dentro del repositorio:

1. Seleccione el recurso y haga clic en **[!UICONTROL Detalles]**.

1. Haga clic en el icono Representaciones disponible en el panel derecho.

1. Seleccionar **[!UICONTROL Dynamic Media con OpenAPI]** disponible en el **[!UICONTROL Dinámico]** sección.

1. Clic **[!UICONTROL Copiar URL]** para copiar la dirección URL de envío del recurso.
   ![copiar URL de envío](/help/assets/assets/copy-delivery-url.png)

   >[!NOTE]
   >
   >La opción para copiar la URL de envío para los recursos aprobados solo está disponible en la vista de Assets.

