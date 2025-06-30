---
title: Búsqueda de recursos en Content Hub
description: Obtenga información sobre cómo buscar recursos en  [!DNL Content Hub]
role: User
exl-id: 8578d7d0-32b9-4e5c-80ef-3827e358ac6c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Buscar Assets en [!DNL Content Hub] {#search-assets}

Cuando tiene un gran número de recursos en el repositorio, la búsqueda del recurso adecuado requiere tiempo. La búsqueda de [!DNL The Content Hub] le permite buscar los recursos aprobados para que pueda realizar acciones adicionales en ellos, como descargar, compartir o crear colecciones. Puede utilizar varias funciones para reducir los resultados de búsqueda, como, por ejemplo, realizar búsquedas basadas en texto, utilizar filtros, realizar búsquedas específicas de etiquetas inteligentes o etiquetas inteligentes, buscar un formato de archivo determinado, etc.

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden realizar las acciones mencionadas en este artículo.

## Qué puede buscar  {#what-you-can-search}

La búsqueda [!DNL Content Hub] proporciona resultados basados en:

* **Texto coincidente:** La búsqueda de [!DNL Content Hub] le permite buscar un recurso con su nombre o descripción. Puede realizar una búsqueda basada en palabras clave que compare la palabra clave con el texto disponible en las propiedades de un recurso.

* **Contexto coincidente:** La lista de resultados de búsqueda de [!DNL Content Hub] contiene los resultados inmediatos de los recursos que obtiene basándose en el contexto coincidente. Por ejemplo, si escribe `cool` en la barra de búsqueda, los recursos relacionados con `winter`, `snow`, `cold surroundings` se muestran en la lista de búsqueda.

* **Información del recurso (título, etiquetas o etiquetas inteligentes):** [!DNL Content Hub] utiliza el algoritmo de búsqueda inteligente para clasificar los resultados de búsqueda con precisión y de la manera más relevante posible. [Metadatos](#asset-properties.md) es la colección de todos los datos disponibles para un recurso, pero es posible que no estén necesariamente contenidos en ese recurso. [Le ayuda a categorizar los recursos y resulta útil a medida que aumenta la cantidad de información digital](/help/assets/configure-content-hub-ui-options.md##configure-metadata-search-content-hub).

* **Fecha de última modificación:** Los recursos que se modificaron recientemente aparecen en la parte superior de la lista de resultados de búsqueda. También puede filtrar el intervalo de fechas según sus necesidades.

* **Uso:** Los recursos que se usan con más frecuencia aparecen en la parte superior de la lista de búsqueda.

* **Historial de búsqueda:** Haga clic dentro del cuadro de búsqueda sin escribir ningún carácter para obtener el historial de búsqueda. También puede quitar cualquier palabra clave en particular del historial. El historial de búsqueda se guarda en la memoria caché de un explorador web, lo que significa que, si accede a la búsqueda [!DNL Content Hub] en un explorador diferente o borra la memoria caché del explorador, ya no podrá ver el historial de búsqueda.

* **Buscar mientras escribe:** La búsqueda de [!DNL Content Hub] mejora su experiencia de búsqueda al proporcionar sugerencias de autocompletar al comenzar a escribir.

## Búsqueda básica {#basic-search}

Para realizar una búsqueda básica de [!DNL the Content Hub], vaya a la barra de búsqueda y especifique la palabra clave que necesita buscar. Vaya a los filtros disponibles en el panel izquierdo y aplíquelos para reducir los resultados de búsqueda.

Por ejemplo, busque todas las imágenes de **[!UICONTROL JPEG]** con la palabra clave `architect` en ella, que se modificó en el último año. Para ejecutar este escenario, ejecute los siguientes pasos:

1. Especifique `architect` como palabra clave de búsqueda.

1. Vaya al panel Filtros > **[!UICONTROL Formato]** > seleccione **[!UICONTROL JPEG]**.

1. Vaya a **[!UICONTROL Modificado]** > especifique el intervalo de fechas.

   ![Búsqueda básica](assets/basic-search.png)

## Reduzca los resultados de búsqueda mediante filtros {#narrow-down-search-results}

Utilice el panel Filtros para buscar recursos basados en metadatos. Puede filtrar los resultados de búsqueda según varios predicados de búsqueda. Puede seleccionar todos los predicados adecuados para minimizar o reducir los resultados de búsqueda. Cuando se seleccionan varias opciones dentro de un filtro, Content Hub muestra los recursos que coinciden con cualquiera de las opciones seleccionadas dentro de un filtro. Sin embargo, cuando selecciona varias opciones en distintos filtros, Content Hub solo muestra los recursos que coinciden con todas las opciones seleccionadas en todos los filtros para reducir los resultados de búsqueda.

Los filtros predeterminados incluyen formato de archivo, aprobado por, fecha de aprobación, recursos caducados y no caducados y fecha de caducidad. Los administradores también pueden configurar los filtros que se muestran en la lista de filtros. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-filters-content-hub).

<!--

<table>
    <tbody>
     <tr>
      <th><strong>Search Predicate</strong></th>
      <th><strong>Description</strong></th>
      <th><strong>Properties</strong></th>
     </tr>
     <tr>
      <td> Campaigns </td>
      <td> Allows you to search using planned activity performed to take any particular action. For example, advertisement campaign run on Ferrari to know the understand the interests of people using number of clicks people perform.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Channels </td>
      <td> Helps you to understand the path from where the asset is coming from. For example, web, social media, books, catalog, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Region </td>
      <td> Helps you to understand the location where the asset is created. For example, Japan, EMEA, Worldwide, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Keywords </td>
      <td> Keyword helps you search using terms or the words that you enter based on the topic. For example, images, low-resolution, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Timeframe </td>
      <td> Helps you search assets using timeline. For example, search by year 2024, Q3 2023, etc.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td>File format</td>
      <td>Composition of an asset. The supported assets include image, document, video, printable media, and so on.</td>
      <td>
        <ul>
            <li>[!UICONTROL JPEG]</li> 
            <li>[!UICONTROL Quicktime]</li> 
            <li>[!UICONTROL PNG]</li> 
            <li>[!UICONTROL WebP]</li> 
            <li>[!UICONTROL MP4]</li> 
            <li>[!UICONTROL Plain]</li> 
            <li>[!UICONTROL PDF]</li>
            <li>[!UICONTROL SVG + XML]</li>
        </ul>
      </td>
     </tr>
     <tr>
      <td>Tags</td>
      <td>Tags help you categorize assets that can be browsed and searched more efficiently based on hierarchical taxonomies.</td>
      <td>
        <ul>
            <li>Field label</li>
            <li>Property name</li>
            <li>Path</li>
            <li>Description</li>
        </ul>
      </td>
     </tr>
     <!--<tr>
      <td>Subject</td>
      <td>Classification of assets based on their theme. For example, colorful, hiking, outdoors.</td>
      <td>NA</td>
     </tr>
          <tr>
      <td>Last modified</td>
      <td>Search assets based on their last modification. Specify the date range using the Start date and End date fields.</td>
      <td>
        <ul>
            <li>Range text (From)</li> 
            <li>Range text (To) </li>
        </ul>
      </td>
     </tr>    
     <!--<tr>
      <td>Asset ID</td>
      <td>Unique number that identifies the asset.</td>
      <td>NA</td>
     </tr>
     <tr>
      <td> Colors </td>
      <td> Helps you search assets using colors that are automatically identified in an asset using Adobe's Sensei AI capabilities.</td>
      <td>NA</td>
     </tr>  
    </tbody>
   </table>

-->

## Haga más con la búsqueda {#do-more-with-search}

[!DNL The Content Hub] no se limita a la búsqueda, sino que le permite realizar acciones adicionales, como [descargar](download-assets-content-hub.md), [compartir](share-assets-content-hub.md) y [agregar recursos a la colección](collections-content-hub.md), directamente desde la interfaz de búsqueda o vista previa. Seleccione los recursos en la página de resultados de búsqueda para ver estas opciones.
