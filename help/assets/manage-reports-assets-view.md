---
title: Administración de informes en la vista Recursos
description: Acceda a los datos de la sección de informes de la vista Recursos para evaluar el uso de productos y funciones, y obtener información sobre las métricas de éxito clave.
exl-id: 26d0289e-445a-4b8e-a5a1-b02beedbc3f1
feature: Asset Insights, Asset Reports
role: User, Admin, Developer
hide: true
hidefromtoc: true
source-git-commit: 132f601e1bbeeea59dc6a14392a9f6c786b20682
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 85%

---

# Administrar informes {#manage-reports}

Los informes de recursos proporcionan a los administradores visibilidad de la actividad del entorno de vista de Adobe Experience Manager Assets. Estos datos proporcionan información útil sobre cómo los usuarios interactúan con el contenido y el producto. Cualquier persona usuaria puede acceder al panel de Insights. Además, las personas asignadas al perfil de producto del rol de administrador pueden crear informes definidos por el usuario.

## Acceso a los informes {#access-reports}

Todos los usuarios asignados al Perfil de producto de los administradores de AEM pueden acceder al panel de perspectivas o crear informes definidos por el usuario en la vista de Assets.

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

## Creación de un informe {#create-report}

El entorno de vista de los AEM Assets ofrece funcionalidades completas de creación de informes a través del panel Informes. Esta función permite a los usuarios generar y descargar informes CSV en los que se detallan las cargas y descargas de recursos en intervalos de tiempo especificados, desde intervalos únicos hasta intervalos diarios, semanales, mensuales o anuales.

**Para crear un informe:**

