---
title: Importación y exportación masiva de metadatos de recursos
description: Este artículo describe cómo importar y exportar metadatos de forma masiva.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Importación y exportación masiva de metadatos de recursos {#import-and-export-asset-metadata-in-bulk}

Recursos AEM permite importar metadatos de recursos de forma masiva mediante un archivo CSV. Puede realizar actualizaciones masivas para los recursos cargados recientemente o los recursos existentes mediante la importación de un archivo CSV. También puede ingerir metadatos de recursos de forma masiva desde sistemas de terceros en formato CSV.

## Importación de metadatos {#import-metadata}

La importación de metadatos es asincrónica y no impide el rendimiento del sistema. La actualización simultánea de los metadatos de varios recursos puede requerir muchos recursos debido a la actividad de reescritura XMP si se marca el indicador de flujo de trabajo. Planifique una importación de este tipo durante el uso del servidor liso para que el rendimiento de otros usuarios no se vea afectado.

>[!NOTE]
>
>Para importar metadatos en espacios de nombres personalizados, primero registre los espacios de nombres.

1. Vaya a la interfaz de usuario de Recursos y toque o haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En el menú, seleccione **[!UICONTROL Metadatos]**.
1. En la página Importación **[!UICONTROL de]** metadatos, toque o haga clic en **[!UICONTROL Seleccionar archivo]**. Seleccione el archivo CSV con los metadatos.
1. Especifique los siguientes parámetros:

   | Parámetro | Descripción |
   | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
   | Tamaño del lote | Número de recursos de un lote para el que se van a importar metadatos. El valor predeterminado es 50. El valor máximo es 100. |
   | Separador de campos | El valor predeterminado es `,` (coma). Puede especificar cualquier otro carácter. |
   | Delimitador de varios valores | Separador para valores de metadatos. El valor predeterminado es `|`. |
   | Lanzar flujos de trabajo | False de forma predeterminada. Cuando se establece en `true` y la configuración predeterminada del iniciador está en vigor para el flujo de trabajo WriteBack de metadatos DAM (que escribe metadatos en los datos XMP binarios). La activación de los flujos de trabajo de inicio ralentiza el funcionamiento del sistema. |
   | Nombre de columna de ruta de activos | Define el nombre de la columna para el archivo CSV con recursos. |

1. Toque o haga clic en **[!UICONTROL Importar]** desde la barra de herramientas. Una vez importados los metadatos, se envía una notificación a la bandeja de entrada de notificaciones. Vaya a la página de propiedades del recurso y compruebe si los valores de metadatos se importan correctamente para los recursos.

## Exportar metadatos {#export-metadata}

Puede exportar menús para varios recursos en formato CSV. Los metadatos se exportan asincrónicamente y no afectan al rendimiento del sistema. Para exportar metadatos, AEM atraviesa las propiedades del nodo de recursos `jcr:content/metadata` y sus nodos secundarios y exporta las propiedades de metadatos en un archivo CSV.

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
1. Abra la notificación de bandeja de entrada para el trabajo de exportación. Seleccione el trabajo y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas. Para descargar el archivo CSV con los metadatos, toque o haga clic en Descarga **** CSV desde la barra de herramientas. Click **[!UICONTROL Close]**.

   ![Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva](assets/csv_download.png)
   *Figura:Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva*
