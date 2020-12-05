---
title: Cómo editar o agregar metadatos
description: Obtenga información sobre los metadatos de los recursos en [!DNL Experience Manager Assets] varias formas de editar los metadatos de los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 3207151a76c51637551907d15a34f1a6b7450d02
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 9%

---


# Cómo editar o agregar metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos a los campos existentes (por ejemplo, cuando un campo de metadatos está en blanco).

Debido a que las compañías necesitan vocabularios de metadatos fiables y controlados, [!DNL Experience Manager Assets] no permite la adición ad hoc de nuevas propiedades de metadatos. Aunque los autores no pueden agregar campos de metadatos nuevos para los recursos, los desarrolladores sí pueden hacerlo. Consulte [Creación de nuevas propiedades de metadatos para recursos](meta-edit.md#editing-metadata-schema).

## Edición de metadatos para un recurso {#editing-metadata-for-an-asset}

Para editar metadatos:

1. Realice una de las acciones siguientes:

   * En la interfaz de usuario de Recursos, seleccione el recurso y toque o haga clic en el icono **[!UICONTROL Propiedades de la Vista]** de la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida **[!UICONTROL Propiedades de la Vista]**.
   * En la página de recursos, toque o haga clic en **[!UICONTROL Propiedades de la Vista]** en la barra de herramientas.

   La página de recursos muestra todos los metadatos del recurso. Estos metadatos se extrajeron automáticamente al cargarse (ingeridos) en AEM Assets.

1. Edite los metadatos de las distintas pestañas, según sea necesario, y cuando termine, pulse o haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios. Pulse o haga clic en **[!UICONTROL Cerrar]** para volver a la interfaz web de Assets.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para agregar esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. Esto se realiza mediante AEM flujo de trabajo de escritura de metadatos. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades creadas recientemente (incluidas las propiedades personalizadas como `cq:tags`) se agregan junto con el esquema.

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Edición del Esquema de metadatos {#editing-metadata-schema}

Para obtener más información sobre cómo editar el esquema de metadatos, consulte [Edición de formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registro de una Área de nombres personalizada dentro de AEM {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias Áreas de nombres dentro de AEM. Al igual que hay Áreas de nombres predefinidas como cq, jcr y sling, puede tener una Área de nombres para los metadatos del repositorio y el procesamiento de XML.

1. Vaya a la página de administración del tipo de nodo *https://&lt;host>:&lt;puerto>/crx/explorer/nodetypes/index.jsp*.
1. Toque o haga clic en **[!UICONTROL Áreas de nombres]** en la parte superior de la página. La página Administración de Áreas de nombres se muestra en una ventana.

1. Para agregar una Área de nombres, toque o haga clic en **[!UICONTROL Nuevo]** en la parte inferior.
1. Especifique una Área de nombres personalizada en la convención de Área de nombres XML (especifique el identificador en forma de URI y un prefijo asociado para el identificador) y toque o haga clic en **[!UICONTROL Guardar]**.
