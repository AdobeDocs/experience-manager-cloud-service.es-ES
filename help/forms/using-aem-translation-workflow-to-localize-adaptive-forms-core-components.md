---
title: ¿Cómo se puede traducir un formulario adaptable basado en componentes principales?
description: Aprenda a crear un modelo de datos de formulario en AEM Forms, probarlo con datos y servicios de muestra y configurar varias opciones para un modelo.
feature: Adaptive Forms, Core Components
exl-id: ad46bf0f-e6ec-4c52-9695-5768a9968e16
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 100%

---

# Utilizar la traducción automática o la traducción humana para traducir un formulario adaptable basado en componentes principales {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

Los formularios localizados le ayudan a llegar a una audiencia más amplia en todas las regiones geográficas. El flujo de trabajo de traducción de Adobe Experience Manager le ayuda a localizar formularios adaptables y sus documentos de registro. Puede usar la **traducción automática** o **traductores humanos** para localizar un formulario adaptable.

## Traducir un formulario adaptable y un documento de registro mediante el uso de traducción automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

El servicio de traducción automática traduce inmediatamente el contenido de los formularios adaptables y los [documentos de registro](/help/forms/generate-document-of-record-core-components.md). AEM Forms as a Cloud Service está preconfigurado para utilizar una versión de prueba de Microsoft Translator para la traducción automática. Realice los siguientes pasos para habilitar la traducción automática en los formularios adaptables y los documentos de registro:

1. En la interfaz de usuario de AEM Forms, selecciona un formulario y selecciona la opción **[!UICONTROL Agregar diccionario]**.
1. En la pantalla Agregar diccionario al proyecto de traducción, para la opción de **[!UICONTROL Proyecto]**

   * Para crear un proyecto de traducción, seleccione la opción de **[!UICONTROL Creación de un nuevo proyecto de traducción]** y en el campo de **Título del proyecto**, especifique el título. Por ejemplo, `Government Reference Site - German locale.`
   * Para añadir un nuevo diccionario a un proyecto de traducción existente, seleccione la opción de **[!UICONTROL Añadir a un proyecto de traducción existente]** y seleccione un **[!UICONTROL Proyecto de traducción existente]**.
1. En el campo **Idiomas de destino**, especifique una configuración regional (por ejemplo, `German(de)`). Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en el campo **Idiomas de destino.** Haga clic en **Listo**.
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**.
1. En la pantalla Proyectos, haga clic en el proyecto creado. Por ejemplo, haga clic en **Sitio de referencia del gobierno - configuración regional en alemán**.
1. En el mosaico **Trabajo de traducción**, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y luego haga clic en **Iniciar**. El estado del mosaico cambia a Borrador. Al finalizar la traducción, el estado cambia a **Aprobado**. Actualice la página después de unos minutos y verifique el estado.

   ![Iniciar traducción](/help/forms/assets/adaptive-forms-core-components-start-translation.png)
1. Después, el estado cambia a **Aprobado** en el **Trabajo de traducción**, haga clic en el icono de ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y haga clic en **Completar**.

1. Para obtener una vista previa del formulario localizado, en la IU de AEM Forms, seleccione el formulario localizado. Haga clic en **[!UICONTROL Vista previa]** >**[!UICONTROL Vista previa como HTML]**. Vuelva a abrir el formulario después de agregar `afAcceptLang=<locale code>` a la dirección URL del formulario. Por ejemplo, añada `afAcceptLang=de`para abrir la versión en alemán del formulario.


   >[!NOTE]
   >
   >* Antes de abrir la versión localizada del formulario en la ventana del explorador, asegúrese de que la configuración regional del explorador esté establecida de forma que coincida con la configuración regional del formulario. Por ejemplo, si el formulario se traduce al alemán (de), establezca la configuración regional del explorador en alemán (de).
   >* Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.

