---
title: Asociación de revisores de envío con un formulario
seo-title: Associating submission reviewers with a form
description: Aprenda a asociar revisores de envío con un formulario en [!DNL AEM Forms]. Los revisores asociados revisan un formulario enviado a través del portal de formularios.
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# Asociación de revisores de envío con un formulario {#associating-submission-reviewers-with-a-form}

Cuando cree un formulario, puede especificar usuarios que revisen los envíos a través del portal de formularios y proporcionar comentarios. Su organización puede recopilar comentarios y rediseñar los formularios enviados.

[!DNL AEM Forms] permite asociar un grupo de revisores con un formulario. Los usuarios agregados a un grupo de revisión de un formulario ven los envíos de este formulario y proporcionan sus comentarios.

Los grupos de revisores asignados a un formulario solo pueden revisar los envíos del formulario especificado.

## Requisitos previos {#prerequisite}

### Habilitación de la propiedad de grupos del revisor de envío para Forms adaptable mediante el editor de esquemas de metadatos {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

Para asociar un grupo de revisores a un formulario, edite el esquema de metadatos de Adaptive Forms. De forma predeterminada, no se puede agregar un grupo de revisores a un formulario enviado.

Para editar el esquema de metadatos:

1. En el modo de autor, en Experience Manager, haga clic en **Herramientas** > **Recursos** > **Esquemas de metadatos**.
1. En la página Esquema de Forms, vaya a **Forms** > **Forms creado en AEM.**

   La dirección URL de la página es:

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. Select **Formulario adaptable** y haga clic en **Editar**.
1. En la página Editar formulario , haga clic en **Avanzadas**.
1. En la ficha Avanzado , arrastre y suelte la **Texto de una sola línea** componente disponible en Generar formulario.
1. Seleccione el componente de texto añadido para ver su configuración.

   En Configuración , introduzca `./jcr:content/metadata/form-submission-reviewer-group` en el campo Asignar a propiedad .

   El campo de grupo del revisor de envío de las propiedades avanzadas del formulario adaptable se habilita con el nombre especificado en Etiqueta de campo.

## Asociación de revisores de envío con un formulario {#associating-submission-reviewers-with-a-form-1}

Para asociar revisores de envío con un formulario adaptable, cree un grupo de revisores y agregue usuarios a él. Agregue el grupo de revisores creado en el campo revisor de envío de formulario de las propiedades avanzadas del formulario.
Los grupos de usuarios permiten asociar diferentes conjuntos de revisores de envío con diferentes Forms adaptables. Esta función evita que un usuario no autorizado revise el envío.

Antes de realizar los pasos siguientes, consulte [Requisito previo](adding-reviewers-form.md#prerequisite).

Para crear un grupo y agregarle miembros, vaya a **Herramientas** > **Operaciones** > **Seguridad** > **Grupos**.
Para obtener más información, consulte [Administración de usuarios y servicios](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
Asegúrese de agregar el grupo que crea como miembro del grupo de usuarios integrado: **forms-submit-reviewers**. Este grupo de usuarios se envía con [!DNL AEM Forms]y garantiza que los usuarios se añadan como revisores de envío.

Para asociar grupos de usuarios con un formulario adaptable:

1. En el modo de creación, vaya a **Forms** > **Forms y documentos**.
1. Utilice la opción **Seleccionar **para seleccionar un formulario adaptable y haga clic en **Ver propiedades**.
1. En la ventana Propiedades del formulario, haga clic en **Editar** y, a continuación, haga clic en **AVANZADO**.
1. Introduzca el grupo en el campo de grupo del revisor de envío y haga clic en **Listo**.

   El campo de grupo del revisor de envío aparece con el nombre especificado en el esquema de metadatos editado de Adaptive Forms.

>[!NOTE]
>
>Replicar usuarios y formularios para garantizar la disponibilidad de los usuarios y formularios en la implementación remota de [!DNL AEM Forms].
>
>Asegúrese de que todos los usuarios estén duplicados como miembros revisores de los grupos de usuarios en la implementación remota.

