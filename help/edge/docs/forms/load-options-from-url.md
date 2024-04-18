---
title: Cargar opciones de lista desplegable desde URL
description: Las opciones de la lista desplegable se incluyen en una hoja de cálculo distinta y luego se importan en la hoja de cálculo principal a través de la dirección URL proporcionada.
feature: Edge Delivery Services
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---


# Cargar opciones de lista desplegable desde URL

Forms suele incluir menús desplegables para que los usuarios seleccionen entre las opciones predefinidas. Estas opciones suelen definirse dentro del propio formulario, pero la administración de listas largas puede resultar engorrosa. Esta guía describe cómo mejorar la creación de formularios cargando opciones desplegables de una hoja de cálculo independiente a través de una dirección URL.


Las ventajas de cargar una lista desplegable desde una hoja de cálculo independiente son las siguientes:

* Administración simplificada: mantenga las opciones desplegables en una ubicación centralizada para facilitar las actualizaciones y adiciones.
* Eficiencia mejorada: Elimine la necesidad de añadir manualmente listas de opciones largas dentro de la definición del formulario.




![Opciones desplegables](/help/forms/assets/drop-down-options.png)


Al final de este artículo, aprenderá lo siguiente:

* [Definir opciones en una hoja de cálculo independiente](#define-options)
* [Añadir URL para cargar las opciones de la lista desplegable](#add-url)

## Definir opciones en una hoja independiente {#define-options}

Definición de opciones en una hoja de cálculo independiente

1. Crear una hoja de cálculo:
   1. AEM Busque la carpeta del proyecto de la en Microsoft® SharePoint o Google Drive.
   1. Añada una hoja nueva. Por ejemplo, &quot;shared-country&quot;.
1. Definir columnas de opciones: añada dos columnas: &quot;Option&quot; y &quot;Value&quot;.
   * &quot;Opción&quot; define el texto que se muestra en el menú desplegable.
   * &quot;Valor&quot; define el valor enviado cuando un usuario selecciona la opción.

   >[!NOTE]
   >
   >Si tanto la opción como el valor son idénticos, solo se requiere la columna Opción.

1. Rellene la hoja de cálculo: introduzca las opciones de país en la columna &quot;Opción&quot; (y la columna &quot;Valor&quot; si es necesario).

   Consulte el ejemplo siguiente para ver la estructura.

   ![Lista desplegable por país](/help/forms/assets/drop-down-country-options.png)

1. Previsualización y publicación de `shared-country` hoja que utiliza [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

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


