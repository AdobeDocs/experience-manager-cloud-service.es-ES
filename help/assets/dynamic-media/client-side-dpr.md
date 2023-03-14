---
title: Uso de imágenes inteligentes con proporción de píxeles de dispositivo del lado del cliente
description: Aprenda a utilizar la proporción de píxeles de dispositivo del lado del cliente con imágenes inteligentes en Adobe Experience Manager as a Cloud Service con Dynamic Media.
contentOwner: Rick Brough
role: Admin,User
exl-id: 556710c7-133c-487a-8cd9-009a5912e94c
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Acerca de las imágenes inteligentes con proporción de píxeles de dispositivo (DPR) del lado del cliente {#client-side-dpr}

La solución actual de imágenes inteligentes utiliza cadenas del agente de usuario para determinar el tipo de dispositivo (escritorio, tableta, móvil, etc.) que se está utilizando.

Las funcionalidades de detección de dispositivos (DPR basadas en cadenas del agente de usuario) suelen ser inexactas, especialmente para dispositivos Apple. Además, cada vez que se inicie un nuevo dispositivo, debe validarse.

El RGPD del lado del cliente le proporciona valores de precisión del 100 % y funciona para cualquier dispositivo, ya sea Apple o cualquier otro dispositivo nuevo que se haya iniciado.

<!-- See also [About network bandwidth optimization](/help/assets/dynamic-media/imaging-faq.md#network-bandwidth-optimization). -->

## Usar el código DPR del lado del cliente

**Aplicaciones procesadas del lado del servidor**

1. Cargar inicialización del trabajador de servicio (`srvinit.js`) al incluir la siguiente secuencia de comandos en la sección de encabezado de la página del HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   El Adobe recomienda cargar este script _antes_ cualquier otro script para que el trabajador de servicio inicie la inicialización de inmediato.

1. Incluya el siguiente código de etiqueta de imagen DPR en la parte superior de la sección del cuerpo de la página de HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   Es obligatorio incluir este código de etiqueta de imagen DPR _antes_ todas las imágenes estáticas de la página del HTML.

**Aplicaciones procesadas del lado del cliente**

1. Incluya los siguientes scripts de DPR en la sección de encabezado de la página de HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   Puede combinar ambos scripts de DPR en uno para evitar varias solicitudes de red.

   El Adobe recomienda cargar estos scripts _antes_ cualquier otro script de la página del HTML.
El Adobe también recomienda almacenar la aplicación en Bootstrap con la etiqueta de HTML de diferencia en lugar de con un elemento de cuerpo. La razón es porque `dprImageInjection.js` inserta dinámicamente la etiqueta de imagen en la parte superior de la sección del cuerpo en la página del HTML.

## Descarga de archivos JavaScript {#client-side-dpr-script}

Los siguientes archivos JavaScript de la descarga se proporcionan solo como referencia de ejemplo. Si tiene intención de utilizar estos archivos en páginas de HTML, asegúrese de editar el código de cada archivo para adaptarlo a sus necesidades.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Descarga de archivos JavaScript](/help/assets/dynamic-media/assets/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md)

