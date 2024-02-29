---
title: Publicar un formulario de Edge Delivery Services de AEM Forms
description: Publicar un formulario de Edge Delivery Services de AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 1%

---


# Publicación del formulario

Una vez que esté listo para compartir el formulario con los clientes para la recopilación o el envío de datos, puede publicarlo de forma sencilla, para que los clientes puedan utilizarlo.

## Requisitos previos

* El [El bloque de formulario está habilitado para su proyecto EDS en Github](/help/edge/docs/forms/create-forms.md).
* El formulario está completamente probado y listo para usarse.
* Su [hoja de cálculo configurada](/help/edge/docs/forms/submit-forms.md) para aceptar datos.

## Publicación del formulario

Para publicar el formulario:

1. Acceda a su cuenta de Microsoft SharePoint o Google Drive y navegue hasta su `[AEM Edge Delivery project directory]`.

1. Abra un archivo de documento donde desee incrustar el formulario. Por ejemplo, puede abrir el archivo de índice o, alternativamente, crear un nuevo documento.

1. Identifique la sección deseada dentro del documento en la que desea insertar el formulario y navegue hasta ella según corresponda.

1. Agregue un bloque denominado &quot;Form&quot; al archivo, similar al ejemplo que se proporciona a continuación:

   | Formulario |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Este bloque sirve como marcador de posición donde está incrustado el formulario. En la segunda fila del bloque, añada la dirección URL de su `<form>.json` archivo como hipervínculo.

   >[!IMPORTANT]
   >
   >
   > Asegúrese de que la dirección URL tenga formato de hipervínculo en lugar de mostrarse como texto sin formato.

   Utilice la URL de vista previa (URL .page) con fines de desarrollo o prueba, o la URL de publicación (.live) para producción. Estos son ejemplos con URL de vista previa y publicación:

   **URL de previsualización**
| Form | |—| | [https://main--portal--wkndforms.hlx.page/enquiry.json](https://main--portal--wkndforms.hlx.page/enquiry.json)  |


   **URL de publicación**
| Form | |—| | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json)  |

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para previsualizar la página. La página ahora muestra el formulario. Por ejemplo, este es el formulario basado en [hoja de cálculo](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Formulario EDS de ejemplo](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Ahora, sus clientes pueden rellenar el formulario y enviarlo.

## Solución de problemas

+++ No se pueden enviar datos al formulario

Si aparece un error similar al siguiente mensaje, indica que la hoja de cálculo aún no está configurada para aceptar los datos enviados.

![error al enviar el formulario](/help/edge/assets/form-error.png)

+++


## Más información

* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)