---
title: 'Administrar audiencias '
description: La consola Audiencias le permite crear, organizar y administrar audiencias para su cuenta de Adobe Destinatario o administrar segmentos para ContextHub
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 60%

---


# Administrar audiencias{#managing-audiences} 

La consola Audiencias le permite crear, organizar y administrar audiencias para su cuenta de Adobe Destinatario o administrar segmentos para ContextHub:

* Añadir audiencias: audiencias de Adobe Target o segmentos de ContextHub.
* Administre audiencias.

An Audience, called *segment* in ContextHub, is a class of visitors defined by specific criteria, which then determines who sees a targeted activity. Al segmentar una actividad, puede seleccionar la audiencia directamente en el proceso de segmentación o crear una nueva en la consola de audiencias.

En la consola de audiencias, las audiencias se organizan según la marca.

Audiences are available in Targeting mode for [authoring targeted content](/help/sites-cloud/authoring/personalization/targeted-content.md), where you can also create audiences (but you need to create Adobe Target audiences in the Audiences console). Las audiencias creadas en el modo Segmentación aparecen en la consola de audiencias.

Las audiencias se muestran con una etiqueta que describe qué tipo de audiencia está definida:

* CH: segmento de ContextHub
* AT: audiencia de Adobe Target

## Crear un segmento de ContextHub en la consola de audiencias {#creating-a-contexthub-segment-in-the-audiences-console}

Puede crear un segmento de ContextHub en la consola de audiencias o durante el proceso de segmentación.

Para crear un segmento de ContextHub en la consola de audiencias:

