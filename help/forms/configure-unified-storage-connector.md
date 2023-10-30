---
title: Cómo configurar el conector de almacenamiento unificado (USC) para AEM Forms
description: Obtenga información sobre cómo administrar el conector de almacenamiento unificado (USC) para AEM Forms. Utilice el conector de almacenamiento unificado (USC) para conectar AEM Forms a almacenes de datos externos.
exl-id: c93d0242-0c15-4d69-82a1-d6fcc7da4bae
source-git-commit: c33f59cb56decf1e5bbbe0b5bb084e906585e702
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 78%

---

# Administrar el conector de almacenamiento unificado (USC) para AEM Forms {#manage-unified-storage-connector}

Puede utilizar el conector de almacenamiento unificado (USC) para conectar AEM Forms a almacenes de datos externos.

Por ejemplo, puede rellenar los valores de los campos de un formulario adaptable y enviarlos a un flujo de trabajo AEM. También puede configurar flujos de trabajo de AEM para almacenar datos en un almacenamiento externo, como el servidor de Microsoft Azure Storage. AEM Utilice el conector de almacenamiento unificado (USC) para crear una conexión entre los flujos de trabajo de la y el almacenamiento externo.

## Conectar los flujos de trabajo de AEM con un servidor de Microsoft Azure Storage {#connect-workflows-with-azure}

Cree una configuración de Azure Storage y consulte esa configuración mediante el conector de almacenamiento unificado (USC). A continuación, podrá configurar modelos de flujo de trabajo de AEM para externalizar el almacenamiento de datos y conectarlos a un servidor de Azure Storage.

### Crear la configuración de [!DNL Azure] Storage {#create-azure-storage-configuration}

Antes de ejecutar estos pasos, asegúrese de que dispone de una cuenta de [!DNL Azure] Storage y una clave de acceso para autorizar el acceso a la cuenta de [!DNL Azure] Storage.

Siga estos pasos para crear la configuración de [!DNL Azure] Storage:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.
1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.
1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.
1. Especifique el nombre de la cuenta de [!DNL Azure] Storage en el campo **[!UICONTROL Cuenta de Azure Storage]**.
1. Especifique la clave para acceder a la cuenta de Azure Storage en el campo **[!UICONTROL Clave de acceso de Azure]** y pulse **[!UICONTROL Guardar]**.

### AEM Configuración del conector de almacenamiento unificado (USC) para flujos de trabajo de la {#configure-unified-storage-connector-workflows}

AEM Realice los siguientes pasos para configurar el conector de almacenamiento unificado (USC) para flujos de trabajo de:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Formularios]** > **[!UICONTROL Conector de almacenamiento unificado]**.

1. En la sección **[!UICONTROL Flujo de trabajo]**, seleccione **[!UICONTROL Azure]** en la lista desplegable Almacenamiento.
1. Especifique la ruta de configuración [para la configuración del almacenamiento de Azure](#create-azure-storage-configuration) en el campo **[!UICONTROL Ruta de configuración del almacenamiento]**.
1. Pulse **[!UICONTROL Publicar]** y, a continuación, pulse **[!UICONTROL Guardar]** para guardar la configuración.

### Configuración de un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo {#configure-workflow-external-data-storage}

Realice los siguientes pasos para configurar un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo:

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. Seleccione el nombre de un modelo y pulse **[!UICONTROL Editar]**.
1. Pulse el icono Información de página y luego pulse **[!UICONTROL Abrir propiedades]**.
1. Seleccione **[!UICONTROL Externalizar el almacenamiento de los datos del flujo de trabajo]**.
1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar las propiedades.

>[!NOTE]
>
>Las opciones para guardar el paso Asignar tarea como borrador y para recuperar su historial se desactivan al configurar un modelo de flujo de trabajo de AEM para el almacenamiento de datos externo.

### Directrices para los flujos de trabajo de AEM de un almacenamiento de datos externo {#guidelines-workflows-external-data-storage}

Estas son las directrices a seguir a la hora de utilizar flujos de trabajo de AEM y almacenar datos en almacenamientos de datos externos, como el servidor de Microsoft Azure Storage:

* Utilice variables para almacenar los datos al definir los archivos de datos de entrada y salida y los archivos adjuntos en los pasos del modelo de flujo de trabajo. No seleccione las opciones **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]**. Las opciones **[!UICONTROL Relativo a carga útil]** y **[!UICONTROL Disponible en una ruta absoluta]** no se muestran automáticamente una vez que [ha configurado un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo](#configure-workflow-external-data-storage).

* Utilice variables para almacenar los archivos de datos y los archivos adjuntos cuando envíe un formulario adaptable a un flujo de trabajo de AEM. No seleccione **[!UICONTROL Relativo a carga útil]** cuando envíe un formulario adaptable a un flujo de trabajo de AEM. La opción **[!UICONTROL Relativo a carga útil]** no se muestra automáticamente una vez que [ha configurado un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo](#configure-workflow-external-data-storage).

* No utilice un paso de un flujo de trabajo de AEM personalizado de un modelo de flujos de trabajo para almacenar datos en el repositorio CRX DE.

* Cuando [configure un modelo de flujo de trabajo de AEM para un almacenamiento de datos externo](#configure-workflow-external-data-storage), no cree columnas personalizadas para la Bandeja de entrada AEM, ya que los valores de las columnas personalizadas no se recuperan si el elemento de trabajo de la Bandeja de entrada AEM pertenece a un flujo de trabajo marcado para un almacenamiento externo.

>[!MORELIKETHIS]
>
>* [Configuración de fuentes de datos para AEM Forms](/help/forms/configure-data-sources.md)
>* [Configuración del almacenamiento de Azure para AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integración de Microsoft Dynamics 365 y Salesforce con Forms adaptable](/help/forms/configure-msdynamics-salesforce.md)
>  [Añadir el portal de Forms a una página de AEM Sites](/help/forms/configure-forms-portal.md)
