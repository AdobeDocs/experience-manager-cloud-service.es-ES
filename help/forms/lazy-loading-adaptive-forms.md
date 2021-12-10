---
title: ¿Cómo mejorar el rendimiento de los formularios grandes con carga diferida?
description: Obtenga información sobre cómo mejorar el rendimiento de los formularios grandes con carga diferida. La carga diferida mejora significativamente el rendimiento de Forms adaptable grande y complejo al aplazar la inicialización y carga de los fragmentos de formulario hasta que sean visibles.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 0cd38edb-2201-4ca6-8b84-6b5b7f76bd90
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 0%

---

# Mejorar el rendimiento de los formularios grandes con carga diferida{#improve-performance-of-large-forms-with-lazy-loading}

## Introducción a la carga diferida {#introduction-to-lazy-loading}

Cuando el formulario se vuelve grande y complejo con cientos y miles de campos, los usuarios finales experimentan un tiempo de respuesta largo al procesar formularios en tiempo de ejecución. Para minimizar el tiempo de respuesta, Adaptive Forms le permite dividir formularios en fragmentos lógicos y configurarlos para retrasar la inicialización o carga de fragmentos hasta que el fragmento tenga que ser visible. Se denomina carga diferida. Además, los fragmentos configurados para la carga diferida se descargan una vez que el usuario navega a otras secciones del formulario y los fragmentos ya no están visibles.

Primero comprendamos los requisitos y pasos preparatorios antes de configurar la carga diferida.

## Preparación para configurar la carga diferida {#preparing-to-configure-lazy-loading}

Antes de configurar la carga diferida de fragmentos en el formulario adaptable, es importante definir estrategias para crear fragmentos, identificar valores que se utilizan en secuencias de comandos o que se mencionan en otros fragmentos y definir reglas para controlar la visibilidad de los campos en fragmentos cargados de forma diferida.

* **Identificar y crear fragmentos**
Solo puede configurar los fragmentos de formulario adaptables para la carga diferida. Un fragmento es un segmento independiente que reside fuera de un formulario adaptable y que puede reutilizarse en todos los formularios. Por lo tanto, el primer paso para implementar la carga diferida es identificar secciones lógicas en un formulario y convertirlas en fragmentos. Puede crear un fragmento desde cero o guardar un panel de formulario existente como fragmento.

   <!--For more information about creating fragments, see [Adaptive Form Fragments](adaptive-form-fragments.md).-->

