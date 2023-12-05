---
title: ¿Cómo configurar los filtros de búsqueda para la bandeja de entrada?
description: Obtenga información sobre cómo configurar filtros de búsqueda para elementos de la bandeja de entrada.
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
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
>Asegúrese de que es miembro de `workflow-administrators` para configurar los filtros de búsqueda de la bandeja de entrada.

## Crear o abrir una configuración personalizada {#creating-opening-customized-configuration}

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar Forms]**.

1. Seleccione el **[!UICONTROL Carril de búsqueda de bandeja de entrada]** y seleccione **[!UICONTROL Editar]**.
1. Incorporar los cambios de configuración de predicado mediante **[!UICONTROL Editar Forms de búsqueda]**.
1. Seleccionar **[!UICONTROL Listo]** para guardar la configuración.

## Eliminar una configuración personalizada {#delete-customized-configuration}

Para eliminar una configuración personalizada:

1. Vaya a **[!UICONTROL Herramientas]**, **[!UICONTROL General]**, **[!UICONTROL Buscar Forms]**.

1. Seleccione el **[!UICONTROL Carril de búsqueda de bandeja de entrada]** y seleccione **[!UICONTROL Eliminar]**.

## Configurar predicado de intervalo {#range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un rango de números dentro de una columna de la bandeja de entrada mediante el predicado de rango. También puede incluir valores decimales para números.

Para configurar un predicado de rango:

