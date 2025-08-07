---
title: Creación de paneles repetibles en los componentes principales del formulario adaptable
description: Aprenda a crear secciones o campos repetibles en un formulario adaptable.
role: Architect, Developer, Admin, User
feature: Adaptive Forms, Core Components
exl-id: 02521bf3-83c1-40a0-8fe6-23af240727e9
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 99%

---

# Crear formularios con secciones repetibles (componentes principales) {#repeat-panel}


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-forms-repeatable-sections.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Una sección repetible hace referencia a una parte de un formulario que se puede duplicar o repetir varias veces para recopilar información para instancias de los mismos datos.

Por ejemplo, considere un formulario utilizado para recopilar información sobre la experiencia laboral de una persona. Puede tener una sección repetible para capturar los detalles de cada trabajo anterior. La sección repetible generalmente contiene campos como nombre de la empresa, cargo, fechas de empleo y responsabilidades del puesto. El usuario puede agregar varias instancias de la sección repetible para introducir información sobre cada trabajo que ha realizado.

![Repetibilidad](/help/forms/assets/repeatable-adaptive-form-example.gif)

Al final de este artículo, aprenderá lo siguiente:

* Crear una sección repetible en un formulario adaptable
* Definir el número mínimo o máximo de repeticiones para un componente de formulario adaptable
* Utilizar el editor de reglas para configurar las acciones de adición o eliminación para secciones repetibles

