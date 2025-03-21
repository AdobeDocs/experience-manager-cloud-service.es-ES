---
title: Administrar colecciones en Content Hub
description: Obtenga información sobre cómo administrar colecciones en Content Hub
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 9%

---

# Administrar colecciones en [!DNL Content Hub] {#manage-collections}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

<!-- ![Manage collections](assets/manage-collections.jpg) -->
![Administrar colecciones](assets/manage-collection.png)

>[!AVAILABILITY]
>
>La guía del centro de contenido ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía del centro de contenido en PDF]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Una colección hace referencia a un conjunto de recursos que se pueden compartir entre los usuarios. Una colección puede incluir recursos de diferentes ubicaciones manteniendo al mismo tiempo su integridad referencial.

[!DNL Content Hub] le permite crear colecciones públicas. Estas colecciones son accesibles para todos los usuarios con derecho a ellas, lo que crea un espacio compartido en el que varios usuarios pueden acceder y utilizar el contenido de forma eficaz. Las colecciones promueven el uso colaborativo de los recursos para aumentar la eficiencia y la comodidad. En la página de exploración de la colección, puede:

* **Crear**: crea una o más colecciones.
* **Ver**: vea los recursos y sus propiedades.
* **Compartir**: comparte recursos como vínculo con otros usuarios.
* **Descargar**: Descargue los recursos.
* **Quitar**: quite recursos específicos de una colección.
* **Eliminar**: elimine toda la colección.

Ayuda a los usuarios a acceder y administrar fácilmente los diversos recursos disponibles en [!DNL Content Hub].

## Requisitos previos {#prerequisites}

[Usuarios de Content Hub](deploy-content-hub.md#onboard-content-hub-users) pueden realizar las acciones mencionadas en este artículo.

## Crear colecciones{#create-collections}

Puede elegir [crear una nueva colección](#create-new-collection) o [agregar recursos a una colección existente](#add-assets-to-existing-collection).

### Crear una nueva colección{#create-new-collection}

Seleccione los recursos que necesita agregar a una colección y haga clic en **[!UICONTROL Agregar a colección]**.

![Crear colección](assets/add-assets-collection.jpg)

Para crear una nueva colección, vaya a la ficha **[!UICONTROL Colecciones]** y haga clic en **[!UICONTROL Crear nueva colección]**. Escriba **[!UICONTROL Title]** y proporcione una **[!UICONTROL Descripción]** opcional para los recursos. Haga clic en **[!UICONTROL Crear]**.

### Agregar recursos a una colección existente{#add-assets-to-existing-collection}

Para agregar recursos a una colección existente, seleccione los recursos que debe agregar a la colección. Haga clic en **[!UICONTROL Agregar a la colección]**. Se le pedirá que seleccione la colección.

![Crear una nueva colección](assets/create-add-collection.jpg)

Elija la colección donde debe agregar el recurso. También puede buscar en la colección existente mediante la barra de búsqueda. <br>Seleccione las colecciones a las que debe agregar los recursos y haga clic en **[!UICONTROL Agregar a la colección]**.

## Ver colecciones{#view-collections}

Vaya a la pestaña **[!UICONTROL Colecciones]** y busque el nombre de la colección. Para ver la lista de recursos disponibles en una colección, haga clic en el nombre de la colección. También puede aplicar filtros dentro de una colección para reducir los resultados del recurso.

Haga clic en el recurso que debe ver dentro de una colección. [!DNL Content Hub] muestra la vista detallada del recurso. [Ver detalles del recurso](asset-properties-content-hub.md).

<!--
![Asset details](assets/view-collection.jpg)

* **A**: Details and metadata of the asset 
* **B**: Zoom In or Zoom Out the asset 
* **C**: Reset Zoom view 
* **D**: View the previous or next asset 
* **E**: Download the asset 
* **F**: Open the asset in Adobe Express 
* **G**: Hide the metadata of the asset 
* **H**: Share the asset as a link 
-->

## Descargar recursos disponibles en una colección{#download-assets-within-collection}

Para descargar los recursos disponibles en una colección, vaya a la ficha **[!UICONTROL Colecciones]**.\
Haga clic en el icono ![descargar](assets/download-icon.svg) de la tarjeta de colección.

![Ficha Colección](assets/download-collection.jpg)

Se descargan todos los recursos de la colección.

También puede abrir la colección para descargar los recursos individualmente. Haga clic en la colección que contiene los recursos que debe descargar. Seleccione los recursos y haga clic en **[!UICONTROL Descargar]**.

Obtenga información sobre cómo [descargar un recurso de [!DNL Content Hub]](download-assets-content-hub.md).

## Compartir recursos disponibles en una colección {#share-assets-available-within-collection}

También puede compartir los recursos disponibles en una colección. Vaya a la pestaña **[!UICONTROL Colecciones]**. Seleccione el icono ![compartir icono](assets/share.svg) en la tarjeta de colección. Se copia el vínculo compartido. Puede compartir el vínculo copiado con el destinatario. Más información sobre [compartir recursos en [!DNL Content Hub]](share-assets-content-hub.md).

## Editar detalles de una colección {#edit-details-of-collection}

Para editar **[!UICONTROL Título]** y **[!UICONTROL Descripción]** de una colección, haga clic en el nombre de la colección y luego en el icono ![icono de información](assets/info-icon.svg). Aparece la pantalla [!UICONTROL Detalles de colección] que le permite editar el **[!UICONTROL Título]** y la **[!UICONTROL Descripción]** de una colección. Haga clic en **[!UICONTROL Guardar cambios]** para confirmar las modificaciones.

![detalles de colección](assets/collection-details.png)

## Eliminación de recursos de una colección{#remove-assets-from-a-collection}

Puede quitar uno o varios recursos de una colección. Para quitar recursos de una colección, haga clic en la colección de la que debe quitarlos, selecciónelos y haga clic en **[!UICONTROL Quitar de la colección]**.

![Quitar colección](assets/remove-collection-new.jpg)

Se le pedirá que confirme la eliminación del recurso. Haga clic en **[!UICONTROL Quitar]**.\
Los recursos seleccionados se han eliminado correctamente de la colección.

## Eliminar una colección{#delete-collection}

Para eliminar una colección, vaya a la ficha **[!UICONTROL Colecciones]** y haga clic en la colección que debe eliminar. Haga clic en el icono ![quitar icono](assets/remove-icon.svg) para eliminar la colección.
