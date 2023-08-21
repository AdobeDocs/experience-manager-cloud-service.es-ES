---
title: Aplicar firmas electrónicas a un formulario utilizando firmas manuscritas
description: Firma de formularios mediante firmas manuscritas
seo-description: Signing forms using scribble
topic-tags: author
source-git-commit: b2c8e739c4e1c5289ca263360f4f59b8a2c05f5b
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 92%

---

# Aplicar firmas electrónicas a un formulario utilizando firmas manuscritas{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/creating-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Este artículo |


Puede usar los componentes **Firma manuscrita** y **Paso de firma** para dibujar la firma (manuscrita) en un formulario adaptable. El componente Paso de firma muestra una versión PDF del formulario adaptable. Para utilizar el componente Paso de firma, necesita activar la opción Documento de registro o un formulario adaptable basado en una plantilla de formulario.

![Cuadro de diálogo Firma manuscrita](assets/scribble-signature.png)

## Las diferentes opciones disponibles en la ventana Firma

* **A:** haga clic en el icono **Pincel** para dibujar su firma en lienzo.
* **B:** haga clic en el icono **Borrar** para borrar la firma en el lienzo.
* **C:** haga clic en el icono **Geolocalización** para añadir geolocalización junto con la firma.
* **D:** haga clic en el icono **Teclado** para escribir su nombre en lienzo.

Una vez que pulse el icono Listo ![aem_forms_save](assets/aem_forms_save.png) en la ventana Firma manuscrita, no podrá editar la firma. Si desea editar la firma, ignore la firma actual y vuelva a firmar el formulario con las opciones Pincel/Teclado mencionadas anteriormente.

Puede pulsar el icono **Configurar** ![configurar](assets/configure.png) para establecer la relación de aspecto del lienzo de la firma manuscrita.
* Cuando la relación de aspecto del lienzo de firma manuscrita es menor que 1, la información de geolocalización se agrega en la parte inferior del lienzo de firma manuscrita.


* Cuando la proporción de aspecto del lienzo de firma manuscrita es mayor que 1, la información de geolocalización se agrega en el lado derecho del lienzo de firma manuscrita.


![firma a-mano-alzada-inferior](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Las firmas se guardan siempre en formato PNG.
>

## Configuración de un formulario adaptable para utilizar una firma manuscrita {#configure-an-adaptive-form-to-use-scribble-signature}

1. Active la opción Documento de registro o utilice un formulario adaptable basado en una plantilla de formulario. Para obtener información paso a paso, consulte [Crear un formulario adaptable](creating-adaptive-form.md).
1. Arrastre y coloque el componente **Firma manuscrita** desde el Explorador de componentes al formulario adaptable.
1. Pulse el icono **Configurar** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del componente Firma manuscrita. Configure las propiedades del componente Firma manuscrita.
1. Arrastre y coloque el componente Paso de firma desde el Explorador de componentes al formulario adaptable.

   >[!NOTE]
   >
   >El componente Paso de firma ocupa el ancho completo disponible en el formulario. Se recomienda no colocar ningún otro componente en la sección que contiene el componente Paso de firma.

1. En el explorador de contenido, pulse **Contenedor de formulario** y haga clic en el icono **Configurar** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del contenedor de formularios adaptables. Vaya a **Contenedor de formulario adaptable** > **Firma electrónica** y deseleccione la opción **Habilitar Adobe Sign**. Pulse el icono Listo ![aem_forms_save](assets/aem_forms_save.png) para guardar los cambios.

   >[!NOTE]
   >
   >Cuando se agrega un componente Paso de firma a un formulario adaptable, la opción Habilitar Adobe Sign se selecciona automáticamente.

1. Pulse el icono **Configurar** ![configurar](assets/configure.png). Se abrirá el explorador de propiedades, donde verá las propiedades del Paso de firma. Configure las siguientes propiedades:

   * **Nombre del elemento**: especifique el nombre del componente.

   * **Título:** especifique un título único para el componente.
   * **Mensaje de plantilla:** especifique el mensaje que se mostrará mientras se carga el PDF de firma. Los servicios de Adobe Sign tardan algún tiempo en preparar y cargar el PDF de firma.
   * **Servicio de firma:** seleccione la opción **Firma manuscrita**.

   * **Clase CSS**: especifique la clase CSS de la biblioteca de cliente, si la hay. Se recomienda utilizar [temáticas](themes.md) y [estilos en línea](inline-style-adaptive-forms.md) en lugar de la clase CSS.

   Pulse el icono Listo ![aem_forms_save](assets/aem_forms_save.png) para guardar los cambios. La firma se ha configurado correctamente.

   Ahora, al rellenar un formulario, se muestra una versión PDF del formulario adaptable y se proporcionan las opciones para firmar el documento PDF. Para obtener información detallada, consulte [Firmar un formulario adaptable con una firma manuscrita](signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firmar un formulario adaptable con una firma manuscrita {#sign-an-adaptive-form-using-scribble-signature}

1. Después de rellenar un formulario adaptable y llegar a la página Paso de firma, se muestra la pantalla de firma.

   ![Pantalla de firma de la página EchoSign](assets/esignscribblesign.jpg)

1. Haga clic en **[!UICONTROL Firmar]**. Aparecerá el cuadro de diálogo Firma manuscrita. Firme el formulario y haga clic en el icono Listo ![aem_forms_save](assets/aem_forms_save.png) para guardar la firma.

   ![Cuadro de diálogo Firma manuscrita](assets/scribblewidget.png)

1. Haga clic en Completar para finalizar el proceso de firma.

   ![Completar el proceso de firma](assets/scribblecomplete.jpg)

Las firmas se agregan al formulario y el control de formulario pasa al siguiente panel.
