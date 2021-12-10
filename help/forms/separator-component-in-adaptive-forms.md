---
title: Componente separador en Forms adaptable
seo-title: Separator component in Adaptive Forms
description: Puede utilizar el componente separador para separar visualmente secciones de un formulario.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---


# Componente separador en Forms adaptable{#separator-component-in-adaptive-forms}

Puede utilizar el componente separador para separar visualmente los paneles de un formulario. Puede definir el aspecto general y el estilo de un componente separador especificando las siguientes propiedades del componente separador:

* **Nombre del elemento:** Especifica el nombre del componente. Las expresiones SOM se dirigen al componente con el valor especificado en el campo Nombre de elemento .
* **Grosor:** Especifica el grosor del componente separador en píxeles.

* **Clase CSS:** Especifica la clase CSS personalizada para el componente separador

* **Estilos en línea:** con [!DNL AEM Forms], ahora puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios en tiempo real.

Puede utilizar el modo Diseño para definir el número de columnas a las que se expande el componente separador. Para obtener más información, consulte [Uso del modo Diseño para cambiar el tamaño de los componentes](resize-using-layout-mode.md).

Para especificar las propiedades de un componente separador:

1. Seleccione un componente separador y toque ![cmppr](assets/cmppr.png). Las propiedades se abren en la barra lateral.
1. Haga clic en una ficha de la sección Propiedades CSS en línea para especificar las propiedades CSS. Por ejemplo: a. En la ficha Campo, haga clic en **Agregar elemento**. Se añade una fila con dos campos.
1. En el primer campo de la izquierda, especifique la propiedad CSS3 que desee aplicar. Por ejemplo, **borde**. También puede seleccionar una propiedad haciendo clic en el botón de flecha hacia abajo. La lista desplegable no es exhaustiva y puede especificar cualquier nombre de propiedad CSS3 admitido en este campo.
1. En el campo adyacente, especifique un valor válido para la propiedad CSS3 especificada. Por ejemplo, **Negro sólido de 3 px**.
1. Haga clic en **Agregar elemento** para especificar otra propiedad y su valor.
1. Haga clic en **Vista previa** para obtener una vista previa de los cambios en el formulario.
1. Haga clic en **OK** para confirmar los cambios o **Cancelar** para salir del cuadro de diálogo sin ningún cambio.

