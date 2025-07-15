---
title: 'Descripción del editor universal: modo adaptable'
description: Este artículo explica cómo obtener una vista previa de los formularios utilizando diferentes emuladores en el editor universal para visualizar su apariencia durante la creación.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 99%

---


# Modo adaptable en la creación de WYSIWYG

<span class="preview"> Esta es una característica previa al lanzamiento disponible a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal previo al lanzamiento</a>. </span>

## Introducción a los formularios adaptables

En el mundo actual, donde se utilizan múltiples dispositivos, los formularios deben tener un aspecto impecable y funcionar correctamente en pantallas de todos los tamaños, desde monitores de escritorio hasta teléfonos inteligentes. El modo adaptable del editor universal le ayuda a conseguirlo, ya que le permite previsualizar y probar los formularios en diferentes tamaños de dispositivo durante el proceso de creación.

El [editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) le permite crear formularios que se adaptan automáticamente a diferentes tamaños de pantalla, lo que proporciona una experiencia del usuario óptima independientemente del dispositivo que se utilice.

## Vista previa de los formularios en modo adaptable para diferentes dispositivos

El editor universal proporciona un icono **Emulador** ubicado en la esquina superior derecha de la pantalla que le permite obtener una vista previa de las páginas en diferentes tamaños de dispositivo y probar el comportamiento de su diseño interactivo para una mejor experiencia del usuario.

Para previsualizar un formulario en modo adaptable:

1. Abra un formulario en el editor universal para editarlo.
2. Haga clic en el ![icono de emulador que muestra un símbolo de vista previa del dispositivo](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} en la barra de herramientas.
3. Seleccione un formato de dispositivo:
   - Escritorio (predeterminado)
   - Tableta
   - Dispositivo móvil
   - Personalizado (especifique la anchura y la altura)

