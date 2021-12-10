---
title: Uso de AEM flujo de trabajo de traducción para localizar Forms adaptable y Documento de registro
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: Aprenda a utilizar flujos de trabajo de traducción AEM para localizar Forms adaptable y Documento de registro.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---


# Uso de AEM flujo de trabajo de traducción para localizar Forms adaptable y Documento de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Los formularios localizados le ayudan a llegar a una audiencia más amplia en todas las regiones geográficas. El flujo de trabajo de traducción de Adobe Experience Manager le ayuda a localizar Adaptive Forms y sus documentos de registro . Puede usar **traducción automática** o **traductores humanos** para localizar un formulario adaptable.

Este artículo explica el proceso para utilizar AEM flujo de trabajo de traducción con Adaptive Forms y documentos de registro.

## Localización de un formulario adaptable y un documento de registro mediante traducción automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

El servicio de traducción automática traduce inmediatamente su contenido en Formulario adaptable y Documento de registro. [!DNL AEM Forms] está preconfigurado para utilizar una versión de prueba de [!DNL Microsoft Translator] para traducción automática. Realice los siguientes pasos para habilitar la traducción automática para su Forms adaptable y documento de registro:

1. En el [!DNL AEM Forms] IU, seleccione un formulario y pulse el botón **Agregar diccionario** .
1. En **Agregar diccionario a proyecto de traducción** seleccione **Crear un nuevo proyecto de traducción** o **Agregar a un proyecto de traducción existente** .
1. En el **Título del proyecto** , especifique el título. Por ejemplo, `Government Reference Site - German locale.`
1. En el **Idiomas de destino** , especifique una configuración regional (por ejemplo, `German(de)`) y haga clic en **Listo**. Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en la variable **Idiomas de destino** campo .
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**. En la pantalla Proyectos , abra el proyecto recién creado.
1. Haga clic en el **elipses** en la parte inferior del **Resumen de traducción** mosaico. Se abre la pantalla Resumen de traducción .
1. Haga clic en el **Editar** en la parte superior del **Resumen de traducción** en el Navegador. Abra el **Traducción** y seleccione Traducción automática en la **Método de traducción** en el Navegador. Seleccione el **Proveedor de traducción** y **Configuración de nube**. Haga clic en el **Listo** en la parte superior de la pantalla.
1. En el **Trabajo de traducción** , haga clic en el botón ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y haga clic en **Inicio**. El estado del mosaico cambia a Borrador. Al finalizar la traducción, el estado cambia a **Listo para revisión**. Actualice la página después de unos minutos y verifique el estado.
1. Después de que el estado cambie a **Listo para revisión** en el **Trabajo de traducción** , abra el formulario en una ventana del explorador. Se muestra una versión localizada del formulario.

   >[!NOTE]
   >
   >* Antes de abrir la versión localizada del formulario en la ventana del explorador, asegúrese de que la configuración regional del explorador esté configurada para que coincida con la configuración regional del formulario. Por ejemplo, si el formulario se traduce al alemán(de) , establezca la configuración regional del explorador en alemán(de).
   >* Los componentes de Formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL). Por ejemplo, hebreo.


   Junto con el formulario adaptable, también está localizado el documento de registro generado automáticamente.

   Para obtener más información sobre la configuración y configuración del documento de registro, consulte:

[Configuración del documento de plantilla de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configuración del documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalización de la información de marca del documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) y asegúrese de que la configuración regional del explorador está configurada en el mismo idioma en el que ha localizado el formulario adaptable mediante el lenguaje del equipo. La configuración regional del explorador ayuda a localizar la información de marca en el Documento de registro.
1. Para ver el documento de registro localizado, pulse Generar previsualización. El PDF Documento de registro se genera y abre en una nueva pestaña del explorador.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that will be displayed to the end users and placeholders for the corresponding localized text.

Perform the following steps to localize a form and its Document of Record using Human Translators:

1. [Connect AEM with your translation service provider](/help/sites-administering/tc-tic.md) and [create translation integration framework configurations](/help/sites-administering/tc-tic.md).

1. [Associate the pages of your language master](/help/sites-administering/tc-tic.md) with the translation service and framework configurations.

1. [Identify the type of content](/help/sites-administering/tc-rules.md) to translate.

1. [Prepare the content for translation](/help/sites-administering/tc-prep.md) by authoring the language master and creating the root pages of language copies.

1. [Create translation projects](/help/sites-administering/tc-manage.md) to gather the content to translate and to prepare the translation process.

1. Use the translation projects to [manage the content translation process](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Adaptive Form components do not support right to left (RTL) languages. For example, Hebrew.
> -->