1. Abra el [formulario para configuración](#creating-opening-customized-configuration).
1. Seleccione el **[!UICONTROL Seleccionar predicado]** tabulación y arrastre **[!UICONTROL Predicado de intervalo]** al formulario.
1. En el **[!UICONTROL Configuración]** pestaña, seleccione el nombre de la columna Bandeja de entrada en la que basar la búsqueda, desde **[!UICONTROL Nombre de columna]** field.
1. Especifique la etiqueta para el filtro en la **[!UICONTROL Etiqueta de filtro]** field. Seleccione el **[!UICONTROL Habilitar valores decimales]** casilla de verificación para aceptar valores decimales para números al definir el rango.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta con una opción para definir los valores máximo y mínimo. Cuando pulsa la tecla Intro, [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

>[!NOTE]
>
>El artículo enumera las últimas opciones de interfaz de usuario de. Los nombres de las opciones se actualizarán en la interfaz de usuario en la próxima versión.

## Configurar predicado de texto {#text-predicate}

Filtre los elementos de la Bandeja de entrada para buscar una cadena de texto dentro de una columna Bandeja de entrada utilizando el Predicado Texto.

Para configurar un predicado de texto:

1. Abra el [formulario para configuración](#creating-opening-customized-configuration).
1. Seleccione el **[!UICONTROL Seleccionar predicado]** tabulación y arrastre **[!UICONTROL Predicado de texto]** al formulario.
1. En el **[!UICONTROL Configuración]** pestaña, seleccione el nombre de la columna Bandeja de entrada en la que basar la búsqueda, desde **[!UICONTROL Nombre de columna]** field.
1. Especifique el texto que se muestra en el cuadro de texto Buscar como texto de marcador de posición en la **[!UICONTROL Buscar marcador de posición de cuadro de texto]** field.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros. Cuando pulsa la tecla Intro, [!DNL Experience Manager] aplica el texto de búsqueda especificado en el paso 4 al nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

## Configurar predicado de intervalo de fechas {#date-range-predicate}

Puede filtrar los elementos de la bandeja de entrada para buscar un intervalo de fechas dentro de una columna de la bandeja de entrada mediante el predicado de intervalo de fechas.

Para configurar un predicado de intervalo de fechas:

1. Abra el [formulario para configuración](#creating-opening-customized-configuration).
1. Seleccione el **[!UICONTROL Seleccionar predicado]** tabulación y arrastre **[!UICONTROL Predicado de intervalo de fechas]** al formulario.
1. En el **[!UICONTROL Configuración]** pestaña, seleccione el nombre de la columna Bandeja de entrada en la que basar la búsqueda, desde **[!UICONTROL Nombre de columna]** field.
1. Especifique la etiqueta para el filtro de intervalo de fechas en la variable **[!UICONTROL Etiqueta de filtro]** field.
1. Especifique las etiquetas de fecha de inicio y fecha de finalización para el filtro.
1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como la etiqueta para el filtro de intervalo de fechas junto con las etiquetas de fecha de inicio y fecha de finalización especificadas en el paso 5. [!DNL Experience Manager] aplica los criterios de búsqueda en el nombre de columna especificado en el paso 3 y devuelve los elementos de la Bandeja de entrada.

## Configurar predicado de opciones de columna personalizadas {#custom-column-options-predicate}

Puede filtrar los elementos de la Bandeja de entrada para buscar una opción personalizada dentro de una columna Bandeja de entrada mediante el Predicado Opciones de columna personalizadas.

Para configurar un predicado de opciones de columna personalizado:

1. Abra el [formulario para configuración](#creating-opening-customized-configuration).
1. Seleccione el **[!UICONTROL Seleccionar predicado]** tabulación y arrastre **[!UICONTROL Predicado de opciones de columna personalizadas]** al formulario.
1. En el **[!UICONTROL Configuración]** pestaña, seleccione el nombre de la columna Bandeja de entrada en la que basar la búsqueda, desde **[!UICONTROL Nombre de columna]** field.
1. Especifique la etiqueta para el filtro de opciones de columna personalizado en la **[!UICONTROL Etiqueta de filtro]** field.
1. Seleccione el **[!UICONTROL Selección única]** casilla de verificación para activar la selección de una sola opción al aplicar el filtro en una columna de bandeja de entrada.
1. En el **[!UICONTROL Agregar opciones]** sección:
   1. Seleccionar **[!UICONTROL Manual]** para definir las opciones de búsqueda de filtros manualmente. Seleccionar **[!UICONTROL Agregar opciones de filtro]** para definir la primera opción. Especifique la etiqueta para la opción de columna y el texto del valor de opción que desea buscar. Por ejemplo, si desea buscar **Femenino** como valor de una columna Bandeja de entrada, puede especificar **F** como etiqueta para la opción de columna y añadir **Femenino** como el texto del valor de opción. Del mismo modo, puede agregar más opciones de filtro.
   1. Seleccionar **[!UICONTROL Ruta de JSON]** para definir opciones mediante una ruta de archivo JSON. El siguiente es un archivo JSON de muestra para definir las opciones de filtro:

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

   1. Seleccionar **[!UICONTROL Ruta de opciones CRX]** para definir opciones mediante las rutas del repositorio CRX. Seleccionar **[!UICONTROL Añadir rutas de opción]** para añadir varias rutas. El siguiente es un ejemplo para definir `Male` y `Female` opciones de filtro:

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

1. Especifique una descripción opcional para la configuración y seleccione **[!UICONTROL Listo]** para guardarlo.

Los cambios de configuración se reflejan al abrir la página Filtros. La etiqueta de filtro especificada en el paso 4 se muestra como etiqueta para el predicado de opción de columna personalizado. [!DNL Experience Manager] aplica los criterios de búsqueda definidos en el paso 6 en el nombre de columna especificado en el paso 3 y devuelve los elementos de la bandeja de entrada.

El siguiente vídeo ilustra los pasos para filtrar una columna en función de la variable `true` y `false` valores de opción.

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## Ver filtros de búsqueda basados en predicados {#view-search-filters-for-predicates}

Puede ver filtros de búsqueda basados en predicados. Seleccionar **[!UICONTROL Filtrar]** en la página Bandeja de entrada. Los filtros se muestran en el panel izquierdo. A continuación, puede especificar los criterios de búsqueda para filtrar los elementos de la Bandeja de entrada.

![Página Filtros](assets/apply-filters.png)

Para obtener más información sobre la administración de configuraciones de predicado, consulte [Configuración de Search Forms](search-forms.md).
