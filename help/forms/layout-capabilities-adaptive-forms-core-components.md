---
title: ¿Cuáles son las funciones de diseño de los Forms adaptables basadas en componentes principales?
description: El diseño y el aspecto visual de los formularios adaptables en diferentes dispositivos se rigen por la configuración de diseño. Obtenga información sobre los distintos diseños y cómo aplicarlos.
feature: Adaptive Forms, Core Components
keywords: Diseño de un formulario adaptable basado en componentes principales, diferentes diseños para formularios, diseños de formularios dinámicos, AEM, diseños de formulario de AEM Cloud Service, tipos de diseños de formulario en los componentes principales de AEM, diseños de formularios adaptables
role: User, Developer, Admin
exl-id: dcc01d84-0d39-4fa8-ac47-71a9aba91b1e
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '2106'
ht-degree: 21%

---

# Funciones de diseño de Forms adaptable basadas en componentes principales


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/layout-capabilities-adaptive-forms.html?lang=es) |
| AEM as a Cloud Service (componentes de base) | [Haga clic aquí](/help/forms/layout-capabilities-adaptive-forms.md) |
| AEM as a Cloud Service (componentes principales) | Este artículo |

Adaptive Forms proporciona componentes de primera clase para diseñar y diseñar los formularios de forma eficaz. El diseño controla cómo se muestran los componentes en un formulario. Los Forms adaptables admiten varios diseños: panel, asistente, acordeón, pestañas en la parte superior/horizontal y pestañas en la parte izquierda/vertical.

<!-- ![Types of Layout](/help/forms/assets/generic-layout-hero-image.png){align="center"}-->

## Requisito previo

Antes de explorar las distintas funcionalidades de un diseño, asegúrese de que los componentes principales estén habilitados para su entorno. Instale la última versión para habilitar los componentes principales adaptables de Forms para su entorno de AEM Cloud Service.

## Tipos de diseño de Forms adaptables

El formulario adaptable basado en componentes principales admite los siguientes tipos de diseños:
* **Diseño de panel**
* **Diseño del asistente**
* **Diseño vertical**
* **Diseño horizontal**
* **Diseño de acordeón**

>[!BEGINTABS]

>[!TAB Diseño de panel]

El diseño de panel es útil para organizar los campos relacionados de una manera que facilite la navegación y la búsqueda del contenido correspondiente. El diseño del panel organiza los componentes del formulario en secciones o paneles distintos de un formulario adaptable.

![Diseño de panel](/help/forms/assets/panel-layout.png)

Diseño de panel

Puede usar el [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) para añadir el diseño de panel en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de panel, consulte el artículo [componente de panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).

>[!TAB Diseño de asistente]

El diseño de asistente ayuda a simplificar un formulario complejo dividiéndolo en distintos pasos. Cada paso representa una parte diferente del proceso y los usuarios navegan por los pasos secuencialmente, a menudo con los botones **Siguiente** y **Anterior**. Puede utilizar el diseño de asistente para crear un formulario que incluya varias secciones o pasos.

![Diseño de asistente](/help/forms/assets/wizard-layout-compare.gif)

Diseño de asistente

Puede usar el [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) para añadir el diseño de asistente en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de asistente, consulte el artículo [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).

>[!TAB Diseño de fichas verticales]

El diseño de pestañas verticales también se conoce como pestañas en el diseño izquierdo. El diseño de pestañas verticales organiza los paneles o las secciones a lo largo del lado izquierdo de un formulario. Es un diseño común para los formularios en los que los paneles/secciones se apilan verticalmente para facilitar la lectura y la navegación.

![Diseño vertical](/help/forms/assets/vertical-tab.gif)

Diseño de pestañas verticales

Puede usar el componente [fichas verticales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) para agregar el diseño de fichas verticales en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de fichas verticales, consulte el artículo [componente de fichas verticales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs).


>[!TAB Diseño horizontal de fichas]

El diseño de pestañas horizontales también se conoce como Tabulaciones en el diseño superior. El diseño de pestañas horizontales organiza los paneles o las secciones en paralelo en una fila. Este diseño presenta las secciones del formulario de forma lineal en toda la anchura del formulario o panel.


