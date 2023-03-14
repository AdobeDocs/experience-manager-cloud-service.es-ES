---
title: Cómo editar o añadir metadatos
description: Obtenga información sobre los metadatos de recursos en [!DNL Experience Manager Assets] existen varias formas de editar los metadatos de los recursos.
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---

# Cómo editar o añadir metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso en el que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos a los campos existentes (por ejemplo, cuando un campo de metadatos está en blanco).

Dado que las empresas necesitan vocabularios de metadatos controlados y fiables, [!DNL Experience Manager Assets] no permite la adición ad hoc de nuevas propiedades de metadatos. Aunque los autores no pueden agregar nuevos campos de metadatos para los recursos, sí pueden hacerlo los desarrolladores. Consulte [Creación de una nueva propiedad de metadatos para los recursos](meta-edit.md#editing-metadata-schema).

## Edición de metadatos para un recurso {#editing-metadata-for-an-asset}

Para editar metadatos:

1. Realice una de las siguientes acciones:

   * En la interfaz de usuario de Assets, seleccione el recurso y pulse o haga clic en **[!UICONTROL Ver propiedades]** de la barra de herramientas.
   * En la miniatura del recurso, seleccione **[!UICONTROL Ver propiedades]** acción rápida.
   * En la página de recursos, pulse o haga clic en **[!UICONTROL Ver propiedades]** en la barra de herramientas.

   La página de recursos muestra todos los metadatos del recurso. Estos metadatos se extraían automáticamente cuando se cargaban (incorporaban) en Experience Manager Assets.

1. Edite los metadatos de las distintas pestañas, según sea necesario, y cuando termine, pulse o haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios. Pulse o haga clic en **[!UICONTROL Cerrar]** para volver a la interfaz web de Assets.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para añadir esa propiedad de metadatos.

XMP Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos de. Esto se realiza mediante el flujo de trabajo de reescritura de metadatos del Experience Manager. Cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades recién creadas (incluidas las propiedades personalizadas como `cq:tags`) se añaden junto con el esquema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Edición del esquema de metadatos {#editing-metadata-schema}

Para obtener más información sobre cómo editar el esquema de metadatos, consulte [Edición de formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registrar un área de nombres personalizada en Experience Manager {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias áreas de nombres en Experience Manager. Al igual que hay áreas de nombres predefinidas como cq, jcr y sling, puede tener un área de nombres para los metadatos del repositorio y el procesamiento xml.

1. Vaya a la página de administración del tipo de nodo *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Haga clic o toque **[!UICONTROL Áreas de nombres]** en la parte superior de la página. La página de administración del área de nombres se muestra en una ventana.

1. Para agregar un área de nombres, toque o haga clic en **[!UICONTROL Nuevo]** en la parte inferior.
1. Especifique un área de nombres personalizada en la convención del área de nombres XML (especifique el ID en forma de URI y un prefijo asociado para el ID) y toque o haga clic en **[!UICONTROL Guardar]**.
