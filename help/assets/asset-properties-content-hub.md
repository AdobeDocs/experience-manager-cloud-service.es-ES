---
title: Propiedades del recurso en [!DNL the Content Hub]
description: Obtenga información sobre cómo ver y administrar propiedades de recursos en [!DNL Content Hub]
role: User
source-git-commit: 5a968440c8841abe7af2c81c4af12258b7e4547f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 8%

---


# Administración de propiedades de recursos en Content Hub {#asset-properties}

![Imagen del titular de metadatos](assets/metadata-banner-image.png)

[!DNL The Content Hub] le permite ver información sobre el recurso, que es crítica para una distribución eficiente de los recursos. Es la recopilación de todos los datos disponibles para un recurso.

La visualización de las propiedades de los recursos le ayuda a categorizar los recursos y resulta útil a medida que aumenta la cantidad de información digital. Es posible administrar algunos cientos de archivos basados únicamente en los nombres de archivo, miniaturas y memoria. Sin embargo, este enfoque no es escalable cuando aumenta el número de personas involucradas y el número de recursos administrados. Además, el valor de un recurso digital aumenta a medida que este se convierte en lo siguiente:

* Más accesible: los sistemas y los usuarios pueden encontrarlo fácilmente.
* Más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades fácilmente y aplicarles cambios.
* Completado: el recurso lleva más información y contexto.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) puede realizar las acciones mencionadas en este artículo.

## Ver las propiedades de un recurso {#properties-ui}

Antes de usar, compartir o descargar un recurso, puede verlo más de cerca. La función de vista previa permite ver no solo las imágenes, sino también algunos otros tipos de recursos admitidos. No solo puede ver el recurso, sino también ver su información detallada y realizar otras acciones. Para ver la información de un recurso, vaya al recurso o [búsqueda](search-assets.md) Seleccione el recurso y haga clic en él para abrir sus propiedades. En la siguiente figura se muestran los campos disponibles en una página de propiedades de recurso:

![Propiedades de la IU de un recurso](assets/properties-ui.png)

* **A:** Título de un recurso
* **B:** Porcentaje de recurso de zoom o vista previa más cercano al acercar o alejar
* **C:** Deshacer zoom en el porcentaje seleccionado anteriormente
* **D:** Pasar al recurso anterior o siguiente
* **E:** Recuento de Assets
* **F:** Descargar el recurso
* **G:** Editar recurso mediante [!DNL Adobe Express]
* **Al.:** Contraer o previsualizar la información de un recurso
* **I:** Compartir el recurso
* **J:** Añadir recurso a [!DNL Collection]
* **K:** Cerrar pantalla de vista previa
* **L:** Información de un recurso que incluye título, formato, tamaño, resolución, etiquetas, etiquetas de color y etiquetas inteligentes.

## Formatos compatibles {#supported-formats}

En la tabla siguiente se muestran los formatos de archivo admitidos en [!DNL the Content Hub]:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo de archivo</strong></th>
      <th><strong>Formatos compatibles</strong></th>
     </tr>
     <tr>
      <td>Imagen</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL SVG]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Vídeo</td>
      <td>
        <ul>
            <li>[!UICONTROL Quicktime]</li>  
            <li>[!UICONTROL MP4]</li> 
        </ul>
      </td>
     </tr>
      <tr>
      <td>Documento</td>
      <td>
        <ul>
            <li>[!UICONTROL txt] (sin formato)</li>  
            <li>[!UICONTROL Doc/Docx]</li> 
            <li>[!UICONTROL XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Medios de impresión</td>
      <td>
        <ul>
            <li>[!UICONTROL PDF]</li>  
        </ul>
      </td>
     </tr>  
    </tbody>
   </table>

### Propiedades derivadas después de cargar un recurso {#derived-properties}

Una vez cargado un recurso, Content Hub obtiene algunas propiedades que se generan automáticamente. A continuación se muestra una lista de algunos de ellos:

* **Tamaño:** El tamaño muestra el valor lógico de un recurso según sus dimensiones. Aclara el espacio que un recurso está ocupando en un repositorio. [!DNL The Content Hub] admite recursos de hasta 2 GB.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Etiquetas inteligentes:** [!DNL The Content Hub] utiliza los servicios de contenido inteligente de Adobe Sensei para formar recursos mediante el algoritmo de reconocimiento en la estructura basada en etiquetas. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. Las etiquetas inteligentes aumentan la velocidad del contenido de los proyectos al ayudarle a encontrar recursos relevantes rápidamente. Las etiquetas inteligentes son un ejemplo de información de recursos que no está contenida en la imagen. [!DNL The Content Hub] aplica automáticamente las etiquetas inteligentes a los recursos de forma predeterminada.

* **Etiquetas de color:** [Etiquetas de color](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) le ayuda a reconocer un recurso mediante colores que se identifican automáticamente en un recurso mediante las funciones de Sensei AI de Adobe.

* Fecha de carga

* Cargado por

* Última modificación

* Última modificación hecha por

También hay propiedades que se especifican al agregar recursos a Content Hub. Para obtener más información, consulte [Añadir recursos aprobados por la marca a Content Hub](upload-brand-approved-assets.md). Estas propiedades también se muestran en la página de propiedades del recurso.

Los administradores también pueden configurar las propiedades que se muestran para cada recurso. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->

