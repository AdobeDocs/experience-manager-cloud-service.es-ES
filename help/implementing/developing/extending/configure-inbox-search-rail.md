---
title: ¿Cómo configurar los filtros de búsqueda para la bandeja de entrada?
description: Obtenga información sobre cómo configurar filtros de búsqueda para elementos de la bandeja de entrada.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Configuración de filtros de búsqueda para la bandeja de entrada {#configure-search-filters-inbox}

Puede configurar filtros de búsqueda para los elementos de la bandeja de entrada. Base los criterios de búsqueda en una columna de bandeja de entrada específica para filtrar los resultados.

Por ejemplo, para filtrar los elementos de la Bandeja de entrada en función de un intervalo de columnas de la Bandeja de entrada Fecha de nacimiento, puede utilizar el predicado Intervalo de fechas para definir el intervalo de fechas.

Los siguientes son los tipos de predicado disponibles para la bandeja de entrada:

* Predicado de intervalo

* Predicado de texto

* Predicado de intervalo de fechas

* Predicado de propiedad de opciones

>[!NOTE]
>
>Asegúrese de que es miembro del grupo `workflow-administrators` para configurar los filtros de búsqueda de la Bandeja de entrada.

## Crear o abrir una configuración personalizada {#creating-opening-customized-configuration}

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar en Forms]**.

1. Seleccione la configuración **[!UICONTROL Carril de búsqueda en la bandeja de entrada]** y seleccione **[!UICONTROL Editar]**.
1. Incorpore los cambios de configuración de predicado mediante **[!UICONTROL Editar búsqueda en Forms]**.
1. Seleccione **[!UICONTROL Listo]** para guardar la configuración.

## Eliminar una configuración personalizada {#delete-customized-configuration}

Para eliminar una configuración personalizada:

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar en Forms]**.

1. Seleccione la configuración **[!UICONTROL Carril de búsqueda en la bandeja de entrada]** y seleccione **[!UICONTROL Eliminar]**.

## Configurar predicado de intervalo {#range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un rango de números dentro de una columna de la bandeja de entrada mediante el predicado de rango. También puede incluir valores decimales para números.

Para configurar un predicado de rango:

