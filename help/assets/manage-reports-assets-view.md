---
title: Administración de informes en la vista Recursos
description: Acceda a los datos de la sección de informes de la vista Recursos para evaluar el uso de productos y funciones, y obtener información sobre las métricas de éxito clave.
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 88%

---

# Administrar informes {#manage-reports}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Los informes de recursos proporcionan a los administradores visibilidad de la actividad del entorno de vista de Adobe Experience Manager Assets. Estos datos proporcionan información útil sobre cómo los usuarios interactúan con el contenido y el producto. Cualquier persona usuaria puede acceder al panel de Insights. Además, las personas asignadas al perfil de producto del rol de administrador pueden crear informes definidos por el usuario.

## Acceso a los informes {#access-reports}

Todas las personas asignadas al perfil de producto Administradores de la vista Recursos pueden acceder al tablero de Insights o crear informes definidos por el usuario en la vista Recursos.

Para acceder a los informes, vaya a **[!UICONTROL Informes]** debajo de **[!UICONTROL Configuración]**.

![Informes](assets/reports.png)
<!--
In the **[!UICONTROL Reports]** screen, various components are shown in the tabular format which includes the following:

* **Title**: Title of the report
* **Type**: Determines whether the report is uploaded or downloaded to the repository
* **Description**: Provide details of the report that was given during uploading/downloading the report
* **Status**: Determines whether the report is completed, under progress, or deleted.
* **Author**: Provides email of the author who has uploaded/downloaded the report.
* **Created**: Gives information of the date when the report was generated.
-->

## Vista Insights {#view-live-statistics}

La vista Recursos le permite ver datos en tiempo real de su entorno de la vista Recursos con el tablero de Insights. Puede ver las métricas de eventos en tiempo real durante los últimos 30 días o 12 meses.

<!--![Toolbar options when you select an asset](assets/assets-essentials-live-statistics.png)-->

Haga clic en **[!UICONTROL Insights]** en el panel de navegación izquierdo para ver los siguientes gráficos generados automáticamente:

* **Descargas**: el número de recursos descargados del entorno de vista de Assets en los últimos 30 días o 12 meses representados mediante un gráfico de líneas.
  ![descargas de información](/help/assets/assets/insights-downloads2341.svg)

* **Cargas**: el número de recursos cargados en el entorno de vista de Assets en los últimos 30 días o 12 meses representados mediante un gráfico de líneas.
  ![cargas de información](/help/assets/assets/insights-uplods2.svg)
  <!--* **Asset Count by Size**: The division of count of assets based on their range of various sizes from 0 MB to 100 GB.-->

* **Uso del almacenamiento**: El uso del almacenamiento, en bytes, para el entorno de vista de Assets representado mediante un gráfico de barras.
  ![cargas de información](/help/assets/assets/insights-storage-usage1.svg)
  <!--* **Delivery**: The graph depicts the count of assets as the delivery dates.-->

<!--* **Asset Count by Asset Type**: Represents count of various MIME types of the available assets. For example, application/zip, image/png, video/mp4, application/postscripte.-->

* **Búsquedas principales**: vea los términos más buscados junto con el número de veces que se buscan en el entorno de vista Recursos en los últimos 30 días o 12 meses representados en formato tabular.
  ![cargas de información](/help/assets/assets/insights-top-search.svg)
  <!--
   ![Insights](assets/insights1.png)
   ![Insights](assets/insights2.png)
   -->

## Creación de un informe de descarga {#create-download-report}

Para crear un informe de descarga, haga lo siguiente:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Informes]** y haga clic en **[!UICONTROL Crear informe]**.

1. En la pestaña [!UICONTROL Configuración], especifique el tipo de informe como **[!UICONTROL Descargar]**.

1. Especifique un título y una descripción opcional para el informe.

1. Seleccione la ruta de la carpeta, que comprende los recursos en los que se ejecutará el informe, utilizando el campo **[!UICONTROL Seleccionar ruta de la carpeta]**.

1. Seleccione el intervalo de fecha para el informe.

   >[!NOTE]
   >
   > La vista Recursos convierte todas las zonas horarias locales a la hora universal coordinada (UTC).

1. En la pestaña [!UICONTROL Columnas], seleccione los nombres de columna que debe mostrar en el informe.

1. Haga clic en **[!UICONTROL Crear]**.

   ![Descargar informe](assets/download-reports-config.png)

En la tabla siguiente se explica el uso de todas las columnas que se pueden agregar al informe:

