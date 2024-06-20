---
title: Cargar opciones de lista desplegable desde una dirección URL u otra hoja para Edge Delivery Services para AEM Forms as a Cloud Service
description: Las opciones de la lista desplegable se incluyen en una hoja de cálculo distinta y luego se importan a la hoja de cálculo principal a través de la dirección URL proporcionada.
feature: Edge Delivery Services
exl-id: 5b0bc1b6-6e33-41f3-b7c1-4d997787b6cd
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 100%

---


# Opciones de una dirección URL u otra hoja para Edge Delivery Services para AEM Forms as a Cloud Service

Los formularios suelen incluir menús desplegables para que los usuarios seleccionen entre las opciones predefinidas. Estas opciones suelen definirse dentro del propio formulario, pero la administración de listas largas puede resultar engorrosa. En esta se guía se describe cómo mejorar la creación de formularios cargando opciones desplegables de una hoja de cálculo independiente a través de una dirección URL.


Las ventajas de cargar una lista desplegable desde una hoja de cálculo independiente son las siguientes:

* Administración simplificada: mantenga las opciones desplegables en una ubicación centralizada para facilitar las actualizaciones y adiciones.
* Mayor eficiencia: elimine la necesidad de añadir manualmente listas de opciones largas dentro de la definición del formulario.




![Opciones desplegables](/help/forms/assets/drop-down-options.png)


Al final de este artículo, aprenderá lo siguiente:

* [Definir opciones en una hoja de cálculo independiente](#define-options)
* [Añadir URL para cargar las opciones de la lista desplegable](#add-url)

## Definir opciones en una hoja independiente {#define-options}

Definición de opciones en una hoja de cálculo independiente

1. Crear una hoja de cálculo:
   1. Localice la carpeta del proyecto de AEM en Microsoft® SharePoint o Google Drive.
   1. Añada una nueva hoja. Por ejemplo, &quot;shared-country&quot;.
1. Definir columnas de opciones: 
Añada dos columnas: &quot;Opción&quot; y &quot;Valor&quot;.
   * &quot;Opción&quot; define el texto que se muestra en el menú desplegable.
   * &quot;Valor&quot; define el valor enviado cuando un usuario selecciona la opción.

   >[!NOTE]
   >
   >Si tanto la opción como el valor son idénticos, solo se requiere la columna &quot;Opción&quot;.

1. Rellenar la hoja de cálculo: 
Introduzca las opciones de país en la columna &quot;Opción&quot; (y la columna &quot;Valor&quot; si es necesario).

   Consulte el siguiente ejemplo para ver la estructura.

   ![Lista desplegable para el país](/help/forms/assets/drop-down-country-options.png)

1. Previsualice y publique la hoja `shared-country` usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   Consulte la URL que muestra la hoja `shared-country`: 
https://main--wefinance--wkndforms.hlx.live/enquiry.json?sheet=country

>[!NOTE]
>
> `?sheet=country` es un parámetro de consulta anexado a la dirección URL. Este parámetro indica el JSON filtrado en función de la hoja `shared-country`. Redirige al archivo JSON que contiene información relacionada con diferentes países.

## Añadir URL para cargar las opciones de la lista desplegable{#add-url}

La propiedad `Options` de un campo `select` acepta una URL. La URL devuelve una matriz JSON utilizada como opciones para la lista desplegable `Destination`. Para añadir la dirección URL para cargar las opciones de la lista desplegable:

1. Vaya a la carpeta del proyecto AEM en Microsoft® SharePoint o Google Drive y abra la hoja de cálculo. También puede crear una nueva hoja de cálculo para un formulario.
1. Copie la dirección URL de `shared-country` y péguela en la columna `Options` del campo `Destination`.

   ![Hoja de cálculo de consulta](/help/forms/assets/drop-down-enquiry.png)

1. Previsualice y publique la hoja usando [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).


   ![Lista desplegable para el país](/help/forms/assets/load-dropdown-options-form.png)

Puede consultar la [hoja de cálculo de consulta](/help/forms/assets/enquiry-options.xlsx) para añadir la URL para cargar las opciones de la lista desplegable.

Después de integrar la dirección URL en la definición de formulario para cargar las opciones de la lista desplegable, las opciones de la lista desplegable `Destination` empiezan a aparecer desde la URL.

Consulte la siguiente dirección URL, que muestra el formulario `enquiry` que muestra las opciones guardadas en la hoja independiente:

https://main--wefinance--wkndforms.hlx.live/enquiry-form

## Consulte también

{{see-more-forms-eds}}


