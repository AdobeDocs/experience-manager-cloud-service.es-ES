---
title: Organizar recursos digitales
description: Organice los recursos digitales mediante varios métodos proporcionados en Adobe Experience Manager Assets.
contentOwner: AG
feature: Administración de recursos,Etiquetado,Distribución de recursos
role: Business Practitioner
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 7256300afd83434839c21a32682919f80097f376
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Organizar recursos digitales {#organize-digital-assets}

Todos los recursos digitales, metadatos y contenido de documentos de Microsoft Office y PDF se extraen y se pueden buscar. La búsqueda permite un filtrado sofisticado de los recursos y respeta por completo los permisos adecuados. Los metadatos se tratan en detalle en Metadatos de Digital Asset Management.

AEM Assets admite varias formas de organizar el contenido. Puede organizarlas de forma jerárquica mediante carpetas o puede organizarlas de forma desordenada y ad hoc mediante, por ejemplo, etiquetas. Los usuarios pueden editar etiquetas en el Editor de recursos DAM, donde se muestran subrecursos, representaciones y metadatos.

## Crear carpetas {#create-folders}

Al organizar una colección de recursos, por ejemplo, todas las imágenes *Nature*, puede crear carpetas para mantenerlas juntas. Puede utilizar carpetas para categorizar y organizar los recursos. AEM Assets no requiere que organice los recursos en carpetas para que funcionen mejor.

>[!NOTE]
>
>No se admite el uso compartido de una carpeta de recursos (en Marketing Cloud) del tipo `sling:OrderedFolder`. Si desea compartir una carpeta, no seleccione Pedido al crear una carpeta.

1. Vaya al lugar de la carpeta de recursos digitales donde desee crear una carpeta nueva.
1. En el menú, haga clic en **[!UICONTROL Crear]**. Seleccione **[!UICONTROL Nueva carpeta]**.
1. En el campo **[!UICONTROL Title]**, proporcione un nombre de carpeta. De forma predeterminada, DAM utiliza el título que ha proporcionado como nombre de carpeta. Una vez creada la carpeta, puede anular el valor predeterminado y especificar otro nombre de carpeta.
1. Haga clic en **[!UICONTROL Crear]**. La carpeta se muestra en la carpeta de recursos digitales.

## Agregar propiedades CUG a carpetas {#add-cug-properties-to-folders}

Puede limitar quién puede acceder a ciertas carpetas en Assets haciendo que la carpeta forme parte de un grupo de usuarios cerrado (CUG). Para hacer que una carpeta forme parte de un CUG:

1. En Assets, haga clic con el botón derecho en la carpeta para la que desee añadir propiedades de grupo de usuarios cerradas y seleccione **Properties**.
1. Haga clic en la pestaña **CUG**.
1. Seleccione la casilla **Enabled** para que la carpeta y sus recursos solo estén disponibles para un grupo de usuarios cerrado.
1. Vaya a la página de inicio de sesión, si la hay, para añadir esa información. Agregue los grupos admitidos haciendo clic en **Agregar elemento**. Si es necesario, añada el reino. Haga clic en **Aceptar** para guardar los cambios.

## Usar etiquetas para organizar los recursos {#use-tags-to-organize-assets}

Puede utilizar carpetas, etiquetas o ambas para organizar los recursos. Añadir etiquetas a los recursos facilita su recuperación durante una búsqueda. Para agregar etiquetas a un recurso, siga estos pasos:

1. En Digital Asset Manager, haga doble clic en el recurso para abrirlo.
1. En el área **Etiquetas**, abra el menú para mostrar las etiquetas disponibles. Seleccione las etiquetas que desee. Para eliminar una etiqueta, pase el puntero sobre ella y haga clic en `X` para eliminarla.
1. Haga clic en **Guardar** para guardar las etiquetas agregadas.
