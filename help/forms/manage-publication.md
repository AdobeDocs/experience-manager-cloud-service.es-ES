---
title: ¿Cómo publicar o cancelar la publicación de formularios en instancias de vista previa o publicación?
description: AEM Obtenga información sobre cómo publicar o cancelar la publicación de formularios desde el entorno de autor de la para previsualizar o publicar instancias. AEM Tanto si está probando los formularios en un entorno de ensayo como si los está implementando en directo para los usuarios finales, proporciona herramientas optimizadas para administrar este proceso de forma eficaz.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: d3c089dcca80255f53c0888d46ee1b4b6246741e
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# &#x200B;Administrar publicación en Experience Manager Forms

Como administrador de Adobe Experience Manager Forms, puede publicar formularios de su instancia de autor en Experience Manager Forms. Puede programar la publicación de un formulario o una carpeta en una fecha u hora posterior. Una vez publicados, los usuarios pueden acceder a los formularios y rellenarlos.

En la interfaz de Experience Manager Forms, puede publicar un formulario mediante los siguientes elementos:
* [Opción de Publish](#publish-forms-using-the-publish-option)
* [Opción Administrar publicación](#publish-forms-using-the-manage-publication-option)

Si realiza las modificaciones posteriores a los formularios o carpetas originales en Experience Manager Forms, los cambios no se reflejarán en la instancia de **Publish** hasta que vuelva a publicar desde Experience Manager Forms. Garantiza que los cambios en curso no estén disponibles en la instancia de **Publish**. Solo los cambios publicados por un administrador están disponibles en la instancia de **Publish**.

## Formularios Publish que utilizan la opción Publish

La opción **Publish** le permite publicar inmediatamente un formulario. Para publicar un formulario de Experience Manager con el botón **Publish** de la barra de herramientas. Para publicar formularios con la opción Publish, haga lo siguiente:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desee publicar.
1. Haga clic en la opción **Publish** de la barra de herramientas. Eche un vistazo a todos los recursos de referencia que se publicarían con el formulario.
1. Haga clic en **[!UICONTROL Publicar]**.

   ![Publish y cancelar la publicación del formulario](/help/edge/docs/forms/assets/publish-form-option.png)

   Una vez que el formulario y sus recursos relacionados se hayan publicado correctamente, aparecerá el cuadro de diálogo **Éxito**. Haga clic en **Cerrar** para cerrar el cuadro de diálogo.

   ![Cuadro de diálogo de éxito](/help/forms/assets/publish-success.png)

### Cancelar la publicación del formulario

Después de publicar correctamente el formulario utilizando la opción **Publish** y sus recursos relacionados, incluso puede cancelar la publicación con el botón **[!UICONTROL Cancelar la publicación]** de la barra de herramientas. Para cancelar la publicación del formulario:

1. Para cancelar la publicación del formulario y sus recursos relacionados, seleccione el formulario y haga clic en **[!UICONTROL Cancelar publicación]** en la barra de herramientas

   Al hacer clic en el botón **[!UICONTROL Cancelar publicación]**, aparece el cuadro de diálogo **Cancelar publicación del recurso**.
1. Haga clic en **[!UICONTROL Cancelar publicación]** para iniciar el proceso de cancelación de publicación

   ![Abrir diálogo](/help/forms/assets/unpublish-asset.png)

   Una vez que se cancele la publicación del formulario y sus recursos relacionados correctamente, aparecerá el cuadro de diálogo **Éxito**. Haga clic en **Cerrar** para cerrar el cuadro de diálogo.

   ![cancelación de publicación correcta](/help/forms/assets/unpublishing-start.png)

## Formularios de Publish que utilizan la opción Administrar publicación

Administrar publicación permite publicar o cancelar la publicación del contenido desde y hacia el destino seleccionado, agregar contenido a la lista de publicaciones desde la carpeta formularios y documentos, seleccionar referencias para publicar y programar la publicación a una fecha u hora posterior.  Para publicar formularios con la opción Administrar publicación, haga lo siguiente:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desee publicar.
1. Haga clic en la opción **[!UICONTROL Administrar publicación]** en la barra de herramientas.

   ![Opción Administrar publicación](/help/forms/assets/manage-publication-option.png)

   Aparecerá la interfaz **Administrar publicación**:

   ![Administrar publicación](/help/forms/assets/manage-publication.png)

   Las siguientes opciones están disponibles en la interfaz **Administrar publicación**:

   * **Acciones**

      * **Publish**: Publish Forms al destino seleccionado
      * **Cancelar publicación**: cancelar la publicación de formularios desde el destino

   * **Destino**

      * **Publish**: instancia de Publish Forms a Experience Manager Forms AEM () Publish.
      * **Vista previa**: la instancia de vista previa de formularios Publish en Experience Manager Forms AEM ().

   * **Programación**

      * **Ahora**: formularios Publish inmediatamente
      * **Más tarde**: formularios de Publish basados en la **fecha de activación** o la hora

1. Haga clic en **Siguiente** para continuar.
1. En la ficha **Ámbito**, use la opción [Agregar contenido](#add-content) para agregar más contenido para la publicación. Por ejemplo, puede agregar más archivos de Forms o de documento de registro.
   ![ficha de ámbito](/help/forms/assets/scope-tab.png)
1. Haga clic en **[!UICONTROL Publish]** para publicar los formularios y los recursos relacionados y aparecerá un mensaje de confirmación.
   ![mensaje de publicación correcta](/help/forms/assets/publish-successful.png)

### Añadir contenido

La publicación en Experience Manager Forms permite agregar más contenido (formularios y carpetas) a la lista de publicaciones. Puede agregar más formularios o carpetas a la lista desde la carpeta `formsanddocuments`. Pero no se pueden agregar formularios de varias carpetas a la vez. Para agregar más formularios para publicarlos:

1. Haga clic en el botón **Agregar contenido** para agregar más contenido.

   ![Agregar contenido](/help/forms/assets/add-content.png)

1. Seleccione el formulario en la pantalla **Seleccionar ruta**. Puede agregar varios formularios desde una carpeta o agregar varias carpetas a la vez. Pero no se pueden agregar formularios de varias carpetas a la vez.

   ![Agregar contenido](/help/forms/assets/add-assets.png)

1. Para configurar las referencias para publicar o no publicar para un formulario, seleccione el formulario y haga clic en **[!UICONTROL Referencias publicadas]**.

   ![referencias publicadas](/help/forms/assets/published-references.png)

1. En el cuadro de diálogo **Referencias publicadas**, anule la selección de los recursos que planea no publicar y haga clic en **[!UICONTROL Listo]**.
   ![diálogo de referencias publicadas](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### Publish o cancelar la publicación de un formulario más tarde

Además de permitirle publicar o cancelar la publicación de formularios en una fecha y hora posteriores, la opción Publicar o cancelar la publicación más tarde también permite configurar un flujo de trabajo. Los formularios se publican o cancelan la publicación después de completar el flujo de trabajo. Para programar la publicación o cancelación de la publicación de un formulario:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea programar para la publicación.
1. Haga clic en la opción **[!UICONTROL Administrar publicación]** en la barra de herramientas.

   ![Administrar publicación](/help/forms/assets/manage-publication.png)

1. Haga clic en **Publish** o **Cancelar la publicación** de **[!UICONTROL Action]** y, a continuación, seleccione el **[!UICONTROL destino]** en el que desea publicar o cancelar la publicación del contenido.
   * **Vista previa**: use la opción **Vista previa** para publicar o cancelar la publicación en un entorno de vista previa de Experience Manager Forms. Los entornos de vista previa de Experience Manager Forms se utilizan para realizar pruebas en formularios de desarrollo.
   * **Publish**: utilice la opción Experience Manager Forms Publish para enviar el formulario al entorno de publicación de Experience Manager Forms una vez que el formulario esté listo para utilizarse en un entorno de producción.

1. Seleccione **[!UICONTROL Más tarde]** en Programación.

   ![Administrar publicación más tarde](/help/forms/assets/manage-publication-later.png)

1. Seleccione una **[!UICONTROL fecha de activación]** y especifique la fecha y la hora.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. En la ficha **Ámbito**, **[!UICONTROL Agregar contenido]** (si es necesario).
   ![Administrar publicación y agregar contenido más tarde](/help/forms/assets/publish-later-add-content.png)
1. Haga clic en **[!UICONTROL Siguiente]**.
1. (Opcional) En la pestaña **Flujos de trabajo**, especifique un **[!UICONTROL título de flujo de trabajo]**.
1. Haga clic en **[!UICONTROL Publish más tarde]**.

   ![Administrar flujo de trabajo de publicación](/help/forms/assets/manage-publication-workflows.png)

## Determinar el estado de publicación

Existen varias formas de determinar el estado de publicación:

* Inicie sesión en la instancia de destino para verificar los formularios publicados y otros recursos (según la fecha u hora programadas).

* Utilice la vista de cronología para determinar el estado de la publicación.

* Utilice el menú de información de página del editor de Forms adaptable.
