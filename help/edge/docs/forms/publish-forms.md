---
title: Publique un Edge Delivery Services para AEM Forms
description: Publique un Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: dcb16da1-dcc2-4529-8859-0716e727b54d
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 100%

---

# Publicar el formulario y empezar a recopilar datos

Una vez que esté listo para compartir el formulario con los clientes para la recopilación o el envío de datos, puede simplemente publicarlo, para que los clientes puedan utilizarlo.

![Ecosistema de creación basado en documentos](/help/edge/assets/document-based-authoring-workflow-publish-form.png)

## Requisitos previos

- Tiene un proyecto de AEM basado en [Formularios de AEM de elementos repetitivos](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [se ha añadido un Bloque de formularios adaptables al proyecto de AEM existente](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)
- El formulario está completamente probado y listo para usarse.
- Su [hoja de cálculo está configurada](/help/edge/docs/forms/submit-forms.md) para aceptar datos.


## Publicación del formulario

+++ &#x200B;1. Publique la hoja de cálculo

1. Abra su cuenta de Microsoft SharePoint o de Google Drive y vaya al directorio del proyecto de Edge Delivery de AEM.

1. Abra la hoja de cálculo que contiene el formulario. Por ejemplo, el libro de Microsoft Excel del formulario de [consulta](/help/edge/assets/enquiry.xlsx).

1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa de la hoja.

   ![Utilice AEM Sidekick para obtener una vista previa de la hoja](/help/edge/assets/preview-form.png)

   Una vez finalizada correctamente la operación de previsualización, el contenido de la hoja de cálculo se convierte a formato JSON. A continuación, la página de vista previa presenta este contenido en un formato de tabla estructurado. Por ejemplo, la imagen adjunta ilustra el contenido de un formulario de &quot;consulta&quot;.

   ![Vista previa de formularios en formato JSON](/help/edge/assets/forms-preview-json-format.png)

1. Utilice AEM Sidekick para publicar la hoja. Asegúrese de capturar la URL de publicación, ya que es necesaria para procesar el formulario en la siguiente sección. El formato de la dirección URL es el siguiente:


   ```JSON
       https://<branch>--<repository>--<owner>.aem.live/<form>.json
   ```

   - `<branch>` hace referencia a la rama del repositorio de GitHub.
   - `<repository>` indica su repositorio de GitHub.
   - `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el repositorio del proyecto se llama “wefinance”, está ubicado en la cuenta “wkndform” y se usa la rama “principal” y el formulario como &quot;consulta&quot;, la dirección URL tiene el siguiente aspecto:

   `https://main--wefinance--wkndform.aem.live/enquiry.json`
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry.json)-->

+++

+++ &#x200B;2. Añada el formulario a su página web

Añada `<form>.json` a una página web para facilitar la interacción con los clientes, lo que permite a los rellenadores de formularios rellenar y enviar fácilmente el formulario.


Para añadir el formulario a la página web:

1. Acceda a su cuenta de Microsoft SharePoint o Google Drive y navegue hasta su `[AEM Edge Delivery project directory]`.

1. Abra un archivo de documento donde quiera incrustar el formulario. Por ejemplo, puede abrir el archivo [enquiry-form.docx](/help/edge/assets/enquiry-form.docx) o, alternativamente crear un nuevo documento.

1. Identifique la sección deseada dentro del documento en la que quiere insertar el formulario y navegue hasta ella según corresponda.

1. Añada un bloque denominado &quot;Formulario&quot; al archivo. Por ejemplo, si el repositorio de su proyecto se llama “wefinance”, está ubicado bajo el propietario de la cuenta “wkndform” y utiliza la rama “principal”.

   | Formulario |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

   ![Añada un bloque denominado &quot;Form&quot; al archivo](/help/edge/assets/enquiry-doc-to-embed-form.png)

   Este bloque sirve como marcador de posición donde está incrustado el formulario. En la segunda fila del bloque, añada la dirección URL de su archivo `<form>.json` como hipervínculo.

   >[!IMPORTANT]
   >
   >
   > Asegúrese de que la dirección URL tenga formato de hipervínculo en lugar de mostrarse como texto sin formato.

   Utilice la URL de vista previa (URL .page) con fines de desarrollo o prueba o la URL de publicación (.live) para producción.

   Por ejemplo, si el repositorio de su proyecto se llama “wefinance”, está ubicado bajo el propietario de la cuenta “wkndform” y utiliza la rama “principal”.

   Estos son ejemplos con URL de vista previa y publicación:

   **URL de vista previa**

   | Formulario |
   |---|
   | `https://main--wefinance--wkndform.aem.page/enquiry.json` |


   **URL de publicación**

   | Formulario |
   |---|
   | `https://main--wefinance--wkndform.aem.live/enquiry.json` |

1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa de la página web. La página ahora muestra el formulario. Por ejemplo, este es el formulario basado en [hoja de cálculo de consulta](/help/edge/assets/enquiry-form.docx):


   ![Un formulario EDS de ejemplo](/help/edge/assets/updated-form.png)

1. Utilice el AEM Sidekick para publicar el formulario. Ahora, sus clientes pueden rellenar el formulario y enviarlo.

+++

## Solución de problemas

+++ No se pueden enviar datos al formulario

Si aparece un error similar al siguiente mensaje, indica que la hoja de cálculo no está configurada aún para [aceptar los datos enviados](/help/edge/docs/forms/submit-forms.md).

![error al enviar el formulario](/help/edge/assets/form-error.png)

+++



