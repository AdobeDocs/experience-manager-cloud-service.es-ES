---
title: Obtención de vista previa de páginas mediante los datos de ContextHub
description: La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub, le permite cambiar datos de los almacenes y resulta útil para obtener una vista previa del contenido
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 25%

---

# Obtención de vista previa de páginas mediante los datos de ContextHub  {#previewing-pages-using-contexthub-data}

La barra de herramientas de ContextHub muestra datos de los almacenes de ContextHub y le permite cambiar datos de los almacenes. La barra de herramientas de ContextHub resulta útil para obtener una vista previa del contenido determinado por los datos de un almacén de ContextHub.

La barra de herramientas consta de una serie de modos de interfaz de usuario que contienen uno o más módulos de interfaz de usuario.

* Los modos de interfaz de usuario son iconos que aparecen en la parte izquierda de la barra de herramientas. Al seleccionar un icono, la barra de herramientas muestra los módulos de interfaz de usuario que contiene.
* Los módulos de IU muestran datos de uno o más almacenes de ContextHub. Algunos módulos de IU también permiten manipular los datos de almacenamiento.

ContextHub instala varios modos de interfaz de usuario y módulos de IU. Es posible que el administrador haya [configurado ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) para que muestre otros.

## Mostrar la barra de herramientas de ContextHub {#revealing-the-contexthub-toolbar}

La barra de herramientas de ContextHub está disponible en el modo de vista previa. La barra de herramientas solo está disponible en instancias de autor y únicamente si el administrador la ha activado.

![Barra de herramientas de ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Con la página abierta para edición, en la barra de herramientas, seleccione Vista previa.

   ![Botón Vista previa](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Para mostrar la barra de herramientas, seleccione el icono de ContextHub.

   ![Botón de ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funciones del módulo de IU {#ui-module-features}

Cada módulo de interfaz de usuario proporciona un conjunto diferente de características, pero los siguientes tipos de características son comunes. Dado que los módulos de IU son ampliables, el desarrollador puede implementar otras funciones según sea necesario.

### Contenido de barra {#toolbar-content}

Los módulos de IU pueden mostrar datos de uno o más almacenes de ContextHub en la barra de herramientas. Los módulos de IU utilizan un icono y un título para identificarse.

![Perfiles de ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Contenido emergente {#popup-content}

Algunos módulos de IU muestran una superposición emergente al pulsar o hacer clic en ellos. Normalmente, la ventana emergente contiene información adicional, aparte de lo que aparece en la barra de herramientas.

![Información de perfil de ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Forms emergente {#popup-forms}

La superposición emergente de un módulo puede incluir elementos de formulario que permiten cambiar los datos en el almacén de ContextHub. Si el contenido de la página está determinado por los datos de almacenamiento, puede utilizar el formulario y observar los cambios en el contenido de la página.

### Modo de pantalla completa {#fullscreen-mode}

Las superposiciones emergentes pueden incluir un icono que se selecciona para expandir el contenido emergente y cubrir toda la ventana o pantalla del explorador.

![Botón Pantalla completa](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
