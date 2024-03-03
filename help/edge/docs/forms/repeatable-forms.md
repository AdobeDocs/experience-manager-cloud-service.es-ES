---
title: Agregar secciones repetibles a un formulario
description: Adición de secciones repetibles a un formulario EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: fd2e5df72e965ea6f9ad09b37983f815954f915c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 13%

---


# Agregar secciones repetibles a un formulario

El bloque de formulario adaptable permite agregar o hacer repetible una sección o componente de un formulario.

Una sección repetible es un componente de un formulario que se duplica o replica varias veces para recopilar información de varias apariciones de datos similares.

Por ejemplo, considere un formulario utilizado para recopilar información sobre la experiencia laboral de una persona. Puede tener una sección repetible para capturar los detalles de cada trabajo anterior. La sección repetible generalmente contiene campos como nombre de la empresa, cargo, fechas de empleo y responsabilidades del puesto. El usuario puede agregar varias instancias de la sección repetible para introducir información sobre cada trabajo que ha realizado.



Al final de este artículo, aprenderá lo siguiente:

* [Creación de una sección repetible en un formulario](#add-repeatable-sections-to-a-form)
* [Establecer un número mínimo o máximo de repeticiones en un formulario](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Creación de una sección repetible en un formulario

La creación de una sección repetible en un formulario permite a los usuarios introducir varias instancias del mismo conjunto de datos, lo que permite recopilar de forma eficaz la información repetitiva. Para crear una sección repetible en un formulario:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo. Por ejemplo, abra una hoja de cálculo denominada `job-application.xlsx`.

1. Agregue un campo de formulario con la variable `type` propiedad establecida en `fieldset` y habilite la repetibilidad configurando `repeatable` hasta `true`. Además, especifique un `label` para el campo, ya que sirve como encabezado de la sección repetible.

   Consulte la siguiente imagen para ver una ilustración de una sección del historial laboral dentro de un formulario de solicitud de empleo.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. En el `Fieldset` de todos los campos que se van a incluir en una sección repetible, especifique la propiedad `Name` del conjunto de campos correspondiente.

   Por ejemplo, designe `experience` en la propiedad Fieldset de todos los campos relevantes que se van a incluir en la `employment history` sección.

   ![](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja. La sección repetible se agrega al formulario.

   Debajo de la sección repetible, los usuarios encuentran un **Añadir** botón, facilitando la adición de múltiples secciones con facilidad.

   ![sección repetible, busque un **Añadir** para añadir varias secciones ](/help/edge/assets/repeatable-section-example.png)


## Defina un número mínimo o máximo de repeticiones para una sección repetible

En el diseño de formularios, es beneficioso establecer repeticiones mínimas y máximas para secciones repetibles. Al hacerlo, establece el control y la coherencia y guía a los usuarios de forma eficaz. Para definir un número mínimo o máximo de repeticiones:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.

1. Configure las variables `min` para especificar el número mínimo de veces que se puede repetir la sección.

   ![Establezca la propiedad min y max para especificar el número de veces que se puede repetir la sección](/help/edge/assets/repeatable-section-set-min-max.png)

1. Configure las variables `max` para especificar el número máximo de veces que se puede repetir la sección.

1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

   Ahora, al agregar secciones repetibles, los usuarios encuentran un **Eliminar** , simplificando el proceso de eliminación de secciones repetibles. Una vez añadidas, estas secciones no se pueden reducir a menos instancias de las especificadas por el `min` propiedad. Esto garantiza el cumplimiento del requisito mínimo establecido para la cumplimentación del formulario.

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Form block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Service project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-sharepoint)._" 


To add repeatable sections in Edge Delivery:

1. [Author a form using Microsoft Excel](#author-form)
2. [Preview and publish the form](#preview-form)

### Author a form using Microsoft Excel {#author-form}

1. Go to your Edge Deliver project folder on Microsoft SharePoint or Google Workspace and open your spreadsheet. For example, open an a spreadsheet named `loan-application.xlsx`.

1. Add a new columns labeled `Repeatable` to the sheet contaning your form fields. By default, the `shared-default` sheet contains the form fields.  

1. Add new columns labeled as `Repeatable`, `Min`, and `Max` in your Microsoft Excel file.
1. Specify the value for the `Repeatable` column as `True` for the fieldset that you want to make repeatable.
1. Specify the values for the `Min` and `Max` columns. The `Min` value represents the minimum number of occurrences for which the panel repeats, while the `Max` value represents the maximum number of occurrences for which the panel repeats.
1. Save your Microsoft Excel file.
     
>[!NOTE]
>
> Here is the [Loan application](/help/forms/assets/loan-application.xlsx) excel sheet for your reference. 

### Preview/Publish the form using your Edge Delivery Service

1. Open or create new document file in a Microsft SharePoint Site to embed the Excel sheet  in it using a `Form Block`. For example, open the `index` file and add a `Form Block`.
2. Open the command prompt, navigate to your AEM Edge Delivery project directory on your local machine, and execute the command as `aem up`.

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## Más información

* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)
* [Componentes de formulario y sus propiedades](/help/edge/docs/forms/form-components.md)