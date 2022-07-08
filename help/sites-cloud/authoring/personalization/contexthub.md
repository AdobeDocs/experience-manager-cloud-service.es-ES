---
title: Obtención de vista previa de páginas mediante los datos de ContextHub
description: La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub, le permite cambiar datos de los almacenes y resulta útil para obtener una vista previa del contenido
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '368'
ht-degree: 100%

---

# Obtención de vista previa de páginas mediante los datos de ContextHub  {#previewing-pages-using-contexthub-data}

La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub y le permite cambiar datos de los almacenes. La barra de herramientas de ContextHub es útil para obtener una vista previa del contenido determinado por los datos de un almacén de ContextHub.

La barra de herramientas se compone de una serie de modos de IU que contienen uno o más módulos de IU.

* Los modos de IU son iconos que aparecen en la parte izquierda de la barra de herramientas. Al tocar o hacer clic en un icono, la barra de herramientas muestra los módulos de IU que contiene.
* Los módulos de IU muestran datos de uno o más almacenes de ContextHub. Algunos módulos de IU también le permiten manipular los datos de los almacenes.

ContextHub instala varios modos y módulos de IU. Es posible que el administrador haya [configurado ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) para que se muestren otros distintos.

## Mostrar la barra de herramientas de ContextHub {#revealing-the-contexthub-toolbar}

La barra de herramientas de ContextHub está disponible en modo de Vista previa. La barra de herramientas solo está disponible en instancias de autor y únicamente si el administrador la ha activado.

![Barra de herramientas de ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Con la página abierta para edición, en la barra de herramientas, toque o haga clic en Vista previa.

   ![Botón Vista previa](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Para mostrar la barra de herramientas, toque o haga clic en el icono de ContextHub.

   ![Botón de ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funciones del módulo de IU {#ui-module-features}

Cada módulo de IU proporciona un conjunto diferente de funciones, pero los siguientes tipos de funciones son comunes. Dado que los módulos de IU son ampliables, el desarrollador puede implementar otras funciones según sea necesario.

### Contenido de la barra de herramientas {#toolbar-content}

Los módulos de IU pueden mostrar datos de uno o más almacenes de ContextHub en la barra de herramientas. Los módulos de IU utilizan un icono y un título para identificarse.

![Perfiles de ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Contenido emergente {#popup-content}

Al tocarlos o hacer clic en ellos, algunos módulos de IU muestran una superposición emergente. Normalmente, la ventana emergente contiene información adicional, aparte de lo que aparece en la barra de herramientas.

![Información de perfil de ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Formularios emergentes {#popup-forms}

La superposición emergente de un módulo puede incluir elementos de formulario que le permiten cambiar los datos del almacén de ContextHub. Si el contenido de la página viene determinado por los datos del almacén, puede utilizar el formulario y observar los cambios en el contenido de la página.

### Modo de pantalla completa {#fullscreen-mode}

Las superposiciones emergentes pueden incluir un icono que toca o en el que hace clic para expandir el contenido emergente para cubrir toda la ventana o la pantalla del navegador.

![Botón Pantalla completa](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
