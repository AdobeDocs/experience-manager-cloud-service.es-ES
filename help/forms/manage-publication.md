---
title: ¿Cómo publicar o cancelar la publicación de formularios en instancias de vista previa o publicación?
description: Obtenga información sobre cómo publicar o cancelar la publicación de formularios desde el entorno de creación de AEM para previsualizar o publicar instancias. Tanto si está probando los formularios en un entorno de ensayo como si los está implementando en directo para los usuarios finales, AEM proporciona herramientas optimizadas para administrar este proceso de forma eficaz.
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
exl-id: 6ade40f1-bad5-4f5e-aa0e-84b7c6a82e02
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 6%

---


# Administración de publicaciones en Experience Manager Forms

Como administrador de Forms de Adobe Experience Manager (AEM), puede publicar formularios de su instancia de autor en Experience Manager Forms. También tiene la opción de programar la publicación de un formulario o carpeta para una fecha u hora posterior. Una vez publicados, los usuarios pueden acceder a los formularios y rellenarlos.

En Experience Manager Forms, puede publicar un formulario mediante uno de los métodos siguientes:

* [Opción de publicación](#publish-forms-using-the-publish-option)
* [Opción Administrar publicación](#publish-forms-using-the-manage-publication-option)

## Cosas que hay que tener en cuenta

* Solo los miembros del grupo `forms-users` pueden usar la opción **Administrar publicación** para publicar los formularios.
* Los cambios realizados en los formularios o carpetas de Experience Manager Forms no aparecerán en la instancia **Publish** hasta que se vuelva a publicar. Esto garantiza que las actualizaciones de trabajo en curso no estén disponibles en la instancia **Publish**. Solo los cambios publicados explícitamente por un administrador se reflejarán en la instancia **Publish**.

## Publicar formularios con la opción Publicar

La opción **Publicar** le permite publicar inmediatamente un formulario. Para publicar un formulario de Experience Manager mediante el botón **Publicar** de la barra de herramientas. Para publicar formularios mediante la opción Publicar, haga lo siguiente:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea publicar.
1. Haga clic en la opción **Publicar** en la barra de herramientas y observe todos los recursos de referencia que se publicarían con el formulario.
1. Haga clic en **[!UICONTROL Publicar]**.

   ![Publicar y cancelar la publicación del formulario](/help/edge/docs/forms/assets/publish-form-option.png)

   Una vez que el formulario y sus recursos relacionados se hayan publicado correctamente, aparecerá el cuadro de diálogo **Éxito**.
1. Haga clic en **Cerrar**.

   ![Cuadro de diálogo de éxito](/help/forms/assets/publish-success1.png)

### Cancelar la publicación del formulario

Después de publicar correctamente el formulario mediante la opción **Publicar** y sus recursos relacionados, incluso puede cancelar la publicación con el botón **[!UICONTROL Cancelar la publicación]** disponible en la barra de herramientas. Para cancelar la publicación del formulario:

1. Para cancelar la publicación del formulario y sus recursos relacionados, seleccione el formulario y haga clic en **[!UICONTROL Cancelar publicación]** en la barra de herramientas

   Al hacer clic en el botón **[!UICONTROL Cancelar publicación]**, aparece el cuadro de diálogo **Cancelar publicación del recurso**.
1. Haga clic en **[!UICONTROL Cancelar publicación]** para iniciar el proceso de cancelación de publicación

   ![Abrir diálogo](/help/forms/assets/unpublish-asset.png)

   Una vez que se cancele la publicación del formulario y sus recursos relacionados correctamente, aparecerá el cuadro de diálogo **Éxito**.
1. Haga clic en **Cerrar**.

   ![cancelación de publicación correcta](/help/forms/assets/unpublishing-start.png)

## Publicar formularios con la opción Administrar publicación

Administrar publicación le permite publicar o cancelar la publicación de contenido desde y hacia el destino seleccionado, agregar contenido a la lista de publicaciones desde la carpeta `forms&documents`, seleccionar referencias para publicar y programar la publicación a una fecha u hora posterior.  Para publicar formularios con la opción **Administrar publicación**, haga lo siguiente:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea publicar.
1. Haga clic en la opción **[!UICONTROL Administrar publicación]** en la barra de herramientas.

   ![Opción Administrar publicación](/help/forms/assets/manage-publication-option.png)

   Aparecerá la interfaz de usuario **Administrar publicación**:

   ![Administrar publicación](/help/forms/assets/manage-publication.png)

   Las siguientes opciones están disponibles en la interfaz de usuario de **Administrar publicación**:

   * **Acciones**

      * **Publicar**: Publicar formularios en el destino seleccionado
      * **Cancelar publicación**: cancelar la publicación de formularios desde el destino

   * **Destino**

      * **Publicar**: Publique formularios en la instancia de publicación de Experience Manager Forms (AEM).
      * **Vista previa**: publique formularios en la instancia de vista previa de Experience Manager Forms (AEM).

   * **Programación**

      * **Ahora**: publicar formularios inmediatamente
      * **Más tarde**: publique formularios en función de la **fecha de activación** o la hora

1. Haga clic en **Siguiente** para continuar.
1. (Opcional) En la ficha **Ámbito**, use la opción [Agregar contenido](#add-content) para agregar más contenido para la publicación. Por ejemplo, puede agregar más archivos de Forms o de documento de registro.
   ![ficha de ámbito](/help/forms/assets/scope-tab.png)
1. Haga clic en **[!UICONTROL Publicar]** para publicar los formularios y los recursos relacionados, y aparecerá un mensaje de confirmación.
   ![mensaje de publicación correcta](/help/forms/assets/publish-successful.png)

### Añadir contenido

La publicación en Experience Manager Forms permite agregar más contenido (formularios) a la lista de publicaciones.
Para agregar más formularios para publicarlos:

1. Haga clic en el botón **Agregar contenido** para agregar más contenido.

   ![Agregar contenido](/help/forms/assets/add-content.png)

2. Seleccione el formulario en la pantalla **Seleccionar ruta**.

   ![Agregar contenido](/help/forms/assets/add-assets.png)

   >[!NOTE]
   >
   > Puede agregar más formularios o carpetas a la lista desde la carpeta `formsanddocuments`. Pero no se pueden agregar formularios de varias carpetas a la vez.

3. Para configurar las referencias para publicar o no publicar para un formulario, seleccione el formulario y haga clic en **[!UICONTROL Referencias publicadas]**.

   ![referencias publicadas](/help/forms/assets/published-references.png)

4. En el cuadro de diálogo **Referencias publicadas**, anule la selección de los recursos que planea no publicar y haga clic en **[!UICONTROL Listo]**.
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


### Publicar o cancelar la publicación de un formulario más tarde

Además de permitirle publicar o cancelar la publicación de formularios en una fecha y hora posteriores, la opción Publicar o cancelar la publicación más tarde también permite configurar un flujo de trabajo. Los formularios se publican o cancelan la publicación después de completar el flujo de trabajo.

Para programar la publicación o cancelación de la publicación de un formulario:

1. En la consola de Experience Manager Forms, vaya a la carpeta principal y seleccione el formulario que desea programar para la publicación.
1. Haga clic en la opción **[!UICONTROL Administrar publicación]** en la barra de herramientas.

   ![Administrar publicación](/help/forms/assets/manage-publication.png)

1. Haga clic en **Publicar** o en **Cancelar la publicación** de **[!UICONTROL Acción]**.
1. Seleccione el **[!UICONTROL destino]** en el que quiere publicar o cancelar la publicación del contenido.
   * **Vista previa**: use la opción **Vista previa** para publicar o cancelar la publicación en un entorno de vista previa de Experience Manager Forms. Los entornos de vista previa de Experience Manager Forms se utilizan para realizar pruebas en formularios de desarrollo.
   * **Publicar**: use la opción **Publicar** de Experience Manager Forms para enviar el formulario al entorno de publicación de Experience Manager Forms después de que el formulario esté listo para usarse en un entorno de producción.

1. Seleccione **[!UICONTROL Más tarde]** de **Programación**.

   ![Administrar publicación más tarde](/help/forms/assets/manage-publication-later.png)

1. Seleccione una **[!UICONTROL fecha de activación]** y especifique la fecha y la hora.
1. Haga clic en **[!UICONTROL Siguiente]**.
1. (Opcional) En la ficha **Ámbito**, agregue contenido mediante **[!UICONTROL Agregar contenido]** .
   ![Administrar publicación y agregar contenido más tarde](/help/forms/assets/publish-later-add-content.png)
1. Haga clic en **[!UICONTROL Siguiente]**.
1. En la ficha **Flujos de trabajo**, especifique un **[!UICONTROL título de flujo de trabajo]**.
1. Haga clic en **[!UICONTROL Publicar más tarde]**.

   ![Administrar flujo de trabajo de publicación](/help/forms/assets/manage-publication-workflows.png)

## Determinar el estado de publicación

Existen varias formas de determinar el estado de publicación:

* Inicie sesión en la instancia de destino para verificar los formularios publicados y otros recursos (según la fecha u hora programadas).

* Utilice la vista de cronología para determinar el estado de la publicación.

* Utilice el menú de información de página del editor de Forms adaptable.
