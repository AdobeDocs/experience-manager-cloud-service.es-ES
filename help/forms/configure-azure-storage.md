---
title: ¿Cómo configurar el almacenamiento de Azure?
description: Obtenga información sobre cómo integrar formularios con el servidor de almacenamiento de Azure.
exl-id: 606383b3-293c-43d2-9ba0-5843c4e0caa8
source-git-commit: 10284b1ac6fbad2e7f6231603c3dd60b6e404299
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Configuración de almacenamiento de [!DNL Azure] {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integración de datos](data-integration.md) proporciona un [!DNL Azure] configuración de almacenamiento para integrar formularios con [!DNL Azure] servicios de almacenamiento. El Modelo de datos de formulario se puede utilizar para crear un Forms adaptable que interactúe con [!DNL Azure] para habilitar los flujos de trabajo empresariales. Por ejemplo:

* Escribir datos en [!DNL Azure] sobre el envío del formulario adaptable.
* Escribir datos en [!DNL Azure] a través de entidades personalizadas definidas en el Modelo de datos de formulario y viceversa.
* Consulta [!DNL Azure] para datos y rellene previamente Forms adaptable.
* Leer datos de [!DNL Azure] servidor.

## Crear [!DNL Azure] configuración de almacenamiento {#create-azure-storage-configuration}

Antes de ejecutar estos pasos, asegúrese de que dispone de un [!DNL Azure] cuenta de almacenamiento y clave de acceso para autorizar el acceso a la variable [!DNL Azure] cuenta de almacenamiento.

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Almacenamiento de Azure]**.
1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.
1. Especifique un título para la configuración en la **[!UICONTROL Título]** campo .
1. Especifique el nombre del [!DNL Azure] cuenta de almacenamiento en la variable **[!UICONTROL Cuenta de almacenamiento de Azure]** campo .
1. Especifique la clave para acceder a la cuenta de almacenamiento de Azure en la **[!UICONTROL Clave de acceso de Azure]** toque y campo **[!UICONTROL Guardar]**.

## Crear modelo de datos de formulario {#create-azure-form-data-model}

Después de crear la variable [!DNL Azure] configuración de almacenamiento, puede [crear el modelo de datos de formulario](create-form-data-models.md). Especifique la carpeta que contiene la variable [!DNL Azure] en el **[!UICONTROL Configuración de fuente de datos]** al crear el Modelo de datos de formulario. A continuación, puede seleccionar la configuración de la lista de configuraciones que existen en el nombre de carpeta especificado.

### Agregar [!DNL Azure] servicios al Modelo de datos de formulario {#add-azure-services}

Después de crear los objetos Modelo de datos de formulario y modelo de datos, puede agregar [!DNL Azure] servicios al Modelo de datos de formulario.

Para agregar [!DNL Azure] servicios:

1. En el modo de edición, seleccione los servicios de la **[!UICONTROL Servicios]** en el panel izquierdo y pulse **[!UICONTROL Agregar selección]**. Los servicios seleccionados se muestran en la **[!UICONTROL Servicios]** del Modelo de datos de formulario.

   ![Añadir servicios seleccionados](assets/select-services.png)

1. En el **[!UICONTROL Servicios]** , seleccione el servicio y **[!UICONTROL Editar propiedades]**. En función del servicio, defina los objetos del modelo de entrada o salida para el servicio.

1. Toque **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

   La tabla siguiente describe las [!DNL Azure] servicios:

   <table>
    <tbody>
     <tr>
      <th><strong>Nombre de servicio</strong></th>
      <th><strong>Descripción</strong></th>
     </tr>
     <tr>
      <td>Obtener blob de Azure</td>
      <td>Recuperar datos almacenados como un blob en el almacenamiento de Azure mediante un ID o un nombre</td>
     </tr>
     <tr>
      <td>Obtener Blob con URL binaria de Azure</td>
      <td>Recuperar datos almacenados como un blob con una URL para binarios en el almacenamiento de Azure mediante un ID o un nombre</td>
     </tr>
     <tr>
      <td>Guardar blob en Azure</td>
      <td>Usar un ID de blob para guardar datos en el almacenamiento de Azure</td>
     </tr>
     <tr>
      <td>Actualizar Blob en Azure</td>
      <td>Usar un ID de blob para actualizar los datos en el almacenamiento de Azure</td>
     </tr>
     <tr>
      <td>Recuperar lista de ID de Blob de Azure</td>
      <td>Recupere una lista de ID de Blob de Azure en función del número definido en la solicitud de entrada.</td>
     </tr>
     <tr>
      <td>Recuperar direcciones URL SAS para blobs desde Azure</td>
      <td>Recupere las direcciones URL SAS para los Blobs de Azure en función de los ID de Blob en la solicitud de entrada.</td>
     </tr>
     <tr>
      <td>Eliminar blob de Azure</td>
      <td>Usar un ID de blob para eliminar datos del almacenamiento de Azure</td>
     </tr>
    </tbody>
   </table>

### Definir una propiedad de objeto del modelo de datos como clave de búsqueda {#define-data-model-object-as-metadata}

Para definir una propiedad de objeto del modelo de datos como clave de búsqueda:

1. En el **[!UICONTROL Modelo]** , seleccione la propiedad del objeto del modelo de datos y pulse **[!UICONTROL Editar propiedades]**.
1. Cambie el **[!UICONTROL Clave de búsqueda]** alterne la opción al estado ON . Esta opción solo está disponible para los tipos de datos principales.
1. Toque **[!UICONTROL Listo]** y, a continuación, toque **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

Después de definir las propiedades del objeto del modelo de datos como claves de búsqueda, los valores hash se almacenan en etiquetas de índice de Azure y los valores codificados de Base64 se almacenan en los metadatos de Azure.

>[!NOTE]
>
>Solo se permiten 10 claves de búsqueda por entidad de Azure, ya que Azure solo permite 10 etiquetas por Blob y el valor de las propiedades marcado como claves de búsqueda se almacena en las etiquetas de índice de Azure después del hash.
