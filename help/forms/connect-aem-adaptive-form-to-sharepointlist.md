---
title: AEM ¿Cómo conectar el formulario adaptable a la lista de Microsoft® SharePoint?
description: Conectar un formulario adaptable a la lista de Microsoft® SharePoint. Obtenga información sobre cómo configurar la lista de Microsoft® SharePoint y crear un modelo de datos de formulario con la configuración. Además, aprenderá a integrar el FDM con su formulario adaptable.
role: User, Developer
keywords: conecte el formulario adaptable a la lista de Microsoft SharePoint, conecte el formulario adaptable a la lista de Microsoft SharePoint, integre el formulario adaptable a la lista de Microsoft SharePoint, integre el formulario adaptable a la lista de AEM AEM, envíe datos de un formulario adaptable a la lista de Microsoft, envíe el flujo de trabajo a la lista de SharePoint y envíe el formulario adaptable a la lista de SharePoint AEM SharePoint.
source-git-commit: 6a8307cd5e53a9568d8fb87f6b2fc5945b6ed8c5
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 4%

---


# Conectar un formulario adaptable a la lista de Microsoft® SharePoint

<span class="preview"> Esta es una función previa al lanzamiento y se puede acceder a ella a través de nuestra [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

**Microsoft® SharePoint**: Microsoft® SharePoint permite la colaboración al proporcionar sitios de equipos dinámicos y eficientes para todos los equipos, departamentos y divisiones. Se utiliza para almacenar, organizar, compartir y acceder a información desde cualquier dispositivo mediante cualquier explorador web, por ejemplo, Microsoft® Edge, Internet Explorer, Chrome o Firefox. Los dos componentes principales de **Microsoft® SharePoint** son:

* **Biblioteca de documentos de Microsoft® SharePoint**: la biblioteca de documentos de Microsoft® SharePoint muestra una lista de archivos y carpetas junto con su información clave, como la fecha de la última modificación y el propietario de un archivo. Esta función facilita la organización y navegación de los archivos.
Para obtener instrucciones sobre cómo integrar un **Biblioteca de documentos de Microsoft® SharePoint** con un formulario adaptable, consulte la [Acción de envío del formulario adaptable](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) artículo.

* **Lista de Microsoft® SharePoint**: la lista de SharePoint de Microsoft® es una colección de datos. Puede agregar columnas para diferentes tipos de datos y crear vistas para mostrar los datos de forma eficaz. Puede agrupar, filtrar, ordenar y dar formato a las listas fácilmente.

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## Requisitos previos para conectar un formulario adaptable a la lista de Microsoft® SharePoint {#prerequisites}

Antes de conectar un formulario adaptable a la lista de Microsoft® SharePoint, realice los siguientes pasos:

1. [Configuración de la lista de Microsoft® SharePoint](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [Crear un modelo de datos de formulario con la configuración de Microsoft® SharePoint List](/help/forms/create-form-data-models.md)
1. [Configurar el modelo de datos de formulario para recuperar y enviar datos](/help/forms/work-with-form-data-model.md#configure-services)
1. [Crear un formulario adaptable](/help/forms/creating-adaptive-form-core-components.md)

Ahora puede:

* [Conexión de la lista de Microsoft® SharePoint a un formulario adaptable](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [Conexión de la lista de Microsoft® SharePoint AEM a un flujo de trabajo de](#connect-sharepoint-list-workflow)

## Conectar un formulario adaptable a la lista de Microsoft® SharePoint {#connect-af-sharepoint-list}

Para integrar Microsoft® SharePoint List en su formulario adaptable [configurar un formulario adaptable para utilizar un modelo de datos de formulario](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

Después de configurar un formulario adaptable para utilizar un modelo de datos de formulario, puede:

* [Configurar la acción de envío mediante un modelo de datos de formulario](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [Configurar el Editor de reglas para invocar un modelo de datos de formulario](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## Conexión de la lista de Microsoft® SharePoint AEM a un flujo de trabajo de {#connect-sharepoint-list-workflow}

Para integrar Microsoft® SharePoint AEM List en un flujo de trabajo de:

1. [Crear un flujo de trabajo para invocar un modelo de datos de formulario](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=es)

   <!--
    To create a new workflow with the editor, perform the following steps:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [AEM Configurar la acción de envío para invocar un flujo de trabajo de](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


Obtenga información sobre cómo [AEM Uso de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) para colaborar, administrar y procesar contenido en un formulario adaptable.

## Prácticas recomendadas {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft® SharePoint List rather than Microsoft® SharePoint Document Library. -->
* En Microsoft® SharePoint List, no se admiten los siguientes tipos de columnas:
   * columna de imagen
   * columna de metadatos
   * columna de persona
   * columna de datos externos

## Vea también {#see-also}

* [Crear un formulario adaptable basado en componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Configurar fuentes de datos](/help/forms/configuring-submit-actions.md)
* [Crear un modelo de datos de formulario](/help/forms/create-form-data-models.md)
* [Uso de flujos de trabajo de centrados en Forms AEM: referencia de pasos para automatizar los procesos empresariales](/help/forms/aem-forms-workflow-step-reference.md)

## Información adicional

* [Crear o agregar un formulario adaptable a una página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Incrustar un formulario adaptable en una página de AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)
* [Crear, utilizar y personalizar temáticas en un formulario adaptable](/help/forms/using-themes-in-core-components.md)







