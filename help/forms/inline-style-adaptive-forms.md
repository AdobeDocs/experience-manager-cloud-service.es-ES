---
title: ¿Cómo se aplican los estilos en línea a los componentes de formulario adaptable?
description: Aunque puede aplicar estilos personalizados en un formulario adaptable, también puede aplicar propiedades CSS en línea en componentes individuales de un formulario adaptable. Aprenda a aplicar estilos en línea a los componentes del formulario adaptable. Profundizar con un ejemplo para aplicar estilo en línea a un componente de campo de texto.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 25adabfb-ff19-4cb2-aef5-0a8086d2e552
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Estilo en línea de los componentes del formulario adaptable {#inline-styling-of-adaptive-form-components}

Puede definir el aspecto y el estilo generales de un formulario adaptable especificando los estilos utilizando [editor de temas](themes.md). Además, puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios sobre la marcha. Los estilos en línea anulan el estilo proporcionado en el tema.

## Aplicar propiedades CSS en línea {#apply-inline-css-properties}

Para añadir estilos en línea a un componente:

1. Abra el formulario en el editor de formularios y cambie el modo a modo de estilo. Para cambiar el modo al modo de estilo, en la barra de herramientas de la página, pulse ![lista desplegable de lienzo](assets/Smock_ChevronDown.svg) > **[!UICONTROL Estilo]**.
1. Seleccione un componente en la página y pulse el botón de edición ![editar-botón](assets/edit.svg). Propiedades de estilo abiertas en la barra lateral.

   También puede seleccionar componentes del árbol de jerarquía de formularios en la barra lateral. El árbol de jerarquía de formularios está disponible como Objetos de formulario en la barra lateral.

   En el [!UICONTROL Estilo] puede ver los componentes enumerados en Objetos de formulario. Sin embargo, la lista Objetos de formulario de la barra lateral enumera componentes como campos y paneles. Los campos y los paneles son componentes genéricos que pueden contener componentes como, por ejemplo, cuadros de texto y botones de opción.

   Cuando seleccione un componente de la barra lateral, verá todos los subcomponentes enumerados y las propiedades del componente seleccionado. Puede seleccionar un subcomponente específico y aplicarle un estilo.

1. Haga clic en una ficha de la barra lateral para especificar las propiedades CSS. Puede especificar propiedades como:

   * [!UICONTROL Dimension y posición] (Mostrar configuración, relleno, altura, anchura, margen, posición, z-index, flotante, borrar, desbordamiento)
   * [!UICONTROL Texto] (Familia de fuentes, peso, color, tamaño, altura de línea y alineación)
   * [!UICONTROL Contexto] (Imagen y degradado, color de fondo)
   * [!UICONTROL Borde] (Anchura, estilo, color, radio)
   * [!UICONTROL Efectos] (Sombra, opacidad)
   * [!UICONTROL Avanzadas] (Permite escribir CSS personalizada para el componente)

1. Del mismo modo, puede aplicar estilos a otras partes de un componente, como [!UICONTROL Widget], [!UICONTROL Pie de ilustración]y [!UICONTROL Ayuda].
1. Toque **[!UICONTROL Listo]** para confirmar los cambios o **[!UICONTROL Cancelar]** para descartar los cambios.

## Ejemplo: estilos en línea para un componente de campo {#example-inline-styles-for-a-field-component}

Las siguientes imágenes muestran un campo de texto antes y después de que se le apliquen estilos en línea.

![Componente de cuadro de texto antes de aplicar estilo en línea](assets/no-style.png)

Componente de cuadro de texto antes de aplicar propiedades de estilo en línea

Observe el cambio en el estilo del cuadro de texto como se muestra en la siguiente imagen después de aplicar las siguientes propiedades CSS.

<table>
 <tbody>
  <tr>
   <td><p>Selector</p> </td>
   <td><p>CSS, propiedad</p> </td>
   <td><p>Value</p> </td>
   <td><p>Efecto</p> </td>
  </tr>
  <tr>
   <td><p>Campo</p> </td>
   <td><p>border</p> </td>
   <td><p>Ancho del borde = 2 px</p> <p>Estilo de borde=Sólido</p> <p>Color del borde=#1111</p> </td>
   <td><p>Crea un borde ancho negro de 2 píxeles alrededor del campo</p> </td>
  </tr>
  <tr>
   <td><p>Cuadro de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia el color de fondo a CornflowerBlue (#6495ED)</p> <p>Nota: Puede especificar un nombre de color o su código hexadecimal en el campo de valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimension y posición &gt; anchura</p> </td>
   <td><p>100px</p> </td>
   <td><p>Corrige la anchura de 100 píxeles para la etiqueta</p> </td>
  </tr>
  <tr>
   <td>Icono de ayuda de campo</td>
   <td>Texto &gt; Color de fuente</td>
   <td>#2ECC40</td>
   <td>Cambia el color de la cara del icono de ayuda.</td>
  </tr>
  <tr>
   <td><p>Descripción larga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Alinea la descripción larga para que la ayuda se centre</p> </td>
  </tr>
 </tbody>
</table>

![Estilo de cuadro de texto después de aplicar estilo en línea](assets/applied-style.png)

Componente de cuadro de texto después de aplicar propiedades de estilo en línea

Siguiendo los pasos anteriores, puede seleccionar y aplicar estilo a otros componentes, como paneles, botones de envío y botones de radio.

>[!NOTE]
>
>Las propiedades de estilo varían en función del componente que seleccione.

## Copiar y pegar estilos {#copy-paste-styles}

También puede copiar y pegar un estilo de un componente a otro componente en un formulario adaptable. En el **[!UICONTROL Estilo]** , pulse el componente y pulse el icono Copiar . ![Copiar](assets/property-copy-icon.svg).

Pulse el otro componente del mismo tipo y pulse el icono Pegar ![Copiar](assets/Smock_Paste_18_N.svg) para pegar el estilo copiado. También puede pulsar el icono Borrar estilo ![Copiar](assets/clear-style-icon.svg) para borrar el estilo aplicado.

## Definir estilos para diferentes estados de un componente {#set-styles-for-states}

Puede definir estilos para diferentes estados de un tipo de componente. Los diferentes estados incluyen: [!UICONTROL Focus], [!UICONTROL Desactivado], [!UICONTROL Hover], [!UICONTROL Error], [!UICONTROL Correcto]y [!UICONTROL Obligatorio].

Para definir el estilo de un estado de un componente:

1. En el **[!UICONTROL Estilo]** , pulse el componente y pulse el icono Editar ![Editar](assets/Smock_Edit_18_N.svg).

1. Seleccione el estado del componente mediante el **[!UICONTROL Estado]** lista desplegable.

   ![Seleccionar estado](assets/select-state.png)

1. Defina el estilo para el estado seleccionado del componente y pulse ![Guardar](assets/save_icon.svg) para guardar las propiedades.

También puede simular los estados de éxito y error. Pulse el icono Expandir para ver el **[!UICONTROL Simular éxito]** y **[!UICONTROL Simular error]** opciones.

![Simular estados](assets/simulate-states.png)
