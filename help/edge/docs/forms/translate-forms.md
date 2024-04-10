---
title: Traducción y localización de un formulario de Edge Delivery Services de AEM Forms
description: Traducción y localización de un formulario de Edge Delivery Services de AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
source-git-commit: eadfc3d448bd2fadce08864ab65da273103a6212
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 6%

---


# Traducción y localización de un formulario de Edge Delivery Services de AEM Forms

En los Edge Delivery Services, la traducción de formularios implica convertir el contenido de los formularios de un idioma a otro con un enfoque en la precisión, la claridad y la coherencia. Los formularios traducidos o localizados permiten un mayor alcance de la audiencia en diferentes ubicaciones geográficas, lo que mejora la experiencia del usuario y facilita una mejor comunicación entre las distintas preferencias de idioma.


Al final del artículo, aprenderá a hacer lo siguiente:

* [Traducir formularios en Google Drive](#translate-form-google-drive)
* [Traducir formularios en el sitio de SharePoint](#translate-form-sharepoint)

## Traducir formularios en Google Drive {#translate-form-google-drive}

El `GOOGLETRANSLATE` La función de Google sheets traduce formularios al pulsar en una herramienta de traducción integrada y cambiar el texto de un idioma a otro directamente en una hoja de Google. Para traducir formularios en Google Drive:

1. AEM Vaya a la carpeta Proyecto de la en Google Drive y abra la hoja de Google.
2. Cambie el nombre de la hoja existente (`shared-default`) a `shared-en`.
3. Añada una hoja con el nombre `shared-default`. El `shared-default` Esta hoja contiene el contenido para la localización en un idioma específico.
4. Añada el contenido localizado en `shared-default` hoja que utiliza el `GOOGLETRANSLATE` función.
Puede utilizar una fórmula para traducir el contenido de la celda D2 desde el `shared-en` en francés dentro de la `shared-default` hoja. Esta es la fórmula que se debe utilizar:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Consulta Traducir hoja de cálculo](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Vista previa y publicación de la hoja mediante [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Puede consultar el [hoja de cálculo](/help/forms/assets/enquirytranslate.xlsx) que contiene la definición del formulario para un `enquiry` formulario traducido de inglés a francés.

![Formulario traducido de consulta](/help/forms/assets/translate-form-french.png)

Consulte la siguiente URL, donde puede ver el formulario con su traducción al francés: https://main--portal--wkndforms.hlx.live/enquirytranslate

## Traducir formularios en el sitio de SharePoint{#translate-form-sharepoint}

Para traducir los formularios en el sitio de Microsoft® SharePoint, debe cambiar manualmente las etiquetas de los campos mediante cualquier servicio de traducción. Para traducir los formularios en un sitio de SharePoint:

1. AEM Vaya a la carpeta Proyecto de en Microsoft® SharePoint y abra la hoja de cálculo.
2. Cambie el nombre de la hoja existente (`shared-default`) a `shared-en`.
3. Añada una hoja con el nombre `shared-default`. El `shared-default` Esta hoja contiene el contenido para la localización en un idioma específico.
4. Añada el contenido localizado en `shared-default` hoja manualmente.

   ![Consulta Traducir hoja de cálculo](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Vista previa y publicación de la hoja mediante [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Consulte la [hoja de cálculo](/help/forms/assets/enquirytranslate-sp.xlsx) que contiene la definición del formulario para un `enquiry` formulario traducido de inglés a francés.

![Formulario traducido de consulta](/help/forms/assets/translate-form-french.png)

Consulte la siguiente URL, donde puede ver el formulario con su traducción al francés: https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemas conocidos {#known-issues}

* Las etiquetas del formulario se traducen al idioma localizado especificado en la `shared-default` , pero los mensajes de error se muestran en el idioma predeterminado del explorador.

  ![Mensaje de error](/help/forms/assets/translate-error-message.png)

* Al abrir el calendario, la lista desplegable de calendario se muestra en el idioma predeterminado del explorador.

  ![Mensaje de error](/help/forms/assets/translate-calender-display.png)


## Preguntas frecuentes {#faq}

**Q**: ¿Cómo puedo escribir los datos en el idioma localizado especificado en un formulario?

**A**: para introducir texto en un idioma localizado específico, ajuste la configuración de teclado en el dispositivo. Consulte los siguientes vínculos para obtener instrucciones sobre cómo hacerlo:

* [Configure su Mac para recibir entradas en otro idioma](https://support.apple.com/en-in/guide/mac-help/mchlp1406/mac)
* [Configure su Windows para recibir entradas en otro idioma](https://support.microsoft.com/en-us/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
* [Configure su Android o iPhone/iPads para recibir entradas en otro idioma](https://support.google.com/gboard/answer/7068494?hl=en&amp;co=GENIE.Platform%3DAndroid)


**Q**: ¿Cómo puedo recuperar una lista de configuraciones regionales utilizadas en la `GOOGLETRANSLATE` función?

**A**: Puede consultar el [documentación oficial de Google](https://cloud.google.com/translate/docs/languages) para obtener una lista completa de las configuraciones regionales utilizadas en GOOGLETRANSLATE.

## Consulte también

{{see-more-forms-eds}}