1. Abra el [formulario para la configuración](#creating-opening-customized-configuration).
1. Seleccione la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de rango]** al formulario.
1. En la ficha **[!UICONTROL Configuración]**, seleccione el nombre de columna de la Bandeja de entrada en la que basar la búsqueda, en el campo **[!UICONTROL Nombre de columna]**.
1. Especifique la etiqueta para el filtro en el campo **[!UICONTROL Etiqueta de filtro]**. Seleccione la casilla de verificación **[!UICONTROL Habilitar valores decimales]** para aceptar valores decimales para números al definir el intervalo.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta con una opción para definir los valores máximo y mínimo. Cuando presiona la tecla Intro, [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

>[!NOTE]
>
>El artículo enumera las últimas opciones de interfaz de usuario de. Los nombres de las opciones se actualizarán en la interfaz de usuario en la próxima versión.

## Configurar predicado de texto {#text-predicate}

Filtre los elementos de la Bandeja de entrada para buscar una cadena de texto dentro de una columna Bandeja de entrada utilizando el Predicado Texto.

Para configurar un predicado de texto:

1. Abra el [formulario para la configuración](#creating-opening-customized-configuration).
1. Seleccione la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de texto]** al formulario.
1. En la ficha **[!UICONTROL Configuración]**, seleccione el nombre de columna de la Bandeja de entrada en la que basar la búsqueda, en el campo **[!UICONTROL Nombre de columna]**.
1. Especifique el texto que se muestra en el cuadro de texto Buscar como texto de marcador de posición en el campo **[!UICONTROL Marcador de posición de cuadro de texto de búsqueda]**.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros. Cuando presiona la tecla Intro, [!DNL Experience Manager] aplica el texto de búsqueda especificado en el paso 4 en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

## Configurar predicado de intervalo de fechas {#date-range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de fechas dentro de una columna de la bandeja de entrada mediante el predicado de intervalo de fechas.

Para configurar un predicado de intervalo de fechas:

1. Abra el [formulario para la configuración](#creating-opening-customized-configuration).
1. Seleccione la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de intervalo de fechas]** al formulario.
1. En la ficha **[!UICONTROL Configuración]**, seleccione el nombre de columna de la Bandeja de entrada en la que basar la búsqueda, en el campo **[!UICONTROL Nombre de columna]**.
1. Especifique la etiqueta para el filtro de intervalo de fechas en el campo **[!UICONTROL Etiqueta de filtro]**.
1. Especifique las etiquetas de fecha de inicio y fecha de finalización para el filtro.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta para el filtro de intervalo de fechas junto con las etiquetas de fecha de inicio y fecha de finalización especificadas en el paso 5. [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

## Configurar predicado de opciones de columna personalizadas {#custom-column-options-predicate}

Puede filtrar los elementos de la Bandeja de entrada para buscar una opción personalizada dentro de una columna Bandeja de entrada mediante el Predicado Opciones de columna personalizadas.

Para configurar un predicado de opciones de columna personalizado:

1. Abra el [formulario para la configuración](#creating-opening-customized-configuration).
1. Seleccione la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de opciones de columna personalizadas]** al formulario.
1. En la ficha **[!UICONTROL Configuración]**, seleccione el nombre de columna de la Bandeja de entrada en la que basar la búsqueda, en el campo **[!UICONTROL Nombre de columna]**.
1. Especifique la etiqueta para el filtro de opciones de columna personalizado en el campo **[!UICONTROL Etiqueta de filtro]**.
1. Seleccione la casilla de verificación **[!UICONTROL Selección única]** para habilitar la selección de una sola opción al aplicar el filtro en una columna de la Bandeja de entrada.
1. En la sección **[!UICONTROL Agregar opciones]**:
   1. Seleccione **[!UICONTROL Manual]** para definir las opciones de búsqueda de filtros manualmente. Seleccione **[!UICONTROL Agregar opciones de filtro]** para definir la primera opción. Especifique la etiqueta para la opción de columna y el texto del valor de opción que desea buscar. Por ejemplo, si desea buscar **Mujer** como valor en una columna de la Bandeja de entrada, puede especificar **F** como etiqueta para la opción de columna y agregar **Mujer** como texto del valor de la opción. Del mismo modo, puede agregar más opciones de filtro.
   1. Seleccione **[!UICONTROL Ruta de acceso JSON]** para definir las opciones mediante una ruta de acceso de archivo JSON. El siguiente es un archivo JSON de muestra para definir las opciones de filtro:

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

   1. Seleccione **[!UICONTROL Ruta de opciones de CRX]** para definir las opciones mediante las rutas del repositorio de CRX. Seleccione **[!UICONTROL Agregar rutas de opciones]** para agregar varias rutas. El siguiente es un ejemplo para definir las opciones de filtro `Male` y `Female`:

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

1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como etiqueta para el predicado de opción de columna personalizado. [!DNL Experience Manager] aplica los criterios de búsqueda definidos en el paso 6 en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

El siguiente vídeo ilustra los pasos para filtrar una columna en función de los valores de las opciones `true` y `false`.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Ver filtros de búsqueda basados en predicados {#view-search-filters-for-predicates}

Puede ver filtros de búsqueda basados en predicados. Seleccione **[!UICONTROL Filtro]** en la página Bandeja de entrada. Los filtros se muestran en el panel izquierdo. A continuación, puede especificar los criterios de búsqueda para filtrar los elementos de la Bandeja de entrada.

![Página de filtros](assets/apply-filters.png)

Para obtener más información sobre la administración de configuraciones de predicado, consulte [Configuración de la búsqueda en Forms](search-forms.md).
