---
title: ¿Cómo se aplican firmas electrónicas a un formulario utilizando firmas manuscritas?
description: Aprenda a aplicar firmas electrónicas a un formulario utilizando firmas manuscritas.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 100%

---

# Firmar electrónicamente un formulario con firmas manuscritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

>[!NOTE]
>
> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear nuevos formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) o [adición de formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear formularios adaptables con componentes de base.

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-redirect-page.html?lang=es) |
| AEM as a Cloud Service | Este artículo |


Puede usar el componente **Firma a mano alzada** para dibujar la firma (garabato) en un formulario adaptable. <!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![Cuadro de diálogo Firma manuscrita](assets/scribble-signature.png)

## Las diferentes opciones disponibles en la ventana Firma

* **A:** haga clic en el icono **Pincel** para dibujar su firma en lienzo.
* **B:** haga clic en el icono **Borrar** para borrar la firma en el lienzo.
* **C:** haga clic en el icono **Geolocalización** para añadir geolocalización junto con la firma.
* **D:** haga clic en el icono **Teclado** para escribir su nombre en lienzo.

Una vez que seleccione el icono Listo ![aem_forms_save](assets/aem_forms_save.png) en la ventana Firma manuscrita, no podrá editar la firma. Si desea editar la firma, ignore la firma actual y vuelva a firmar el formulario con las opciones Pincel/Teclado mencionadas anteriormente.

Puede seleccionar el icono **Configurar** ![configurar](assets/configure.png) para establecer la relación de aspecto del lienzo de la firma manuscrita.

* Cuando la relación de aspecto del lienzo de firma manuscrita es menor que 1, la información de geolocalización se agrega en la parte inferior del lienzo de firma manuscrita.
* Cuando la proporción de aspecto del lienzo de firma manuscrita es mayor que 1, la información de geolocalización se agrega en el lado derecho del lienzo de firma manuscrita.


