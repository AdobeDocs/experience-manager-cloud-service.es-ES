---
title: Cómo integrar el modelo de datos de formulario (FDM) para un formulario con un formulario adaptable
description: Aprenda a crear formularios basados en un modelo de datos de formulario (FDM). Genere y edite datos de muestra para objetos del modelo de datos en el modelo de datos de formulario (FDM).
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 62134c5b67d610f801c407e696e761ed05e02c87
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 31%

---

# Integrar formularios con el modelo de datos de formulario

La integración de formularios con un modelo de datos de formulario (FDM) le permite utilizar diversas fuentes de datos back-end para crear un modelo de datos de formulario (FDM). Puede utilizar el modelo de datos de formulario (FDM) como esquema en varios flujos de trabajo de formulario. Configure las fuentes de datos y cree un modelo de datos de formulario (FDM) basado en los objetos y servicios de modelo de datos disponibles en las fuentes de datos. 

## Ventajas de integrar Forms con el modelo de datos de formulario (FDM)

* **Conectividad back-end perfecta**: conecte formularios a varios sistemas back-end (p. ej., bases de datos, API de REST, servicios de SOAP, CRM) sin código personalizado. Esto permite el intercambio de datos en tiempo real y reduce el esfuerzo de integración.
* **Esquema de datos centralizado**: el modelo de datos de formulario sirve como esquema de datos unificado que simplifica la asignación y administración de objetos de datos y servicios utilizados en varios formularios y flujos de trabajo.

* **Envío y rellenado previos de formularios mejorados**: configure fácilmente las acciones de envío y rellenado previo mediante los servicios de datos de formulario, lo que garantiza una recuperación y un almacenamiento de datos precisos y actualizados.

* **Compatibilidad con flujos de trabajo dinámicos**: el modelo de datos de formulario se puede integrar con flujos de trabajo para automatizar procesos empresariales basados en datos enviados o recuperados, lo que mejora la eficacia general.

## Requisitos previos

Antes de configurar el formulario con el modelo de datos de formulario, asegúrese de completar los siguientes pasos:

* [Configuración de la fuente de datos](/help/forms/configure-data-sources.md): configure la fuente de datos para conectar el formulario a los datos de back-end.
* [Creación de un modelo de datos de formulario (FDM)](/help/forms/create-form-data-models.md): cree un modelo de datos mediante objetos y servicios de datos de la fuente de datos configurada.
* [Configuración de objetos y servicios de modelo de datos](/help/forms/work-with-form-data-model.md): asigne los objetos y servicios de modelo de datos para garantizar un flujo de datos fluido entre el formulario y la fuente de datos.

>[!BEGINTABS]

>[!TAB Componente Base]

Realice los siguientes pasos para configurar el modelo de datos de formulario con el formulario adaptable basado en el componente de base como:

1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Envío]** de las propiedades del contenedor del formulario adaptable.
1. En la lista desplegable **[!UICONTROL Enviar acción]**, seleccione **[!UICONTROL Enviar mediante el modelo de datos de formulario]**.

   ![enviar mediante modelo de datos de formulario](/help/forms/assets/submit-uisng-fdm-fc.png)

1. Seleccione el modelo de datos **[!UICONTROL creado para enviar]** la configuración.
Para enviar datos adjuntos a la base de datos, seleccione **Enviar datos adjuntos del formulario**. El documento de registro (DoR) se guardará en la base de datos al seleccionar **Enviar documento de registro**.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

>[!TAB Componente principal]

Realice los siguientes pasos para configurar el modelo de datos de formulario con el formulario adaptable basado en el componente principal como:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Enviar acción]**, seleccione **[Enviar mediante el modelo de datos de formulario]**.

   ![enviar mediante modelo de datos de formulario](/help/forms/assets/submit-uisng-fdm-cc.png)

1. Seleccione el modelo de datos **[!UICONTROL creado para enviar]** la configuración.
Para enviar datos adjuntos a la base de datos, seleccione **Enviar datos adjuntos del formulario**. El documento de registro (DoR) se guardará en la base de datos al seleccionar **Enviar documento de registro**.
1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración de envío.

>[!TAB Editor universal]

Realice los siguientes pasos para configurar el modelo de datos de formulario con el formulario adaptable creado en Universal as:

1. Abra el formulario adaptable para editarlo.
1. Haga clic en la extensión **Editar propiedades del formulario** en el editor.

   Aparecerá el cuadro de diálogo **Propiedades del formulario**.

   >[!NOTE]
   >
   > * Si no ve el icono **Editar propiedades de formulario** en la interfaz de Universal Editor, habilite la extensión **Editar propiedades de formulario** en Extension Manager.
   > * Consulte el artículo [Aspectos destacados de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para obtener información sobre cómo habilitar o deshabilitar extensiones en el editor universal.

1. Haga clic en la pestaña **Envío** y seleccione **[!UICONTROL Enviar mediante el modelo de datos de formulario]**.

   ![OneDrive GIF](/help/forms/assets/submit-uisng-fdm-ue.png)
Si selecciona **Guardar archivos adjuntos con el nombre original**, los archivos adjuntos se almacenarán en la carpeta utilizando sus nombres de archivo originales. También puede guardar el documento de registro (DoR) en Azure Blob Storage.

1. Seleccione la **[!UICONTROL Configuración de almacenamiento]**, donde desee guardar los datos.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**

Para obtener instrucciones detalladas sobre cómo integrar formularios creados en el editor universal, consulte el artículo [Integrar Forms con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

>[!ENDTABS]

## Artículos relacionados

{{af-submit-action}}
