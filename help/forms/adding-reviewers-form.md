---
title: Enviar un formulario adaptable para revisión
description: Comparta un formulario adaptable para su revisión con uno o más revisores.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 100%

---


# Asociar revisores de envío con un formulario {#associating-submission-reviewers-with-a-form}

Cuando crea un formulario, puede especificar usuarios que revisen los envíos del formulario a través del portal de formularios y proporcionen comentarios. Su organización puede recopilar comentarios y volver a diseñar los formularios enviados.

[!DNL AEM Forms] permite asociar un grupo de revisores con un formulario. Los usuarios agregados al grupo de revisión de un formulario ven los envíos de este formulario y proporcionan comentarios.

Los grupos de revisores asignados a un formulario solo pueden revisar los envíos del formulario especificado.

## Requisitos previos {#prerequisite}

### Habilitar la propiedad de los grupos de revisores de envío para los formularios adaptables mediante el editor de esquemas de metadatos {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para asociar un grupo de revisores a un formulario, edite el esquema de metadatos de los formularios adaptables. De forma predeterminada, no se puede agregar un grupo de revisores a un formulario enviado.

Para editar el esquema de metadatos:

1. En el modo Autor, en Experience Manager, haga clic en **Herramientas** > **Recursos** > **Esquemas de metadatos**.
1. En la página Formularios de esquema, vaya a **Formularios** > **Formularios creados en AEM.**

   La URL de la página es:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Seleccione **Formulario adaptable** y haga clic en **Editar**.
1. En la página Editar formulario, haga clic en **Avanzadas**.
1. En la pestaña Avanzadas, arrastre y suelte el componente **Texto de una línea** disponible en Generar formulario.
1. Seleccione el componente de texto agregado para ver su configuración.

   En Configuración, introduzca `./jcr:content/metadata/form-submission-reviewer-group` en el campo Asignar a propiedad.

   El campo del grupo de revisores de envío de las Propiedades avanzadas del formulario adaptable se habilita con el nombre especificado en Etiqueta de campo.

## Asociar revisores de envío con un formulario {#associating-submission-reviewers-with-a-form-1}

Para asociar revisores de envío con un formulario adaptable, cree un grupo de revisores y agréguele usuarios. Agregue el grupo de revisores creado en el campo del revisor de envío de las propiedades avanzadas del formulario. 
Los grupos de usuarios permiten asociar diferentes conjuntos de revisores de envío con diferentes formularios adaptables. Esta función evita que un usuario no autorizado revise el envío.

Antes de realizar los siguientes pasos, consulte [Requisito previo](adding-reviewers-form.md#prerequisite).

Para crear un grupo y agregarle miembros, vaya a **Herramientas** > **Operaciones** > **Seguridad** > **Grupos**.
Para obtener más información, consulte [Administración de usuarios y servicios](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=es). 
Asegúrese de agregar el grupo que crea como miembro del grupo de usuarios predeterminado: **forms-submit-reviewers**. Este grupo de usuarios está incluido en [!DNL AEM Forms] y garantiza que los usuarios se añadan como revisores de envío.

Para asociar grupos de usuarios con un formulario adaptable:

1. En el modo Autor, vaya a **Formularios** > **Formularios y documentos**.
1. Utilice la opción **Seleccionar** para seleccionar un formulario adaptable y haga clic en **Ver propiedades**.
1. En la ventana Propiedades del formulario, haga clic en **Editar** y, a continuación, haga clic en **AVANZADAS**.
1. Introduzca el grupo en el campo del grupo de revisores de envío y haga clic en **Listo**.

   El campo del grupo de revisores de envío aparece con el nombre especificado en el esquema de metadatos editado de los formularios adaptables.

>[!NOTE]
>
>Replique los usuarios y los formularios para garantizar su disponibilidad en la implementación remota de [!DNL AEM Forms].
>
>Asegúrese de que todos los usuarios están replicados como miembros revisores de los grupos de usuarios en la implementación remota.

>[!MORELIKETHIS]
>
>* [Creación y administración de revisiones en formularios](/help/forms/create-reviews-forms.md)
>* [Creación y administración de revisiones para un formulario adaptable](/help/forms/review-adaptiveforms-in-sites-page.md)