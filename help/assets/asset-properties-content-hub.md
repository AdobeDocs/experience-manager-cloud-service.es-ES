---
title: Vista previa del recurso y sus propiedades en  [!DNL the Content Hub]
description: Obtenga información sobre cómo obtener una vista previa de recursos y propiedades en  [!DNL Content Hub]
role: User
exl-id: a85af980-4c51-4d30-9fad-afd16370e9db
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 11%

---

# Vista previa del recurso y sus propiedades en Content Hub {#asset-properties}

![Imagen del titular de metadatos](assets/metadata-banner-image.png)

[!DNL The Content Hub] le permite ver información sobre el recurso que es crítica para una distribución eficiente de los recursos. Es la recopilación de todos los datos disponibles para un recurso.

La visualización de la vista previa de recursos y sus propiedades le ayuda a categorizar los recursos y resulta útil a medida que aumenta la cantidad de información digital. Es posible administrar algunos cientos de archivos basados únicamente en los nombres de archivo, miniaturas y memoria. Sin embargo, este enfoque no es escalable cuando aumenta el número de personas involucradas y el número de recursos administrados. Además, el valor de un recurso digital aumenta a medida que este se convierte en lo siguiente:

* Más accesible: los sistemas y los usuarios pueden encontrarlo fácilmente.
* Más fácil de actuar: tiene información completa sobre los elementos visuales de los recursos e información relacionada, para poder actuar en ellos más rápido y con más confianza.
* Completado: el recurso lleva más información y contexto.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden realizar las acciones mencionadas en este artículo.

## Previsualizar el recurso y sus propiedades {#properties-ui}

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

## Formatos de recurso admitidos {#supported-formats}

[!DNL Content Hub] admite todos los tipos de recursos y formatos que admite el repositorio [!DNL Assets] subyacente. En la tabla siguiente se enumeran los formatos de archivo clave de [!DNL the Content Hub], que proporcionan compatibilidad adicional para obtener una vista previa de los recursos visualmente:

<table> 
    <tbody>
     <tr>
      <th><strong>Tipo de archivo</strong></th>
      <th><strong>Formatos compatibles</strong></th>
     </tr>
     <tr>
        <td rowspan="3"> Imagen </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL JPEG]</td>
    </tr>
    <tr>
        <td>[!UICONTROL PNG]</td>
    </tr>
    <tr>
        <td rowspan="4"> Vídeo </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL Quicktime]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MP4]</td>
    </tr>
    <tr>
        <td>[!UICONTROL MPEG]</td>
    </tr>
    <tr>
        <td rowspan="4"> Documento </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL txt] (sin formato)</td>
    </tr>
    <tr>
        <td>[!UICONTROL Doc/Docx]</td>
    </tr>
    <tr>
        <td>[!UICONTROL XML]</td>
    </tr>
    <tr>
        <td rowspan="2"> Medios de impresión </td>
    </tr>
    </tr>
    <tr>
        <td>[!UICONTROL PDF]</td>
    </tr>
    </tbody>
</table>

### Propiedades derivadas {#derived-properties}

Algunas propiedades de los recursos mostrados en [!DNL Content Hub] se derivan o se generan automáticamente cuando los recursos se cargan en [!DNL Assets] y se aprueban para su disponibilidad en [!DNL Content Hub]. A continuación se muestra una lista de algunos de ellos:

* **Tamaño:** El tamaño representa el tamaño del binario de recursos almacenado en el repositorio subyacente.

<!--* **Tags:** Tags help you categorize assets that can be browsed and searched more efficiently. Tagging helps in propagating the appropriate taxonomy to other users and workflows. -->

* **Etiquetas inteligentes:** [!DNL The Content Hub] utiliza los servicios de contenido inteligente de Adobe AI para entrenar recursos mediante el algoritmo de reconocimiento en la estructura basada en etiquetas. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. Las etiquetas inteligentes aumentan la velocidad del contenido de los proyectos al ayudarle a encontrar recursos relevantes rápidamente. Las etiquetas inteligentes son un ejemplo de información de recursos que no está contenida en la imagen. [!DNL Experience Manager Assets] aplica automáticamente las etiquetas inteligentes a los recursos, de manera predeterminada.

* **Etiquetas de color:** [Las etiquetas de color](#https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/color-tag-images.html?lang=es) le ayudan a reconocer un recurso mediante colores que se identifican automáticamente en un recurso mediante las capacidades de IA de Adobe.

* Fecha de carga

* Cargado por

* Última modificación

* Última modificación hecha por

También hay propiedades que se especifican al agregar recursos a Content Hub. Para obtener más información, consulte [Agregar recursos aprobados por la marca a Content Hub](upload-brand-approved-assets.md). Estas propiedades también se muestran en la página de propiedades del recurso.

Los administradores también pueden configurar las propiedades, que se muestran para cada recurso:

* En la interfaz de usuario de vista previa de recursos: consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-asset-details-content-hub).
* En tarjetas de recursos en resultados de búsqueda o colecciones: consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#asset-card).

<!--

### Date range {#date-range} 

The date range allows you to select dates you want to see the assets. You can customize date range by choosing the start and end dates. 

-->
