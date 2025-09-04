---
title: Integración nativa de AEM Assets con Adobe Express
description: La integración nativa de AEM Assets con Adobe Express permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 4fcb17f6fd6db9d33d08574420633b06f18bd9b2
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 9%

---

# Integración nativa con Adobe Express {#native-integration-adobe-express}

AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. La integración ofrece las siguientes ventajas clave:

* Se ha aumentado la reutilización del contenido editando y guardando nuevos recursos en AEM.

* Se ha reducido el tiempo y esfuerzo generales para crear nuevos recursos o crear nuevas versiones de los recursos existentes.

## Requisitos previos {#prerequisites}

Derechos para acceder a Adobe Express y al menos a un entorno dentro de los AEM Assets. El entorno puede ser cualquiera de los repositorios de Assets as a Cloud Service o Assets Essentials.

## Uso de AEM Assets en el editor de Adobe Express {#use-aem-assets-in-express}

Siga estos pasos para empezar a utilizar AEM Assets en el editor de Adobe Express:

1. Abra la aplicación web de Adobe Express.

2. Abra un nuevo lienzo en blanco cargando una nueva plantilla o proyecto, o creando un recurso.

3. Haga clic en **[!UICONTROL Assets]**, disponible en el panel de navegación izquierdo. Adobe Express muestra la lista de repositorios a los que puede acceder junto con la lista de recursos y carpetas disponibles en el nivel raíz.

4. Examine o busque recursos en su repositorio para arrastrarlos y colocarlos en el lienzo. Puede filtrar recursos mediante varios filtros disponibles, como el tipo de archivo, el tipo MIME y las dimensiones.

   >[!NOTE]
   >
   >El filtro por dimensión no se aplica a los vídeos.

   ![Incluir recursos del complemento Recursos](assets/adobe-express-native-integration.png)


## Guardar proyectos de Adobe Express en AEM Assets {#save-express-projects-in-assets}

Después de incorporar las modificaciones adecuadas en el lienzo Express, puede guardarlo en el repositorio de AEM Assets.

1. Haga clic en **[!UICONTROL Compartir]** para abrir el cuadro de diálogo **[!UICONTROL Compartir]**.

   ![Guardar recursos en AEM](assets/adobe-express-share.png)

2. En la sección Almacenamiento del panel derecho, seleccione **AEM Assets**. Adobe Express muestra el cuadro de diálogo de carga.
3. Seleccione **Página actual** o **Todas las páginas**. Especifique un nombre y un formato para los recursos que desea exportar. Puede exportar el contenido del lienzo en los formatos PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. El formato se ajusta automáticamente en función de los recursos de las páginas de lienzo.
Al seleccionar **Página actual**, se guardará el recurso de la página actual en la carpeta de destino. Si selecciona **Todas las páginas** y el formato de exportación no es PDF, todas las páginas de lienzo se guardarán como archivos independientes en una nueva carpeta dentro de la carpeta de destino. Si el formato de exportación es PDF, todas las páginas de lienzo se guardan como un solo archivo PDF en la carpeta de destino.

4. Haga clic en el icono de la carpeta en **Carpeta de destino** para seleccionar una ubicación y guardar los recursos.

   ![Guardar recursos en AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Opcional: puede agregar metadatos de campaña para la carga mediante el campo **Nombre del proyecto o de la campaña**. Puede utilizar un nombre existente o crear uno nuevo. Puede definir varios nombres de proyecto o campaña para la carga. Para registrar el nombre, simplemente escriba el nombre y pulse Intro.
Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

6. Del mismo modo, defina los valores para los campos **[!UICONTROL Palabras clave]** y **[!UICONTROL Canales]**.

7. Haga clic en **[!UICONTROL Cargar]** para cargar los recursos a los AEM Assets.

Consulte [Formatos de archivo compatibles](asset-properties-content-hub.md#supported-formats).

[!DNL Content Hub] admite todos los tipos de recursos y formatos que admite el repositorio [!DNL Assets] subyacente. En la tabla siguiente se enumeran los formatos de archivo clave de [!DNL the Content Hub], que proporcionan compatibilidad adicional para obtener una vista previa de los recursos visualmente:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo de archivo</strong></th>
      <th><strong>Formatos compatibles</strong></th>
      <th><strong>Tamaño</strong></th>
     </tr>
     <tr>
        <td rowspan="4"> Imagen </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
        <td> 8000 X 8000 píxeles, máximo 40 MB</td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
        <td> 8000 X 8000 píxeles, máximo 40 MB</td>
    </tr>
    <tr>
        <td>[!UICONTROL SVG]</td>
        <td> Máximo 250 KB</td>
    </tr>
    <tr>
        <td rowspan="4"> Vídeo </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL Quicktime]</td>
        <td> - </td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
        <td> 3840 X 3840 píxeles, máximo 200 MB</td>
    </tr>
    <tr>
        <td>[!UICONTROL MPEG]</td>
        <td> 200 MB como máximo </td>
    </tr>
    <tr>
        <td rowspan="4"> Documento </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL txt] (sin formato)</td>
        <td> - </td>
    </tr>
    <tr>
        <td>[!UICONTROL Doc/Docx]</td>
        <td> - </td>
    </tr>
    <tr>
        <td>[!UICONTROL XML]</td>
        <td> - </td>
    </tr>
    <tr>
        <td rowspan="2"> Medios de impresión </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL PDF]</td>
        <td> - </td>
    </tr>
    </tbody>
</table>

## Limitaciones {#limitations}

1. Para importar y exportar, el tipo de archivo de vídeo admitido es MP4.

2. Para la **importación de vídeo MP4**, consulte los [formatos de archivo compatibles](asset-properties-content-hub.md#supported-formats). Tampoco se admiten vídeos con fondos transparentes (canal alfa).
   <!--
   1. The maximum file size supported is 200 MB. If this limit exceeds, an alert message displays.
   2. The maximum supported resolution is 3840 X 3840 pixels.
   3. Videos with transparent backgrounds (alpha channel) are not supported.
   -->

3. Para la **exportación de vídeo MP4**, el tamaño máximo de archivo admitido es de 200 MB. Si se supera este límite, se recomienda recortar el vídeo a 200 MB o menos o cargarlo manualmente en la carpeta de destino de AEM Assets después de descargarlo.



