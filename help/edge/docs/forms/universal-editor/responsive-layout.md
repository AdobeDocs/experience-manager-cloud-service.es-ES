---
title: 'Descripción del editor universal: modo adaptable'
description: Este artículo explica cómo obtener una vista previa de los formularios utilizando diferentes emuladores en el editor universal para visualizar su apariencia durante la creación.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1285'
ht-degree: 42%

---


# Modo adaptable en la creación de WYSIWYG

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico con el nombre de su organización de GitHub y el nombre del repositorio desde su dirección oficial a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . Por ejemplo, si la URL del repositorio es https://github.com/adobe/abc, el nombre de la organización es adobe y el nombre del repositorio es abc.</span>

## Introducción a Forms interactivo

En el mundo multidispositivo actual, los formularios deben tener un aspecto impecable y funcionar bien en pantallas de todos los tamaños, desde monitores de escritorio hasta smartphones. El modo interactivo del editor universal le ayuda a conseguirlo, ya que le permite previsualizar y probar los formularios en diferentes tamaños de dispositivo durante el proceso de creación.

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) le permite crear formularios que se adaptan automáticamente a diferentes tamaños de pantalla, lo que proporciona una experiencia de usuario óptima independientemente del dispositivo que se utilice.

## Vista previa de los formularios en modo adaptable para diferentes dispositivos

El editor universal proporciona un icono **Emulador** ubicado en la esquina superior derecha de la pantalla que le permite obtener una vista previa de las páginas en diferentes tamaños de dispositivo y probar el comportamiento de su diseño interactivo para una mejor experiencia del usuario.

Para obtener una vista previa de un formulario en modo interactivo:

1. Abra un formulario en el editor universal para editarlo.
2. Haga clic en el icono ![Emulador que muestra un símbolo de vista previa del dispositivo](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} en la barra de herramientas.
3. Seleccione un formato de dispositivo:
   - Escritorio (predeterminado)
   - Tableta
   - Dispositivo móvil
   - Personalizado (especifique la anchura y la altura)