<table>
    <tbody>
     <tr>
      <th><strong>El nombre de la columna</strong></th>
      <th><strong>Descripción</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>El título del recurso.</td>
     </tr>
     <tr>
      <td>Ruta </td>
      <td>Ruta de la carpeta en la que el recurso está disponible en la vista Recursos.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>Tipo MIME del recurso.</td>
     </tr>
     <tr>
      <td>Tamaño</td>
      <td>El tamaño del recurso en bytes.</td>
     </tr>
     <tr>
      <td>Descargado por</td>
      <td>ID de correo electrónico del usuario que descargó el recurso.</td>
     </tr>
     <tr>
      <td>Fecha de descarga</td>
      <td>La fecha en la que se realiza la acción de descarga de recursos.</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>El autor del recurso.</td>
     </tr>
     <tr>
      <td>Fecha de creación</td>
      <td>La fecha en la que el recurso se carga en la vista Recursos.</td>
     </tr>
     <tr>
      <td>Fecha de modificación</td>
      <td>La fecha de la última modificación del recurso.</td>
     </tr>
     <tr>
      <td>Caducado</td>
      <td>Estado de caducidad del recurso.</td>
     </tr>
     <tr>
      <td>Descargado por (nombre de usuario)</td>
      <td>Nombre del usuario que descargó el recurso.</td>
     </tr>           
    </tbody>
   </table>

## Creación de un informe de carga {#create-upload-report}

Para crear un informe de carga:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Informes]** y haga clic en **[!UICONTROL Crear informe]**.

1. En la pestaña [!UICONTROL Configuración], especifique el tipo de informe como **[!UICONTROL Cargar]**.

1. Especifique un título y una descripción opcional para el informe.

1. Seleccione la ruta de la carpeta, que comprende los recursos en los que se ejecutará el informe, utilizando el campo **[!UICONTROL Seleccionar ruta de la carpeta]**.

1. Seleccione el intervalo de fecha para el informe.

1. En la pestaña [!UICONTROL Columnas], seleccione los nombres de columna que debe mostrar en el informe.

1. Haga clic en **[!UICONTROL Crear]**.

   ![Informe de carga](assets/upload-reports-config.png)

En la tabla siguiente se explica el uso de todas las columnas que se pueden agregar al informe:

<table>
    <tbody>
     <tr>
      <th><strong>El nombre de la columna</strong></th>
      <th><strong>Descripción</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>El título del recurso.</td>
     </tr>
     <tr>
      <td>Ruta </td>
      <td>Ruta de la carpeta en la que el recurso está disponible en la vista Recursos.</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>Tipo MIME del recurso.</td>
     </tr>
     <tr>
      <td>Tamaño</td>
      <td>El tamaño del recurso.</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>El autor del recurso.</td>
     </tr>
     <tr>
      <td>Fecha de creación</td>
      <td>La fecha en la que el recurso se carga en la vista Recursos.</td>
     </tr>
     <tr>
      <td>Fecha de modificación</td>
      <td>La fecha de la última modificación del recurso.</td>
     </tr>
     <tr>
      <td>Caducado</td>
      <td>Estado de caducidad del recurso.</td>
     </tr>              
    </tbody>
   </table>

## Ver informes existentes {#view-report-list}

Después de la [creación del informe](#create-download-report), puede ver la lista de informes y seleccionar para descargarlos en formato CSV o eliminarlos.

Para ver la lista de informes, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Informes]**.

Para cada informe, puede ver el título del informe, el tipo de informe, la descripción especificada al crear el informe, el estado del informe, el ID de correo electrónico del autor que lo creó y la fecha de creación del informe.

`Completed ` el estado del informe indica que el informe está listo para descargarse.

![Lista de informes](assets/list-of-reports.png)


## Descargar un informe CSV {#download-csv-report}

Para descargar un informe en formato CSV, haga lo siguiente:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Informes]**.

1. Seleccione un informe y haga clic en **[!UICONTROL Descargar CSV]**.

El informe seleccionado se descarga en formato CSV. Las columnas que se muestran en el informe CSV dependen de las columnas que seleccione al [crear el informe](#create-download-report).

## Eliminar un informe {#delete-report}

Para eliminar un informe, haga lo siguiente:

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Informes]**.

1. Seleccione un informe y haga clic en **[!UICONTROL Eliminar]**.

1. Haga clic en **[!UICONTROL Eliminar]** de nuevo para confirmar.