![firma a-mano-alzada-inferior](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Las firmas se guardan siempre en formato PNG.

## Configuración de un formulario adaptable para utilizar una firma manuscrita {#configure-an-adaptive-form-to-use-scribble-signature}

1. Abra un formulario adaptable en modo de edición.
1. Arrastre y coloque el componente **Firma manuscrita** desde el Explorador de componentes al formulario adaptable.
1. Seleccione el icono **Configurar** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del componente Firma manuscrita. [Configure las propiedades de la firma a mano alzada](#properties-of-scribble-signature-component) tal como se describe en la siguiente sección.

   ![Firma a mano alzada](/help/forms/assets/scribblesig.png)

1. Seleccione el icono Listo ![aem_forms_save](assets/aem_forms_save.png) para guardar los cambios. La firma se ha configurado correctamente.

## Configure las propiedades del componente Firma a mano alzada.

Puede personalizar fácilmente el componente Firma a mano alzada para los visitantes con el cuadro de diálogo de configuración.

### Pestaña Básicos

![Pestaña Básicos](/help/forms/assets/scribblesig-basic.png)

* **Nombre**: puede identificar fácilmente un componente de formulario con su nombre único tanto en el formulario como en el editor de reglas, pero el nombre no debe contener espacios ni caracteres especiales.

* **Título**: con su título, puede identificar fácilmente un componente en un formulario y, de forma predeterminada, el título aparece sobre el componente. Si no agrega un título, se mostrará el nombre del componente en lugar del texto del título.

* **Permitir texto enriquecido en el título**: esta función permite a los usuarios dar formato a los títulos de texto sin formato, incorporando funciones como negrita, cursiva, texto subrayado, varias fuentes, tamaños de fuente, colores y opciones adicionales para mejorar la presentación visual y la personalización. Ofrece una mayor flexibilidad y control creativo para hacer que los títulos destaquen dentro de los documentos, sitios web o aplicaciones.\
  Al seleccionar la casilla de verificación de **Permitir texto enriquecido en el título**, las opciones de formato se vuelven visibles para aplicar estilo al título del componente. Para acceder a todas las opciones de formato disponibles, puede hacer clic en la pestaña ![Icono de pantalla completa](/help/forms/assets/fullscreen-icon.png).

  ![Compatibilidad del texto enriquecido](/help/forms/assets/richtext-support-title.png)

* **Ocultar título**: seleccione la opción para ocultar el título del componente.
* **Campo obligatorio**: seleccione la opción para que el campo sea obligatorio.
* **Mensaje de campo obligatorio**: el **Mensaje de campo obligatorio** es un mensaje personalizable que se muestra a los usuarios cuando intentan enviar un formulario sin rellenar un campo obligatorio.
* **Referencia a un vínculo del modelo de datos**: una referencia a un vínculo es una referencia a un elemento de datos que se almacena en una fuente de datos externa y se utiliza en un formulario. La referencia de enlace permite enlazar datos de forma dinámica a campos de formulario, de modo que el formulario pueda mostrar los datos más actualizados de la fuente de datos. Por ejemplo, se puede utilizar una referencia de enlace para mostrar el nombre y la dirección de un cliente en un formulario, según el ID introducido en el formulario por el cliente. La referencia de enlace también se puede utilizar para actualizar la fuente de datos con los datos del formulario. De este modo, AEM Forms permite crear formularios que interactúen con fuentes de datos externas, lo que proporciona al usuario una experiencia óptima para recopilar y administrar datos.
* **Ocultar objeto**: seleccione la opción para ocultar el componente del formulario. El componente permanece accesible para otros fines, como utilizarlo para los cálculos en el Editor de reglas. Esto resulta útil cuando necesita almacenar información que el usuario no necesita ver o cambiar directamente.
* **Deshabilitar objeto**: seleccione la opción para deshabilitar el componente. El componente desactivado no está activo ni puede editarlo el usuario final. El usuario puede ver el valor del campo, pero no modificarlo. El componente permanece accesible para otros fines, como utilizarlo para los cálculos en el Editor de reglas.
* **Relación de aspecto**: la relación de aspecto de un componente de firma a mano alzada define la relación proporcional entre su anchura y altura.
* **Diseño de campo**: la opción **Diseño de campo** determina cómo se sitúan los elementos de formulario, incluidas las etiquetas (títulos) y los mensajes de error, en relación con el componente. **Pie de ilustración y error en la parte superior del widget** coloca el pie de ilustración (etiqueta) del campo y los mensajes de error encima del componente. **Heredar configuración de formulario adaptable** utiliza la configuración predeterminada de diseño de campo especificada en la configuración del formulario adaptable.
* **Clase de CSS**: la **clase de CSS** le permite aplicar estilos personalizados a un componente al asignar una o más clases CSS definidas en su hoja de estilo. Permite aplicar un estilo y una personalización del diseño coherentes en todo el formulario adaptable.

### Contenido de Ayuda

![Pestaña Contenido de ayuda](/help/forms/assets/scribblesig-help.png)

* **Descripción breve**: una descripción breve es una explicación de texto corta que proporciona información adicional o aclaraciones acerca del propósito de un campo de formulario específico. Ayuda al usuario a comprender qué tipo de datos se deben escribir en el campo y puede proporcionar directrices o ejemplos para garantizar que la información introducida sea válida y cumpla los criterios deseados. De forma predeterminada, las descripciones cortas permanecen ocultas. Habilite la opción **Mostrar siempre una descripción breve** para mostrarla debajo del componente.

* **Mostrar siempre una descripción breve**: habilite esta opción para mostrar la descripción breve debajo del componente.

* **Descripción larga**: hace referencia a información o guía adicionales que se proporcionan al usuario para ayudarle a rellenar correctamente un campo de formulario. Aparece cuando el usuario hace clic en el icono de ayuda (i) situado junto al componente. Proporciona información más detallada que la etiqueta de un campo de formulario o el texto del marcador de posición y está diseñado para ayudar al usuario a comprender los requisitos o restricciones del campo. También puede ofrecer sugerencias o ejemplos para que el formulario sea más fácil y preciso.

### Pestaña Accesibilidad {#accessibility}

![Pestaña Accesibilidad](/help/forms/assets/scribblesig-acc.png)

En la pestaña **Accesibilidad**, se pueden configurar valores para las etiquetas de [Accesibilidad ARIA](https://www.w3.org/WAI/standards-guidelines/aria/) del componente. Hay varias opciones disponibles para usar el texto del lector de pantalla:

* **Prioridad de lector de pantalla**: la Prioridad de lector de pantalla se refiere a texto adicional que está específicamente diseñado para ser leído por tecnologías de soporte, como lectores de pantalla, se utilizan personas con deficiencias visuales. Este texto proporciona una descripción del audio del propósito del campo de formulario y puede incluir información sobre el título, la descripción, el nombre y cualquier mensaje relevante (texto personalizado) del campo. El texto del lector de pantalla ayuda a garantizar que el formulario sea accesible para todos los usuarios, incluidos los que tengan deficiencias visuales, y les ofrezca una comprensión completa del campo del formulario y de sus requisitos.

   * **Texto personalizado**: seleccione esta opción para utilizar el texto personalizado para las etiquetas de accesibilidad de ARIA. Al seleccionar esta opción, aparece el cuadro de diálogo Texto personalizado. Puede agregar información relevante en el cuadro de diálogo Texto personalizado.
   * **Descripción breve**: seleccione esta opción para utilizar la descripción para las etiquetas de accesibilidad de ARIA.
   * **Título**: seleccione esta opción para utilizar el título para las etiquetas de accesibilidad de ARIA.
   * **Nombre**: seleccione esta opción para utilizar el nombre para las etiquetas de accesibilidad de ARIA.
   * **Ninguno**: seleccione esta opción si no desea añadir etiquetas de accesibilidad de ARIA.

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## Ver también {#see-also}

{{see-also}}