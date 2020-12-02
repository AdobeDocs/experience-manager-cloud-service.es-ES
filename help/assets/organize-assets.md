---
title: Organización de recursos digitales
description: Organice los recursos digitales utilizando los distintos métodos que se proporcionan en Adobe Experience Manager Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9c5dd93be316417014fc665cc813a0d83c3fac6f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Organizar recursos digitales {#organize-digital-assets}

Todos los recursos digitales, los metadatos y el contenido de los documentos de Microsoft Office y PDF se extraen y permiten realizar búsquedas. La búsqueda permite un filtrado sofisticado de los recursos y respeta plenamente los permisos adecuados. Los metadatos se tratan en detalle en Metadatos en Digital Asset Management.

AEM Assets admite varias formas de organizar el contenido. Puede organizarlas jerárquicamente mediante carpetas o bien puede organizarlas de forma no ordenada y ad hoc, por ejemplo mediante etiquetas. Los usuarios pueden editar etiquetas en el Editor de recursos de DAM, donde se muestran subrecursos, representaciones y metadatos.

## Crear carpetas {#create-folders}

Al organizar una colección de recursos, por ejemplo, todas las imágenes *Naturaleza*, puede crear carpetas para mantenerlas juntas. Puede utilizar carpetas para categorizar y organizar los recursos. AEM Assets no requiere que organice los recursos en carpetas para que funcionen mejor.

>[!NOTE]
>
>No se admite el uso compartido de una carpeta de recursos (en Marketing Cloud) del tipo `sling:OrderedFolder`. Si desea compartir una carpeta, no seleccione Pedido al crear una carpeta.

1. Vaya al lugar de la carpeta de recursos digitales en el que desea crear una nueva carpeta.
1. En el menú, haga clic en **[!UICONTROL Crear]**. Seleccione **[!UICONTROL Nueva carpeta]**.
1. En el campo **[!UICONTROL Título]**, proporcione un nombre de carpeta. De forma predeterminada, DAM utiliza el título que ha proporcionado como nombre de carpeta. Una vez creada la carpeta, puede anular el valor predeterminado y especificar otro nombre de carpeta.
1. Haga clic en **[!UICONTROL Crear]**. La carpeta se muestra en la carpeta de recursos digitales.

## Añadir propiedades de CUG en carpetas {#add-cug-properties-to-folders}

Puede limitar quién puede acceder a determinadas carpetas en Recursos haciendo que la carpeta forme parte de un grupo de usuarios cerrado (CUG). Para que una carpeta forme parte de un CUG:

1. En Recursos, haga clic con el botón derecho en la carpeta para la que desee agregar propiedades de grupo de usuarios cerradas y seleccione **Propiedades**.
1. Haga clic en la ficha **CUG**.
1. Seleccione la casilla de verificación **Habilitado** para que la carpeta y sus recursos solo estén disponibles para un grupo de usuarios cerrado.
1. Vaya a la página de inicio de sesión, si la hay, para agregar esa información. Añada los grupos admitidos haciendo clic en **Añadir elemento**. Si es necesario, agregue el reino. Haga clic en **Aceptar** para guardar los cambios.

## Utilice etiquetas para organizar los recursos {#use-tags-to-organize-assets}

Puede utilizar carpetas, etiquetas o ambos para organizar los recursos. Añadir etiquetas en recursos facilita su recuperación durante una búsqueda. Para agregar etiquetas a un recurso, siga estos pasos:

1. En Digital Asset Manager, haga clic en el recurso con el botón doble para abrirlo.
1. En el área **Etiquetas**, abra el menú para mostrar las etiquetas disponibles. Seleccione las etiquetas que desee. Para eliminar una etiqueta, coloque el puntero sobre ella y haga clic en `X` para eliminarla.
1. Haga clic en **Guardar** para guardar las etiquetas agregadas.
