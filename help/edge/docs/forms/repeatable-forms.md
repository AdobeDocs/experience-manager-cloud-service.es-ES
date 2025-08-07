---
title: Añadir secciones repetibles a un formulario
description: Adición de secciones repetibles a un formulario EDS
feature: Edge Delivery Services
exl-id: 062d5a88-48ca-421f-bf0d-1483e3cfee28
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 100%

---

# Añadir secciones repetibles a un formulario

El bloque de Formularios adaptables permite agregar o hacer repetible una sección o componente de un formulario. Esto permite a los usuarios introducir información varias veces para el mismo tipo de datos, lo que facilita la recopilación de información, como la experiencia laboral o los antecedentes educativos.

Por ejemplo, considere un formulario utilizado para recopilar información sobre la experiencia laboral de una persona. Puede tener una sección repetible para capturar los detalles de cada trabajo anterior. La sección repetible generalmente contiene campos como nombre de la empresa, cargo, fechas de empleo y responsabilidades del puesto. El usuario puede agregar varias instancias de la sección repetible para introducir información sobre cada trabajo que ha realizado.

Al final de este artículo, aprenderá lo siguiente:

- [Crear una sección repetible en un formulario](#add-repeatable-sections-to-a-form)
- [Establecer un número mínimo o máximo de repeticiones en un formulario](#set-minimum-or-maximum-number-of-repetitions-for-a-repeatable-section)

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

   - configure la propiedad `min` para especificar el número mínimo de veces que se puede repetir la sección.

   - configure la propiedad `max` para especificar el número máximo de veces que se puede repetir la sección.

   ![Establezca la propiedad mín. y máx. para especificar el número de veces que se puede repetir la sección](/help/edge/assets/repeatable-section-set-min-max.png)

1. Utilice [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa y publicar la hoja.

   Al añadir una sección repetible, el icono **Eliminar** les parece intuitivo a los usuarios, lo que facilita la eliminación de las secciones repetibles. Una vez añadidas, estas secciones no se pueden reducir a menos instancias de las especificadas por la propiedad `min`. Esto garantiza el cumplimiento del requisito mínimo establecido para la cumplimentación del formulario.


