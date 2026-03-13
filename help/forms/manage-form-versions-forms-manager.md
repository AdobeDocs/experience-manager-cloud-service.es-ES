---
title: Administrar versiones de formularios en Forms Manager
description: Aprenda a crear y administrar versiones de Forms adaptable, fragmentos de formulario, temáticas y otros recursos en la interfaz de usuario de Forms Manager.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 5%

---

# Administrar versiones de Form Assets en la interfaz de usuario de Forms Manager

<span class="preview"> Esta característica está disponible a través del programa Acceso anticipado. Para solicitar acceso, envía un correo electrónico desde tu dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com). </span>

Forms Manager ahora admite el control de versiones de recursos de formulario. Puede crear versiones, ver el historial de versiones y restaurar versiones anteriores de los recursos desde la interfaz de usuario de Forms Manager.

## Tipos de recursos admitidos {#supported-asset-types}

Puede crear y administrar versiones para los siguientes tipos de recursos:

| Tipo de recurso | Descripción |
|---|---|
| Forms adaptable (componentes principales) | Forms adaptable creado con componentes principales |
| Forms adaptable (componentes de base) | Forms adaptable creado con componentes de base |
| Fragmentos de formulario | Secciones de formulario reutilizables compartidas en varios formularios |
| Temáticas | Definiciones de estilos visuales aplicadas a Forms adaptable |
| Plantillas XDP | Plantillas de formulario basadas en XFA |
| Recursos binarios | Otros archivos almacenados en el repositorio DAM de Forms |

## Crear una versión {#create-version-forms-manager}

Para crear una versión de un recurso de formulario:

1. Vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario o recurso.
1. En el panel izquierdo, seleccione **[!UICONTROL Cronología]**.
1. Haga clic en **[!UICONTROL Guardar como versión]** en la barra de herramientas de la cronología.
   ![Guardar como versión](/help/forms/assets/create-version.png)
1. Escriba una **[!UICONTROL Etiqueta]** y un **[!UICONTROL Comentario]** opcional para describir los cambios.
1. Haga clic en **[!UICONTROL Crear]**.
   ![Guardar como versión2](/help/forms/assets/create-version1.png)

La versión aparece en el panel de cronología con su etiqueta, comentario y marca de tiempo.

## Versión de un recurso durante la carga {#version-on-upload}

Cuando se carga un recurso con el mismo nombre que uno existente, Forms Manager muestra un cuadro de diálogo **Cargar archivos** que indica los recursos que se van a actualizar. El cuadro de diálogo muestra el nombre, la sección y la ruta del recurso.

Cuando ya existe un recurso con el mismo nombre, la carga reemplaza el recurso existente y crea una nueva versión automáticamente. Puede ver la versión creada en la cronología.

![Cuadro de diálogo de carga de archivos que muestra la carga con versiones](/help/forms/assets/version-upload.png)

## Ver historial de versiones {#view-version-history}

Para ver el historial de versiones de un recurso:

1. Seleccione el recurso en Forms Manager.
1. En el panel izquierdo, seleccione **[!UICONTROL Cronología]**.
   ![Historial de versiones](/help/forms/assets/version-history.png)

La cronología muestra todas las entradas de la versión junto con los eventos de actividad. Cada entrada muestra la etiqueta, el comentario, el autor y la marca de tiempo.

## Restaurar una versión anterior {#restore-version}

Para restaurar un recurso a una versión anterior:

1. Seleccione el recurso en Forms Manager.
1. En el panel izquierdo, seleccione **[!UICONTROL Cronología]**.
1. Seleccione la versión que desea restaurar.
1. Haga clic en **[!UICONTROL Revertir a esta versión]**.
   ![Revertir versión](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>Las imágenes no se pueden revertir a una versión anterior. Todos los demás tipos de recursos, incluidos Forms adaptable, fragmentos de formulario, temáticas y plantillas XDP, admiten la restauración de versiones.

## Ver también {#see-also}

* [Creación de versiones, revisión y comentarios sobre un formulario adaptable](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [Importar y exportar formularios y recursos relacionados](/help/forms/import-export-forms-templates.md)
* [Publicar y cancelar la publicación de formularios](/help/forms/publishing-unpublishing-forms.md)
