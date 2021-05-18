---
title: Importe y exporte metadatos de recursos de manera masiva
description: Este artículo describe cómo importar y exportar metadatos de forma masiva.
contentOwner: AG
feature: Metadatos
role: Business Practitioner,Administrator
exl-id: fb70a068-3ba3-4459-952d-79155d286c42
source-git-commit: 1dc639265570b54c42d04f61178d8d2faec1b433
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 12%

---

# Importe y exporte metadatos de recursos de manera masiva {#import-and-export-asset-metadata-in-bulk}

AEM Assets permite importar metadatos de recursos de forma masiva mediante un archivo CSV. Puede realizar actualizaciones masivas de los recursos cargados recientemente o de los existentes mediante la importación de un archivo CSV. También puede introducir metadatos de recursos de forma masiva desde sistemas de terceros en formato CSV.

## Importar metadatos {#import-metadata}

La importación de metadatos es asíncrona y no impide el rendimiento del sistema. La actualización simultánea de los metadatos de varios recursos puede requerir muchos recursos, ya que la actividad de reescritura de metadatos utiliza microservicios de recursos. Adobe recomienda planificar las operaciones masivas durante el uso del servidor liviano para que el rendimiento de otros usuarios no se vea afectado.

>[!NOTE]
>
>Para importar metadatos en áreas de nombres personalizadas, registre primero las áreas de nombres.

1. Vaya a la interfaz de usuario de Assets y pulse o haga clic en **[!UICONTROL Crear]** en la barra de herramientas.
1. En el menú, seleccione **[!UICONTROL Metadatos]**.
1. En la página **[!UICONTROL Importación de metadatos]**, pulse o haga clic en **[!UICONTROL Seleccionar archivo]**. Seleccione el archivo CSV con los metadatos.
1. Especifique los siguientes parámetros:

   | Parámetro | Descripción |
   | ---------------------- | ------- |
   | Tamaño del lote | Número de recursos de un lote para los que se van a importar metadatos. El valor predeterminado es 50. El valor máximo es 100. |
   | Separador de campos | El valor predeterminado es `,` (una coma). Puede especificar cualquier otro carácter. |
   | Delimitador de varios valores | Separador para valores de metadatos. El valor predeterminado es `|`. |
   | Lanzar flujos de trabajo | False de forma predeterminada. Cuando se establece en `true` y la configuración predeterminada de Launch está en vigor para el flujo de trabajo de escritura de metadatos DAM (que escribe metadatos en los datos de XMP binarios). Al habilitar los flujos de trabajo de lanzamiento, el sistema se ralentiza. |
   | Nombre de columna de ruta de activos | Define el nombre de columna del archivo CSV con recursos. |

1. Haga clic **[!UICONTROL Import]** en la barra de herramientas. Una vez importados los metadatos, se envía una notificación a la bandeja de entrada de notificaciones. Vaya a la página de propiedades del recurso y compruebe si los valores de metadatos se importan correctamente para los recursos.

Para agregar fecha y marca de hora al importar metadatos, use el formato `YYYY-MM-DDThh:mm:ss.fff-00:00` para fecha y hora. La fecha y la hora están separadas por `T`, `hh` es horas en formato de 24 horas, `fff` es nanosegundos y `-00:00` es compensación de zona horaria. Por ejemplo, `2020-03-26T11:26:00.000-07:00` es el 26 de marzo de 2020 a las 11:26:00.000 (hora PST).

>[!CAUTION]
>
>Si el formato de fecha no coincide con `YYYY-MM-DDThh:mm:ss.fff-00:00`, no se establecen los valores de fecha. Los formatos de fecha del archivo CSV de metadatos exportado tienen el formato `YYYY-MM-DDThh:mm:ss-00:00`. Si desea importarla, conviértala al formato aceptable añadiendo el valor de nanosegundos indicado por `fff`.

## Exportar metadatos {#export-metadata}

Puede exportar metadatos de varios recursos en formato CSV. Los metadatos se exportan de forma asíncrona y no afectan al rendimiento del sistema. Para exportar metadatos, AEM atraviesa las propiedades del nodo de recursos `jcr:content/metadata` y sus nodos secundarios y exporta las propiedades de metadatos en un archivo CSV.

Algunos casos de uso para exportar metadatos de forma masiva son:

* Importe los metadatos en un sistema de terceros al migrar recursos.
* Comparta metadatos de recursos con un equipo de proyecto más amplio.
* Probar o auditar los metadatos para comprobar el cumplimiento.
* Externalice los metadatos para una localización independiente.

1. Seleccione la carpeta de recursos que contiene los recursos para los que desea exportar metadatos. En la barra de herramientas, seleccione **[!UICONTROL Export metadata]**.
1. En el cuadro de diálogo Exportación de metadatos, especifique un nombre para el archivo CSV. Para exportar metadatos de recursos en subcarpetas, seleccione **[!UICONTROL Incluir recursos en subcarpetas]**.

   ![Interfaz y opciones para exportar metadatos de todos los recursos en una ](assets/export_metadata_page.png "carpetaInterfaz y opciones para exportar metadatos de todos los recursos de una carpeta")

1. Seleccione las opciones que desee. Proporcione un nombre de archivo y, si es necesario, una fecha.

1. En el campo **[!UICONTROL Properties to be export]** , especifique si desea exportar todas las propiedades o propiedades específicas. Si elige Propiedades selectivas para exportar, añada las propiedades que desee.

1. En la barra de herramientas, pulse o haga clic en **[!UICONTROL Exportar]**. Un mensaje confirma que se exportan los metadatos. Cierre el mensaje.
1. Abra la notificación de la bandeja de entrada para el trabajo de exportación. Seleccione el trabajo y haga clic en **[!UICONTROL Abrir]** en la barra de herramientas. Para descargar el archivo CSV con los metadatos, pulse o haga clic en **[!UICONTROL Descargar CSV]** desde la barra de herramientas. Haga clic en **[!UICONTROL Cerrar]**.

   ![Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva](assets/csv_download.png)

   *Figura: Cuadro de diálogo para descargar el archivo CSV que contiene metadatos exportados de forma masiva.*
