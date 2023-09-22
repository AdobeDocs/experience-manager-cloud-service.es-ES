---
title: Componente Separador en formularios adaptables
description: Puede utilizar el componente Separador para separar visualmente las secciones de un formulario.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 60%

---


# Componente Separador en formularios adaptables{#separator-component-in-adaptive-forms}

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto y el estilo generales de un componente Separador especificando las siguientes propiedades del componente Separador:

* **Nombre del elemento:** especifica el nombre del componente. Las expresiones SOM se dirigen al componente con un valor especificado en el campo Nombre del elemento.
* **Grosor:** especifica el grosor del componente Separador en píxeles.

* **Clase CSS:** especifica la clase CSS personalizada para el componente Separador.

* **Estilos en línea:** con [!DNL AEM Forms], ahora puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente Separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](resize-using-layout-mode.md).

Para especificar las propiedades de un componente Separador:

1. Seleccione un componente Separador y pulse ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una pestaña de la sección Propiedades CSS en línea para poder especificar las propiedades CSS. Por ejemplo, un. En la pestaña Field, haga clic en **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **border**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **3 píxeles negro sólido**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Clic **Previsualizar** para que pueda ver los cambios en el formulario.
1. Realice una de las siguientes acciones:
   * Confirme los cambios haciendo clic en **OK**
   * Salga del cuadro de diálogo sin ningún cambio haciendo clic en **Cancelar**.

