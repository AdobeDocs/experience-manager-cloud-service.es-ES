---
title: Cargar opciones de lista desplegable desde URL
description: Las opciones de la lista desplegable se incluyen en una hoja de cálculo distinta y luego se importan en la hoja de cálculo principal a través de la dirección URL proporcionada.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---


# Cargar opciones de lista desplegable desde URL

En los formularios de Edge Delivery Services, los usuarios tienen la opción de seleccionar un valor de un conjunto predefinido de opciones. Los autores de formularios utilizan el `select` , que proporciona una lista de opciones.
Por ejemplo, la variable `enquiry` El formulario presenta un menú desplegable para seleccionar países, que ofrece a los usuarios una amplia gama de países predefinidos entre los que elegir. Puede ver que esta lista incluye una larga lista de países separados por comas.

![Opciones desplegables](/help/forms/assets/drop-down-options.png)

La administración de listas largas de opciones para menús desplegables puede resultar complicada al agregarlas directamente a la hoja que contiene la definición del formulario. La creación de una hoja independiente para almacenar estas opciones desplegables puede simplificar y optimizar el proceso. Esta hoja actúa como un repositorio centralizado para todas las opciones desplegables, organizadas en un formato estructurado. Cada opción se enumera en su propia fila, lo que facilita la administración y las actualizaciones.

Exploremos la mejora del proceso de creación de formularios cargando la lista de opciones de otra hoja de cálculo a través de una dirección URL.

Al final de este artículo, aprenderá lo siguiente:

* [Definir opciones en una hoja de cálculo independiente](#define-options)
* [Añadir URL para cargar las opciones de la lista desplegable](#add-url)

## Definir opciones en una hoja independiente {#define-options}

Cree una hoja con dos columnas:`Option` y `Value`, para definir las opciones:

1. AEM Vaya a la carpeta Proyecto de la carpeta en Microsoft® SharePoint o Google Drive.
2. Añada una hoja con el nombre `shared-country` en el sitio de Microsoft® SharePoint o en la carpeta Google Drive y agregue lo siguiente:

   * **Opción**: representa los valores de visualización de las opciones del menú desplegable.
   * **Valor**: representa el valor enviado cuando un usuario selecciona la opción.

   >[!NOTE]
   >
   > Si el valor y la opción de una opción desplegable son el mismo, la hoja de cálculo solo puede contener los siguientes elementos **Opción** columna.

   Vamos a añadir una nueva hoja, [país-compartido](/help/forms/assets/enquiry-options.xlsx) para las opciones mostradas en la `Destination` en la lista desplegable de `enquiry` formulario.

   Consulte la siguiente ilustración, que muestra el `shared-country` hoja de cálculo:

   ![Lista desplegable por país](/help/forms/assets/drop-down-country-options.png)
3. Previsualización y publicación de `shared-country` hoja que utiliza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Consulte la URL que muestra el `shared-country` hoja: https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` es un parámetro de consulta anexado a la dirección URL. Este parámetro indica el JSON filtrado en función de `shared-country` hoja. Redirige al archivo JSON que contiene información relacionada con diferentes países.

## Añadir URL para cargar las opciones de la lista desplegable{#add-url}

El `Options` propiedad de a `select` Este campo acepta una URL. La URL devuelve una matriz JSON utilizada como opciones para `Destination` lista desplegable. Para añadir la dirección URL para cargar las opciones de la lista desplegable:

1. AEM Vaya a la carpeta Proyecto de la en Microsoft® SharePoint o Google Drive y abra la hoja de cálculo. También puede crear una nueva hoja de cálculo para un formulario.
1. Copie la dirección URL de `shared-country` y péguelo en la hoja de cálculo de `Options` para la columna `Destination` field.

   ![Hoja de cálculo de consulta](/help/forms/assets/drop-down-enquiry.png)

1. Vista previa y publicación de la hoja mediante [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Lista desplegable por país](/help/forms/assets/load-dropdown-options-form.png)

Puede consultar el [hoja de cálculo](/help/forms/assets/enquiry-options.xlsx) para añadir las opciones de la lista desplegable URL para cargar.

Después de integrar la dirección URL en la definición del formulario para cargar las opciones de la lista desplegable, las opciones del `Destination` La lista desplegable de aparece desde la dirección URL.

Consulte la siguiente URL, que muestra la variable `enquiry` formulario que muestra las opciones guardadas en la hoja independiente:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Consulte también

{{see-more-forms-eds}}


