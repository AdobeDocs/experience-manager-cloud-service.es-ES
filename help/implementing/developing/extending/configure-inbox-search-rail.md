---
title: ¿Cómo configurar los filtros de búsqueda para la bandeja de entrada?
description: Obtenga información sobre cómo configurar filtros de búsqueda para elementos de la Bandeja de entrada.
source-git-commit: ee32ab3659ee4696caa55b945b6b7895d94914a9
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# Configurar filtros de búsqueda para la bandeja de entrada {#configure-search-filters-inbox}

Puede configurar filtros de búsqueda para elementos de la Bandeja de entrada. Base los criterios de búsqueda en una columna Bandeja de entrada específica para filtrar los resultados.

Por ejemplo, para filtrar los elementos de la Bandeja de entrada en función de un intervalo de columnas de la Bandeja de entrada de fecha de nacimiento, puede utilizar el predicado Intervalo de fechas para definir el intervalo de fechas.

Los siguientes son los tipos de predicados disponibles para la Bandeja de entrada:

* Predicado de intervalo

* Predicado de texto

* Predicado de intervalo de fechas

* Predicado de propiedad de opciones

>[!NOTE]
>
>Asegúrese de que es miembro del grupo `workflow-administrators` para configurar los filtros de búsqueda de la Bandeja de entrada.

## Crear o abrir una configuración personalizada {#creating-opening-customized-configuration}

1. Vaya a **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Seleccione la configuración **[!UICONTROL Inbox Search Rail]** y pulse **[!UICONTROL Editar]**.
1. Incorpore los cambios de configuración de predicado utilizando **[!UICONTROL Editar búsqueda Forms]**.
1. Seleccione **[!UICONTROL Listo]** para guardar la configuración.

## Eliminar una configuración personalizada {#delete-customized-configuration}

Para eliminar una configuración personalizada:

1. Vaya a **[!UICONTROL Tools]**, **[!UICONTROL General]**, **[!UICONTROL Search Forms]**.

1. Seleccione la configuración **[!UICONTROL Inbox Search Rail]** y pulse **[!UICONTROL Delete]**.

## Configurar predicado de rango {#range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de números dentro de una columna Bandeja de entrada mediante el predicado Intervalo. También puede optar por incluir valores decimales para los números.

Para configurar un predicado de rango:

