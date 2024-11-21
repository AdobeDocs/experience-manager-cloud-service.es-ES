---
Title: How to configure Marketo Engage data for Adaptive Forms?
Description: Learn how to use Marketo Engage schema in Adaptive Forms.
Keywords: Use Marketo Engage data source in Adaptive Forms, How to connect a Marketo instance data source with form? , Connect a form to Marketo.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 15%

---


# Configuración de la fuente de datos del Marketo Engage para Forms adaptable existente

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

![Flujo de trabajo](/help/forms/assets/workflow-marketo-2.png)

Después de crear la configuración del servicio en la nube para integrar Marketo Engage con AEM Forms existente, puede configurar la fuente de datos para los formularios.

La configuración de la integración de datos permite a los usuarios conectarse a varias fuentes de datos o esquemas. La integración con la fuente de datos del Marketo Engage y su uso en diferentes formularios facilita las operaciones con esos datos. Para explorar las fuentes de datos predeterminadas admitidas para un formulario adaptable, consulte el artículo [Configurar fuentes de datos](/help/forms/configure-data-sources.md).

## Consideración para configurar la fuente de datos del Marketo Engage para formularios

Al configurar la fuente de datos del Marketo Engage para los formularios, se tienen en cuenta los siguientes aspectos:

* No es posible conectar Edge Delivery Services Forms con Marketo Engage.

## Requisito previo para utilizar la fuente de datos de Marketo Engage en los formularios

Requisito previo para utilizar la fuente de datos de Marketo Engage con formularios:

* Cree la configuración del servicio en la nube [para integrar al Marketo Engage con formularios](/help/forms/integrate-form-to-marketo-engage.md).

## Configurar el formulario adaptable existente para la fuente de datos del Marketo Engage

Para configurar un formulario adaptable con la fuente de datos del Marketo Engage, realice los siguientes pasos:
1. Inicie sesión en la instancia de autor de [!DNL Experience Manager Forms].

1. Abra el formulario adaptable para editarlo.
1. Abra el árbol de contenido y seleccione **[!UICONTROL Contenedor de guía]**.
1. Haga clic en el icono de las ![Propiedades del contenedor del formulario adaptable](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable para configurar la fuente de datos.
1. Abra la ficha **[!UICONTROL Modelo de datos]** y seleccione un modelo de formulario como **Conector**.
1. Seleccione **[!UICONTROL Connector]** de la lista desplegable.

1. Después de seleccionar **[!UICONTROL Connector]**, puede seleccionar la configuración de nube.

   ![Seleccionar Conector De Marketo](/help/forms/assets/select-marketo-connector.png)

   Según la configuración del Marketo Engage seleccionado, los elementos del formulario se muestran en la pestaña **[!UICONTROL Objetos del modelo de datos]** del **[!UICONTROL Explorador de contenido]** en la barra lateral. Puede arrastrar y soltar estos elementos para crear su formulario adaptable.

   ![Source de datos de Marketo](/help/forms/assets/marketo-engage-data-source.png)

1. Haga clic en **[!UICONTROL Listo]**.

También puede editar las propiedades del formulario adaptable para cambiar su configuración asociada.

El formulario adaptable ahora se configura con la fuente de datos de la instancia de Marketo Engage conectada. Ahora, configúrelo para enviar datos a Adobe Marketo Engage.

## Preguntas más frecuentes (FAQ)

**Q: ¿Qué sucede cuando cambia el conector del formulario?**\
**A:** Si cambia el conector del formulario, los enlaces existentes dejarán de ser válidos.

**Q: ¿Cuáles son las tres operaciones disponibles en el servicio de invocación del Editor de reglas para los formularios integrados con el Marketo Engage?**\
**A:** Las tres operaciones predeterminadas disponibles en **Invocar servicio** para formularios integrados con el Marketo Engage son:
* Sincronizar posible cliente
* Obtener posible cliente por ID
* Obtener posible cliente por tipo de filtro

## Siguiente paso

Ahora, ha configurado la fuente de datos del Marketo Engage para Forms adaptable. A continuación, puede [configurar un formulario adaptable para enviar datos al Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md).

## Artículos relacionados

{{af-submit-action}}

## Consulte también

{{marketo-engage-see-also}}