![Captura de pantalla del editor universal que muestra las opciones de modo interactivo para diferentes dispositivos](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

También puede usar el icono **Rotador de pantalla** para alternar entre las orientaciones horizontal y vertical al obtener una vista previa en tabletas o dispositivos móviles.

El editor universal proporciona diferentes emuladores para obtener una vista previa de los formularios en varios dispositivos. En la tabla siguiente se enumeran los tipos de emulador disponibles junto con sus representaciones de dispositivo correspondientes:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo de emulador</th>
        <th style="width: 80%">Imagen del dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Escritorio</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Vista de escritorio de un formulario que muestra el diseño de ancho completo" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tableta</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Vista en tableta de un formulario que muestra un diseño de ancho medio con componentes ajustados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo móvil</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Vista móvil de un formulario que muestra un diseño estrecho con componentes apilados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizado</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Vista de dispositivo personalizada de un formulario con dimensiones especificadas por el usuario" style="width: auto; height: auto"></td>
    </tr>
</table>

## Capacidades de diseño

El editor universal le permite crear formularios fáciles de usar que ofrecen experiencias dinámicas a los usuarios finales. El diseño del formulario controla cómo se muestran los elementos o los componentes de un formulario.

El editor universal admite los siguientes tipos de diseños para formularios:

- [Diseño de panel](#panel-layout)
- [Diseño de asistente](#wizard-layout)
- [Diseño de acordeón](#accordion-layout)

### Diseño de panel

El diseño de panel es útil para organizar los campos relacionados de una manera que facilite la navegación y la búsqueda del contenido correspondiente. El diseño del panel organiza los componentes del formulario en secciones o paneles distintos de los formularios.

![Diseño de panel que muestra varias secciones distintas dentro de un formulario](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Ejemplo:** Un formulario de solicitud de empleo podría usar paneles para separar &quot;Información personal&quot;, &quot;Educación&quot;, &quot;Experiencia laboral&quot; y &quot;Referencias&quot; en secciones distintas.

**Comportamiento interactivo:** En pantallas más pequeñas, los paneles suelen apilarse verticalmente, manteniendo sus diferentes agrupaciones y ajustándose a la anchura más estrecha.

Puede usar el [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para añadir el diseño de panel en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de panel, consulte el artículo [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Diseño de asistente

El diseño del asistente ayuda a simplificar un formulario complejo dividiéndolo en pasos distintos. Cada paso representa una parte diferente del proceso y los usuarios navegan por los pasos secuencialmente, a menudo con los botones **Siguiente** y **Atrás**. Puede utilizar el diseño de asistente para crear un formulario que incluya varias secciones o pasos.

![Diseño del asistente que muestra un formulario de varios pasos con controles de navegación](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Ejemplo:** Un formulario de reclamación de seguro podría usar un asistente para guiar a los usuarios proporcionando detalles del incidente, cargando pruebas, introduciendo información personal y revisando el envío.

**Comportamiento interactivo:** En dispositivos móviles, el asistente mantiene su enfoque paso a paso, pero ajusta el contenido de cada paso para que se ajuste a la pantalla más estrecha y, a menudo, apilando elementos que aparecerían uno al lado del otro en pantallas más grandes.

Puede usar el [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para añadir el diseño de asistente en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de asistente, consulte el artículo [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Diseño de acordeón

El diseño de acordeón muestra el contenido en secciones o paneles contraíbles en un formulario adaptable. Cuando se expande una sección, se muestra el contenido incluido en ella, mientras que las demás secciones permanecen contraídas. Este diseño es ideal para mostrar grandes cantidades de información en un formulario compacto.

![Diseño de acordeón que muestra secciones ampliables en un formulario](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Ejemplo:** Un formulario de configuración de producto puede usar secciones de acordeón para &quot;Opciones básicas&quot;, &quot;Características avanzadas&quot;, &quot;Accesorios&quot; y &quot;Planes de pago&quot;, lo que permite a los usuarios centrarse en un aspecto a la vez.

**Comportamiento interactivo:** Los acordeones funcionan especialmente bien en dispositivos móviles, ya que conservan espacio vertical de forma natural al mostrar únicamente la sección de contenido expandida, lo que los hace ideales para pantallas más pequeñas.

Puede usar el [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para añadir el diseño de acordeón en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de acordeón, consulte el artículo [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### ¿Cómo elegir el diseño correcto?

Es importante seleccionar el diseño adecuado para optimizar la experiencia del usuario y la funcionalidad del formulario. La tabla le ayuda a comprender las diferentes opciones de diseño disponibles y le guía para seleccionar el diseño más adecuado según sus necesidades específicas y casos de uso:

| Funcionalidad | Diseño de panel | Diseño de asistente | Diseño de acordeón |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Propósito** | Agrupa el contenido relacionado en secciones distintas | Guía a los usuarios a través de un proceso o formulario con varias etapas | Organiza el contenido en secciones contraíbles |
| **Estructura** | Secciones distintas | Pasos/páginas secuenciales | Paneles/secciones contraíbles |
| **Navegación** | Haga clic en los encabezados del panel para navegar | - Adelante: botón &quot;Siguiente&quot;<br>- Atrás: botón &quot;Atrás&quot;<br>- Pasos de omisión opcionales | Haga clic en los encabezados para expandir o contraer secciones |
| **Experiencia del usuario** | Organiza grandes cantidades de contenido de una manera manejable | Guía paso a paso para reducir la sobrecarga | Vista compacta con secciones expandidas/contraídas |
| **Caso práctico** | Formularios complejos con secciones clasificadas | Configuración de procesos, formularios complejos | Preguntas frecuentes, menús de configuración, secciones de contenido detalladas |
| **Lo mejor para dispositivos móviles** | Moderar: los paneles se apilan verticalmente | Bueno: mantiene el enfoque solo en el paso actual | Excelente - conserva el espacio con secciones plegables |

## Prácticas recomendadas para Forms interactivo

Para garantizar que los formularios proporcionen la mejor experiencia en todos los dispositivos, siga estas prácticas recomendadas:

1. **Primero diseñe para dispositivos móviles:** Comience por diseñar el formulario para dispositivos móviles y, a continuación, mejore para pantallas más grandes. Este enfoque garantiza que la funcionalidad principal funcione en las pantallas más pequeñas.

2. **Usar tipos de campo apropiados:** Elija tipos de campo que funcionen bien en dispositivos táctiles:
   - Utilice menús desplegables en lugar de botones de opción cuando haya muchas opciones
   - Uso de selectores de fechas diseñados para la entrada táctil
   - Asegúrese de que los botones y los destinos táctiles tengan al menos 44 px x 44 px.

3. **Simplificar para pantallas más pequeñas:**
   - Mostrar menos campos por fila en dispositivos móviles
   - Considere la posibilidad de ocultar los campos opcionales detrás de la opción &quot;Mostrar más&quot;.
   - Divida formularios complejos en más pasos en dispositivos móviles

4. **Realizar pruebas exhaustivas:** Pruebe siempre los formularios en dispositivos reales o con el modo de emulador en el Editor universal para asegurarse de que funcionan correctamente en todos los tamaños de pantalla.

5. **Considere los tiempos de carga:** Optimice el tamaño de las imágenes y minimice los recursos necesarios, especialmente para los usuarios móviles que pueden tener conexiones más lentas.

## Solución de problemas de Forms interactivo

| Problema | Causa posible | Solución |
|-------|---------------|----------|
| El formulario aparece cortado en dispositivos móviles | Configuración de anchura fija o problemas de desbordamiento | Utilice unidades relativas (%, rem) en lugar de píxeles y compruebe las propiedades overflow:hidden |
| Elementos táctiles difíciles de interactuar con | Tocar objetivos demasiado pequeños o demasiado cerca | Aumente el tamaño del botón/entrada a al menos 44 px x 44 px y añada más espacio entre los elementos interactivos |
| Desbordamientos de contenido en pantallas pequeñas | Sin reglas adaptables para ventanillas móviles más pequeñas | Añada consultas de medios o clases adaptables para ajustar el diseño en diferentes tamaños de pantalla |
| Formulario demasiado lento en dispositivos móviles | Imágenes grandes o secuencias de comandos excesivas | Optimizar imágenes, minimizar JavaScript y considerar la carga diferida de elementos no críticos |
| Diferente apariencia entre el emulador y los dispositivos reales | Representación específica del explorador o variaciones de dispositivo | Realizar pruebas en dispositivos reales siempre que sea posible, no solo en emuladores |

## Consulte también

{#see-more-eds-forms}
