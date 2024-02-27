---
description: Este tutorial incluye toda la información relacionada con los componentes de EDS.
title: 'Componentes de formulario admitidos en el bloque de formulario: tutorial para desarrolladores'
feature: Edge Delivery Services
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 6%

---


# Componentes de HTML admitidos en la entrega perimetral de bloque de formulario

AEM Forms Edge Delivery incluye un bloque de formulario. El bloque de formulario le ayuda a crear fácilmente formularios para capturar y almacenar los datos capturados.

El bloque de formulario admite componentes de HTML-5 como texto, correo electrónico, número, fecha y muchos más. También admite elementos de área de texto, selección y conjunto de campos, e incluye funciones de validación de entrada nativas de HTML-5. El bloque de formulario crea una estructura de HTML uniforme para todos los tipos de campo y contenedores, lo que garantiza la coherencia. Usted también [Aplicar estilo a los tipos de campo](https://adobe-rnd.github.io/form-block/customization/styling_form) uso del `form.css` archivo.

## HTML compatible 5 tipos de entrada en el bloque de formulario

El bloque de formulario admite una serie de tipos de entrada de HTML AEM 5 y también procesa sin problemas formularios creados con componentes principales de.

Esta es la tabla que describe cómo se corresponden los componentes principales con los tipos de entrada de HTML-5 en la entrega de Edge:

<table>
 <tbody>
  <tr>
   <td><b>Componentes principales</b> </td>
   <td><b>Tipo de entrada de HTML 5</b> </td>
   <td><b>Detalles</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Contenedor del formulario</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">formulario </td>
   <td> Cree un formulario para capturar las entradas del usuario.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Entrada de texto</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Define un campo de entrada de texto de una sola línea. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Entrada de número</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">número</a></td>
   <td>Permite al usuario introducir un número. También puede agregar una validación integrada para rechazar las entradas no numéricas. Permite al usuario introducir un número. También puede agregar una validación integrada para rechazar las entradas no numéricas. Inicialmente, el campo de entrada se muestra como una entrada de número. Si un usuario aplica un patrón de visualización, cambia al texto para permitir que el autor aplique el formato de número, ya que el HTML 5 no es compatible con los patrones de visualización. Sin embargo, cuando el usuario hace clic en él, vuelve a escribir números.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Selector de fecha</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">fecha </a></td>
   <td> Cree un campo de entrada para introducir una fecha. Tiene la opción de introducir la fecha a través de un cuadro de texto, que valida la entrada, o a través de una interfaz de selector de fechas dedicada. Inicialmente, se muestra el campo de entrada de fecha nativo. Si un usuario aplica un patrón de visualización, cambia al texto para permitir que el usuario aplique el formato, ya que el HTML 5 no admite patrones de visualización. Sin embargo, cuando el usuario hace clic en él, vuelve a escribir una fecha.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">Archivo adjunto</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">archivo</a></td>
   <td> Permite al usuario elegir uno o varios archivos del almacenamiento del dispositivo. Admite validaciones de entrada de archivos mejoradas, como tipos de archivo aceptados, restricciones de tamaño de archivo y límites de selección de archivos mínimos y máximos. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Lista desplegable</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Permite a los usuarios seleccionar una o varias opciones de una lista de opciones predefinidas. Las opciones pueden ser de tipo Cadena, Número o Booleano.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Grupo de casillas de verificación</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">casilla de verificación múltiple</a></td>
   <td> Permite que los usuarios seleccionen una o más opciones de una lista. Se generan varias casillas de verificación con nombres idénticos, cada una correspondiente a un elemento de la enumeración. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Grupo de botones de opción</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">radio múltiple</a></td>
   <td> Permite al usuario seleccionar una opción de un grupo de opciones relacionadas. Se generan varios botones de opción con nombres idénticos, cada uno correspondiente a un elemento de la enumeración.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Botón</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">botón</a></td>
   <td>Elemento de la interfaz de usuario que permite a los usuarios almacenar en déclencheur una acción cuando se hace clic. </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">conjunto de campos con leyenda</a></td>
   <td> Agrupe secciones dentro de un formulario, donde un elemento *leyenda* anidado agrega un rótulo para el formulario.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=es">Asistente</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Agrupa secciones relacionadas dentro de un formulario. También controla la disposición y admite opciones de visualización para colocarlas en la parte superior o en el lado izquierdo. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Texto</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>Una etiqueta p marca un párrafo. En el contenido visual, los párrafos son fragmentos de texto separados por líneas en blanco o una primera línea con sangría</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Botón Enviar</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> Elemento de la IU que permite a los usuarios enviar un formulario al servidor al hacer clic en. Si un usuario agrega una regla de envío a un botón, funciona como el botón de envío. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Botón Restablecer</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">restablecer</a></td>
   <td>Elemento de la interfaz de usuario que restablece un formulario al hacer clic en. Si un usuario agrega una regla de restablecimiento a un botón, funciona como el botón de restablecimiento. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Entrada de correo electrónico</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">correo electrónico</a></td>
   <td> Permite al usuario introducir y editar una dirección de correo electrónico. Si el usuario agrega varios atributos, se puede agregar o editar una lista de direcciones de correo electrónico.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Entrada de teléfono</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Permite al usuario introducir y editar un número de teléfono.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Encabezado</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> encabezado</a></td>
   <td>Incluye contenido introductorio, normalmente un grupo de ayudas de introducción o navegación. Se admite fuera del contenedor de formularios. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Pie de página</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">pie de página</a></td>
   <td> Contiene información como datos de copyright o vínculos a documentos relacionados. Se admite fuera del contenedor de formularios.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms//adaptive-forms-components/accordion.html?lang=es">Acordeón<a></td>
   <td><i>Aún no es compatible con el bloque de formulario</i></td>
   <td> Permite al usuario crear secciones expansibles y contraíbles en un formulario. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=es">Pestañas horizontales</a></td>
   <td><i>Aún no es compatible con el bloque de formulario</i></td>
   <td>Organiza varias secciones de un formulario en pestañas independientes que se muestran horizontalmente.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Imagen</a></td>
   <td><i>Aún no es compatible con el bloque de formulario</i></td>
   <td> Permite al usuario incluir imágenes en un formulario.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Título</a></td>
   <td><i>Aún no es compatible con el bloque de formulario</i></td>
   <td> Se refiere al texto que aparece en la parte superior del formulario. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Interruptor</td>
   <td><i>Aún no es compatible con el bloque de formulario</i></td>
   <td> Alternancia de dos estados que permite al usuario seleccionar entre dos estados, como habilitar o deshabilitar una característica, configuración o funcionalidad.</td>
  </tr>
 </tbody>
</table>


