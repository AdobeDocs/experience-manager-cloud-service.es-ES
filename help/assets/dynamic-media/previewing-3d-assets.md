---
title: Vista previa de activos 3D
description: Obtenga información sobre cómo previsualizar recursos 3D en Experience Manager.
contentOwner: Rick Brough
feature: 3D Assets
role: User
exl-id: e873bd25-f841-4063-824f-7e48f40bb678
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 6%

---

# Vista previa de recursos 3D en Adobe Experience Manager{#previewing-3d-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/previewing-3d-assets.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Experience Manager Assets admite la ingesta, administración, previsualización y entrega de recursos 3D.

Puede obtener una vista previa de los recursos 3D con las representaciones de miniaturas generadas automáticamente o el visor 3D interactivo. El visor 3D interactivo está disponible en la página de detalles de recursos de Experience Manager. El visor incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten girar, aplicar zoom y desplazarse por la escena 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/dynamic-media/assets-3d.md). -->

## Formatos compatibles para la vista previa de miniaturas en Experience Manager{#supported-thumbnail-previewing-assets}

Experience Manager genera miniaturas para los siguientes formatos de archivo de forma predeterminada:

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary |  |
| FBX | Autodesk FBX | application/octet-stream |  |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| 3DS | Modelo de estudio 3D | application/x-3ds |  |
| USDz | Descripción de escena universal | model/vnd.usdz+zip |  |

## Formatos admitidos para la previsualización 3D interactiva en Experience Manager{#supported-3d-previewing-assets}

Experience Manager admite la previsualización 3D interactiva para los siguientes formatos de archivo de forma nativa:

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary |  |
| GLTF | Formato de transmisión GL | model/gltf+json | Ver la **nota** a continuación. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografía | application/vnd.ms-pki.stl |  |


>[!NOTE]
>
>Si los materiales no se representan en la vista previa de un modelo gLTF, asegúrese de que se les asignen nombres correctamente y que se encuentren en una carpeta `textures` en la misma carpeta raíz que el modelo, de forma similar a la siguiente:

    Recurso (carpeta)
    model.gltf
    model.bin
    textures (carpeta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Consideraciones de rendimiento al previsualizar recursos 3D en Experience Manager{#performance-3d-previewing-assets}

El tiempo que se tarda en abrir un recurso 3D en la página de vista de detalles del recurso depende de varios factores, como el ancho de banda, la complejidad de la imagen y las latencias al servidor.

Además, las capacidades del equipo cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes a la hora de manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización 3D interactiva sea más fluida y favorable.

**Para obtener una vista previa de recursos 3D en Experience Manager:**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.
Ver [Formatos compatibles para vista previa 3D](#supported-3d-previewing-assets) y [Cargar recursos](/help/assets/manage-digital-assets.md#uploading-assets).
1. Desde Experience Manager, en la página **[!UICONTROL Navegación]**, ve a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.

   ![Página de navegación](/help/assets/dynamic-media/assets/navigation-assets.png)

1. Cerca de la esquina superior derecha de la página, en la lista desplegable Ver, seleccione **[!UICONTROL Vista de tarjeta]** y, a continuación, desplácese hasta un recurso 3D que desee previsualizar.

   ![Selección de la tarjeta 3D](/help/assets/dynamic-media/assets/3d-card-select.png)
   _En la vista de tarjeta, seleccione la tarjeta del recurso 3D que desea previsualizar._

1. Seleccione la tarjeta del recurso 3D.

   ![Vista previa 3D interactiva](/help/assets/dynamic-media/assets/3d-preview.png)
   _Vista previa interactiva de un recurso 3D en la página de vista de detalles del recurso._
1. En la página de vista de detalles del recurso para el recurso 3D, realice una de las siguientes acciones:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gira tu cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica tu cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho + arrastre. | Presione con dos dedos + arrastre. |
   | **Haz zoom en tu cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Haga doble clic en. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

1. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