![Diseño horizontal](/help/forms/assets/horizontal-layout.gif)

Diseño de pestañas horizontales

Puede usar el componente [pestañas horizontales](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs) para agregar el diseño de pestañas horizontales en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de pestañas horizontales, consulte el artículo [componente de pestañas horizontales](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs).


>[!TAB Diseño de acordeón]

El diseño de acordeón muestra el contenido en secciones o paneles contraíbles en un formulario adaptable. Cuando se expande una sección, se muestra el contenido incluido en ella, mientras que las demás secciones permanecen contraídas. Este diseño es ideal para mostrar grandes cantidades de información en un formulario compacto.

![Diseño de acordeón](/help/forms/assets/accordion-layout-compare.gif)

Diseño de acordeón

Puede usar el [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) para añadir el diseño de acordeón en un formulario. Para obtener instrucciones detalladas sobre cómo configurar las distintas propiedades del componente de acordeón, consulte el artículo [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).

>[!ENDTABS]

Para aprender a insertar un diseño y agregarle componentes de formulario, consulte la sección titulada [¿Cómo insertar un diseño y agregarle componentes de formulario?](#how-to-insert-a-layout-and-add-form-components-to-it)

### ¿Cómo elegir el diseño de formulario adaptable adecuado?

Es importante seleccionar el diseño de formulario adaptable adecuado para optimizar la experiencia del usuario y la funcionalidad del formulario. La tabla le ayuda a comprender las diferentes opciones de diseño disponibles y le guía en la selección del diseño más adecuado según sus necesidades específicas y casos de uso:

| Funcionalidad | Diseño de panel | Diseño de asistente | Fichas del diseño de fichas superior/vertical | Fichas del diseño de pestañas izquierda/horizontal | Diseño de acordeón |
|--------------------------|-----------------------------------------------------|----------------------------------------------------|-----------------------------------------------------|--------------------------------------------------------|--------|
| **Propósito** | Agrupa el contenido relacionado en secciones distintas | Guía a los usuarios a través de un proceso o formulario con varias etapas | Permite cambiar entre secciones o vistas en la misma página | Similar a las pestañas superiores, pero organizado verticalmente a la izquierda | Organiza el contenido en secciones contraíbles |
| **Estructura** | Secciones distintas | Pasos/páginas secuenciales | Tabulaciones horizontales en la parte superior | Tabulaciones verticales a la izquierda | Paneles/secciones contraíbles |
| **Navegación** | Haga clic en los encabezados del panel para navegar | - Adelante: botón “Siguiente”<br>- Atrás: botón “Atrás”<br>- Omisión opcional de pasos | Haga clic en las pestañas para cambiar de sección | Haga clic en las pestañas para cambiar de sección | Haga clic en los encabezados para expandir o contraer secciones |
| **Experiencia del usuario** | Organiza grandes cantidades de contenido de una manera manejable | Guía paso a paso para reducir la sobrecarga | Conmutación entre vistas clara y accesible | Uso eficiente del espacio vertical, pestañas siempre visibles | Vista compacta con secciones expandidas/contraídas |
| **Caso práctico** | Formularios complejos con secciones clasificadas | Configuración de procesos, formularios complejos | Organización de configuraciones o categorías de contenido | Paneles, vistas de datos complejas | Preguntas frecuentes, menús de configuración, secciones de contenido detalladas |


## ¿Cómo se inserta un diseño y se le agregan componentes de formulario?

El diagrama siguiente muestra los pasos para insertar un diseño en un formulario y agregarle componentes de formulario:

![Flujo de trabajo para agregar un diseño y componentes de formulario](/help/forms/assets/workflow-to-add-component-to-a-layout.png)

Considere el **formulario de solicitud de TI** que se muestra en la sección [Tipos de diseños adaptables de Forms](#adaptive-forms-layout-types). El formulario recopila información de los empleados que tienen problemas técnicos relacionados con su red o portátil. Incluye tres paneles:

* **Detalles del empleado**: el panel recopila información sobre el empleado y contiene tres cuadros de texto denominados Nombre, Id. de correo electrónico y Departamento.

* **Detalles del problema**: el panel captura los detalles del problema. Incluye una casilla de verificación para la categoría del problema con tres opciones: Red, Equipo u Otro. También incluye dos cuadros de texto etiquetados como Especifique y Comentarios.

* **Archivos adjuntos**: el panel permite a los usuarios cargar documentos de soporte relacionados con el problema.

Exploremos el proceso paso a paso para insertar un diseño y agregarle componentes. En este ejemplo, se inserta un diseño de pestañas horizontales en un formulario.

### &#x200B;1. Insertar un componente de diseño en un formulario

1. Inicie sesión en su instancia de [!DNL Experience Manager Forms].
1. En la esquina superior izquierda, seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
1. Abra un formulario adaptable existente en modo de edición si ya se ha creado.

   ![Abrir un formulario adaptable](/help/forms/assets/insert-layout.png)

   También puede [crear un nuevo formulario adaptable](/help/forms/creating-adaptive-form-core-components.md).

1. Busque la sección en el editor de formularios que le permite agregar un diseño.

   ![Editor de formularios](/help/forms/assets/form-editor.png)
1. Haga clic en el icono **Añadir**. El icono es un signo más (+) que representa la opción de añadir nuevos componentes.

   ![Insertar diseño](/help/forms/assets/insert-layout-add-icon.png)

   Al hacer clic en el icono **Añadir** aparece un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   >[!NOTE]
   >
   > También puede [arrastrar y soltar el componente de diseño](#extra-bytes).

1. Examine los componentes disponibles en el cuadro de diálogo y seleccione el diseño que desee en la lista. En nuestro caso, seleccionamos el componente Pestañas horizontales para insertar el diseño de pestañas horizontales.

   ![Seleccionar fichas horizontales](/help/forms/assets/select-horizontal-tab.png)

   Al agregar el componente de pestañas horizontales al formulario, inicialmente consta de dos paneles vacíos, llamados Item1 y Item2, de forma predeterminada. Debe agregar manualmente componentes de formulario a estos paneles.

   ![Pestañas horizontales](/help/forms/assets/insert-tabs-on-top.png)

1. Abra las propiedades del componente pestañas horizontales y especifique el nombre del componente.
Por ejemplo, en este caso, agregamos el nombre del componente de pestañas horizontales como Formulario de solicitud de TI.

   ![Agregar nombre para fichas horizontales](/help/forms/assets/change-name-of-horizontal-tabs.png)

1. Haga clic en **Listo**.

   ![Pestañas horizontales](/help/forms/assets/tabs-on-top-rename-component.png)

Una vez añadido el componente de diseño en el formulario, modifique el número de paneles según los requisitos.

### &#x200B;2. Agregar paneles al diseño

Agregar un nuevo panel al componente de pestañas horizontales:

1. Abra las propiedades del componente de pestañas horizontales y haga clic en la pestaña **Elementos**.

   ![Ficha de elementos para fichas horizontales](/help/forms/assets/tabs-on-top-items-tab.png)

1. Haga clic en el icono **Agregar** para agregar un panel nuevo.

   ![Agregar nuevo panel](/help/forms/assets/tabs-on-top-add-panel.png)

   Al hacer clic en el icono **Agregar**, aparece el cuadro de diálogo **Insertar nuevo componente**.

1. Seleccione el componente del panel.

   ![Agregar nuevo panel](/help/forms/assets/tabs-on-top-new-panel.png)

   Al seleccionar el componente Panel, el nuevo panel se agrega al diseño horizontal.

   ![Agregar nuevo panel](/help/forms/assets/tabs-on-top-add-new-panel.png)

   Proporcione un nombre para el nuevo panel; de lo contrario, no podrá guardar las propiedades del componente de pestañas horizontales.

1. Especifique los nombres de los paneles como se muestra en la figura siguiente:

   ![Nombres de panel](/help/forms/assets/tabs-on-tops-panel-name.png)

1. Haga clic en **Listo**.

   Una vez que haga clic en **Listo**, los tres paneles aparecerán uno al lado del otro en una fila. Los nombres de panel se muestran como encabezados para cada panel y puede agregar componentes de formulario a cada panel.

   ![Nombres de panel](/help/forms/assets/tabs-on-top-initial-view.png)

   Puede configurar las propiedades del componente del panel. Por ejemplo, el formulario de solicitud de TI no incluye títulos de panel. A continuación se indican los pasos para configurar las propiedades del componente de panel.

1. Abra las propiedades del primer panel.

   ![Propiedades del panel 1](/help/forms/assets/tabs-on-tops-panel1-properties.png)

1. Seleccione la casilla de verificación **Ocultar título** de la ficha **Básico**.

   ![Ocultar título](/help/forms/assets/tabs-on-top-hide-panel.png)

1. Haga clic en **Listo**.

Del mismo modo, también puede ocultar los títulos de los otros dos paneles. Una vez finalizado, puede continuar agregando componentes de formulario a cada panel.

### &#x200B;3. Agregar componentes de formulario al panel

<!-- You can employ one of the following method to add form components to the panel:
* [Add components to a layout's panel using the Add icon](#add-components-to-a-layouts-panel-using-the-add-icon)
* [Drag and drop components into a layout's panel](#drag-and-drop-components-into-a-layouts-panel) -->

1. Busque la sección dentro del panel que le permite agregar componentes.
1. Haga clic en el icono **Añadir**. El icono es un signo más (+) que representa la opción de añadir nuevos componentes.
   ![Insertar diseño](/help/forms/assets/tabs-on-top-add-component.png)

   Al hacer clic en el icono **Añadir** aparece un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   ![Insertar nuevo componente (Cuadro de diálogo)](/help/forms/assets/insert-new-component.png)

1. Examine los componentes disponibles en el cuadro de diálogo que aparece y seleccione el componente deseado. En este caso, seleccione el componente Cuadro de texto.
1. Abra las propiedades del componente agregado y especifique su nombre. Permite editar las propiedades del componente Cuadro de texto agregado y especificar su nombre.
   ![Insertar diseño](/help/forms/assets/tabs-on-top-textbox-component.png)
1. Del mismo modo, agregue dos componentes de cuadro de texto más y asigne un nombre a los componentes como ID de correo electrónico y Departamento.\
   ![Primer panel](/help/forms/assets/tabs-on-tops-first-panel.png)

   Ahora que se han agregado los componentes del primer panel, puede continuar agregando los componentes al segundo panel.

1. Para cambiar el panel, haga clic en **Seleccionar panel** en la barra de herramientas.

   ![Panel de conmutación](/help/forms/assets/tabs-on-top-select-panel.png)

   Al hacer clic en **Seleccionar panel**, aparece la lista de los paneles agregados en el componente Pestañas horizontales.

   ![Panel de conmutación](/help/forms/assets/tabs-on-tops-panel2.png)

1. Seleccione **2 panel** de la lista de paneles y la vista cambiará del primer panel al segundo.

   ![Segundo panel](/help/forms/assets/tabs-on-top-panel2-component.png)

1. Repita los pasos descritos del paso 2 al paso 4 para añadir los componentes deseados en el panel 2, como se muestra en la siguiente figura:

   ![Componentes del segundo panel](/help/forms/assets/panel-2-components.png)

1. Cambie al panel **3** siguiendo los pasos descritos en los pasos 6 y 7.

1. Repita los pasos descritos del paso 2 al paso 4 para agregar el componente deseado en el panel 3:

   ![Componentes del tercer panel](/help/forms/assets/panel-3-component.png)

1. Haga clic en **[!UICONTROL Vista previa]** en la esquina superior derecha del entorno de creación.
   ![Diseño horizontal](/help/forms/assets/horizontal-layout.gif)

También puede [arrastrar y soltar los componentes](#extra-bytes) para agregar los componentes del formulario a cada panel.


<!-- #### Drag and drop components into a layout's panel 

1. Locate the section within the panel that allows you to add components. 
2. Navigate to the left panel within your authoring environment and click **Components**.

    ![Component Panel](/help/forms/assets/add-new-component.png){width="200" align="center"}

    When you click the **Components** option, the list of the available components appears.   

    ![Component Panel](/help/forms/assets/add-new-component2.png){width="200" align="center"}

3. Browse the available components and select the Text Box component.

4. Drag the component by clicking and holding the selected component, then drag it over to the panel area to place it.

5. Drop the component into the panel by releasing the mouse. 

6. Open the properties of the added Text Box component and specify its name as Name.
    ![Insert layout](/help/forms/assets/tabs-on-top-textbox-component.png){width="200" align="center"}
7. Similarly, add two more Text Box components and name added the components as Email ID and Department.   
    ![First Panel](/help/forms/assets/tabs-on-tops-first-panel.png){width="200" align="center"}

    Now that the components in the first panel have been added, you can proceed with adding the components to the second panel. 

8. To switch the panel, click **Select Panel** from the toolbar. 

    ![Switch Panel](/help/forms/assets/tabs-on-top-select-panel.png){width="200" align="center"}

    When you click the **Select Panel**, the list of the added panels in the Horizontal Tabs component appears.

    ![Switch Panel](/help/forms/assets/tabs-on-tops-panel2.png){width="200" align="center"}

9. Select **2 Panel** from the panel list and the view changes from the first panel to the second panel.

    ![Second Panel](/help/forms/assets/tabs-on-top-panel2-component.png){width="200" align="center"}

10. Repeat the steps outlined from Step 2 to Step 6 for adding the desired components in panel 2 as shown in the below figure:   

     ![Second Panel components](/help/forms/assets/panel-2-components.png){width="200" align="center"}

11. Switch to the **3 Panel** by following the steps outlined in Step 8 and Step 9.

12. Repeat the steps outlined from Step 2 to Step 6 for adding the desired component in panel 3:

    ![Third Panel components](/help/forms/assets/panel-3-component.png){width="200" align="center"} 

    -->



También puede eliminar el componente de formulario del panel mediante el icono ![Eliminar icono](/help/forms/assets/Smock_Delete_18_N.svg).

![Eliminando un componente](/help/forms/assets/delete-component.png)

También puede añadir las validaciones necesarias para los componentes según sea necesario.

## ¿Cómo reemplazar un diseño existente por uno nuevo?

Puede reemplazar la presentación de un formulario por una nueva presentación, que implica modificar cómo se organizan y muestran los componentes dentro de un formulario.

Siga estos pasos para reemplazar la presentación existente de un formulario:

1. Haga clic en el icono Reemplazar de la barra de herramientas del componente de diseño y aparecerá el cuadro de diálogo **[!UICONTROL Reemplazar componente]**.

   ![Reemplazar diseño](/help/forms/assets/replace-layout.png)

1. Seleccione el diseño que desee en el cuadro de diálogo **[!UICONTROL Reemplazar componente]**.

   ![Cuadro de diálogo Reemplazar componente](/help/forms/assets/replace-component.png)

   Después de seleccionar el diseño, la disposición de los componentes dentro del diseño cambia en consecuencia. Por ejemplo, seleccione el componente de fichas verticales del cuadro de diálogo **[!UICONTROL Reemplazar componente]**; la disposición del panel cambiará a fichas a la izquierda:

   ![Diseño vertical](/help/forms/assets/vertical-tab.gif)

## Bytes adicionales

Para arrastrar y soltar componentes en el editor de formularios, realice los siguientes pasos:

1. Busque la sección que le permite agregar componentes.
1. Vaya al panel izquierdo del entorno de creación y haga clic en **Componentes**.

   ![Panel de componentes](/help/forms/assets/add-new-component.png)

   Al hacer clic en la opción **Componentes**, aparece la lista de los componentes disponibles.

   ![Panel de componentes](/help/forms/assets/add-new-component2.png)

1. Examine los componentes disponibles y seleccione el componente deseado.

1. Arrastre el componente haciendo clic y manteniendo presionado el componente seleccionado, y después arrástrelo al área del panel para colocarlo.

1. Suelte el componente en el panel soltando el ratón.

## Próximos pasos

Una vez que conozca las distintas funcionalidades de diseño de un formulario adaptable basado en componentes principales, puede pasar a los siguientes pasos:

* [Cree su primer formulario adaptable basado en componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Crear y utilizar temáticas de formularios adaptables](/help/forms/using-themes-in-core-components.md)



## Véase también

{{see-also}}
