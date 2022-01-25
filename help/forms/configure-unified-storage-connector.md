---
title: ¿Cómo configurar el conector de almacenamiento unificado para AEM Forms?
description: Obtenga información sobre cómo administrar el conector de almacenamiento unificado para AEM Forms. Utilice el conector de almacenamiento unificado para conectar AEM Forms a almacenes de datos externos.
source-git-commit: da3cef0a0a28dd16e627a157f02bbe6a84f59da5
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---


# Administrar el conector de almacenamiento unificado para AEM Forms {#manage-unified-storage-connector}

Puede utilizar el conector de almacenamiento unificado para conectar AEM Forms a almacenes de datos externos.

Por ejemplo, puede rellenar valores para campos en un formulario adaptable y enviarlos a un flujo de trabajo AEM. Puede configurar aún más AEM Flujos de trabajo para almacenar datos en un almacenamiento externo, como el servidor de almacenamiento de Microsoft Azure. Utilice el conector de almacenamiento unificado para crear una conexión entre AEM flujos de trabajo y el almacenamiento externo.

## Conectar AEM flujos de trabajo con un servidor de almacenamiento de Microsoft Azure {#connect-workflows-with-azure}

Cree una configuración de almacenamiento de Azure y consulte esa configuración mediante el conector de almacenamiento unificado. A continuación, puede configurar AEM modelos de flujo de trabajo para externalizar el almacenamiento de datos y conectarlos a un servidor de almacenamiento de Azure.

### Crear [!DNL Azure] configuración de almacenamiento {#create-azure-storage-configuration}

Antes de ejecutar estos pasos, asegúrese de que dispone de un [!DNL Azure] cuenta de almacenamiento y clave de acceso para autorizar el acceso a la variable [!DNL Azure] cuenta de almacenamiento.

Siga estos pasos para crear un [!DNL Azure] configuración de almacenamiento:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.
1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.
1. Especifique un título para la configuración en la **[!UICONTROL Título]** campo .
1. Especifique el nombre del [!DNL Azure] cuenta de almacenamiento en la variable **[!UICONTROL Cuenta de almacenamiento de Azure]** campo .
1. Especifique la clave para acceder a la cuenta de almacenamiento de Azure en la **[!UICONTROL Clave de acceso de Azure]** toque y campo **[!UICONTROL Guardar]**.

### Configuración del conector de almacenamiento unificado para flujos de trabajo AEM {#configure-unified-storage-connector-workflows}

Realice los siguientes pasos para configurar el conector de almacenamiento unificado para AEM flujos de trabajo:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de almacenamiento unificado]**.

1. En el **[!UICONTROL Flujo de trabajo]** , seleccione **[!UICONTROL Azure]** en la lista desplegable Almacenamiento .
1. Especifique la variable [ruta de configuración para la configuración de almacenamiento de Azure](#create-azure-storage-configuration) en el **[!UICONTROL Ruta de configuración de almacenamiento]** campo .
1. Toque **[!UICONTROL Publicación]** y, a continuación, toque **[!UICONTROL Guardar]** para guardar la configuración.

### Configuración de un modelo de flujo de trabajo AEM para almacenamiento de datos externos {#configure-workflow-external-data-storage}

Realice los siguientes pasos para configurar un modelo de flujo de trabajo AEM para un almacenamiento de datos externo:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Seleccione un nombre de modelo y pulse **[!UICONTROL Editar]**.
1. Pulse el icono Información de página y pulse **[!UICONTROL Abrir propiedades]**.
1. Select **[!UICONTROL Externalización del almacenamiento de datos de flujo de trabajo]**.
1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las propiedades.

>[!NOTE]
>
>Las opciones para guardar el paso Asignar tarea como borrador y para recuperar el historial del paso Asignar tarea se desactivan al configurar un modelo de flujo de trabajo AEM para el almacenamiento de datos externos.

### Directrices para flujos de trabajo de AEM para almacenamiento de datos externos {#guidelines-workflows-external-data-storage}

A continuación se indican las directrices que se siguen cuando se utilizan AEM Flujos de trabajo y se almacenan datos en almacenes de datos externos, como el servidor de almacenamiento de Microsoft Azure:

* Utilice variables para almacenar datos al definir archivos de datos de entrada y salida y archivos adjuntos en los pasos del modelo de flujo de trabajo. No seleccione **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]** opciones. La variable **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]** las opciones no se muestran automáticamente una vez que [configurar un modelo de flujo de trabajo AEM para el almacenamiento de datos externos](#configure-workflow-external-data-storage).

* Utilice variables para almacenar archivos de datos y archivos adjuntos al enviar un formulario adaptable a un flujo de trabajo AEM. No seleccione **[!UICONTROL Relativo a carga útil]** al enviar un formulario adaptable a un flujo de trabajo AEM. La variable **[!UICONTROL Relativo a carga útil]** no se muestra automáticamente una vez que [configurar un modelo de flujo de trabajo AEM para el almacenamiento de datos externos](#configure-workflow-external-data-storage).

* No utilice un paso de flujo de trabajo AEM personalizado en un modelo de flujo de trabajo para almacenar datos en el repositorio CRX DE.

* Cuando [configurar un modelo de flujo de trabajo AEM para el almacenamiento de datos externos](#configure-workflow-external-data-storage), no cree columnas personalizadas para AEM Bandeja de entrada, ya que los valores de las columnas personalizadas no se recuperan si el elemento de trabajo de la Bandeja de entrada de AEM pertenece a un flujo de trabajo marcado para almacenamiento externo.