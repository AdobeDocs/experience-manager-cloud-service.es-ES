---
title: ¿Cómo configurar los filtros de búsqueda para la bandeja de entrada?
description: Obtenga información sobre cómo configurar filtros de búsqueda para elementos de la Bandeja de entrada.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# Configuración de filtros de búsqueda para la bandeja de entrada {#configure-search-filters-inbox}

Puede configurar filtros de búsqueda para elementos de la Bandeja de entrada. Base los criterios de búsqueda en una columna Bandeja de entrada específica para filtrar los resultados.

Por ejemplo, para filtrar los elementos de la Bandeja de entrada en función de un intervalo de columnas de la Bandeja de entrada de fecha de nacimiento, puede utilizar el predicado Intervalo de fechas para definir el intervalo de fechas.

Los siguientes son los tipos de predicados disponibles para la Bandeja de entrada:

* Predicado de intervalo

* Predicado de texto

* Predicado de intervalo de fechas

* Predicado de propiedad de opciones

>[!NOTE]
>
>Asegúrese de que es miembro de la función `workflow-administrators` para configurar los filtros de búsqueda de la Bandeja de entrada.

## Crear o abrir una configuración personalizada {#creating-opening-customized-configuration}

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar en Forms]**.

1. Seleccione el **[!UICONTROL Carril de búsqueda de la bandeja de entrada]** configuración y toque **[!UICONTROL Editar]**.
1. Incorporar los cambios de configuración de predicado mediante **[!UICONTROL Editar Forms de búsqueda]**.
1. Select **[!UICONTROL Listo]** para guardar la configuración.

## Eliminar una configuración personalizada {#delete-customized-configuration}

Para eliminar una configuración personalizada:

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar en Forms]**.

1. Seleccione el **[!UICONTROL Carril de búsqueda de la bandeja de entrada]** configuración y toque **[!UICONTROL Eliminar]**.

## Configurar predicado de rango {#range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de números dentro de una columna Bandeja de entrada mediante el predicado Intervalo. También puede optar por incluir valores decimales para los números.

Para configurar un predicado de rango:

1. Abra el [formulario de configuración](#creating-opening-customized-configuration).
1. Toque . **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de rango]** al formulario.
1. En el **[!UICONTROL Configuración]** , seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, desde **[!UICONTROL Nombre de columna]** campo .
1. Especifique la etiqueta para el filtro en la variable **[!UICONTROL Etiqueta de filtro]** campo . Seleccione el **[!UICONTROL Habilitar valores decimales]** casilla de verificación para aceptar valores decimales de números al definir el intervalo.
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta con una opción para definir los valores máximo y mínimo. Al pulsar la tecla Intro, [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

>[!NOTE]
>
>El artículo enumera las últimas opciones de la interfaz de usuario. Los nombres de las opciones se actualizarán en la interfaz de usuario en la próxima versión.

## Configurar predicado de texto {#text-predicate}

Filtre los elementos de la bandeja de entrada para buscar una cadena de texto dentro de una columna Bandeja de entrada mediante el predicado de texto.

Para configurar un predicado de texto:

1. Abra el [formulario de configuración](#creating-opening-customized-configuration).
1. Toque . **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de texto]** al formulario.
1. En el **[!UICONTROL Configuración]** , seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, desde **[!UICONTROL Nombre de columna]** campo .
1. Especifique el texto que aparece en el cuadro de texto Buscar como texto de marcador de posición en la variable **[!UICONTROL Marcador de posición de cuadro de texto de búsqueda]** campo .
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros . Al pulsar la tecla Intro, [!DNL Experience Manager] aplica el texto de búsqueda especificado en el paso 4 al nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

## Configurar predicado de intervalo de fechas {#date-range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de fechas dentro de una columna Bandeja de entrada mediante el predicado Intervalo de fechas.

Para configurar un predicado de intervalo de fechas:

1. Abra el [formulario de configuración](#creating-opening-customized-configuration).
1. Toque . **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de intervalo de fechas]** al formulario.
1. En el **[!UICONTROL Configuración]** , seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, desde **[!UICONTROL Nombre de columna]** campo .
1. Especifique la etiqueta para el filtro de intervalo de fechas en la variable **[!UICONTROL Etiqueta de filtro]** campo .
1. Especifique las etiquetas de fecha de inicio y fecha de finalización para el filtro.
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta para el filtro de intervalo de fechas junto con las etiquetas de fecha de inicio y fecha de finalización especificadas en el paso 5. [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

## Configurar el predicado de opciones de columna personalizadas {#custom-column-options-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar una opción personalizada dentro de una columna Bandeja de entrada mediante el predicado Opciones de columna personalizadas .

Para configurar un predicado de opciones de columna personalizadas:

1. Abra el [formulario de configuración](#creating-opening-customized-configuration).
1. Toque . **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de opciones de columna personalizadas]** al formulario.
1. En el **[!UICONTROL Configuración]** , seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, desde **[!UICONTROL Nombre de columna]** campo .
1. Especifique la etiqueta para el filtro de opciones de columna personalizada en la variable **[!UICONTROL Etiqueta de filtro]** campo .
1. Seleccione el **[!UICONTROL Selección única]** para activar la selección de una sola opción al aplicar el filtro en una columna Bandeja de entrada.
1. En el **[!UICONTROL Agregar opciones]** sección:
   1. Select **[!UICONTROL Manual]** para definir manualmente las opciones de búsqueda de filtro. Toque **[!UICONTROL Agregar opciones de filtro]** para definir la primera opción. Especifique la etiqueta de la opción de columna y el texto del valor de opción que desea buscar. Por ejemplo, si desea buscar **Mujer** como valor de una columna Bandeja de entrada, puede especificar **F** como etiqueta para la opción de columna y agregue **Mujer** como texto de valor de opción. Del mismo modo, puede agregar más opciones de filtro.
   1. Select **[!UICONTROL Ruta de JSON]** para definir opciones utilizando una ruta de archivo JSON. El siguiente es un archivo JSON de muestra para definir las opciones de filtro:

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. Select **[!UICONTROL Ruta de opciones de CRX]** para definir opciones utilizando las rutas del repositorio CRX. Toque **[!UICONTROL Agregar rutas de opciones]** para agregar varias rutas. A continuación se muestra un ejemplo para definir `Male` y `Female` opciones de filtro:

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta del predicado de opciones de columna personalizadas. [!DNL Experience Manager] aplica los criterios de búsqueda definidos en el paso 6 en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

El siguiente vídeo ilustra los pasos para filtrar una columna en función de la variable `true` y `false` valores de opción.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Ver filtros de búsqueda basados en predicados {#view-search-filters-for-predicates}

Puede ver filtros de búsqueda basados en predicados. Select **[!UICONTROL Filtro]** en la página Bandeja de entrada. Los filtros se muestran en el panel izquierdo. A continuación, puede especificar los criterios de búsqueda para filtrar los elementos de la Bandeja de entrada.

![Página Filtros](assets/apply-filters.png)

Para obtener más información sobre la administración de configuraciones de predicado, consulte [Configuración de Search Forms](search-forms.md).
