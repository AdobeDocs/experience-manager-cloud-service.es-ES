---
title: Usar el flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro
seo-title: Using AEM translation workflow to localize Adaptive Forms and Document of Record
description: Aprenda a utilizar los flujos de trabajo de traducción AEM para localizar formularios adaptables y documentos de registro.
seo-description: Learn to use AEM translation workflows to localize Adaptive Forms and Document of Record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: ht
source-wordcount: '538'
ht-degree: 100%

---


# Usar el flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Los formularios localizados le ayudan a llegar a una audiencia más amplia en todas las regiones geográficas. El flujo de trabajo de traducción de Adobe Experience Manager le ayuda a localizar formularios adaptables y sus documentos de registro. Puede usar la **traducción automática** o **traductores humanos** para localizar un formulario adaptable.

Este artículo explica el proceso para utilizar el flujo de trabajo de traducción de AEM con formularios adaptables y documentos de registro.

## Localizar un formulario adaptable y un documento de registro mediante traducción automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

El servicio de traducción automática traduce inmediatamente el contenido de los formularios adaptables y los documentos de registro. [!DNL AEM Forms] está preconfigurado para utilizar una versión de prueba de [!DNL Microsoft Translator] para la traducción automática. Realice los siguientes pasos para habilitar la traducción automática en los formularios adaptables y los documentos de registro:

1. En la IU de [!DNL AEM Forms], seleccione un formulario y pulse el botón **Agregar diccionario**.
1. En la pantalla **Agregar diccionario al proyecto de traducción**, seleccione las opciones **Crear un nuevo proyecto de traducción** o **Agregar a un proyecto de traducción existente**.
1. En el campo **Título del proyecto**, especifique el título. Por ejemplo, `Government Reference Site - German locale.`
1. En el campo **Idiomas de destino**, especifique una configuración regional (por ejemplo, `German(de)`) y haga clic en **Listo**. Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en el campo **Idiomas de destino**.
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**. En la pantalla Proyectos, abra el proyecto recién creado.
1. Haga clic en los **puntos suspensivos** que aparecen en la parte inferior del mosaico **Resumen de la traducción**. Se abre la pantalla Resumen de la traducción.
1. Haga clic en el icono **Editar** que aparece en la parte superior de la pantalla **Resumen de la traducción**. Abra la pestaña **Traducción** y seleccione Traducción automática en la pantalla **Método de traducción**. Seleccione el **Proveedor de traducción** y la **Configuración en la nube** adecuados. Haga clic en el icono **Listo** que aparece en la parte superior de la pantalla.
1. En el mosaico **Trabajo de traducción**, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y luego haga clic en **Iniciar**. El estado del mosaico cambia a Borrador. Al finalizar la traducción, el estado cambia a **Listo para revisión**. Actualice la página después de unos minutos y verifique el estado.
1. Una vez que el estado haya cambiado a **Listo para revisión** en el mosaico **Trabajo de traducción**, abra el formulario en una ventana del explorador. Se muestra una versión localizada del formulario.

   >[!NOTE]
   >
   >* Antes de abrir la versión localizada del formulario en la ventana del explorador, asegúrese de que la configuración regional del explorador esté establecida de forma que coincida con la configuración regional del formulario. Por ejemplo, si el formulario se traduce al alemán (de), establezca la configuración regional del explorador en alemán (de).
   >* Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.

   Junto con el formulario adaptable, también se localiza el documento de registro generado automáticamente.

   Para obtener más información sobre la configuración y las opciones del documento de registro, consulte:

[Configuración de la plantilla de un documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configuración del documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalice la información de marca del documento de registro](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) y asegúrese de que la configuración regional del explorador está establecida en el mismo idioma en el que ha localizado el formulario adaptable mediante lenguaje de máquina. La configuración regional del explorador ayuda a localizar la información de marca en el documento de registro.
1. Para ver el documento de registro localizado, pulse Generar previsualización. El PDF del documento de registro se genera y abre en una nueva pestaña del explorador.

<!-- ## Localizing an Adaptive Form and its Document of Record using Human Translation {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

In Human translation the content is sent to a translation provider and translated by professional translators. When complete, the translated content is returned and imported into AEM. When your translation provider is integrated with AEM, content is automatically sent between AEM and the translation provider.

For translation, a dictionary containing files in XLIFF format is shared with the professional translators. The dictionary includes a separate XLIFF file for each locale. Each XLIFF file contains text that is displayed to the end users and placeholders for the corresponding localized text.

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

