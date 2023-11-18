---
title: Aplicación de flujos de trabajo a páginas
description: Durante la creación, puede invocar flujos de trabajo para que actúen en las páginas; también es posible aplicar más de un flujo de trabajo.
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 83%

---

# Aplicación de flujos de trabajo a páginas {#applying-workflows-to-pages}

Durante la creación, puede invocar flujos de trabajo para que actúen en las páginas; también es posible aplicar más de un flujo de trabajo.

A la hora de aplicar el flujo de trabajo, se especifica la siguiente información:

* Flujo de trabajo que se va a aplicar.
   * Puede aplicar cualquier flujo de trabajo (al que tenga acceso, según lo haya asignado el administrador de AEM).
* De forma opcional, un título que ayude a identificar la instancia de flujo de trabajo en la bandeja de entrada del usuario.
* La carga útil de los flujos de trabajo; pueden ser una o varias páginas.

Los flujos de trabajo se pueden iniciar desde:

* [la consola Sitios](#starting-a-workflow-from-the-sites-console).
* [al editar una página, en Información de la página](#starting-a-workflow-from-the-page-editor). 

>[!NOTE]
>
>Consulte también lo siguiente:
>
>* Cómo aplicar flujos de trabajo a recursos DAM.
>* [Uso de flujos de trabajo de proyecto](/help/sites-cloud/authoring/projects/workflows.md).

<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>Los administradores de AEM pueden iniciar flujos de trabajo mediante varios métodos.

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Inicio de un flujo de trabajo desde la consola Sites {#starting-a-workflow-from-the-sites-console}

Puede iniciar un flujo de trabajo desde las ubicaciones siguientes:

* [la opción Crear de la barra de herramientas del sitio](#starting-a-workflow-from-the-sites-toolbar).
* [el carril Escala de tiempo de la consola Sitios](#starting-a-workflow-from-the-timeline).

En ambos casos, debe [Especifique los Detalles del flujo de trabajo en el Asistente de creación de flujos de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Inicio de un flujo de trabajo desde la barra de herramientas de Sites {#starting-a-workflow-from-the-sites-toolbar}

Puede iniciar un flujo de trabajo desde la barra de herramientas de la consola **Sitios**:

1. Busque y seleccione la página deseada. 

1. En la opción **Crear** de la barra de herramientas, ahora puede seleccionar el **Flujo de trabajo**.

   ![Crear flujo de trabajo desde la barra de herramientas](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. El asistente **Crear flujo de trabajo** le ayudará a [especificar los detalles del flujo de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Inicio de un flujo de trabajo desde la cronología {#starting-a-workflow-from-the-timeline}

Desde la **Cronología** puede iniciar un flujo de trabajo para aplicarlo al recurso seleccionado.

1. [Seleccione el recurso](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) y abra [Cronología](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) (o abra Cronología y seleccione el recurso).
1. La punta de flecha junto al campo Comentario puede utilizarse para mostrar **Iniciar flujo de trabajo**:

   ![Crear flujo de trabajo a partir de la cronología](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. El asistente **Crear flujo de trabajo** le ayudará a [especificar los detalles del flujo de trabajo](#specifying-workflow-details-in-the-create-workflow-wizard).

### Especificación de los detalles del flujo de trabajo en el asistente Crear flujo de trabajo {#specifying-workflow-details-in-the-create-workflow-wizard}

El asistente **Crear flujo de trabajo** le ayudará a seleccionar el flujo de trabajo y a especificar los detalles necesarios.

Después de abrir el asistente **Crear flujo de trabajo** desde:

* [la opción Crear de la barra de herramientas del sitio](#starting-a-workflow-from-the-sites-toolbar).
* [el carril Escala de tiempo de la consola Sitios](#starting-a-workflow-from-the-timeline).

Puede especificar los detalles:

1. En la etapa **Propiedades**, se definen las opciones básicas del flujo de trabajo:

   * **Modelo de flujo de trabajo**
   * **Título del flujo de trabajo**

      * Puede especificar un título para esta instancia, de modo que pueda identificarla en una etapa posterior.

   Según el modelo de flujo de trabajo, también están disponibles las siguientes opciones. Estas permiten conservar el paquete creado como carga útil después de que se haya completado el flujo de trabajo.

   * **Conservar paquete de flujo de trabajo**
   * **Título del paquete**

      * Puede especificar un título para el paquete para facilitar su identificación.

   >[!NOTE]
   >
   >La opción **Mantener paquete de flujo de trabajo** está disponible cuando el flujo de trabajo se ha configurado para la compatibilidad con varios recursos y se han seleccionado varios recursos.

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   Cuando haya terminado, seleccione **Siguiente** para continuar.

   ![Especificación de las propiedades del flujo de trabajo](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. En la etapa **Ámbito**, puede seleccionar lo siguiente:

   * **Añadir contenido** para abrir [explorador de rutas](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) y seleccione recursos adicionales; en el explorador, seleccione **Seleccionar** para añadir el contenido a la instancia de flujo de trabajo.

   * Un recurso existente para ver acciones adicionales:

      * **Incluir elementos secundarios** para especificar que en el flujo de trabajo se incluyen los elementos secundarios de ese recurso.
Se abre un cuadro de diálogo para que pueda ajustar la selección según lo siguiente:

         * Incluir solo los elementos secundarios inmediatos.
         * Incluir solo las páginas modificadas.
         * Incluir solo las páginas ya publicadas.

        Los elementos secundarios especificados se añaden a la lista de recursos a los que se aplicará el flujo de trabajo.

      * **Eliminar la selección** para eliminar ese recurso del flujo de trabajo.

   ![Definición del ámbito del flujo de trabajo](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >Si agrega recursos adicionales, puede utilizar **Atrás** para ajustar la configuración **Mantener flujo de trabajo del paquete** en el paso **Propiedades**.

1. Use la opción **Crear** para cerrar el asistente y crear la instancia de flujo de trabajo. Se muestra una notificación en la consola Sites.

## Inicio de un flujo de trabajo desde el Editor de página {#starting-a-workflow-from-the-page-editor}

Al editar una página, puede seleccionar **Información de página** en la barra de herramientas. El menú desplegable tiene la opción **Iniciar en flujo de trabajo**. Esto abre un cuadro de diálogo en el que puede especificar el flujo de trabajo requerido, junto con un título si es necesario:

![Inicio de un flujo de trabajo desde el Editor de página](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