![Captura de pantalla del editor universal que muestra las opciones del modo adaptable para diferentes dispositivos](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

Puede usar el icono de **Rotador de pantalla** para alternar entre las orientaciones vertical y horizontal al previsualizar contenido en tabletas o dispositivos móviles.

El editor universal proporciona diferentes emuladores para obtener una vista previa de los formularios en varios dispositivos. En la tabla siguiente se enumeran los tipos de emulador disponibles junto con sus representaciones de dispositivo correspondientes:

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">Tipo de emulador</th>
        <th style="width: 80%">Imagen del dispositivo</th>
    </tr>
    <tr>
        <td style="width: 20%">Escritorio</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="Vista de escritorio de un formulario que muestra el diseño de anchura completa" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Tableta</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="Vista de tableta de un formulario que muestra un diseño de anchura media con los componentes ajustados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo móvil</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="Vista de móvil de un formulario que muestra un diseño estrecho con los componentes apilados" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">Dispositivo personalizado</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="Vista personalizada del dispositivo de un formulario con dimensiones especificadas por el usuario" style="width: auto; height: auto"></td>
    </tr>
</table>

## Capacidades de diseño

El editor universal le permite crear formularios fáciles de usar que ofrecen experiencias dinámicas a los usuarios finales. El diseño del formulario controla cómo se muestran los elementos o los componentes de un formulario.

El editor universal admite los siguientes tipos de diseños para formularios:

- [Diseño de panel](#panel-layout)
- [Diseño de asistente](#wizard-layout)
- [Diseño de acordeón](#accordion-layout)

### Diseño de panel

El diseño de panel es útil para organizar los campos relacionados de una manera que facilite la navegación y la búsqueda del contenido correspondiente. El diseño de panel organiza los componentes del formulario en secciones o paneles diferenciados.

![Diseño de panel que muestra varias secciones distintas en un formulario](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Ejemplo:** un formulario de solicitud de empleo puede usar paneles para separar “Información personal”, “Educación”, “Experiencia laboral” y “Referencias” en secciones distintas.

**Comportamiento adaptable:** en pantallas más pequeñas, los paneles suelen apilarse verticalmente, lo que mantiene sus agrupaciones diferenciadas al tiempo que se ajustan a una anchura más estrecha.

Puede usar el [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para añadir el diseño de panel en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de panel, consulte el artículo [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

### Diseño de asistente

El diseño de asistente ayuda a simplificar un formulario complejo dividiéndolo en distintos pasos. Cada paso representa una parte diferente del proceso y los usuarios navegan por los pasos secuencialmente, a menudo con los botones **Siguiente** y **Atrás**. Puede utilizar el diseño de asistente para crear un formulario que incluya varias secciones o pasos.

![Diseño de asistente que muestra un formulario de varios pasos con controles de navegación](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Ejemplo:** un formulario de reclamación de seguro puede utilizar un diseño de asistente para guiar a los usuarios a la hora de proporcionar detalles del incidente, cargar pruebas, introducir información personal y revisar el envío.

**Comportamiento adaptable:** en dispositivos móviles, el asistente mantiene su enfoque paso a paso, pero adapta el contenido de cada paso para que se ajuste a la pantalla más estrecha y, a menudo, se apilan elementos que aparecerían uno al lado del otro en pantallas más grandes.

Puede usar el [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para añadir el diseño de asistente en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de asistente, consulte el artículo [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

### Diseño de acordeón

El diseño de acordeón muestra el contenido en secciones o paneles contraíbles en un formulario adaptable. Cuando se expande una sección, se muestra el contenido incluido en ella, mientras que las demás secciones permanecen contraídas. Este diseño es ideal para mostrar grandes cantidades de información en un formulario compacto.

![Diseño de acordeón que muestra secciones ampliables en un formulario](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Ejemplo:** un formulario de configuración de producto puede usar secciones de acordeón para “Opciones básicas”, “Características avanzadas”, “Accesorios” y “Planes de pago”, lo que permite a los usuarios centrarse en un aspecto a la vez.

**Comportamiento adaptable:** los acordeones funcionan especialmente bien en dispositivos móviles, ya que conservan espacio vertical de forma natural al mostrar únicamente la sección de contenido expandida, lo que los hace ideales para pantallas más pequeñas.

Puede usar el [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para añadir el diseño de acordeón en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de acordeón, consulte el artículo [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

### ¿Cómo elegir el diseño correcto?

Es importante seleccionar el diseño adecuado para optimizar la experiencia del usuario y la funcionalidad del formulario. La tabla le ayuda a comprender las diferentes opciones de diseño disponibles y le guía para seleccionar el diseño más adecuado según sus necesidades específicas y casos de uso:

| Funcionalidad | Diseño de panel | Diseño de asistente | Diseño de acordeón |
|----------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
| **Propósito** | Agrupa el contenido relacionado en secciones distintas | Guía a los usuarios a través de un proceso o formulario con varias etapas | Organiza el contenido en secciones contraíbles |
| **Estructura** | Secciones distintas | Pasos/páginas secuenciales | Paneles/secciones contraíbles |
| **Navegación** | Haga clic en los encabezados del panel para navegar | - Adelante: botón “Siguiente”<br>- Atrás: botón “Atrás”<br>- Omisión opcional de pasos | Haga clic en los encabezados para expandir o contraer secciones |
| **Experiencia del usuario** | Organiza grandes cantidades de contenido de una manera manejable | Guía paso a paso para reducir la sobrecarga | Vista compacta con secciones expandidas/contraídas |
| **Caso práctico** | Formularios complejos con secciones clasificadas | Configuración de procesos, formularios complejos | Preguntas frecuentes, menús de configuración, secciones de contenido detalladas |
| **Lo mejor para dispositivos móviles** | Moderado: los paneles se apilan verticalmente | Bueno: mantiene el enfoque solo en el paso actual | Excelente: conserva el espacio con secciones contraíbles |

## Prácticas recomendadas para formularios adaptables

Para garantizar que los formularios proporcionen la mejor experiencia en todos los dispositivos, siga estas prácticas recomendadas:

1. **Primero diseñe para dispositivos móviles:** comience por diseñar el formulario para dispositivos móviles y, a continuación, mejórelo para que se ajuste a pantallas más grandes. Este enfoque garantiza que la funcionalidad principal funcione en las pantallas más pequeñas.

2. **Utilice tipos de campo apropiados:** elija tipos de campo que funcionen bien en dispositivos táctiles:
   - Utilice menús desplegables en lugar de botones de opción cuando haya muchas opciones
   - Utilice selectores de fecha diseñados para la entrada táctil
   - Asegúrese de que los botones y los objetivos táctiles tengan al menos 44 px x 44 px

3. **Simplifique el formulario para pantallas más pequeñas:**
   - Muestre menos campos por fila en los dispositivos móviles
   - Considere la posibilidad de ocultar los campos opcionales detrás de una opción “Mostrar más”
   - Divida formularios complejos en más pasos en dispositivos móviles

4. **Realice pruebas exhaustivas:** pruebe siempre los formularios en dispositivos reales o con el modo de emulador en el editor universal para asegurarse de que funcionan correctamente en todos los tamaños de pantalla.

5. **Considere los tiempos de carga:** optimice el tamaño de las imágenes y minimice los recursos necesarios, especialmente para los usuarios de dispositivos móviles, que pueden tener conexiones más lentas.

## Solución de problemas de formularios adaptables

| Problema | Causa posible | Solución |
|-------|---------------|----------|
| El formulario aparece cortado en dispositivos móviles | Configuración de anchura fija o problemas de desbordamiento | Utilice unidades relativas (%, rem) en lugar de píxeles y compruebe las propiedades overflow:hidden |
| Elementos táctiles con los que es difícil interactuar | Objetivos táctiles demasiado pequeños o demasiado juntos | Aumente el tamaño del botón/entrada a al menos 44 px x 44 px y añada más espacio entre los elementos interactivos |
| Desbordamientos de contenido en pantallas pequeñas | No hay reglas adaptables para ventanas gráficas más pequeñas | Añada consultas de medios o clases adaptables para ajustar el diseño en diferentes tamaños de pantalla |
| Formulario demasiado lento en dispositivos móviles | Imágenes grandes o scripts en exceso | Optimice las imágenes, minimice el uso de JavaScript y considere habilitar la carga a medida para los elementos menos importantes |
| Diferencia de apariencia entre el emulador y los dispositivos reales | Representación específica del explorador o variaciones de dispositivo | Realice pruebas en dispositivos reales, siempre que sea posible, y no solo en emuladores |

## Vea también

{#see-more-eds-forms}
