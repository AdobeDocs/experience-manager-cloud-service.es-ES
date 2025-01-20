---
title: Publicación de Forms para Edge Delivery Services
description: Aprenda cómo funciona la publicación de formularios con Edge Delivery Services AEM y cómo publicar formularios de la con Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# Publicación de Forms para Edge Delivery Services

AEM Este artículo le guía a través del proceso de publicación de formularios a los Edge Delivery Services de la.
Para publicar formularios en Edge Delivery Services AEM, primero debe establecer una conexión entre el entorno de la aplicación y el repositorio de GitHub. Una vez conectado, puede crear los formularios con el Editor universal, que sigue un enfoque de WYSIWYG (What You See Is What You Get) para una experiencia de usuario fluida y coherente con Sites.

## Requisitos previos

* ¿Es nuevo en el Forms adaptable? Configure su repositorio de GitHub siguiendo el [tutorial](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project) proporcionado.
* Si ya usa Edge Delivery Services, agregue la versión más reciente del [bloque de Forms adaptable](/help/edge/docs/forms/tutorial.md#) a su repositorio de GitHub.
* La instancia de autor de AEM Forms incluye una plantilla basada en Edge Delivery Services. Asegúrese de que la [última versión de los componentes principales](https://github.com/adobe/aem-core-forms-components) esté instalada en su entorno.
* Tenga a mano la URL de la instancia de autor del as a Cloud Service de AEM Forms y del repositorio de GitHub.

## Publish Forms para Edge Delivery Services

Para publicar formularios para Edge Delivery Services, realice los siguientes pasos:

[AEM 1. Vincule el repositorio de GitHub a la instancia de](#link-github-repository-to-aem-instance)

[AEM 2. Vincular instancia de la al repositorio de GitHub](#link-aem-instance-to-github-repository)

### AEM Vincular repositorio de GitHub a instancia de

Para vincular [su proyecto en el repositorio de GitHub](/help/edge/docs/forms/tutorial.md) a la instancia de autor de AEM Forms, realice los siguientes pasos:

1. Vaya al repositorio de GitHub que ha creado o configurado para sus Edge Delivery Services.
1. Abra el archivo `fstab.yaml` para editarlo.
1. Actualice el archivo `fstab.yaml` en su repositorio de GitHub con la URL de su instancia as a Cloud Service de AEM Forms.

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   Por ejemplo, si el repositorio de GitHub se llama &quot;aemcrosswalk&quot;, está ubicado en la cuenta &quot;wkndform&quot; y está usando la rama &quot;principal&quot;, la URL de la instancia de autor tendrá el siguiente aspecto:

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. Confirme los cambios realizados en el archivo `fstab.yaml`.

### AEM Vincular instancia a repositorio de GitHub

Para vincular la instancia de autor de AEM Forms a [su proyecto en el repositorio de GitHub](/help/edge/docs/forms/tutorial.md), realice los siguientes pasos:

[1. Cree un formulario adaptable basado en la plantilla Edge Delivery Services](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[AEM 2. Busque el contenedor de configuración del formulario en la instancia de autor de la](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. Crear el formulario en el editor universal](#3-author-the-form-in-the-universal-editor)

[4. Publish y previsualizar el formulario](#4-publish-and-preview-the-form)

#### 1. Cree un formulario adaptable basado en la plantilla Edge Delivery Services

1. Acceda a la instancia de autor del as a Cloud Service de AEM Forms.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Forms adaptable]**. Se abre el asistente. En la pestaña Source, seleccione una plantilla de formulario basada en Edge Delivery Services:

   ![Crear Forms EDS](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. Haga clic en **[!UICONTROL Crear]** y aparecerá el asistente **Crear formulario**.
1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama &quot;aemcrosswalk&quot; y está ubicado en la cuenta &quot;wkndform&quot;, la dirección URL es la siguiente:
   `https://github.com/wkndform/aemcrosswalk`
1. Haga clic en **[!UICONTROL Crear]**.

   ![Asistente para crear formularios](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   Tan pronto como haga clic en **[!UICONTROL Crear]**, el formulario se abrirá en el editor universal para la creación.

   ![crear el formulario](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > La configuración de Edge Delivery Services para los formularios basados en la plantilla de Edge Delivery Services se crea automáticamente en el contenedor de configuración del formulario.

#### AEM 2. Busque el contenedor de configuración del formulario en la instancia de autor de la

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuración de Edge Delivery Services]** en la instancia de as a Cloud Service de AEM Forms.
1. Seleccione la carpeta que coincida con el nombre del formulario. Por ejemplo, si el formulario se llama &quot;contact-us&quot;, elija la carpeta `forms/contact-us`, seleccione la configuración y publique la configuración:

   ![Configuración de Edge Delivery Services](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. Haga clic en **[!UICONTROL Propiedades]** para ver la configuración.\
   ![Configuración creada automáticamente](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   Puede dejar la opción Host de Edge tal cual. El formulario se publicaría en los entornos de vista previa (.page) y en directo (.live).

1. Haga clic en **[!UICONTROL Guardar y cerrar]**. La configuración se ha guardado.

#### 3. Crear el formulario en el editor universal

Al hacer clic en **[!UICONTROL Crear]**, el formulario se abrirá en el Editor universal para la creación.

1. Abra el Explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.

   ![árbol de contenido](/help/edge/assets/content-tree.png){width=50%, align-center}

1. Haga clic en el icono **[!UICONTROL Agregar]** y agregue los componentes deseados de la lista **Componentes de formulario adaptable**.

   ![agregar componente](/help/edge/assets/add-component.png){width=50%, align-center}

1. Seleccione el componente de formulario adaptable agregado y actualice sus propiedades mediante **[!UICONTROL Propiedades]**.

   ![abrir propiedades](/help/edge/assets/component-properties.png){width=50%, align-center}

   La siguiente captura de pantalla muestra el formulario &quot;Contáctenos&quot; sencillo creado en el editor universal:

   ![formulario de contacto](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. Publish y previsualizar el formulario

Ahora, publique el formulario para los Edge Delivery Services haciendo clic en el botón **[!UICONTROL Publish]** en la esquina superior derecha del editor universal.

![publicar formulario](/help/edge/assets/publish-form.png){width=50%, align-center}


Así se accede al formulario en Edge Delivery Services:

* **Versión ensayada (para pruebas)**: la versión ensayada muestra la versión de trabajo sin publicar del formulario para realizar pruebas. Utilice el siguiente formato de URL para previsualizar el formulario antes de que se active:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Por ejemplo, si el repositorio de su proyecto se llama &quot;aemcrosswalk&quot;, está ubicado en la cuenta &quot;wkndform&quot; y está usando la rama &quot;principal&quot; y el formulario como &quot;contáctenos&quot;, la URL de la versión ensayada tendrá el siguiente aspecto:
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **Versión activa (formulario publicado)**:   La versión activa muestra la versión publicada más recientemente del formulario, accesible para los usuarios finales. Utilice el siguiente formato de URL para acceder a la versión publicada y activa del formulario:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Por ejemplo, si el repositorio de su proyecto se llama &quot;aemcrosswalk&quot;, está ubicado en la cuenta &quot;wkndform&quot; y está usando la rama &quot;principal&quot; y el formulario como &quot;contáctenos&quot;, la URL de la versión ensayada tendrá el siguiente aspecto:
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

La estructura de la URL sigue siendo la misma para las versiones organizadas y activas. Sin embargo, el contenido que ve difiere según el contexto:

![Ver formulario publicado](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## Solución de problemas

¿Tiene problemas para cargar el formulario? Estos son algunos problemas comunes y cómo solucionarlos:

* **Dirección URL del formulario**: Compruebe que la dirección URL del formulario no incluya la extensión &quot;.html&quot; al final. El servicio de envío de Edge no requiere esta extensión.

* AEM AEM **URL de autor de** L: asegúrese de que la URL de autor de la lista del archivo `fstab.yaml` tenga el formato correcto. Debe incluir los siguientes detalles:

   * El propietario correcto de GitHub
   * El nombre de repositorio correcto
   * La rama específica que utiliza para los Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Consulte también

{{see-more-forms-eds}}