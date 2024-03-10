---
title: Publicar un formulario de Edge Delivery Services de AEM Forms
description: Publicar un formulario de Edge Delivery Services de AEM Forms
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Publicación del formulario

Una vez que esté listo para compartir el formulario con los clientes para la recopilación o el envío de datos, puede publicarlo de forma sencilla, para que los clientes puedan utilizarlo.

![Ecosistema de creación basado en documentos](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Requisitos previos

* El [El bloque de Forms adaptable está habilitado para su proyecto EDS en GitHub](/help/edge/docs/forms/create-forms.md).
* El formulario está completamente probado y listo para usarse.
* Su [hoja de cálculo configurada](/help/edge/docs/forms/submit-forms.md) para aceptar datos.

## Publicación del formulario

+++ 1. Publique la hoja de cálculo

1. Abra la cuenta de Microsoft SharePoint o Google AEM Drive y vaya al directorio del proyecto de entrega perimetral de la red de distribución de la red de.

1. Abra la hoja de cálculo que contiene el formulario. Por ejemplo, la variable `enquiry` del libro de Excel de Microsoft.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para previsualizar la hoja.

   ![Usar el AEM Sidekick para obtener una vista previa de la hoja](/help/edge/assets/preview-form.png)

   Una vez finalizada correctamente la operación de previsualización, el contenido de la hoja de cálculo se convierte a formato JSON. A continuación, la página de vista previa presenta este contenido en un formato de tabla estructurado. Por ejemplo, la imagen adjunta ilustra el contenido de un formulario de &quot;consulta&quot;.

   ![Previsualización de Forms en formato JSON](/help/edge/assets/forms-preview-json-format.png)

1. Utilice el AEM Sidekick para publicar la hoja. Asegúrese de capturar la URL de publicación, ya que es necesaria para procesar el formulario en la siguiente sección. El formato de la URL es el siguiente:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   ```

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el repositorio del proyecto se llama &quot;portal&quot;, está ubicado en la cuenta &quot;wkndforms&quot; y está usando la rama &quot;principal&quot;, la dirección URL tiene el siguiente aspecto:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`

+++

+++ 2. Agregue el formulario a su página web

Añada el `<form>.json` a una página web para facilitar la interacción con los clientes, lo que permite a los rellenadores de formularios rellenar y enviar fácilmente el formulario.


Para agregar el formulario a la página web:

1. Acceda a su cuenta de Microsoft SharePoint o Google Drive y navegue hasta su `[AEM Edge Delivery project directory]`.

1. Abra un archivo de documento donde desee incrustar el formulario. Por ejemplo, puede abrir el `index.docx` o, alternativamente, crear un nuevo documento.

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

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa de la página web. La página ahora muestra el formulario. Por ejemplo, este es el formulario basado en [hoja de cálculo](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Formulario EDS de ejemplo](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

1. Utilice el AEM Sidekick para publicar el formulario. Ahora, sus clientes pueden rellenar el formulario y enviarlo.

+++

## Solución de problemas

+++ No se pueden enviar datos al formulario

Si aparece un error similar al siguiente mensaje, indica que la hoja de cálculo no está configurada para [aceptar los enviados](/help/edge/docs/forms/submit-forms.md) datos aún.

![error al enviar el formulario](/help/edge/assets/form-error.png)

+++




## Más información
