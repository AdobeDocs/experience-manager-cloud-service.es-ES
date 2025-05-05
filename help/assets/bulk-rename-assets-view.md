---
title: Cambiar nombre y cambiar el nombre de los recursos en bloque en  [!DNL Assets view]
description: Obtenga información sobre cómo cambiar el nombre de los recursos de forma masiva mediante la nueva interfaz de usuario de Assets (vista Assets). Permite cambiar el nombre de varios recursos a la vez.
role: User
exl-id: e041811b-0246-408f-9246-248da55f66a1
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 17%

---

# Cambiar nombre de recurso o carpeta en [!DNL Assets view] {#rename-single-asset-or-folder}

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

Cambiar el nombre puede ayudar a organizar, clasificar e identificar los recursos mejor sin alterar su contenido o ubicación. [!DNL Assets view] le permite cambiar el nombre del recurso o la carpeta seleccionados.

Siga estos pasos para cambiar el nombre de un recurso o una carpeta:

1. Busque el recurso o la carpeta cuyo nombre desea cambiar.

1. Utilice una de las siguientes formas de cambiar el nombre de un recurso o una carpeta:

   * Seleccione el recurso o la carpeta y haga clic en ![cambiar nombre del icono](assets/do-not-localize/rename-icon.png) **[!UICONTROL Cambiar nombre]** en el menú superior.
   * Haga clic en más opciones `...` del recurso o la carpeta y seleccione **[!UICONTROL Cambiar nombre]**.
   * Haga clic en el título de un recurso o en una carpeta para cambiarle el nombre. Mencione el nuevo texto en el cuadro de texto **Cambiar nombre de recurso** y haga clic en **Guardar**. Esta funcionalidad está disponible en las vistas Cuadrícula, Galería, Cascada y Lista.

## Nombre masivo de recursos con tecnología de IA {#rename-bulk-assets-using-ai}

[!DNL Assets view] le permite cambiar el nombre de varios recursos a la vez mediante IA. La funcionalidad de cambio de nombre masivo de IA solo se puede aplicar a archivos, no a carpetas. Puede seleccionar varios archivos a la vez y cambiarles el nombre.

Siga los pasos a continuación para cambiar el nombre de la mayor parte de los recursos a la vez mediante mensajes generados por IA:

1. Seleccione varios recursos y haga clic en **[!UICONTROL Cambiar nombre en lotes]** en el menú superior.

1. Añada el mensaje que describe cómo desea cambiar el nombre de los recursos seleccionados. Consulte [algunos ejemplos que ilustran el cambio de nombre masivo de IA](#examples-ai-bulk-rename).

1. Haga clic en **[!UICONTROL Ejecutar]** para permitir que AI cambie el nombre de los recursos como se menciona en la solicitud.

1. [Opcional] Haga clic en ![deshacer icono](assets/do-not-localize/undo.svg) para revertir o cancelar la última acción que realizó.

1. Compruebe sus cambios en la columna [!UICONTROL Nueva vista previa de nombre] y haga clic en **[!UICONTROL Guardar]**.

   ![cambio de nombre masivo de IA](assets/ai-bulk-rename.png)

## Algunos ejemplos que ilustran el cambio masivo de nombre de IA {#examples-ai-bulk-rename}

A continuación se muestran algunos ejemplos de cómo utilizar IA para cambiar el nombre de los recursos de forma masiva en función de un mensaje de IA:

* El prefijo 00, 01, etc. y el sufijo con la fecha de hoy.
* Cambie todos los archivos a &#39;my-file&#39; y añada un número incremental.
* Elimine el prefijo y el sufijo, solo mantenga la parte central del nombre.
* Agregue a los archivos el prefijo 001, 002, etc. y traducirlo al inglés.

>[!VIDEO](https://video.tv.adobe.com/v/3440975)

>[!NOTE]
>
> * No puedes convertir emojis en texto.
> * Utilice un nombre único para evitar mensajes de advertencia al cambiar el nombre de los recursos. Aunque puede intentarlo de nuevo con un nombre nuevo.
> * También puede convertir caracteres Unicode o no alfanuméricos en texto.

## Siguientes pasos {#next-steps}

* [Vea un vídeo para administrar formularios de metadatos en la vista de Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/configuring/metadata-forms.html?lang=es)

* Realice comentarios del producto mediante la opción [!UICONTROL Comentarios] disponible en la interfaz de usuario de la vista Recursos

* Proporcione comentarios sobre la documentación usando [!UICONTROL Editar esta página] ![editar la página](assets/do-not-localize/edit-page.png) o [!UICONTROL Registrar una incidencia] ![crear una incidencia de GitHub](assets/do-not-localize/github-issue.png), disponibles en la barra lateral derecha

* Contacto con el [Servicio de atención al cliente](https://experienceleague.adobe.com/es?support-solution=General&amp;lang=es#support)
