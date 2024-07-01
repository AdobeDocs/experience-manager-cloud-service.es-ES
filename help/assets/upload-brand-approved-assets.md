---
title: Cargar los recursos aprobados por la marca a [!DNL Content Hub]
description: Obtenga información sobre cómo cargar los recursos aprobados por la marca en Content Hub
role: User
source-git-commit: c85b4e1c828ed1fb7f4063f965fe116215ca0244
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Cargar recursos aprobados por la marca en Content Hub {#upload-brand-approved-assets-content-hub}

[Usuarios de Content Hub con derechos para añadir recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) Puede agregar recursos a Content Hub desde el sistema de archivos local o importarlos desde OneDrive o fuentes de datos de Dropbox. Todos los recursos se muestran en el nivel superior en Content Hub, independientemente de la estructura de carpetas disponible en el sistema de archivos local o en OneDrive y las fuentes de datos de Dropbox, para mejorar las funciones de búsqueda.

Para mejorar aún más la búsqueda de recursos, Content Hub le permite:

* Defina los detalles clave relevantes para la carga de recursos, como el nombre de la campaña, las palabras clave, los canales, etc.

* Genere automáticamente más propiedades para cada recurso tras la carga correcta, como tamaño de archivo, formato, resolución y algunas otras propiedades.

* Utilice la inteligencia artificial proporcionada por [Adobe Sensei](https://www.adobe.com/es/sensei.html) para aplicar automáticamente las etiquetas relevantes a todos los recursos cargados. Estas etiquetas, que reciben el adecuado nombre de Etiquetas inteligentes, aumentan la velocidad del contenido de los proyectos al ayudarle a encontrar recursos relevantes con rapidez.

Asegúrese de cargar únicamente los [recursos aprobados por la marca para Content Hub](/help/assets/approve-assets.md).

![Cargar recursos aprobados por la marca](assets/upload-brand-approved-assets.png)

## Requisitos previos {#prerequisites-add-assets}

[Usuarios de Content Hub con derechos para añadir recursos](/help/assets/deploy-content-hub.md#onboard-content-hub-users-add-assets) Puede cargar recursos en Content Hub.

## Agregar recursos a Content Hub desde el sistema de archivos local {#add-assets-local-file-system}

Para agregar recursos a Content Hub, realice los siguientes pasos:

1. Clic **[!UICONTROL Añadir Assets]** para ver la **[!UICONTROL Añadir los recursos aprobados]** que le permite crear una carga.

1. En el **[!UICONTROL Arrastre archivos o carpetas aquí]** disponible en el panel derecho, puede arrastrar los recursos desde el sistema de archivos local o hacer clic en **[!UICONTROL Examinar]** para seleccionar manualmente archivos o carpetas disponibles en el sistema de archivos local. Esta lista de archivos que forman parte de la carga están disponibles como una lista.


   También puede obtener una vista previa de las imágenes seleccionadas mediante las miniaturas y hacer clic en el icono X para eliminar cualquier imagen concreta de la lista. El icono X solo se muestra cuando pasa el ratón sobre el nombre o el tamaño de la imagen. También puede hacer clic en **[!UICONTROL Eliminar todo]** para eliminar todos los elementos de la lista de carga.

   Para finalizar el proceso de carga y activar la **[!UICONTROL Botón Cargar]**, debe agrupar los recursos con un nombre de campaña.

   ![Carga de recursos en Content Hub](assets/upload-assets-content-hub.png)

1. Defina el nombre de la carga mediante la variable **[!UICONTROL Nombre de campaña]** field. Puede utilizar un nombre existente o crear uno nuevo. Content Hub proporciona más opciones a medida que escribe el nombre. <!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

1. Del mismo modo, defina los valores de **[!UICONTROL Palabras clave]**, **[!UICONTROL Canales]**, **[!UICONTROL Periodo de tiempo]**, y **[!UICONTROL Región]** campos. El etiquetado y la agrupación de recursos por palabras clave, canales y ubicación permite a todas las personas que utilicen el contenido aprobado de la empresa encontrar estos recursos y mantenerlos organizados.

1. Clic **[!UICONTROL Cargar]** para cargar recursos en Content Hub. [!UICONTROL Revisar detalles] Aparecerá el cuadro de confirmación. Haga clic en [!UICONTROL Continuar].

1. Assets iniciar carga. Clic [!UICONTROL Nueva carga] para reiniciar el procedimiento de carga. Clic [!UICONTROL Listo] para completar la carga.

Los administradores también pueden configurar los campos obligatorios y opcionales que se muestran al cargar recursos, como Nombre de campaña, Palabras clave, Canales, etc. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).


## Agregar recursos a Content Hub desde OneDrive o fuentes de datos de Dropbox {#add-assets-onedrive-dropbox}

Para agregar recursos a Content Hub desde fuentes de datos de OneDrive o Dropbox:

1. Clic **[!UICONTROL Añadir Assets]** para ver la **[!UICONTROL Añadir los recursos aprobados]** que permite importar recursos desde OneDrive o Dropbox.

1. Clic **[!UICONTROL OneDrive]** o **[!UICONTROL Dropbox]** para iniciar el proceso de importación. Content Hub le pide que inicie sesión en su cuenta de OneDrive o de Dropbox y, a continuación, muestra la estructura de carpetas de OneDrive o de Dropbox en el panel izquierdo.

1. Haga clic en el icono + situado junto al nombre del archivo o de la carpeta para ver el elemento en la lista Elementos seleccionados. Después de seleccionar todos los archivos que debe agregar al portal de Content Hub, repita los pasos del 3 al 6 de [Añadir recursos a Content Hub desde el sistema de archivos local](#add-assets-local-file-system) para completar el proceso de carga.

   ![Cargar recursos a Content Hub desde OneDrive o Dropbox](assets/add-assets-onedrive-dropbox.png)

Los administradores también pueden configurar los campos obligatorios y opcionales que se muestran al cargar recursos, como Nombre de campaña, Palabras clave, Canales, etc. Para obtener más información, consulte [Configuración de la interfaz de usuario de Content Hub](configure-content-hub-ui-options.md#configure-upload-options-content-hub).