1. Abra el formulario [de configuración](#creating-opening-customized-configuration).
1. Pulse la pestaña **[!UICONTROL Select Predicate]** y arrastre **[!UICONTROL Range Predicate]** al formulario.
1. En la pestaña **[!UICONTROL Settings]**, seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, en el campo **[!UICONTROL Column Name]**.
1. Especifique la etiqueta para el filtro en el campo **[!UICONTROL Filter Label]**. Active la casilla **[!UICONTROL Enable Decimal Values]** para aceptar valores decimales para números mientras define el intervalo.
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta con una opción para definir los valores máximo y mínimo. Al pulsar la tecla Intro, [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

>[!NOTE]
>
>El artículo enumera las últimas opciones de la interfaz de usuario. Los nombres de las opciones se actualizarán en la interfaz de usuario en la próxima versión.

## Configurar predicado de texto {#text-predicate}

Filtre los elementos de la bandeja de entrada para buscar una cadena de texto dentro de una columna Bandeja de entrada mediante el predicado de texto.

Para configurar un predicado de texto:

1. Abra el formulario [de configuración](#creating-opening-customized-configuration).
1. Pulse la pestaña **[!UICONTROL Select Predicate]** y arrastre **[!UICONTROL Text Predicate]** al formulario.
1. En la pestaña **[!UICONTROL Settings]**, seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, en el campo **[!UICONTROL Column Name]**.
1. Especifique el texto que aparece en el cuadro de texto Buscar como texto de marcador de posición en el campo **[!UICONTROL Marcador de posición de cuadro de texto de búsqueda]**.
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros . Al pulsar la tecla Intro, [!DNL Experience Manager] aplica el texto de búsqueda especificado en el paso 4 del nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

## Configurar predicado de intervalo de fechas {#date-range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de fechas dentro de una columna Bandeja de entrada mediante el predicado Intervalo de fechas.

Para configurar un predicado de intervalo de fechas:

1. Abra el formulario [de configuración](#creating-opening-customized-configuration).
1. Pulse la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de intervalo de fechas]** al formulario.
1. En la pestaña **[!UICONTROL Settings]**, seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, en el campo **[!UICONTROL Column Name]**.
1. Especifique la etiqueta para el filtro de intervalo de fechas en el campo **[!UICONTROL Etiqueta de filtro]**.
1. Especifique las etiquetas de fecha de inicio y fecha de finalización para el filtro.
1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta para el filtro de intervalo de fechas junto con las etiquetas de fecha de inicio y fecha de finalización especificadas en el paso 5. [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

## Configurar el predicado de opciones de columna personalizadas {#custom-column-options-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar una opción personalizada dentro de una columna Bandeja de entrada mediante el predicado Opciones de columna personalizadas .

Para configurar un predicado de opciones de columna personalizadas:

1. Abra el formulario [de configuración](#creating-opening-customized-configuration).
1. Pulse la pestaña **[!UICONTROL Seleccionar predicado]** y arrastre **[!UICONTROL Predicado de opciones de columna personalizadas]** al formulario.
1. En la pestaña **[!UICONTROL Settings]**, seleccione el nombre de la columna Bandeja de entrada en la que desea basar la búsqueda, en el campo **[!UICONTROL Column Name]**.
1. Especifique la etiqueta para el filtro de opciones de columna personalizada en el campo **[!UICONTROL Etiqueta de filtro]**.
1. Active la casilla **[!UICONTROL Selección única]** para activar la selección de una sola opción al aplicar el filtro en una columna Bandeja de entrada.
1. En la sección **[!UICONTROL Agregar opciones]**:
   1. Seleccione **[!UICONTROL Manual]** para definir las opciones de búsqueda de filtro manualmente. Toque **[!UICONTROL Agregar opciones de filtro]** para definir la primera opción. Especifique la etiqueta de la opción de columna y el texto del valor de opción que desea buscar. Por ejemplo, si desea buscar **Mujer** como valor en una columna Bandeja de entrada, puede especificar **F** como etiqueta para la opción de columna y agregar **Mujer** como texto de valor de opción. Del mismo modo, puede agregar más opciones de filtro.
   1. Seleccione **[!UICONTROL JSON Path]** para definir las opciones mediante una ruta de archivo JSON. El siguiente es un archivo JSON de muestra para definir las opciones de filtro:

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

   1. Seleccione **[!UICONTROL CRX Options Path]** para definir opciones usando las rutas del repositorio CRX. Toque **[!UICONTROL Agregar rutas de opción]** para agregar varias rutas. A continuación se muestra un ejemplo para definir las opciones de filtro `Male` y `Female`:

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

1. Especifique una descripción opcional para la configuración y pulse **[!UICONTROL Listo]** para guardarla.

Los cambios de configuración se reflejan al abrir la página Filtros . La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta del predicado de opciones de columna personalizadas. [!DNL Experience Manager] aplica los criterios de búsqueda definidos en el paso 6 en el nombre de columna especificado en el paso 3 y devuelve los elementos Bandeja de entrada.

El siguiente vídeo ilustra los pasos para filtrar una columna en función de los valores de opción `true` y `false`.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Ver filtros de búsqueda basados en predicados {#view-search-filters-for-predicates}

Puede ver filtros de búsqueda basados en predicados. Seleccione **[!UICONTROL Filter]** en la página Bandeja de entrada. Los filtros se muestran en el panel izquierdo. A continuación, puede especificar los criterios de búsqueda para filtrar los elementos de la Bandeja de entrada.

![Página Filtros](assets/apply-filters.png)

Para obtener más información sobre la administración de configuraciones de predicado, consulte [Configuración de la búsqueda en Forms](search-forms.md).


