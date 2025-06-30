---
title: Importación y exportación de metadatos de recursos de forma masiva
description: Este artículo describe cómo importar y exportar metadatos por lotes.
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 10%

---

# Importación y exportación de metadatos de recursos de forma masiva {#import-and-export-asset-metadata-in-bulk}

Adobe Experience Manager Assets permite importar metadatos de recursos de forma masiva mediante un archivo CSV. Puede realizar actualizaciones masivas de los recursos cargados recientemente o de los recursos existentes importando un archivo CSV. También puede introducir metadatos de recursos de forma masiva desde sistemas de terceros en formato CSV.

## Importar metadatos {#import-metadata}

La importación de metadatos es asíncrona y no impide el rendimiento del sistema. La actualización simultánea de los metadatos de varios recursos puede consumir muchos recursos debido a la actividad de reescritura de metadatos mediante microservicios de recursos. Adobe recomienda planificar cualquier operación masiva durante el uso del servidor lean para que el rendimiento de otros usuarios no se vea afectado.

>[!NOTE]
>
>Para importar metadatos en áreas de nombres personalizadas, primero registre las áreas de nombres.

1. Vaya a la interfaz de usuario [!DNL Assets], seleccione **[!UICONTROL Crear]** en la barra de herramientas y seleccione **[!UICONTROL Metadatos]** en el menú.
1. En la página **[!UICONTROL Importación de metadatos]**, haga clic en **[!UICONTROL Seleccionar archivo]**. Seleccione el archivo CSV con los metadatos.
1. Proporcione los siguientes parámetros:

   | Parámetro | Descripción |
   | ---------------------- | ------- |
   | Tamaño de lote | Número de recursos de un lote cuyos metadatos se van a importar. El valor predeterminado es 50. El valor máximo es 100. |
   | Separador de campos | El valor predeterminado es `,` (una coma). Puede especificar cualquier otro carácter. |
   | Delimitador de varios valores | Separador para valores de metadatos. El valor predeterminado es `|`. |
   | Lanzar flujos de trabajo | False de forma predeterminada. Cuando se establece en `true` y la configuración predeterminada está activa para el flujo de trabajo de escritura de metadatos DAM (que escribe metadatos en los datos binarios de XMP). Al habilitar los flujos de trabajo, el sistema se ralentiza. |
   | Nombre de columna de ruta de activos | Define el nombre de columna del archivo CSV con recursos. |

1. Seleccione **[!UICONTROL Importar]** en la barra de herramientas. Una vez importados los metadatos, se envía una notificación a la bandeja de entrada de notificaciones. Vaya a la página de propiedades del recurso y compruebe si los valores de los metadatos se importan correctamente para los recursos.

1. Para agregar la fecha y la marca de tiempo para importar los metadatos, use el formato `YYYY-MM-DDThh:mm:ss.fff-00:00` para la fecha y la hora. La fecha y la hora están separadas por `T`, `hh` es horas en formato de 24 horas, `fff` es nanosegundos y `-00:00` es un desplazamiento de zona horaria. Por ejemplo, `2020-03-26T11:26:00.000-07:00` es el 26 de marzo de 2020 a las 11:26:00.000 AM PST.

   * El formato de fecha depende del encabezado de la columna y del formato que contenga. Por ejemplo, si la fecha es una queja con el formato `yyyy-MM-dd'T'HH:mm:ssXXX`, el encabezado de columna correspondiente debe ser `Date: DateFormat: yyyy-MM-dd'T'HH:mm:ssXXX`.
   * El formato de fecha predeterminado es `yyyy-MM-dd'T'HH:mm:ss.SSSXXX`.

<!-- Hidden via cqdoc-17869>

>[!CAUTION]
>
>If the date format does not match `YYYY-MM-DDThh:mm:ss.fff-00:00`, the date values are not set. The date formats of exported metadata CSV file is in the format `YYYY-MM-DDThh:mm:ss-00:00`. If you want to import it, convert it to the acceptable format by adding the nanoseconds value denoted by `fff`.
-->

## Exportar metadatos {#export-metadata}

Puede exportar metadatos de varios recursos en formato CSV. Los metadatos se exportan de forma asíncrona y no afectan al rendimiento del sistema. Para exportar metadatos, Experience Manager recorre las propiedades del nodo de recursos `jcr:content/metadata` y sus nodos secundarios y exporta las propiedades de metadatos en un archivo CSV.

Algunos casos de uso para exportar metadatos por lotes son:

* Importe los metadatos en un sistema de terceros al migrar recursos.
* Comparta metadatos de recursos con un equipo de proyecto más amplio.
* Probar o auditar el cumplimiento de los metadatos.
* Externalice los metadatos para una localización independiente.

>[!NOTE]
>
>Las exportaciones de metadatos están limitadas a 1 048 575 Assets, que corresponde al tamaño máximo de hoja de cálculo en Microsoft Excel. Si una jerarquía exportada contiene más de este número de Assets, solo se incluirán en el archivo CSV los metadatos de los primeros 1 048 575 Assets.

1. Seleccione la carpeta de recursos que contiene los recursos para los que desea exportar metadatos. En la barra de herramientas, seleccione **[!UICONTROL Exportar metadatos]**.
1. En el cuadro de diálogo Exportación de metadatos, especifique un nombre para el archivo CSV. Para exportar metadatos de recursos en subcarpetas, seleccione **[!UICONTROL Incluir recursos en subcarpetas]**.

   ![Interfaz y opciones para exportar metadatos de todos los recursos de una carpeta](assets/export_metadata_page.png "Interfaz y opciones para exportar metadatos de todos los recursos de una carpeta")

1. Seleccione las opciones que desee. Proporcione un nombre de archivo y, si es necesario, una fecha.

1. En el campo **[!UICONTROL Propiedades que se van a exportar]**, especifique si desea exportar todas las propiedades o las propiedades específicas. Si elige Propiedades selectivas para exportar, añada las propiedades deseadas.

1. En la barra de herramientas, seleccione **[!UICONTROL Exportar]**. Un mensaje confirma que se exportan los metadatos. Cierre el mensaje.
1. Abra la notificación de la bandeja de entrada para el trabajo de exportación. Seleccione el trabajo y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas. Para descargar el archivo CSV con los metadatos, seleccione **[!UICONTROL Descarga de CSV]** en la barra de herramientas. Haga clic en **[!UICONTROL Cerrar]**.

   ![Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados en bloque](assets/csv_download.png)

   *Imagen: cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados en lotes.*

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Importar metadatos al importar recursos de forma masiva](/help/assets/add-assets.md#asset-bulk-ingestor)
