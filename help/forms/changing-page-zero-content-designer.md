---
title: Cambiar el contenido de la página cero en Designer
description: Cambie el mensaje que se muestra en la página cero de un PDF de XFA para los visualizadores PDF que no son de Adobe.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms
role: User
exl-id: 726ba8a8-bfa4-44ac-8e74-e86a32505f36
source-git-commit: a9adbb1886dcfedfc3fccb6f56939c46ba1365ee
workflow-type: ht
source-wordcount: '246'
ht-degree: 100%

---

# Cambiar el contenido de la página cero en Designer {#changing-page-zero-content-in-designer}

El contenido de la página cero se muestra de forma predeterminada cuando un visor que no es Adobe PDF, como el visor de PDF predeterminado de [!DNL Chrome] o [!DNL Firefox], no puede leer el contenido del formulario PDF/XFA. A continuación, se muestra el mensaje predeterminado de la página cero.

![defaultpage0message](assets/defaultpage0message.png)

La versión de Designer de [!DNL AEM Forms] permite cambiar el mensaje que se muestra en la página cero. Para cambiar el mensaje de la página cero, realice los siguientes pasos:

1. Asegúrese de que ha instalado la versión de Designer de [!DNL AEM Forms]. Puede comprobar la versión desde la pantalla Acerca de Designer.

1. Abra el formulario para el cual desea cambiar el contenido de la página cero.

1. Haga clic en **[!UICONTROL Archivo]** > **[!UICONTROL Propiedades del formulario]**.

1. En el cuadro de diálogo [!UICONTROL Propiedades del formulario], haga clic en ![plus](assets/plus.png) (icono + ) para añadir una propiedad personalizada.

1. Especifique **_pagezerocontent** como el nombre de la propiedad.
1. Agregue el nuevo mensaje de la página cero en formato de texto enriquecido como valor. Por ejemplo:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download_es.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Guarde el formulario como PDF.

1. Vea el formulario PDF en el explorador para confirmar que el mensaje se ha actualizado. El valor del ejemplo anterior aparece de la siguiente forma:

   ![change.message](assets/changedmessage.png)

>[!NOTE]
>
>Es posible que la propiedad personalizada que has creado no aparezca correctamente en el cuadro de diálogo Propiedades del formulario cuando vuelvas a abrir el formulario. Sin embargo, funciona bien, y el formulario muestra el mensaje de la página cero actualizado.

>[!MORELIKETHIS]
>
>* [Descargar e instalar Forms Designer para crear plantillas de documento de registro](/help/forms/installing-configuring-designer.md)
>* [Utilice Forms Designer para crear plantillas de documento de registro (DoR) y fragmentos de formulario](/help/forms/use-forms-designer.md)
