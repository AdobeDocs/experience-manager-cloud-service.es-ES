---
title: ¿Qué es el componente separador en el formulario adaptable?
description: El componente separador de formularios adaptables ayuda a separar visualmente las secciones de un formulario.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 100%

---


# Componente Separador en formularios adaptables{#separator-component-in-adaptive-forms}

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto general y el estilo de un componente separador especificando las siguientes propiedades del componente separador:

* **Nombre del elemento:** especifica el nombre del componente. Las expresiones SOM se dirigen al componente con el valor especificado en el campo Nombre del elemento.
* **Grosor:** especifica el grosor del componente Separador en píxeles.

* **Clase CSS:** especifica la clase CSS personalizada para el componente Separador.

* **Estilos en línea:** con [!DNL AEM Forms], ahora puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente Separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](resize-using-layout-mode.md).

Para especificar las propiedades de un componente separador:

1. Seleccione un componente separador y seleccione ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una pestaña de la sección Propiedades CSS en línea para especificar las propiedades CSS. Por ejemplo: a. En la pestaña Campo, seleccione **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **border**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **3px solid black**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Haga clic en **Previsualizar** para que pueda ver los cambios en el formulario.
1. Realice una de las siguientes acciones:
   * Confirme los cambios haciendo clic en **OK**
   * Salga del cuadro de diálogo sin ningún cambio haciendo clic en **Cancelar**.

