---
title: Obtención de vista previa de páginas mediante los datos de ContextHub
description: La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub, le permite cambiar datos de los almacenes y resulta útil para obtener una vista previa del contenido
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 89%

---


# Vista previa de páginas mediante datos de ContextHub{#previewing-pages-using-contexthub-data} 

La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub y le permite cambiar datos de los almacenes. La barra de herramientas de ContextHub es útil para obtener una vista previa del contenido determinado por los datos de un almacén de ContextHub.<!--The [ContextHub](/help/sites-developing/contexthub.md) toolbar displays data from ContextHub stores and enables you to change store data. The ContextHub toolbar is useful for previewing content that is determined by data in a ContextHub store.-->

La barra de herramientas se compone de una serie de modos de IU que contienen uno o más módulos de IU.

* Los modos de IU son iconos que aparecen en la parte izquierda de la barra de herramientas. Al tocar o hacer clic en un icono, la barra de herramientas muestra los módulos de IU que contiene.
* Los módulos de IU muestran datos de uno o más almacenes de ContextHub. Algunos módulos de IU también le permiten manipular los datos de los almacenes.

ContextHub instala varios modos y módulos de IU. Es posible que el administrador haya configurado ContextHub para que se muestren otros distintos.<!--ContextHub installs several UI modes and UI modules. Your administrator may have [configured ContextHub](/help/sites-administering/contexthub-config.md) to display different ones.-->

## Mostrar la barra de herramientas de ContextHub {#revealing-the-contexthub-toolbar}

La barra de herramientas de ContextHub está disponible en modo de Vista previa. La barra de herramientas solo está disponible en instancias de autor y únicamente si el administrador la ha activado.

![Barra de herramientas de ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Con la página abierta para edición, en la barra de herramientas, toque o haga clic en Vista previa.

   ![El botón Previsualización](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Para mostrar la barra de herramientas, toque o haga clic en el icono de ContextHub.

   ![Botón ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funciones del módulo de IU {#ui-module-features}

Cada módulo de IU proporciona un conjunto diferente de funciones, pero los siguientes tipos de funciones son comunes. Dado que los módulos de IU son ampliables, el desarrollador puede implementar otras funciones según sea necesario.

### Contenido de la barra de herramientas {#toolbar-content}

Los módulos de IU pueden mostrar datos de uno o más almacenes de ContextHub en la barra de herramientas. Los módulos de interfaz de usuario utilizan un icono y un título para identificarse.

![Funciones de ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Contenido emergente {#popup-content}

Algunos módulos de interfaz de usuario muestran una superposición emergente cuando se hace clic o se toca. Normalmente, la ventana emergente contiene información adicional, aparte de lo que aparece en la barra de herramientas.

![Información de perfil de ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Formularios emergentes {#popup-forms}

La superposición emergente de un módulo puede incluir elementos de formulario que le permiten cambiar los datos del almacén de ContextHub. Si el contenido de la página viene determinado por los datos del almacén, puede utilizar el formulario y observar los cambios en el contenido de la página.

### Modo de pantalla completa {#fullscreen-mode}

Las superposiciones emergentes pueden incluir un icono que toca o en el que hace clic para expandir el contenido emergente para cubrir toda la ventana o la pantalla del navegador.

![Botón de pantalla completa](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