1. Vaya a **Informes** y haga clic en **Crear informe** (en la parte superior derecha). El cuadro de diálogo **crear informe** muestra los siguientes campos:
   ![create-report](/help/assets/assets/executed-reports1.svg)

   **En pestaña Configuración:**

   1. **Tipo de informe:** seleccione entre el tipo [!UICONTROL cargar], [!UICONTROL descargar] o [Informe de entrega de Dynamic Media](#dynamic-media-delivery-reports).
   1. **Título:** añada un título al informe.
   1. **Descripción:** añada una descripción opcional al informe.
   1. **Seleccionar ruta de la carpeta:** seleccione una ruta de la carpeta para generar el informe de los recursos cargados y descargados dentro de esa carpeta específica. Por ejemplo, si necesita que el informe de recursos se cargue en una carpeta, especifique la ruta a esa carpeta.
   1. **Seleccionar intervalo de fechas:** seleccione el intervalo de fechas para ver la actividad de carga o descarga dentro de la carpeta.

   <br>

   >[!NOTE]
   >
   > La vista Recursos convierte todas las zonas horarias locales a la hora universal coordinada (UTC).

   **Pestaña En las columnas:** seleccione los nombres de columna que se mostrarán en el informe. En la tabla siguiente se explica el uso de todas las columnas:

   <table>
    <tbody>
     <tr>
      <th><strong>El nombre de la columna</strong></th>
      <th><strong>Descripción</strong></th>
      <th><strong>Tipo de informe</strong></th>
     </tr>
     <tr>
      <td>Título</td>
      <td>El título del recurso.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Ruta</td>
      <td>Ruta de la carpeta en la que el recurso está disponible en la vista Recursos.</td>
      <td>Carga, descarga y distribución de Dynamic Media</td>
     </tr>
     <tr>
      <td>Tipo MIME</td>
      <td>Tipo MIME del recurso.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Tamaño</td>
      <td>El tamaño del recurso en bytes.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Descargado por</td>
      <td>ID de correo electrónico del usuario que descargó el recurso.</td>
      <td>Descargar</td>
     </tr>
     <tr>
      <td>Fecha de descarga</td>
      <td>La fecha en la que se realiza la acción de descarga de recursos.</td>
      <td>Descargar</td>
     </tr>
     <tr>
      <td>Autor</td>
      <td>El autor del recurso.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Fecha de creación</td>
      <td>La fecha en la que el recurso se carga en la vista Recursos.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Fecha de modificación</td>
      <td>La fecha de la última modificación del recurso.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Caducado</td>
      <td>Estado de caducidad del recurso.</td>
      <td>Cargar y descargar</td>
     </tr>
     <tr>
      <td>Descargado por (nombre de usuario)</td>
      <td>Nombre del usuario que descargó el recurso.</td>
      <td>Descargar</td>
     </tr> 
     <tr>
      <td>Remitente del reenvío</td>
      <td>La URL donde se entrega o se incluye el recurso</td>
      <td>Entrega de Dynamic Media</td>
     </tr>  
     <tr>
      <td>Visitas</td>
      <td>El número de veces que se entrega el recurso (recuento de envíos)</td>
      <td>Entrega de Dynamic Media</td>
     </tr>          
    </tbody>
   </table>

## Informes de envío de Dynamic Media {#dynamic-media-delivery-reports}

Obtenga información de envío para los recursos que se envían con Dynamic Media, con el recuento de envíos a nivel de recurso, información del remitente del envío, ruta de recursos en AEM Assets e ID de recurso único. Se pueden generar informes para todos los recursos que se envían mediante el repositorio de Dynamic Media para AEM o para una jerarquía de carpetas específica en AEM Assets. Además, la información de envío de Dynamic Media ayuda a medir el retorno de la inversión de los recursos enviados, a medir el rendimiento del canal y ayuda a realizar tareas de administración de recursos con conocimiento de causa para los recursos.

<!--
>[!NOTE]
> 
>To get early access to the Dynamic Media Delivery Report on your Dynamic Media account, [create and submit an Adobe Customer Support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
-->

### Requisitos previos {#prereqs-dynamic-media-delivery-reports}

Debe tener una licencia de Dynamic Media para crear y utilizar este informe.

>[!IMPORTANT]
> 
>* Se proporcionan informes para los recursos enviados a través de Dynamic Media.
>* Los informes se generan para el primer millón de filas. Para capturar todos los archivos que se encuentran dentro de este límite, considere la posibilidad de incluir la columna de referente para las carpetas más pequeñas.
>* Solo se pueden generar informes de los últimos 3 meses.

### Creación de un informe de envío de Dynamic Media{#create-dynamic-media-delivery-report}

1. Cree un informe de envío de Dynamic Media siguiendo los pasos mencionados en [Crear un informe](#create-report).

1. Seleccione **[!UICONTROL Entrega de Dynamic Media]** de la lista desplegable **[!UICONTROL Tipo de informe]**.

   ![Informe de envío de Dynamic Media](assets/dynamic-media-delivery-report-option.png)


1. En la pestaña **[!UICONTROL Columnas]**, puede seleccionar la columna **[!UICONTROL Remitente del reenvío]** para incluirla en el informe.

   ![Remitente del reenvío](assets/referrer.png)

   Todas las columnas del informe descargado son de solo lectura, excepto la columna **Referente**, que puede modificar para incluir o excluir del informe. <!--Choosing a referrer displays the number of visitors received from each referred report that directs traffic to the site. It offers insights into the sources of traffic and the origin of the visitors. Such insights help measure ROI of delivered assets, measure channel performance, and help take informed asset management tasks for assets.-->

### Acciones realizadas en el informe de envío de Dynamic Media {#actions-performed-dynamic-media-delivery-reports}

Después de crear el informe, puede realizar las siguientes acciones:

* **[!UICONTROL Eliminar]**: puede eliminar el informe seleccionado.
* **[!UICONTROL Descargar CSV]**: puede descargar el informe seleccionado en formato CSV. El informe descargado consta de las columnas Nombre, Ruta, DynamicMediaID, Referente, Visitas.
   * La columna **Remitente del reenvío** enumera la dirección URL donde se entrega o se incluye el recurso.

   * La columna **Visitas** enumera la cantidad de veces que se entrega el recurso (recuento de envíos).

Para eliminar o descargar el informe de entrega de Dynamic Media como CSV, consulte [Ver y descargar el informe existente](#View-and-download-existing-report).

![CSV descargado en el informe de entrega de Dynamic Media](assets/csv-dynamic-media-delivery-report.png)


## Visualización y descarga de un informe existente {#View-and-download-existing-report}

Los informes existentes se muestran en la pestaña **Informes ejecutados**. Haga clic en **Informes** y seleccione **Informes ejecutados** para ver todos los informes creados con el estado **completado**, lo que indica que están listos para descargarse. Para descargar el informe en formato CSV o eliminarlo, seleccione la fila del informe. A continuación, seleccione **Descargar CSV** o **Eliminar**.
![ver y descargar informes existentes](/help/assets/assets/view-download-existing-report.png)


## Programación de un informe {#schedule-report}

En la interfaz de usuario de la vista AEM Assets, **Programar informe** configura la generación automática de informes en intervalos futuros especificados, como diario, semanal, mensual o anual. Esta función ayuda a optimizar las necesidades recurrentes de creación de informes y garantiza actualizaciones de datos puntuales. En **Crear informe** se generan informes para fechas pasadas. Los informes completados se indican en **Informes ejecutados** y los próximos informes se encuentran en **Informes programados**.

Para programar un informe, siga los pasos que se indican a continuación:

1. Haga clic en Informes en el panel izquierdo y, a continuación, haga clic en Crear informe (desde la parte superior derecha).
1. El cuadro de diálogo del informe muestra la siguiente información:
   1. **Tipo de informe:** seleccione entre el tipo de carga y descarga.
   1. **Título:** añada un título al informe.
   1. **Descripción**: añada una descripción opcional al informe.
   1. **Seleccionar ruta de carpeta:** seleccione una ruta de la carpeta para generar un informe para los recursos que se cargarán o descargarán de esa carpeta específica en el futuro.
   1. Marque **Programar informe:** marque para programar el informe para un momento posterior o para que se repita.

      ![programar informe](/help/assets/assets/schedule-reports1.svg)

   1. **Elegir frecuencia:** especifique el intervalo de generación del informe (por ejemplo, diario, semanal, mensual, anual o una vez) y establezca la fecha y la hora para ejecutar el informe junto con la fecha de finalización para la periodicidad. Para un informe único, seleccione el intervalo de fechas para el informe sobre el tipo de actividad seleccionado en el entorno de AEM. Por ejemplo, si necesita un informe sobre los recursos descargados del 10 al 29 (fechas futuras) de un mes específico, seleccione estas fechas en el campo **Seleccionar intervalo de fechas**.

   >[!NOTE]
   >
   > La vista Recursos convierte todas las zonas horarias locales a la hora universal coordinada (UTC).

## Visualización de informes programados {#view-scheduled-reports}

Los informes programados se muestran en la ficha **Informes programados** de una manera organizada de manera sistemática. Todos los informes completados de cada informe programado se almacenan en una sola carpeta de informes. Haga clic![expandir contracción](/help/assets/assets/expand-icon1.svg)para ver los informes completados. Por ejemplo, si ha programado un informe diario, todos los informes completados se agrupan conjuntamente en una carpeta. Esta organización simplifica tanto la navegación como la capacidad de detección de informes. Para ver los informes programados, haga clic en **Informes** y luego haga clic en **Informes programados**. Se muestran todos los informes programados con su estado en curso o completado. Los informes completados están listos para descargarse.\
![informe programado](/help/assets/assets/scheduled-reports-tab.png)

## Edición y cancelación de informes programados {#edit-cancel-scheduled-reports}

1. Vaya a la pestaña **Informes programados**.
1. Seleccione la fila del informe.
1. Haga clic en **Editar**.
1. Haga clic en **Cancelar programación** y, a continuación, haga clic en **Confirmar** para cancelar el informe programado. Para los informes cancelados, el siguiente tiempo de ejecución pasa a estar vacío y el estado se muestra cancelado.
   ![editar y cancelar informe programado](/help/assets/assets/cancel-edit-scheduled-reports.png)

### Reanudar programación {#resume-schedule}

Para reanudar la programación cancelada, seleccione la fila del informe y haga clic en **Reanudar programación**. Cuando se reanuda, las siguientes entradas en tiempo de ejecución se muestran de nuevo y el estado se muestra en curso.
![reanudar programación](/help/assets/assets/resume-schedule.png)

>[!NOTE]
>
> Si reanuda un informe cancelado antes de la fecha de finalización programada, los informes desde la fecha de cancelación hasta la fecha de reanudación se generan automáticamente.

## Vista Insights {#view-live-statistics}

La vista Recursos le permite ver datos en tiempo real de su entorno de la vista Recursos con el tablero de Insights. Puede ver las métricas de eventos en tiempo real durante los últimos 30 días o 12 meses.

<!--![Toolbar options when you select an asset](assets/assets-view-live-statistics.png)-->

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
* **Número de recursos por tamaño:** segmenta el número de recursos total dentro del entorno de Assets View en diferentes intervalos de tamaño, destacando el recuento y el porcentaje de recursos en cada intervalo de tamaño, representados por un gráfico de sectores.
  ![insights-assets-count-by-size](/help/assets/assets/insights-assets-count-by-size.svg)
* **Recuento de recursos por tipo de recurso:** Segmenta el recuento total de recursos en su entorno de vista de Assets, destacando el recuento y el porcentaje de recursos en función de sus tipos de archivos, representados por un gráfico circular.
  ![insights-assets-count-by-size](/help/assets/assets/insights-assest-count-by-asset-type1.svg)