<!-- 
   Along with the Adaptive form, the auto-generated document of record is also localized.

   For more information on Document of Record settings and configuration, see:

   [Document of Record Template](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [Document of Record settings](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Customize the branding information of the document of record](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) and ensure that the browser locale is set to the same language to which you have localized the Adaptive Form using machine language. The browser locale helps localize the branding information in the document of record.
1. To view the localized document of record, select Generate Preview. The document of record PDF is generated and opened in a new tab in your browser.

-->

## Localizar un formulario adaptable y su documento de registro mediante traducción humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

En la traducción humana, el contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente a AEM y al proveedor de traducción.

Para la traducción, un diccionario que contiene archivos en formato XLIFF se comparte con los traductores profesionales. El diccionario incluye un archivo XLIFF independiente para cada configuración regional. Cada archivo XLIFF contiene texto que se mostrará a los usuarios finales y marcadores de posición para el texto localizado correspondiente.

Realice los siguientes pasos para localizar un formulario y su documento de registro mediante traductores humanos:

1. En la interfaz de usuario de AEM Forms, selecciona un formulario y selecciona la opción **[!UICONTROL Agregar diccionario]**.
1. En la pantalla Agregar diccionario al proyecto de traducción, para la opción de **[!UICONTROL Proyecto]**

   * Para crear un proyecto de traducción, seleccione la opción de **[!UICONTROL Creación de un nuevo proyecto de traducción]** y en el campo de **Título del proyecto**, especifique el título. Por ejemplo, `Government Reference Site - German locale.`
   * Para añadir un nuevo diccionario a un proyecto de traducción existente, seleccione la opción de **[!UICONTROL Añadir a un proyecto de traducción existente]** y seleccione un **[!UICONTROL Proyecto de traducción existente]**.
1. En el campo **Idiomas de destino**, especifique una configuración regional (por ejemplo, `German(de)`). Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en el campo **Idiomas de destino.** Haga clic en **Listo**.
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**.
1. En la pantalla Proyectos, haga clic en el proyecto creado. Por ejemplo, haga clic en **Sitio de referencia del gobierno - configuración regional en alemán**.
1. En la parte inferior del **Resumen**, haga clic en las **elipses**. Se abre la pantalla Propiedades del proyecto de traducción.
1. Abra la pestaña **[!UICONTROL Avanzadas]** en la parte superior de la pantalla **Propiedades del proyecto de traducción**. Para el **[!UICONTROL Campo de traducción]**, seleccione **[!UICONTROL Traducción humana]**. Haga clic en **Guardar y cerrar** en la parte superior de la pantalla.
1. En **Trabajo de traducción**, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y, a continuación, haga clic en **Exportar**. En el cuadro de diálogo Exportar, haga clic en la opción Descargar archivo exportado. Descarga un archivo .zip.
   ![Exportar archivo de traducción](/help/forms/assets/adaptive-forms-core-components-start-translation-export.png)
1. Extraer el archivo .zip descargado. La carpeta extraída tiene dos archivos:
   * translation_export_summary.xml
   * [form-fields-file].xml.
1. Abra el [form-fields-file].xml para editar. Agregue las cadenas y mensajes localizados para los campos de formulario. Guarde y cierre el archivo.
1. Comprima los archivos translation_export_summary.xml y [form-fields-file].xml.
1. En **Trabajo de traducción**, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y luego haga clic en **Importar**. Seleccione el archivo que contiene [form-fields-file].xml. con cadenas y mensajes localizados para campos de formulario.

   ![Importar archivo de traducción](/help/forms/assets/adaptive-forms-core-components-start-translation-import.png)

1. Para obtener una vista previa del formulario localizado, en la IU de AEM Forms, seleccione el formulario localizado. Haga clic en **[!UICONTROL Vista previa]** >**[!UICONTROL Vista previa como HTML]**. Vuelva a abrir el formulario después de agregar `afAcceptLang=<locale code>` a la dirección URL del formulario. Por ejemplo, añada `afAcceptLang=de`para abrir la versión en alemán del formulario.

## Ver también {#see-also}

{{see-also}}