---
title: Traduce y localiza un Edge Delivery Services para AEM Forms
description: Traduce y localiza un Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 8a0c826f-8acc-4a00-bd84-7b0df9a82457
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 100%

---


# Traduce y localiza un Edge Delivery Services para AEM Forms

En Edge Delivery Services, la traducción de formularios implica convertir el contenido de los formularios de un idioma a otro con un enfoque en la precisión, claridad y coherencia. Los formularios traducidos o localizados permiten llegar a un público más amplio en diferentes ubicaciones geográficas, lo que mejora la experiencia del usuario y facilita una mejor comunicación entre las distintas preferencias de idioma.


Al final de este artículo, aprenderá lo siguiente:

- [A traducir formularios en Google Drive](#translate-form-google-drive)
- [A traducir formularios en el sitio de SharePoint](#translate-form-sharepoint)

## A traducir formularios en Google Drive {#translate-form-google-drive}

La función `GOOGLETRANSLATE` de Hojas de cálculo de Google traduce formularios al pulsar en una herramienta de traducción integrada, cambiando el texto de un idioma a otro directamente en una hoja de Google. Para traducir formularios en Google Drive:

1. Vaya a la carpeta Proyecto de AEM en Google Drive y abra su hoja de Google.
2. Cambie el nombre de la hoja existente (`shared-default`) por `shared-en`.
3. Añada una hoja con el nombre `shared-default`. La hoja `shared-default` contiene el contenido para la localización en un idioma específico.
4. Añada el contenido localizado en la hoja `shared-default` utilizando la función `GOOGLETRANSLATE`.
Puede utilizar una fórmula para traducir el contenido de la celda D2 desde la hoja `shared-en` al francés dentro de la hoja `shared-default`. Esta es la fórmula que debe utilizar:
   `=GOOGLETRANSLATE('shared-en'!D2,"en","fr")`

   ![Hoja de cálculo Enquiry Translate](/help/forms/assets/translate-enquiry-spreadsheet.png)

5. Previsualice y publique mediante [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Puede consultar la [hoja de cálculo](/help/forms/assets/enquirytranslate.xlsx) que contiene la definición de formulario para un formulario `enquiry` traducido del idioma inglés a francés.

![Formulario Enquiry Translated](/help/forms/assets/translate-form-french.png)

Consulte la siguiente URL, donde puede ver el formulario con su traducción al francés: 
https://main--portal--wkndforms.hlx.live/enquirytranslate

## A traducir formularios en el sitio de SharePoint{#translate-form-sharepoint}

Para traducir los formularios en el sitio de Microsoft® SharePoint, debe cambiar manualmente las etiquetas de los campos mediante cualquier servicio de traducción. Para traducir los formularios en un sitio de SharePoint:

1. Vaya a la carpeta Proyecto de AEM en Microsoft® SharePoint y abra la hoja de cálculo.
2. Cambie el nombre de la hoja existente (`shared-default`) por `shared-en`.
3. Añada una hoja con el nombre `shared-default`. La hoja `shared-default` contiene el contenido para la localización en un idioma específico.
4. Añada el contenido localizado en la hoja `shared-default` manualmente.

   ![Hoja de cálculo Enquiry Translate](/help/forms/assets/translate-enquiry-sp-spreadsheet.png)

5. Previsualice y publique la hoja mediante [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

Consulte la [hoja de cálculo](/help/forms/assets/enquirytranslate-sp.xlsx) que contiene la definición de formulario para un formulario `enquiry` traducido del idioma inglés a francés.

![Formulario Enquiry Translated](/help/forms/assets/translate-form-french.png)

Consulte la siguiente URL, donde puede ver el formulario con su traducción al francés: 
https://main--wefinance--wkndforms.hlx.live/enquirytranslate

## Problemas conocidos {#known-issues}

- Las etiquetas del formulario se traducen al idioma localizado especificado en la hoja `shared-default`, pero los mensajes de error se muestran en el idioma predeterminado del explorador.

  ![Mensaje de error](/help/forms/assets/translate-error-message.png)

- Al abrir el calendario, la lista desplegable de calendario se muestra en el idioma predeterminado del explorador.

  ![Mensaje de error](/help/forms/assets/translate-calender-display.png)


## Preguntas frecuentes {#faq}

**P**: ¿Cómo puedo escribir los datos en el idioma localizado especificado en un formulario?

**R**: para introducir texto en un idioma localizado específico, ajuste la configuración de teclado en el dispositivo. Consulte los siguientes vínculos para obtener instrucciones sobre cómo hacerlo:

- [Configure su Mac para recibir entradas en otro idioma](https://support.apple.com/es-ES/guide/mac-help/mchlp1406/mac)
- [Configure su Windows para recibir entradas en otro idioma](https://support.microsoft.com/es-ES/windows/manage-the-input-and-display-language-settings-in-windows-12a10cb4-8626-9b77-0ccb-5013e0c7c7a2#:~:text=Select%20the%20Start%20%3E%20Settings%20%3E%20Time,you%20want%2C%20then%20select%20Options)
- [Configure su Android o iPhone/iPads para recibir entradas en otro idioma](https://support.google.com/gboard/answer/7068494?hl=en&co=GENIE.Platform%3DAndroid)


**P**: ¿Cómo puedo recuperar una lista de configuraciones regionales utilizadas en la función `GOOGLETRANSLATE`?

**R**: Puede consultar la [documentación oficial de Google](https://cloud.google.com/translate/docs/languages) para obtener una lista completa de las configuraciones regionales utilizadas en el TRADUCTOR DE GOOGLE.