* **Identificar y marcar valores globales**
Las transacciones basadas en Forms implican elementos dinámicos para capturar datos relevantes de los usuarios y procesarlos para simplificar la experiencia de cumplimentación de formularios. Por ejemplo, el formulario tiene el campo A en el fragmento X cuyo valor determina la validez del campo B en otro fragmento. En este caso, si el fragmento X está marcado para una carga diferida, el valor del campo A debe estar disponible para validar el campo B incluso cuando el fragmento X no está cargado. Para conseguirlo, puede marcar el campo A como global, lo que garantiza que su valor esté disponible para validar el campo B cuando el fragmento X no se carga.

   Para obtener información sobre cómo convertir un valor de campo en global, consulte [Configuración de la carga diferida](lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Escribir reglas para controlar la visibilidad de los campos**
Forms incluye algunos campos y secciones que no son aplicables a todos los usuarios y en todas las condiciones. Los autores y desarrolladores de Forms utilizan la visibilidad o las reglas de mostrar y ocultar para controlar su visibilidad en función de las entradas del usuario. Por ejemplo, el campo Dirección de oficina no se muestra a los usuarios que eligen Desempleado en el campo Estado de empleo en un formulario. Para obtener más información sobre cómo escribir reglas, consulte [Uso del editor de reglas](rule-editor.md).

   Puede utilizar reglas de visibilidad en los fragmentos cargados de forma diferida, de modo que los campos condicionales solo se muestren cuando sean necesarios. Además, marque el campo condicional global para hacer referencia a él en la expresión de visibilidad del fragmento cargado lentamente.

## Configuración de la carga diferida {#configuring-lazy-loading}

Realice los siguientes pasos para habilitar la carga diferida en un fragmento de formulario adaptable:

1. Abra el formulario adaptable en modo de creación que contenga el fragmento que desea activar para la carga diferida.
1. Seleccione el fragmento de formulario adaptable y pulse ![configure](assets/configure-icon.svg).
1. En la barra lateral, active **[!UICONTROL Cargar fragmento de forma diferida]** y toque **Listo**.

   ![Habilitar la carga diferida para el fragmento de formulario adaptable](assets/lazy-loading-fragment.png)

   El fragmento ahora está habilitado para la carga diferida.

Puede marcar los valores de los objetos del fragmento cargado a medida como globales de modo que estén disponibles para su uso en secuencias de comandos cuando no se cargue el fragmento que los contiene. Haga lo siguiente:

1. Abra el fragmento del formulario adaptable en modo de creación.
1. Pulse el campo cuyo valor desee marcar como global y, a continuación, pulse ![configure](assets/configure-icon.svg).
1. En la barra lateral, active **[!UICONTROL Utilizar valor durante la carga diferida]**.

   ![Campo de carga diferida en la barra lateral](assets/enable-lazy-loading.png)

   El valor ahora está marcado como global y está disponible para su uso en scripts incluso cuando se descarga el fragmento que lo contiene.

## Consideraciones y prácticas recomendadas para configurar la carga diferida {#considerations-and-best-practices-for-configuring-lazy-loading}

Algunas limitaciones, recomendaciones y puntos importantes que se deben tener en cuenta al trabajar con carga diferida son las siguientes:

* Se recomienda utilizar Forms adaptable basado en esquemas XSD sobre Forms adaptable basado en XFA para configurar la carga diferida en formularios grandes. La mejora del rendimiento debido a la implementación de carga diferida en Forms adaptable basado en XFA es relativamente menor que ganancia en Forms adaptable basado en XSD.
* No configure la carga diferida en fragmentos de un formulario adaptable que utilicen **[!UICONTROL Responsable: todo en una página sin navegación]** diseño para el panel raíz. Como resultado de la configuración de diseño adaptable, todos los fragmentos se cargan simultáneamente en un formulario adaptable. También puede provocar una degradación del rendimiento.
* Se recomienda no configurar la carga diferida en los fragmentos del primer panel que se muestre al cargar el formulario adaptable.
* La carga diferida es compatible con hasta dos niveles en la jerarquía de fragmentos.
* Asegúrese de que los campos marcados como globales sean únicos en un formulario adaptable.
* Considere la posibilidad de escribir reglas de visibilidad para fragmentos que deban mostrarse u ocultarse según una condición. Por ejemplo, puede mostrar u ocultar el fragmento Detalles del cónyuge en función del estado civil especificado por el usuario.
* Los componentes de archivo adjunto y Términos y condiciones no son compatibles con los fragmentos cargados de forma diferida.

### Prácticas recomendadas de secuencias de comandos para configurar la carga diferida {#scripting-best-practices-for-configuring-lazy-loading}

Los puntos importantes que se deben tener en cuenta al desarrollar secuencias de comandos para paneles de carga diferida son los siguientes:

* Asegúrese de que las secuencias de comandos initialize y calculate utilizadas en los campos de un fragmento cargado diferentemente tengan un carácter idéntico. Los scripts independientes son aquellos que tienen el mismo efecto incluso después de varias ejecuciones.
* Utilice la propiedad de campos disponible globalmente para que el valor de los campos situados en un panel de carga diferida esté disponible para todos los demás paneles de un formulario.
* No reenvíe el valor de referencia de un campo dentro de un panel flotante independientemente de si el campo se marca globalmente en los fragmentos o no.
* Utilice la función de restablecimiento del panel para restablecer todo lo visible en el panel mediante la siguiente expresión de clic.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;): &quot;navigablePanel&quot;})).resetData()
