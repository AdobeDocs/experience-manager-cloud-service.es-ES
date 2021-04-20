---
title: Edición o adición de metadatos
description: Obtenga información sobre los metadatos de recursos en [!DNL Experience Manager Assets] y sobre varias formas de editarlos.
contentOwner: AG
feature: Metadata
role: Business Practitioner,Administrator
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---


# Editar o agregar metadatos {#how-to-edit-or-add-metadata}

Los metadatos son información adicional sobre el recurso que se puede buscar. Se extrae automáticamente al cargar una imagen. Puede editar los metadatos existentes o agregar nuevas propiedades de metadatos a los campos existentes (por ejemplo, cuando un campo de metadatos está en blanco).

Debido a que las empresas necesitan vocabularios de metadatos fiables y controlados, [!DNL Experience Manager Assets] no permite la adición ad hoc de nuevas propiedades de metadatos. Aunque los autores no pueden agregar nuevos campos de metadatos para los recursos, los desarrolladores sí pueden. Consulte [Creación de una nueva propiedad de metadatos para Assets](meta-edit.md#editing-metadata-schema).

## Edición de metadatos de un recurso {#editing-metadata-for-an-asset}

Para editar metadatos:

1. Realice una de las acciones siguientes:

   * En la interfaz de usuario de Assets, seleccione el recurso y pulse o haga clic en el icono **[!UICONTROL Ver propiedades]** de la barra de herramientas.
   * En la miniatura del recurso, seleccione la acción rápida **[!UICONTROL Ver propiedades]**.
   * En la página de recursos, pulse o haga clic en **[!UICONTROL Ver propiedades]** en la barra de herramientas.

   La página de recursos muestra todos los metadatos del recurso. Estos metadatos se extraían automáticamente cuando se cargaban (incorporaban) en AEM Assets.

1. Edite los metadatos de las distintas pestañas, según sea necesario, y cuando termine, pulse o haga clic en **[!UICONTROL Guardar]** en la barra de herramientas para guardar los cambios. Pulse o haga clic en **[!UICONTROL Cerrar]** para volver a la interfaz web de Assets.

   >[!NOTE]
   >
   >Si un campo de texto está vacío, no hay ningún conjunto de metadatos existente. Puede introducir un valor en el campo y guardarlo para añadir esa propiedad de metadatos.

Cualquier cambio en los metadatos de un recurso se vuelve a escribir en el binario original como parte de sus datos XMP. Esto se realiza mediante AEM flujo de trabajo de reescritura de metadatos. Los cambios realizados en las propiedades existentes (como `dc:title`) se sobrescriben y las propiedades creadas recientemente (incluidas las propiedades personalizadas como `cq:tags`) se agregan junto con el esquema .

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## Edición del esquema de metadatos {#editing-metadata-schema}

Para obtener más información sobre cómo editar el esquema de metadatos, consulte [Edición de formularios de esquema de metadatos](metadata-schemas.md#edit-metadata-schema-forms).

## Registro de un espacio de nombres personalizado en AEM {#registering-a-custom-namespace-within-aem}

Puede agregar sus propias áreas de nombres dentro de AEM. Del mismo modo que hay áreas de nombres predefinidas como cq, jcr y sling, puede tener un espacio de nombres para los metadatos del repositorio y el procesamiento xml.

1. Vaya a la página de administración del tipo de nodo *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. Toque o haga clic en **[!UICONTROL Espacios de nombres]** en la parte superior de la página. La página de administración del área de nombres se muestra en una ventana.

1. Para agregar un área de nombres, toque o haga clic en **[!UICONTROL Nuevo]** en la parte inferior.
1. Especifique un área de nombres personalizada en la convención de área de nombres XML (especifique el id en forma de URI y un prefijo asociado para el id) y pulse o haga clic en **[!UICONTROL Guardar]**.
