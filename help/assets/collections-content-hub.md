---
title: Administrar colecciones en Content Hub
description: Obtenga información sobre cómo administrar colecciones en Content Hub
role: User
exl-id: ea74456c-f980-4a02-b26b-d7c46dac6aee
source-git-commit: 6bc838ff76edda3e03cbde8da4a28f65cba3b36a
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 10%

---

# Administrar colecciones en [!DNL Content Hub] {#manage-collections}

<table>

    <tr>

        <td>

            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>

        </td>

        <td>

            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>

        </td>

        <td>

            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>Integración de AEM Assets con Edge Delivery Services</b></a>

        </td>

        <td>

            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>New</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidad de la IU</b></a>

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

Puede elegir [crear una nueva colección](#create-new-collection) o [agregar recursos a una colección existente](#add-assets-to-existing-collection) mientras administra el control.

### Crear una nueva colección{#create-new-collection}

Siga estos pasos para controlar el acceso al crear colecciones:

1. Vaya a la ficha **[!DNL Collections]** y haga clic en **[!UICONTROL Crear colección]**. Aparecerá la ventana Nueva colección.

1. Agregue **[!UICONTROL Título]** y **[!UICONTROL Descripción]** para la colección.

   ![permisos de colección](assets/collection-permissions.png)

1. En **[!UICONTROL Quién puede acceder a]**, lista desplegable > seleccione el tipo de control de acceso. Las opciones disponibles son las siguientes:

   | Método de acceso | Tipo de acceso | Descripción |
   |---|---|---|
   | **Solo usted y los administradores pueden tener acceso a** | Privado | Solo el creador y los administradores pueden editar y acceder a esta colección. |
   | **Cualquier persona puede acceder a** | Público | Todos pueden acceder a esta colección, pero solo el creador y los administradores pueden editarla. |
   | **Cualquier persona puede acceder y editar** | Público | Esta colección está abierta a todos, con acceso completo y permisos de edición concedidos sin restricciones. |

1. Haga clic en **[!UICONTROL Crear]**. Una vez finalizado, puede [agregar recursos a la colección](#add-assets-to-existing-collection).

>[!VIDEO](https://video.tv.adobe.com/v/3463336)

>[!NOTE]
>
>La gobernanza de colecciones es una función de disponibilidad limitada. Puede habilitarlo creando un ticket de asistencia. Una vez que esté habilitado, tendrá que [configurar colecciones en Content Hub](configure-content-hub-ui-options.md#configure-collections-content-hub).

<!--To create a new collection, navigate to the **[!UICONTROL Collections]** tab and click **[!UICONTROL Create new collection]**. Enter the **[!UICONTROL Title]** and provide an optional **[!UICONTROL Description]** for the assets. Click **[!UICONTROL Create]**.
![Create collection](assets/add-assets-collection.jpg)          
-->

### Agregar recursos a una colección existente{#add-assets-to-existing-collection}

Para agregar recursos a una colección existente, seleccione los recursos que debe agregar a la colección. Haga clic en **[!UICONTROL Agregar a la colección]**. Se le pedirá que seleccione la colección.

![Crear una nueva colección](assets/create-add-collection.jpg)

Elija la colección donde debe agregar el recurso. También puede buscar en la colección existente mediante la barra de búsqueda. <br>Seleccione las colecciones a las que debe agregar los recursos y haga clic en **[!UICONTROL Agregar a la colección]**.

## Ver colecciones{#view-collections}

Vaya a la pestaña **[!UICONTROL Colecciones]** y busque el nombre de la colección. Puede utilizar filtros para restringir los resultados de búsqueda seleccionando criterios específicos, lo que le ayuda a encontrar rápidamente las colecciones más relevantes.

Para ver la lista de recursos disponibles en una colección, haga clic en el nombre de la colección. También puede aplicar filtros dentro de una colección para reducir los resultados del recurso. Haga clic en el recurso que debe ver dentro de una colección. [!DNL Content Hub] muestra la vista detallada del recurso. [Ver detalles del recurso](asset-properties-content-hub.md).

### Filtrar vista de colecciones {#filter-collections-view}

Content Hub le permite filtrar la vista de colecciones para encontrar fácilmente lo que está buscando, restringiendo las opciones en función de sus preferencias. Asegúrese de que [se hayan configurado las colecciones en Content Hub](configure-content-hub-ui-options.md#configure-collections-content-hub).

Para filtrar la vista de colecciones, vaya a la pestaña **[!DNL Collections]** y navegue hasta la lista desplegable Colecciones. Elija entre las siguientes opciones:

* **[!UICONTROL Todas las colecciones]:** Seleccione esta opción para ver todas las colecciones que son privadas y compartidas con usted.
* **[!UICONTROL Solo yo]:** Seleccione esta opción para ver las colecciones a las que tiene acceso.
* **[!UICONTROL Cualquier persona puede ver]:** Esta opción le permite filtrar colecciones que son accesibles para todos pero que solo el creador puede editar.
* **[!UICONTROL Cualquier persona puede editar]:** Seleccione esta opción para filtrar colecciones que sean accesibles y editables para todos.

  ![filtrar vista de colecciones](assets/filter-collection-view.png)

Además, para filtrar la vista de colecciones en función de los permisos de acceso, vaya a la pestaña **[!DNL Collections]** y desplácese a una de las siguientes opciones:

* **[!UICONTROL Creado por cualquier persona]:** Este filtro restringe la visualización de colecciones creadas por cualquier usuario.

* **[!UICONTROL Creado por mí]:** Este filtro te restringe a ver las colecciones que has creado.

  ![filtrar vista de colecciones](assets/filter-collection-view1.png)

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

![Ficha Colección](assets/download-collection.png)

Se descargan todos los recursos de la colección.

También puede abrir la colección para descargar los recursos individualmente. Haga clic en la colección que contiene los recursos que debe descargar. Seleccione los recursos y haga clic en **[!UICONTROL Descargar]**.

Obtenga información sobre cómo [descargar un recurso de [!DNL Content Hub]](download-assets-content-hub.md).

## Compartir recursos disponibles en una colección {#share-assets-available-within-collection}

También puede compartir los recursos disponibles en una colección. Asegúrese de [habilitar el uso compartido de vínculos públicos en Content Hub](configure-content-hub-ui-options.md#enable-public-link-sharing). Vaya a la pestaña **[!UICONTROL Colecciones]**. Seleccione el icono ![compartir icono](assets/share.svg) en la tarjeta de colección. Se copia el vínculo compartido. Puede compartir el vínculo copiado con el destinatario. Más información sobre [compartir recursos en [!DNL Content Hub]](share-assets-content-hub.md).

Al compartir colecciones en Content Hub, puede definir el ámbito de acceso y las acciones que los destinatarios pueden realizar en los recursos digitales dentro del sistema. Content Hub Collections proporciona herramientas de gobernanza completas para una administración eficaz de los recursos, incluidos permisos de uso compartido personalizables y funciones de colaboración. Desde el acceso de solo lectura hasta el control administrativo completo, esta configuración admite la buena gobernanza en la distribución de recursos.

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



