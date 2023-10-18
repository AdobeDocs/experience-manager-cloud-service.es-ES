---
title: ¿Cómo cambiar el contenido de la página cero en Designer?
description: Cambie el mensaje que se muestra en la página cero de un PDF XFA para los visualizadores que no son de Adobe PDF.
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
source-git-commit: 0f8aed76af4d2640094a76f2805f73a0a619e33f
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 80%

---


# Cambiar el contenido de la página cero en Designer {#changing-page-zero-content-in-designer}

El contenido de la página cero se muestra de forma predeterminada cuando un visor que no es Adobe PDF, como el visor de PDF predeterminado de [!DNL Chrome] o [!DNL Firefox], no puede leer el contenido del formulario PDF/XFA. A continuación, se muestra el mensaje predeterminado de la página cero.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] La versión de Designer de permite cambiar el mensaje que se muestra en la página cero. Para cambiar el mensaje de la página cero, realice los siguientes pasos:

1. Asegúrese de que ha instalado la versión de Designer de [!DNL AEM Forms]. Puede comprobar la versión desde la pantalla Acerca de Designer.

1. Abra el formulario para el cual desea cambiar el contenido de la página cero.

1. Haga clic en **[!UICONTROL Archivo]** > **[!UICONTROL Propiedades del formulario]**.

1. En el cuadro de diálogo [!UICONTROL Propiedades del formulario], haga clic en ![plus](assets/plus.png) (icono + ) para añadir una propiedad personalizada.

1. Especifique **_pagezerocontent** como el nombre de la propiedad.
1. Agregue el nuevo mensaje de la página cero en formato de texto enriquecido como valor. Por ejemplo:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Guarde el formulario como PDF.

1. Vea el formulario PDF en el explorador para confirmar que el mensaje se ha actualizado. El valor del ejemplo anterior aparece de la siguiente forma:

   ![change.message](assets/changedmessage.png)

>[!NOTE]
>
>Es posible que la propiedad personalizada que acaba de crear no aparezca correctamente en el cuadro de diálogo Propiedades del formulario cuando vuelva a abrir el formulario. Sin embargo, funciona bien, y el formulario muestra el mensaje de la página cero actualizado.

>[!MORELIKETHIS]
>
>* [Descargue e instale Forms Designer para crear plantillas de documento de registro](/help/forms/installing-configuring-designer.md)
>* [Utilice Forms Designer para crear plantillas de documento de registro (DoR) y fragmentos de formulario?](/help/forms/use-forms-designer.md)
