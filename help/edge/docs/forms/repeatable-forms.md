---
title: Añadir secciones repetibles a un formulario
description: Adición de secciones repetibles a un formulario EDS
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: 6612abbd95599791ff9571b59154aa8ab34fb5f8
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 100%

---

# Añadir secciones repetibles a un formulario

El bloque de Formularios adaptables permite agregar o hacer repetible una sección o componente de un formulario. Esto permite a los usuarios introducir información varias veces para el mismo tipo de datos, lo que facilita la recopilación de información, como la experiencia laboral o los antecedentes educativos.

Por ejemplo, considere un formulario utilizado para recopilar información sobre la experiencia laboral de una persona. Puede tener una sección repetible para capturar los detalles de cada trabajo anterior. La sección repetible generalmente contiene campos como nombre de la empresa, cargo, fechas de empleo y responsabilidades del puesto. El usuario puede agregar varias instancias de la sección repetible para introducir información sobre cada trabajo que ha realizado.

Al final de este artículo, aprenderá lo siguiente:

* [Crear una sección repetible en un formulario](#add-repeatable-sections-to-a-form)
* [Establecer un número mínimo o máximo de repeticiones en un formulario](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

## Crear una sección repetible

La creación de una sección repetible en un formulario permite a los usuarios introducir varias instancias del mismo conjunto de datos, lo que permite recopilar de forma eficaz la información repetitiva. Para crear una sección repetible en un formulario, haga lo siguiente:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.

1. Agregue un campo de formulario con la propiedad `type` establecida en `fieldset`
1. Especifique el código `Name` del campo. La propiedad nombre se utiliza para crear una sección repetible.
1. Habilitar la repetibilidad estableciendo `repeatable` en `true`.
1. Especifique el elemento descriptivo `label` para el campo. Sirve como encabezado para la sección repetible.

   Consulte la siguiente imagen para ver una ilustración de una sección del historial laboral dentro de un formulario de solicitud de empleo.

   ![](/help/edge/assets/repeatable-section-example-job-application-form.png)

1. Para cada campo que desee incluir en la sección, establezca su propiedad `Fieldset` con el mismo nombre elegido en el paso 3.

   Por ejemplo, designe `experience` en la propiedad Fieldset de todos los campos relevantes que se van a incluir en la sección `employment history`.

   ![ejemplo de un campo de sección repetible y sus propiedades](/help/edge/assets/repeatable-section--mention-fieldset-name-example-job-application-form.png)

1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja. La sección repetible se agrega al formulario.

   Debajo de la sección repetible, los usuarios encuentran el botón **Añadir**, que facilita la adición de múltiples secciones con facilidad.

   ![sección repetible, botón Añadir, para agregar varias secciones ](/help/edge/assets/repeatable-section-example.png)


## Configuración de repeticiones mínimas y máximas

En el diseño de formularios, es beneficioso establecer repeticiones mínimas y máximas para secciones repetibles. Al hacerlo, establece el control y la coherencia, y guía a los usuarios de forma eficaz. Para definir un número mínimo o máximo de repeticiones, haga lo siguiente:

1. Vaya a la carpeta del proyecto Edge Deliver en Microsoft SharePoint o Google Workspace y abra la hoja de cálculo.

1. Para un campo de `type` y `fieldset` y propiedad `repeatable` establecida en `true`, haga lo siguiente:

   * configure la propiedad `min` para especificar el número mínimo de veces que se puede repetir la sección.

   * configure la propiedad `max` para especificar el número máximo de veces que se puede repetir la sección.

   ![Establezca la propiedad mín. y máx. para especificar el número de veces que se puede repetir la sección](/help/edge/assets/repeatable-section-set-min-max.png)

1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

   Al añadir una sección repetible, el icono **Eliminar** les parece intuitivo a los usuarios, lo que facilita la eliminación de las secciones repetibles. Una vez añadidas, estas secciones no se pueden reducir a menos instancias de las especificadas por la propiedad `min`. Esto garantiza el cumplimiento del requisito mínimo establecido para la cumplimentación del formulario.

<!--

For example, consider a form used to collect information from users applying for a loan. . You may have a repeatable section for capturing details of each co-applicant. The repeatable section would typically contain fields such as co-co-applicant

The form allows users to provide personal information, including details of the co-applicants. Users can enter details for co-applicants, with this section being repeatable.

![Repeatable sections in forms](/help/forms/assets/eds-repeatable.png)

## Prerequisites

The [Adaptive Forms Block is enabled](/help/edge/docs/forms/create-forms.md) for your Edge Delivery Services project. 

## Add a repeatable section to a form 

Let's take an example of a loan application form. The form enables users to submit personal information. You can include co-applicant details using repeatable sections, with the option to add a minimum and maximum of three co-applicant sections.

"_You can use a Microsoft Excel file on your SharePoint Site or Google Sheet file on Google Drive to develop a form. Examples in this document are based on a [Microsoft Excel file on your SharePoint Site](https://www.aem.live/docs/setup-customer-SharePoint)._" 


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

The form is accessible at `https://localhost:3000`, where clicking the `Add` button adds new repeatable section for entering co-applicant details. You can also delete the repeatable section by clicking the `Delete` button. 

>[!NOTE]
>
> If you encounter a "Page Not Found" error while accessing your form at localhost, add the directory name of the Microsoft SharePoint Site in front of the URL where your form is located. For example, `http://localhost:3000/<dir-name>/`

-->


## Consulte también

{{see-more-forms-eds}}
