---
title: Importe y exporte metadatos de recursos de manera masiva
description: Este artículo describe cómo importar y exportar metadatos de forma masiva.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 823925be9d0777f7d501d9a64e84937172b1028d
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 12%

---


# Importe y exporte metadatos de recursos de manera masiva {#import-and-export-asset-metadata-in-bulk}

AEM Assets permite importar metadatos de recursos de forma masiva mediante un archivo CSV. Puede realizar actualizaciones masivas para los recursos cargados recientemente o los recursos existentes mediante la importación de un archivo CSV. También puede ingerir metadatos de recursos de forma masiva desde sistemas de terceros en formato CSV.

## Importación de metadatos {#import-metadata}

La importación de metadatos es asincrónica y no impide el rendimiento del sistema. La actualización simultánea de los metadatos de varios recursos puede requerir muchos recursos debido a XMP actividad de reescritura si se marca el indicador de flujo de trabajo. Planifique una importación de este tipo durante el uso del servidor liso para que el rendimiento de otros usuarios no se vea afectado.

>[!NOTE]
>
>Para importar metadatos en Áreas de nombres personalizadas, primero registre las Áreas de nombres.

1. Vaya a la interfaz de usuario de Recursos y toque o haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En el menú, seleccione **[!UICONTROL Metadatos]**.
1. En la página **[!UICONTROL Importación de metadatos]**, pulse o haga clic en **[!UICONTROL Seleccionar archivo]**. Seleccione el archivo CSV con los metadatos.
1. Especifique los siguientes parámetros:

   | Parámetro | Descripción |
   | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
   | Tamaño del lote | Número de recursos de un lote para el que se van a importar metadatos. El valor predeterminado es 50. El valor máximo es 100. |
   | Separador de campos | El valor predeterminado es `,` (coma). Puede especificar cualquier otro carácter. |
   | Delimitador de varios valores | Separador para valores de metadatos. El valor predeterminado es `|`. |
   | Lanzar flujos de trabajo | False de forma predeterminada. Cuando se establece en `true` y la configuración predeterminada del iniciador está en vigor para el flujo de trabajo WriteBack de metadatos DAM (que escribe metadatos en los datos de XMP binarios). Al habilitar los flujos de trabajo de inicio se ralentiza el sistema. |
   | Nombre de columna de ruta de activos | Define el nombre de la columna para el archivo CSV con recursos. |

1. Toque o haga clic en **[!UICONTROL Importar]** desde la barra de herramientas. Una vez importados los metadatos, se envía una notificación a la bandeja de entrada de notificaciones. Vaya a la página de propiedades del recurso y compruebe si los valores de metadatos se importan correctamente para los recursos.

Para agregar la fecha y la marca de hora al importar metadatos, utilice `YYYY-MM-DDThh:mm:ss.fff-00:00` el formato de fecha y hora. La fecha y la hora se separan por `T`, `hh` es hora en formato de 24 horas, `fff` es nanosegundos y `-00:00` es desplazamiento de zona horaria. Por ejemplo, `2020-03-26T11:26:00.000-07:00` es 26 de marzo de 2020 a las 11:26:00.000 AM hora PST.

>[!CAUTION]
>
>Si el formato de fecha no coincide `YYYY-MM-DDThh:mm:ss.fff-00:00`, no se establecen los valores de fecha. Los formatos de fecha del archivo CSV de metadatos exportado tienen el formato `YYYY-MM-DDThh:mm:ss-00:00`. Si desea importarla, conviértala al formato aceptable agregando el valor de nanosegundos indicado por `fff`.

## Exportar metadatos {#export-metadata}

Puede exportar menús para varios recursos en formato CSV. Los metadatos se exportan asincrónicamente y no afectan al rendimiento del sistema. Para exportar metadatos, AEM las propiedades del nodo de recursos `jcr:content/metadata` y sus nodos secundarios y exporta las propiedades de metadatos en un archivo CSV.

Algunos casos de uso para exportar metadatos de forma masiva son:

* Importe los metadatos en un sistema de terceros al migrar recursos.
* Comparta metadatos de recursos con un equipo de proyecto más amplio.
* Probar o auditar los metadatos para comprobar la conformidad.
* Externalice los metadatos para una localización independiente.

1. Seleccione la carpeta de recursos que contiene los recursos para los que desea exportar metadatos. En la barra de herramientas, seleccione **[!UICONTROL Exportar metadatos]**.
1. En el cuadro de diálogo Exportar metadatos, especifique un nombre para el archivo CSV. Para exportar metadatos de recursos en subcarpetas, seleccione **[!UICONTROL Incluir recursos en subcarpetas]**.

   ![Interfaz y opciones para exportar metadatos de todos los recursos de una](assets/export_metadata_page.png "carpetaInterfaz y opciones para exportar metadatos de todos los recursos de una carpeta")

1. Seleccione las opciones que desee. Proporcione un nombre de archivo y, si es necesario, una fecha.

1. En el campo **[!UICONTROL Propiedades que exportar]** , especifique si desea exportar todas las propiedades o determinadas. Si selecciona Propiedades selectivas para exportar, agregue las propiedades que desee.

1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Exportar]**. Un mensaje confirma que se exportan los metadatos. Cierre el mensaje.
1. Abra la notificación de la bandeja de entrada para el trabajo de exportación. Seleccione el trabajo y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas. Para descargar el archivo CSV con los metadatos, pulse o haga clic en **[!UICONTROL Descargar CSV]** desde la barra de herramientas. Haga clic en **[!UICONTROL Cerrar]**.

   ![Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva](assets/csv_download.png)
   *Figura: Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva*