1. En la consola de navegación, haga clic o pulse **Personalización**. Click or tap **Audiences**.
1. Haga clic o pulse **Crear segmento de ContextHub**.

   ![Creación de un segmento](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. En cuadro de diálogo **Nuevo segmento de ContextHub**, introduzca un título, ajuste el aumento y haga clic en **Crear**. El nuevo segmento de ContextHub aparece en la lista de audiencias.

   >[!NOTE]
   >
   >Puede ordenar la lista modificada pulsando o haciendo clic en **Modificado** para clasificar en orden descendente y ver las audiencias recién creadas.

Para obtener más información sobre cómo crear segmentos con ContextHub, consulte la documentación de Configurar la segmentación con ContextHub. <!--For further detail about creating segments using ContextHub, please see the [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) documentation.-->

## Crear una audiencia de Adobe Target mediante la consola de audiencias {#creating-an-adobe-target-audience-using-the-audience-console}

Puede crear audiencias de Adobe Target directamente en AEM mediante la consola de audiencias.

Las audiencias se definen mediante reglas que determinan quién se incluye o excluye de una actividad de destino. Una definición de audiencia puede incluir varias reglas y cada regla puede incluir varios parámetros.

Al utilizar más de una regla, estas reglas se combinan según el operador booleano Y (AND), lo que significa que cualquier posible miembro de la audiencia debe cumplir todas las condiciones que se detallaron para ser incluido en la actividad. Por ejemplo, si define una regla de sistema operativo Y (AND) una regla de explorador, solo se incluyen en la actividad los visitantes que usan el sistema operativo definido Y (AND) el explorador definido.

>[!NOTE]
>
>Si no ve **Crear audiencia de Target** en el menú **Crear**, no tiene los permisos necesarios para crear una audiencia. Debe disponer de permisos de escritura en `/etc/segmentation` para poder crear audiencias. Los autores de contenido del grupo tienen permisos de escritura de forma predeterminada.

Para crear una audiencia de Adobe Target:

1. En la consola de navegación, haga clic o pulse **Personalización**. Click or tap **Audiences**.

   ![Navegación a audiencias](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. In the Audiences console, tap or click **Create** and then** Create Target Audience**.

   ![Creación de una audiencia de Destinatario](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. En el cuadro de diálogo **Configuración de Adobe Target**, seleccione la configuración de destino y haga clic o pulse **Aceptar**.
1. En el área de la Regla n.º 1, haga clic o pulse el tipo de atributo e introduzca la información de atributo en los campos que están disponibles. Cuando termine, seleccione la marca de verificación situada a la derecha del atributo para guardarlo. Consulte [Atributos y sus opciones](#attributes-and-their-options) para obtener más información acerca de todos los atributos.
1. Haga clic en **Agregar regla** para añadir otra regla. Escriba tantas reglas como sea necesario. Las reglas se combinan con el operador booleano Y, lo que significa que la audiencia debe cumplir todos los requisitos de cada regla para poder optar a una actividad.
1. Haga clic o pulse **Siguiente**.
1. Especifique un nombre para la audiencia y haga clic o pulse **Guardar**.
1. Tap or click **Save**. La audiencia se enumera en la lista de audiencias.

### Atributos y sus opciones {#attributes-and-their-options}

Puede crear reglas de segmentación para cada uno de los atributos siguientes:

| **Atributo** | **Descripción** | **Para obtener más información** |
|---|---|---|
| **Móvil** | Destinatario los dispositivos móviles en función de parámetros como dispositivos móviles, tipo de dispositivo, proveedor de dispositivos, dimensiones de pantalla (en píxeles), etc. | Consulte la documentación [de](https://marketing.adobe.com/resources/help/en_US/target/target/c_mobile.html) Mobile en Adobe Destinatario. |
| **Personalizado** | Los parámetros personalizados son parámetros de mbox. Si pasa algún parámetro mbox a mboxes, o usa la función targetPageParams, ese parámetro aparece aquí para su uso en audiencias. | Consulte la documentación [Parámetros](https://marketing.adobe.com/resources/help/en_US/target/target/c_custom_parameters.html) personalizados en Adobe Destinatario. |
| **SO** | Puede destinatario visitantes que utilicen un sistema operativo determinado. | Usuarios de Target que usen Linux, Macintosh o Windows. |
| **Páginas del sitio** | visitantes de Destinatario que se encuentran en una página específica o que tienen un parámetro de mbox específico. | Consulte la documentación [de Páginas](https://marketing.adobe.com/resources/help/en_US/target/target/c_site_pages.html) del sitio en Adobe Destinatario. |
| **Explorador** | Puede asignar destinatarios a los usuarios que utilicen un explorador específico o opciones específicas del explorador cuando visiten la página. | Consulte la documentación [de las opciones del explorador](https://marketing.adobe.com/resources/help/en_US/target/target/c_browser_options.html)en Adobe Destinatario. |
| **Perfil del visitante** | visitantes de Destinatario que cumplen parámetros de perfil específicos. | Consulte la documentación [de](https://marketing.adobe.com/resources/help/en_US/target/target/c_visitor_profile.html) Visitante Perfil en Adobe Destinatario. |
| **Fuentes de tráfico** | visitantes de Destinatario basados en el motor de búsqueda o la página de aterrizaje que los remite a su sitio. | Consulte la documentación [de fuentes](https://marketing.adobe.com/resources/help/en_US/target/target/c_traffic_sources.html) de tráfico en Adobe Destinatario. |

## Modificar una audiencia en la consola de audiencias {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Solo puede editar las audiencias de Adobe Target que se crearon en la misma instancia de AEM en la cual realizó las modificaciones. Las audiencias de destino que se crearon en diferentes entornos de AEM no se pueden editar.

Puede editar cualquier audiencia de ContextHub desde la consola Audiencias. También puede editar audiencias de Adobe Destinatario, pero solo aquellas que se crearon en AEM:

1. En la consola de navegación, haga clic o pulse **Personalización**. Click or tap **Audiences**.
1. Tap or click the icon next to the ContextHub segment you want to edit, and tap or click **Edit**.
1. Haga los cambios necesarios en el editor de segmentos. Consulte la documentación de ContextHub para obtener más información. <!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
