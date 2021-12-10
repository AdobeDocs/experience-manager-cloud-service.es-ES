---
title: Uso de expresiones SOM en Forms adaptable
seo-title: Using SOM expressions in Adaptive Forms
description: Obtenga información sobre cómo extraer expresiones SOM de un panel de un formulario adaptable.
seo-description: Learn how to extract SOM expressions of a panel of an Adaptive Form.
uuid: c5d55aff-fb69-4a1c-96ea-fb3f9322cbb0
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 13f00bb2-561f-4d64-8829-292c663abeab
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# Uso de expresiones SOM en Forms adaptable{#using-som-expressions-in-adaptive-forms}

Forms adaptable se modelan como AEM Página que se representa como estructura de contenido JCR en AEM repositorio. El elemento clave de la estructura de contenido es el nodo guideContainer . Debajo de guideContainer, hay rootPanel que puede contener paneles y campos anidados.

Puede utilizar un modelo de objetos de secuencias de comandos (SOM) para hacer referencia a valores, propiedades y métodos dentro de un modelo de objetos de documento (DOM) concreto. Un DOM organiza los objetos de memoria y las propiedades en una jerarquía de árbol. Una expresión SOM hace referencia a los elementos y paneles Campos/Dibujar.

La siguiente imagen muestra una estructura de nodos a la que se traduce un formulario adaptable cuando se agregan componentes a un formulario. Por ejemplo, puede agregar un panel al panel raíz y un botón de opción del panel que se transforme en DOM durante la ejecución. La expresión SOM para el campo de botón de radio del formulario adaptable se especifica como `guide[0].guide1[0].guideRootPanel[0].panel1[0].radiobutton[0]`.

![Árbol DOM](assets/hierarchy.png)

Árbol DOM

Una expresión SOM para cualquier elemento de un formulario adaptable lleva el prefijo `guide[0].guide1[0]`. La posición de un componente en la jerarquía de estructura de nodos se utiliza para derivar su expresión SOM.

![Árbol DOM con dos botones de opción](assets/hierarchy_radio_button.png)

Árbol DOM con dos botones de opción

La expresión SOM cambia al cambiar la posición de los botones de opción del formulario adaptable. En el modo de creación, puede ver la expresión SOM de un campo o elemento dentro de [!DNL AEM Forms] uso de la opción Ver expresión SOM . La opción aparece en el panel y al hacer clic con el botón derecho en el campo o elemento.

![Extracción de expresiones SOM en un formulario adaptable](assets/som-expressions.png)

Extracción de expresiones SOM en un formulario adaptable

En los paneles, puede acceder a la función desde la barra de herramientas del panel. La función facilita las secuencias de comandos de los autores del formulario adaptable.

![Extracción de expresiones SOM mediante la barra de herramientas del panel](assets/som-expression.png)

Extracción de expresiones SOM mediante la barra de herramientas del panel

Algunas API enumeradas en [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) utilice la expresión SOM de un elemento. Por ejemplo, para centrar la atención en un campo concreto de un formulario adaptable, pase la expresión SOM correspondiente a la variable `getFocus`API en `guideBridge`.