Puede utilizar los componentes [Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel), [Acordeón](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms//adaptive-forms-components/accordion.html?lang=es), [Pestañas horizontales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=es), [Pestañas verticales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) o [Asistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=es) para que las secciones de un formulario adaptable sean repetibles. Puede añadir componentes secundarios a estos componentes para crear secciones repetibles en un formulario.


Los ejemplos de este documento se basan en el componente [Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel). Puede seguir los mismos pasos para que los componentes [Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel), [Acordeón](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms//adaptive-forms-components/accordion.html?lang=es), [Pestañas horizontales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=es), [Pestañas verticales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs) o [Asistente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=es) sean repetibles.

## Agregar o eliminar secciones repetibles en un formulario {#add-or-delete-repeatable-section-in-panel-container}

Para repetir un panel en el formulario o quitar paneles repetibles, un autor de formularios utiliza un componente de botón para agregar o quitar instancias del panel. Para agregar o eliminar secciones repetibles (paneles) en un formulario, haga lo siguiente:

* [Hacer repetible el contenedor del panel](#make-panel-container-repeatable)
* [Añada una sección repetible](#add-repeatable-section-using-instance-manager-via-scripts)
* [Elimine las secciones repetibles](#delete-repeatable-section-using-instance-manager-via-scripts)

### Hacer repetible el contenedor del panel {#make-panel-container-repeatable}

![Pestaña Accesibilidad](/help/forms/assets/repeat-panel.png)

Para hacer que un panel sea repetible, realice los siguientes pasos:

1. Seleccione un contenedor de panel y seleccione ![cmppr](/help/forms/assets/cmppr.png).
1. Haga clic en **repetir panel** y active la opción para **hacer repetible el panel**.
1. Establezca **repeticiones mínimas** según sea necesario para las secciones mínimas repetibles. Puede establecer las **repeticiones mínimas** a cero para la no repetición de paneles o para quitar los paneles repetidos. De forma predeterminada, el valor de repetición mínima es cero.
1. Establezca **repeticiones máximas** para repetir el panel el número de veces necesarias. De forma predeterminada, el valor es infinito.

   >[!NOTE]
   >
   > 
   > * La repetición mínima no puede ser un valor -ve.
   > * Para crear un panel no repetible, establezca el valor del campo máximo y mínimo en uno.

### Adición de una sección repetible mediante Instance Manager (mediante secuencias de comandos) {#add-repeatable-section-using-instance-manager-via-scripts}

El elemento principal del panel que se va a repetir debe contener un botón de adición para administrar la instancia de repetición del panel. Realice los siguientes pasos para insertar botones en el elemento principal y habilitar scripts en los botones:

1. Añada un **componente de botón** al elemento principal del panel. En el siguiente vídeo de ejemplo, se utiliza un componente de botón con el nombre de etiqueta **Agregar** y el nombre de campo **AgregarPanel**. Seleccione el componente y seleccione ![edit-rules](/help/forms/assets/edit-rules.png). Las reglas del botón se abren en el editor de reglas.
1. En la ventana Editor de reglas, haga clic en **Crear**.

   Seleccione **Editor visual** en la fila Objetos y funciones de formularios.

   1. En el área de regla, en CUANDO, **se hace clic** en seleccionar estado.
   1. En LUEGO, seleccione **Añadir instancia**, y arrastre y suelte el panel mediante el ![panel lateral de alternancia](/help/forms/assets/toggle-side-panel.png) o selecciónelo utilizando **Colocar objeto o seleccionar aquí.**

   Seleccione **Editor de código** en la fila Objetos y funciones de formularios. Haga clic en **Editar reglas** y en el área de código:

   * Para crear un botón de añadir panel, especifique `this.panel.instanceManager.addInstance()`

   Haga clic en **Listo**.

>[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)


### Eliminar secciones repetibles con Instance Manager (mediante secuencias de comandos) {#delete-repeatable-section-using-instance-manager-via-scripts}

El elemento principal del panel debe contener un botón de eliminación para eliminar la instancia de los paneles repetibles. Realice los siguientes pasos para insertar botones en el elemento principal y habilitar secuencias de comandos en los botones para eliminar paneles repetibles:

1. Añada un **componente de botón** al elemento principal del panel. En el siguiente vídeo, se utiliza un componente de botón con el nombre de etiqueta **eliminar** y nombre de campo **EliminarPanel**. Seleccione el componente y seleccione ![edit-rules](/help/forms/assets/edit-rules.png). Las reglas del botón se abren en el editor de reglas.
1. En la ventana Editor de reglas, haga clic en **Crear**.

   Seleccione **Editor visual** en la fila Objetos y funciones de formularios.

   1. En el área de reglas, en CUANDO **EliminarPanel**, **se hace clic** en seleccionar estado.
   1. En LUEGO, seleccione **Quitar instancia**, y arrastre y suelte el panel utilizando el ![panel lateral de alternancia](/help/forms/assets/toggle-side-panel.png) o selecciónelo utilizando **Colocar objeto o seleccionar aquí.**

   Seleccione **Editor de código** en la fila Objetos y funciones de formularios. Haga clic en **Editar reglas** y en el área de código:

   * Para crear un botón de eliminar panel, especifique `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

   Haga clic en **Listo**.

>[!VIDEO](https://video.tv.adobe.com/v/3421620/adaptive-forms-repeatable-sections)

>[!NOTE]
>
>Si un campo pertenece a un panel repetible, no puede acceder a él directamente utilizando su nombre en los scripts. Para acceder al campo, especifique la instancia repetible a la que pertenece el campo utilizando la API de `instances` en `InstanceManager`. La sintaxis para usar la API de `instances` en `InstanceManager` es la siguiente:
>
>
>`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
>
>
>Por ejemplo, crea un formulario adaptable con un panel repetible que tiene un cuadro de texto. Cuando rellene automáticamente el formulario con tres cuadros de texto repetibles, necesitará el siguiente xml:
>
>
>`<panel1><textbox1>AA1</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA2</panel1></textbox1>`
>
>
>`<panel1><textbox1>AA3</panel1></textbox1>`
>
>
>Para leer datos de AA1, especifique:
>
>
>`Panel1.instanceManager.instances[0].textbox.value`
>
>
>Para leer datos de AA2, especifique:
>
>
>`Panel1.instanceManager.instances[1].textbox.value`
>
>
>

>[!NOTE]
>
> Cuando todas las instancias de un panel se quiten de un formulario adaptable, para agregar una instancia del panel quitado, utilice la sintaxis _panelName para capturar el Instance Manager del panel y use la API addInstance de Instance Manager para agregar la instancia eliminada. Por ejemplo, &#39;_panelName.addInstance()&#39;. Añade una instancia del panel eliminado.

## Usar subformularios repetibles de la plantilla de formulario (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

El subformulario repetible es similar a los paneles repetibles de los formularios adaptables. En AEM Forms Designer, realice los siguientes pasos para crear un subformulario repetible:

1. En la paleta Jerarquía, seleccione el subformulario principal del subformulario que desea que se repita.
1. En la paleta Objeto, haga clic en la pestaña Subformulario y seleccione De posición variable en la lista Contenido.
1. Seleccione el subformulario que desea repetir.
1. En la paleta Objeto, haga clic en la pestaña Subformulario y seleccione De posición variable o De posición fija en la lista Contenido.
1. Haga clic en la pestaña Enlace y seleccione Repetir subformulario para cada elemento de datos.
1. Para especificar el número mínimo de repeticiones, seleccione Mínimo y escriba un número en el cuadro correspondiente. Si la opción se ajusta a 0 y no se suministran datos para los objetos del subformulario en el momento de la combinación de datos, el subformulario no se coloca al procesar el formulario.
1. Para especificar el número máximo de repeticiones de subformulario, seleccione Máx. y escriba un número en el cuadro correspondiente. Si no se especifica un valor en el cuadro Máx., el número de repeticiones de subformulario es ilimitado.
1. Para especificar un número definido de repeticiones de subformulario, independientemente de la cantidad de datos, seleccione la opción Recuento inicial y escriba un número en el cuadro correspondiente. Si se selecciona esta opción y no hay ningún dato disponible o existen menos entradas de datos que el valor especificado en Recuento inicial, las instancias vacías del subformulario todavía se colocan en el formulario.
1. Agregue dos botones en el subformulario principal: uno para añadir instancias y otro para eliminar instancias de subformularios repetibles. Para ver los pasos detallados, consulte [Generar una acción](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Ahora, vincule la plantilla del formulario al formulario adaptable. Para ver los pasos detallados, consulte [Crear un formulario adaptable basado en una plantilla](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=es#create-an-adaptive-form-based-on-an-xfa-form-template).
1. Utilice los botones creados en el paso 9 para añadir y quitar subformularios.

El archivo .zip adjunto contiene un subformulario repetible de ejemplo.

[Obtener archivo](/help/forms/assets/samplerepeatablesubform.zip)

## Utilizar la configuración repetida de un esquema XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Puede crear paneles repetibles a partir de un esquema XML y de la propiedad minOccours y maxOccurs de cualquier elemento de tipo complejo. Para obtener información detallada sobre el esquema XML, consulte [Crear formularios adaptables mediante el esquema XML como modelo de formulario](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-xml-schema-form-model.html?lang=es).

En el siguiente código, el panel `SampleType` utiliza la propiedad minOccours y maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```


## Consulte también {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
>* [Create style or themes for your forms](using-themes-in-core-components.md)
>* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
>* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/console-layout.md)

-->