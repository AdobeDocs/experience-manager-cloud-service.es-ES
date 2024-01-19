---
Title: How to integrate AEM workflow with an Adaptive Form?
Description: Explore the process of automated workflow initiation with AEM Forms Submit Action.
keywords: AEM AEM AEM Flujo de trabajo de, Integrar formulario adaptable con flujo de trabajo de formularios adaptables, Invocar flujo de trabajo de envío de acción de flujo de trabajo de
feature: Adaptive Forms, Core Components
source-git-commit: 95af49839d206f67ac02116730229f5b0531c5bb
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 56%

---


# AEM AEM Integración de formularios adaptables de la con el flujo de trabajo: racionalización de los procesos empresariales

El **[!UICONTROL AEM Invocar un flujo de trabajo de]** AEM La acción de envío asocia un formulario adaptable con un flujo de trabajo de. Cuando se envía un formulario, el flujo de trabajo asociado se inicia automáticamente en la instancia de autor. Puede guardar los archivos de datos, los archivos adjuntos y el documento de registro en la ubicación de carga útil del flujo de trabajo o en una variable. Si el flujo de trabajo está marcado y configurado para el almacenamiento de datos externo, solo estará disponible la opción de variable. Puede seleccionar de la lista de variables disponibles para el modelo de flujo de trabajo. Si el flujo de trabajo está marcado para el almacenamiento de datos externos en una fase posterior y no en el momento de la creación del flujo de trabajo, asegúrese de que las configuraciones de variables requeridas estén establecidas.

>[!NOTE]
>
>  Obtenga información sobre cómo [crear un modelo del flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es#extending-aem) para definir la serie de pasos que se ejecutan cuando un usuario inicia el flujo de trabajo. También puede definir propiedades del modelo, como si el flujo de trabajo es transitorio o utiliza varios recursos.

AEM as a Cloud Service ofrece varias acciones de envío listas para usar para administrar los envíos de formularios. Puede obtener más información sobre estas opciones en la [Acción de envío del formulario adaptable](/help/forms/configure-submit-actions-core-components.md)  artículo.

## Ventajas

AEM Algunas de las ventajas de integrar el flujo de trabajo de la con Forms adaptable son:

* AEM La integración del flujo de trabajo de permite la automatización de procesos empresariales complejos que implican envíos de formularios.
* AEM El flujo de trabajo de admite la lógica condicional, lo que permite tomar decisiones dinámicas basadas en datos de formulario o factores externos.
* AEM El flujo de trabajo de enruta las tareas en función de reglas y condiciones predefinidas, lo que garantiza que las tareas se asignen a las personas o grupos adecuados.

<!--
## Prerequisites

Before using the **[!UICONTROL Invoke an AEM Workflow]** Submit Action configure the following for the **[!UICONTROL AEM DS settings service]** configuration: 

* **[!UICONTROL Processing Server URL]**: The Processing Server is the server where the Forms or AEM Workflow is triggered. This can be same as the URL of the AEM author instance or another server.

* **[!UICONTROL Processing Server User Name]**: Workflow user's username

* **[!UICONTROL Processing Server Password]**: Workflow user's password -->

## AEM Integración de flujo de trabajo de con Forms adaptable {#steps-to-integrate-workflow-with-af}

Para configurar el proceso automatizado con [AEM Flujo de trabajo de](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es#extending-aem) para un formulario adaptable, realice los siguientes pasos:

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la pestaña **[!UICONTROL Envío]**.
1. Desde el **[!UICONTROL Acción de envío]** , seleccione la opción **[!UICONTROL AEM Invocar un flujo de trabajo de]** .
   ![Configuración de acción de Enviar correo electrónico](/help/forms/assets/configure-invoke-aem-workflow.png)

1. Seleccione el modelo de flujo de trabajo de **[!UICONTROL Modelo de flujo de trabajo]** lista desplegable.
1. Seleccione una opción de la **[!UICONTROL Almacenar archivo de datos mediante]** lista desplegable.

   **Archivo de datos**: Contiene datos enviados al formulario adaptable. Puede usar la opción **[!UICONTROL Ruta del archivo de datos]** para especificar el nombre y la ruta del archivo en relación con la carga útil. Por ejemplo, la ruta `/addresschange/data.xml` crea una carpeta llamada `addresschange` y la coloca en relación a la carga útil. También puede especificar únicamente `data.xml` para enviar solo los datos enviados sin crear una jerarquía de carpetas. Si el flujo de trabajo está marcado para el almacenamiento de datos externos, utilice la opción de variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.

1. Seleccione una opción de la **[!UICONTROL Almacenar archivos adjuntos mediante]** lista desplegable.

   **Archivos adjuntos**: Puede usar la opción **[!UICONTROL Ruta de archivos adjuntos]** para especificar el nombre de la carpeta en la que se almacenarán los archivos adjuntos cargados en el formulario adaptable. La carpeta se creará en relación con la carga útil. Si el flujo de trabajo está marcado para el almacenamiento de datos externos, utilice la opción de variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.

1. Seleccione una opción de la **[!UICONTROL Documentos de registro mediante]** lista desplegable.

   **Documento de registro**: Contiene el documento de registro generado para el formulario adaptable. Puede usar la opción **[!UICONTROL Ruta del documento de registro]** para especificar el nombre y la ruta del documento de registro en relación con la carga útil. Por ejemplo, la ruta `/addresschange/DoR.pdf` crea una carpeta llamada `addresschange` en relación con la carga útil y coloca `DoR.pdf` en relación con la carga útil. También puede especificar únicamente `DoR.pdf` para guardar solo el documento de registro sin crear una jerarquía de carpetas. Si el flujo de trabajo está marcado para el almacenamiento de datos externos, utilice la opción de variable y seleccione la variable de la lista de variables disponibles para el modelo de flujo de trabajo.
1. Haga clic en **[!UICONTROL Listo]**.

>[!NOTE]
>
> Más información sobre [Flujos de trabajo de centrados en Forms AEM: referencia de pasos para automatizar los procesos empresariales](/help/forms/aem-forms-workflow-step-reference.md).

<!--
## Best Practices

* When configuring the **[!UICONTROL Invoke an AEM Workflow]** Submit Action, select the appropriate workflow model that aligns with the desired business process.
* In case, the workflow involves external data storage, be sure to configure the workflow accordingly. It is recommended to set up variables appropriately and in accordance with any external storage requirements. -->

## Artículos relacionados

{{af-submit-action}}