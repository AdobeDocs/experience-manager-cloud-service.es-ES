---
title: 'Descripción del editor universal: modo adaptable'
description: Este artículo explica cómo obtener una vista previa de los formularios utilizando diferentes emuladores en el editor universal para visualizar su apariencia durante la creación.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 8f5b4d863ab469c44b4c221eab1fb128706b45c7
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 34%

---

# Modo adaptable en la creación de WYSIWYG

<span class="preview"> Esta característica está disponible a través del programa de acceso anticipado. Para solicitar acceso, envía un correo electrónico desde tu dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con tu nombre de organización de GitHub y el nombre del repositorio. Por ejemplo, si la dirección URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>


El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) le permite obtener una vista previa de los formularios de Edge Delivery Services con diferentes emuladores para ver la apariencia del formulario durante la creación.

El modo adaptable permite a los desarrolladores crear diseños que se adaptan automáticamente a diferentes tamaños de pantalla, incluidos escritorios, tabletas y dispositivos móviles. El editor universal admite emuladores para equipos de escritorio, tabletas y dispositivos móviles. Puede establecer la altura y la anchura según el tamaño de la pantalla y realizar las siguientes acciones:

* Establecer la orientación
* Definir la anchura y la altura
* Cambiar la orientación

## Vista previa de los formularios en modo adaptable para diferentes dispositivos

El editor universal proporciona un icono **Emulador** ubicado en la esquina superior derecha de la pantalla que le permite obtener una vista previa de las páginas en diferentes tamaños de dispositivo y probar el comportamiento de su diseño interactivo para una mejor experiencia de usuario.

Para ver cómo el editor universal procesa los formularios en diferentes tamaños de pantalla, realice los siguientes pasos:

1. Abra un formulario en el editor universal para editarlo.
1. Seleccione el ![icono Emulador](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} disponible en la barra de herramientas del editor universal y haga clic en el icono Emulador para mostrar la opción.

   ![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. Seleccione una opción para emular un formulario en el editor universal en un dispositivo seleccionado: escritorio, tableta, móvil.

   ![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%,height=40%}

   De forma predeterminada, el editor se abre en un diseño de escritorio en el que el explorador define automáticamente la altura y la anchura. También puede emular un formulario en un dispositivo móvil o tableta. También puede personalizar la anchura y la altura de la pantalla para dispositivos personalizados.

El editor universal proporciona diferentes emuladores para obtener una vista previa de los formularios en varios dispositivos. En la tabla siguiente se enumeran los tipos de emulador disponibles junto con sus representaciones de dispositivo correspondientes:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo de emulador</th>
        <th style="width: 80%">Imagen del dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Escritorio</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Emulador de escritorio" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tableta</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Emulador de tableta" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo móvil</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Emulador móvil" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizado</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Emulador de dispositivo personalizado" style="width: auto; height: auto"></td>
    </tr>
</table>

Puede usar el icono de **Rotador de pantalla** para conmutar entre las orientaciones vertical y horizontal al obtener una vista previa de un formulario en diferentes dispositivos. Ayuda a los desarrolladores a probar cómo el diseño adaptable se adapta a las rotaciones de pantalla en varios dispositivos.

El editor universal admite los distintos diseños de formulario. Para explorar los diferentes diseños, consulte la sección [Funciones de diseño](#layout-capabilities).

## Funciones de diseño

El editor universal permite crear formularios fáciles de usar que ofrecen experiencias dinámicas a los usuarios finales. El diseño del formulario controla cómo se muestran los elementos o los componentes de un formulario.

El editor universal admite los siguientes tipos de diseños para formularios:
* [Diseño de panel](#panel-layout)
* [Diseño del asistente](#wizard-layout)
* [Diseño de acordeón](#accordion-layout)

### Diseño de panel

El diseño del panel es útil para organizar los campos relacionados de una manera que facilite la navegación y la búsqueda del contenido correspondiente. El diseño del panel organiza los componentes del formulario en secciones o paneles distintos de los formularios.

![Diseño de panel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

Puede usar [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para agregar el diseño de panel en un formulario. Para obtener instrucciones detalladas sobre cómo configurar varias propiedades del componente del panel, consulte el artículo [componente del panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Diseño del asistente


El diseño del asistente ayuda a simplificar un formulario complejo dividiéndolo en pasos distintos. Cada paso representa una parte diferente del proceso y los usuarios navegan por los pasos secuencialmente, a menudo con los botones **Siguiente** y **Atrás**. Puede utilizar el diseño de asistente para crear un formulario que incluya varias secciones o pasos.

![Diseño del asistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

Puede usar el [componente de asistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para agregar el diseño de asistente en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de asistente, consulte el artículo [componente de asistente](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Diseño de acordeón

El diseño de acordeón muestra el contenido en secciones o paneles contraíbles de un formulario adaptable. Cuando se expande una sección, muestra el contenido dentro de, mientras que otras secciones permanecen contraídas. Este diseño es ideal para mostrar grandes cantidades de información en un formulario compacto.

![Diseño de acordeón](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

Puede usar el [componente de acordeón](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para agregar el diseño de acordeón en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de acordeón, consulte el artículo [componente de acordeón](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### ¿Cómo elegir el diseño correcto?

Es importante seleccionar el diseño adecuado para optimizar la experiencia del usuario y la funcionalidad del formulario. La tabla le ayuda a comprender las diferentes opciones de diseño disponibles y le guía para seleccionar el diseño más adecuado según sus necesidades específicas y casos de uso:

| Funcionalidad | Diseño de panel | Diseño del asistente | Diseño de acordeón |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Propósito** | Agrupa el contenido relacionado en secciones distintas | Guía a los usuarios a través de un formulario o un proceso de varios pasos | Organiza el contenido en secciones contraíbles |
| **Estructura** | Secciones distintas | Pasos/páginas secuenciales | Paneles/secciones contraíbles |
| **Navegación** | Haga clic en los encabezados del panel para desplazarse | - Adelante: botón &quot;Siguiente&quot;<br>- Atrás: botón &quot;Atrás&quot;<br>- Pasos de omisión opcionales | Haga clic en los encabezados para expandir o contraer secciones |
| **Experiencia del usuario** | Organiza grandes cantidades de contenido de una manera manejable | Guía paso a paso para reducir la sobrecarga | Vista compacta con secciones expandidas/contraídas |
| **Caso práctico** | Formularios complejos con secciones categorizadas | Configuración de procesos, formularios complejos | Preguntas más frecuentes, menús de configuración y secciones de contenido detalladas |

## Véase también

{{universal-editor-see-also}}
