---
title: Propiedades del recurso en  [!DNL the Content Hub]
description: Obtenga información sobre cómo ver y administrar propiedades de recursos en  [!DNL Content Hub]
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 9%

---

# Administración de propiedades de recursos en Content Hub {#asset-properties}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

![Imagen del titular de metadatos](assets/metadata-banner-image.png)

[!DNL The Content Hub] le permite ver información sobre el recurso que es crítica para una distribución eficiente de los recursos. Es la recopilación de todos los datos disponibles para un recurso.

La visualización de las propiedades de los recursos le ayuda a categorizar los recursos y resulta útil a medida que aumenta la cantidad de información digital. Es posible administrar algunos cientos de archivos basados únicamente en los nombres de archivo, miniaturas y memoria. Sin embargo, este enfoque no es escalable cuando aumenta el número de personas involucradas y el número de recursos administrados. Además, el valor de un recurso digital aumenta a medida que este se convierte en lo siguiente:

* Más accesible: los sistemas y los usuarios pueden encontrarlo fácilmente.
* Más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades fácilmente y aplicarles cambios.
* Completado: el recurso lleva más información y contexto.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden realizar las acciones mencionadas en este artículo.

## Ver las propiedades de un recurso {#properties-ui}

Antes de usar, compartir o descargar un recurso, puede verlo más de cerca. La función de vista previa permite ver no solo las imágenes, sino también algunos otros tipos de recursos admitidos. No solo puede ver el recurso, sino también ver su información detallada y realizar otras acciones. Para ver información de un recurso, navegue hasta él o [busque](search-assets.md) el recurso y, a continuación, haga clic en él para abrir sus propiedades. En la siguiente figura se muestran los campos disponibles en una página de propiedades de recurso:

![Propiedades de la interfaz de usuario de un recurso](assets/properties-ui.png)

* **A:** Título de un recurso
* **B:** Porcentaje de recurso de zoom o vista previa que se acerca más al acercar o alejar
* **C:** Deshacer zoom en el porcentaje seleccionado anteriormente
* **D:** Continúe con el recurso anterior o siguiente
* **E:** recuento de Assets
* **F:** Descargar el recurso
* **G:** Editar recurso con [!DNL Adobe Express]
* **H:** Contraer o previsualizar la información de un recurso
* **I:** Compartir el recurso
* **J:** Agregar recurso a [!DNL Collection]
* **K:** Cerrar pantalla de vista previa
* **L:** información de un recurso que incluye título, formato, tamaño, resolución, etiquetas, etiquetas de color y etiquetas inteligentes.

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

* **Etiquetas inteligentes:** [!DNL The Content Hub] utiliza los servicios de contenido inteligente de Adobe Sensei para entrenar recursos mediante el algoritmo de reconocimiento en la estructura basada en etiquetas. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. Las etiquetas inteligentes aumentan la velocidad del contenido de los proyectos al ayudarle a encontrar recursos relevantes rápidamente. Las etiquetas inteligentes son un ejemplo de información de recursos que no está contenida en la imagen. [!DNL The Content Hub] aplica automáticamente las etiquetas inteligentes a los recursos, de manera predeterminada.

* **Etiquetas de color:** [Las etiquetas de color](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=en) le ayudan a reconocer un recurso mediante colores que se identifican automáticamente en un recurso mediante las capacidades de IA de Sensei de Adobe.

* Fecha de carga

* Cargado por

* Última modificación

* Última modificación hecha por

También hay propiedades que se especifican al agregar recursos a Content Hub. Para obtener más información, consulte [Agregar recursos aprobados por la marca a Content Hub](upload-brand-approved-assets.md). Estas propiedades también se muestran en la página de propiedades del recurso.

Los administradores también pueden configurar las propiedades que se muestran para cada recurso. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->
