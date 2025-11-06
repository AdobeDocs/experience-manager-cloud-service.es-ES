---
title: Configuración de datos de Marketo Engage para los formularios adaptables
description: Aprenda a utilizar el esquema de Marketo Engage en formularios adaptables.
keywords: Utilizar la fuente de datos de Marketo Engage en formularios adaptables, Conexión de una fuente de datos de instancia de Marketo con un formulario, Conectar un formulario a Marketo.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 4656ec65-f1ad-4e97-8d93-25933cdc7f7b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 100%

---

# Configuración de la fuente de datos de Marketo Engage para los formularios adaptables existentes

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

![Flujo de trabajo](/help/forms/assets/workflow-marketo-2.png)

Después de crear la configuración del servicio en la nube para integrar Marketo Engage con los AEM Forms existentes, puede configurar la fuente de datos para formularios.

La configuración de la integración de datos permite a los usuarios conectarse a varias fuentes de datos o esquemas. La integración con la fuente de datos de Marketo Engage y su uso en diferentes formularios facilita las operaciones con esos datos. Para explorar las fuentes de datos predeterminadas admitidas para un formulario adaptable, consulte el artículo [Configuración de las fuentes de datos](/help/forms/configure-data-sources.md).

## Requisito previo para utilizar la fuente de datos de Marketo Engage para formularios

Requisito previo para utilizar la fuente de datos de Marketo Engage con formularios:

* Cree [la configuración del servicio en la nube para integrar Marketo Engage con formularios](/help/forms/integrate-form-to-marketo-engage.md).

## ¿Cómo configurar el formulario adaptable existente para la fuente de datos de Marketo Engage?

>[!VIDEO](https://video.tv.adobe.com/v/3442871/marketo-aem-forms-aem-marketo-engage)

<span> Este vídeo solo es aplicable a los componentes principales. Para componentes del editor universal o de base, consulte el artículo.</span>

>[!BEGINTABS]

>[!TAB Componente base]

Para configurar un formulario adaptable basado en componentes de base con la fuente de datos de Marketo Engage, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].
1. Abra el formulario adaptable para editarlo y vaya a la sección **[!UICONTROL Modelo de datos]** de las propiedades del contenedor del formulario adaptable y seleccione un modelo de formulario como **Conector**.
1. Seleccione el **[!UICONTROL Conector]** en la lista desplegable.
1. Después de seleccionar el **[!UICONTROL Conector]**, puede seleccionar la configuración de la nube.

   ![Seleccionar conector de Marketo](/help/forms/assets/select-marketo-connector-af1.png){width=50%, height=50%}

   En función de la configuración de Marketo Engage seleccionada, los elementos del formulario se muestran en la pestaña **[!UICONTROL Objetos de modelo de datos]** del **[!UICONTROL Explorador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

   ![Fuente de datos de Marketo](/help/forms/assets/marketo-engage-data-source-af1.png){width=50%, height=50%}

1. Haga clic en **[!UICONTROL Listo]**.

También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada.

El formulario adaptable ahora está configurado con la fuente de datos de la instancia de Marketo Engage conectada. Ahora, configúrelo para enviar datos a Adobe Marketo Engage.

>[!TAB Componente principal]

Para configurar un formulario adaptable basado en componentes principales con la fuente de datos de Marketo Engage, realice los siguientes pasos:

1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].

1. Abra el formulario adaptable para editarlo.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar la fuente de datos.
1. Abra la pestaña **[!UICONTROL Modelo de datos]** y seleccione un modelo de formulario como **Conector**.
1. Seleccione el **[!UICONTROL Conector]** en la lista desplegable.

1. Después de seleccionar el **[!UICONTROL Conector]**, puede seleccionar la configuración de la nube.

   ![Seleccionar conector de Marketo](/help/forms/assets/select-marketo-connector.png){width=50%, height=50%}

   En función de la configuración de Marketo Engage seleccionada, los elementos del formulario se muestran en la pestaña **[!UICONTROL Objetos de modelo de datos]** del **[!UICONTROL Explorador de contenido]** en la barra lateral. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

   ![Fuente de datos de Marketo](/help/forms/assets/marketo-engage-data-source.png){width=50%, height=50%}

1. Haga clic en **[!UICONTROL Listo]**.

También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada.

El formulario adaptable ahora está configurado con la fuente de datos de la instancia de Marketo Engage conectada. Ahora, configúrelo para enviar datos a Adobe Marketo Engage.

>[!TAB Editor universal]

Para configurar un formulario adaptable creado en el editor universal con la fuente de datos de Marketo Engage, realice los siguientes pasos:

1. Abra las propiedades del formulario para editarlo.
1. Seleccione **[!UICONTROL Modelo de formulario]**.
1. Seleccione **Conector** en **[!UICONTROL Modelo de formulario]**.
1. Después de seleccionar el **[!UICONTROL Conector]**, puede seleccionar la configuración de la nube.

   ![Seleccionar conector de Marketo](/help/forms/assets/select-marketo-connector-ue.png)

1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

En función de la configuración de Marketo Engage seleccionada, los elementos del formulario se muestran en la pestaña **[!UICONTROL Fuente de datos]** del explorador de contenido en el panel Propiedades. También puede arrastrar y soltar estos elementos para crear su formulario adaptable.

![Fuente de datos de Marketo](/help/forms/assets/marketo-engage-data-source-ue.png)

El formulario ahora está configurado con la fuente de datos de la instancia de Marketo Engage conectada. Ahora, configúrelo para enviar datos a Adobe Marketo Engage.

>[!ENDTABS]

## Preguntas más frecuentes (FAQ)

**P: ¿Qué sucede cuando cambia el conector del formulario?**\
**R:** Si cambia el conector del formulario, los enlaces existentes dejarán de ser válidos.

**P: ¿Cuáles son las tres operaciones disponibles en Invocar servicio del Editor de reglas para los formularios integrados con Marketo Engage?**

**P:** Las tres operaciones predeterminadas disponibles en **Invocar servicio** para los formularios integrados con Marketo Engage son:

* Sincronizar posible cliente
* Obtener posible cliente por el ID
* Obtener posible cliente por el tipo de filtro

## Siguiente paso

Ahora, ha configurado la fuente de datos de Marketo Engage para formularios adaptables. A continuación, puede [configurar un formulario adaptable para enviar datos a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Artículos relacionados

{{af-submit-action}}

## Véase también

{{marketo-engage-see-also}}
