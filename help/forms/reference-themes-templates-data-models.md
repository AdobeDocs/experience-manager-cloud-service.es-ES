---
title: Temas de referencia, plantillas y modelos de datos de formulario
seo-title: Reference Themes, Templates, and Form Data models
description: AEM Forms proporciona temas de formularios adaptables, plantillas y modelos de datos de formulario que puede obtener de Distribución de software
seo-description: AEM Forms provides adaptive forms themes, templates, and form data models that you can get from Software Distribution
source-git-commit: 196a2f221c637d58ea6642177f530f158888efe0
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 48%

---

# Temas de referencia, plantillas y modelos de datos de formulario {#reference-themes-templates-and-data-models}

AEM Forms as a Cloud Service proporciona varios temas de referencia, plantillas y modelos de datos de formulario para ayudarle a empezar rápidamente a crear Forms adaptable. Puede descargar el [paquete de contenido de referencia del portal de distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) y utilice el [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) para instalar el [paquete de contenido de referencia](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) en su entorno de desarrollo local, de desarrollo o de producción para llevar estos recursos de referencia a su entorno.

Los temas, las plantillas y los modelos de datos de formulario incluidos en el paquete de contenido de referencia son:


| Temáticas | Plantillas | Modelos de datos de formulario |
---------|----------|---------
| Canvas 3.0 | Basic | Microsoft Dynamics 365 |
| Tranquilo | Blank | Salesforce |
| Urbane |  |  |
| Ultramarine |  |  |
| Beryl |  |  |
| Atención sanitaria |  |  |
| FSI |  |  |

## Temáticas de referencia {#reference-themes}

[Temáticas](/help/forms/themes.md) permite aplicar un estilo a los formularios sin tener conocimientos profundos de CSS. Para obtener los temas siguientes, instale la [Paquete de contenido de referencia](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Beryl
* Canvas 3.0
* Tranquilo
* Urbane
* Ultramarine
* Atención sanitaria
* SIF (Servicios financieros y seguros)

Cada tema contiene un estilo único y elegante que puede utilizar para crear formularios adaptables para los usuarios. Contiene un estilo único para selectores como panel, cuadro de texto, cuadro numérico, botón de radio, tabla y conmutador. El estilo de estos temas dependerá de los requisitos. Por ejemplo, en una situación concreta se requiere una temática minimalista con fuentes limpias. La temática Liberty permite conseguir esa apariencia.

![Temas de referencia](assets/ref-themes.png)

Los temas incluidos en este paquete son adaptables y el estilo de dichos temas está diseñado para las pantallas móviles y de ordenador. La mayoría de los navegadores modernos de una variedad de dispositivos pueden procesar formularios aplicados con uno de estos temas sin ningún inconveniente.

Para obtener más información sobre la instalación del paquete, consulte [Cómo trabajar con paquetes](/help/implementing/developing/tools/package-manager.md).

## Beryl {#beryl}

El tema de Beryl enfatiza el uso de la imagen de fondo, la transparencia y los iconos grandes y planos. En la captura de pantalla siguiente, puede ver el aspecto del tema Beryl y cómo puede mejorar el estilo del formulario.

![Tema Beryl](assets/beryl.png)

## Canvas 3.0 {#canvas}

Canvas 3.0 es el tema predeterminado para Adaptive Forms y enfatiza el uso de colores básicos, transparencia e iconos planos. En la captura de pantalla siguiente, puede ver el aspecto del tema Canvas 3.0.

![Tema Beryl](assets/canvas.png)


## Tranquilo {#tranquil}

El tema Tranquil ofrece tonos claros y oscuros de su esquema de colores para resaltar los diferentes componentes de un formulario. Por ejemplo, los botones de radio, los paneles y las pestañas tienen un color verde diferente.

![Tema Tranquil](assets/tranquil.png)


## Urbane {#urbane}

El tema de Urbane destaca el aspecto minimalista y funcional de su formulario. Al aplicar el tema Urbane al formulario, puede ver que los componentes son planos. Los paneles tienen contornos finos para crear un aspecto moderno.

![Tema Urbane](assets/urbane.png)


## Ultramarine {#ultramarine}

El tema Ultramarine utiliza tonos azules profundos para resaltar componentes como fichas, paneles, cuadros de texto y botones.

![Tema Ultramarine](assets/ultramarine.png)

## Atención sanitaria {#healthcare}

El tema de asistencia sanitaria utiliza tonos verdes profundos para resaltar componentes como fichas, paneles, cuadros de texto y botones.

![Tema de FSI](assets/healthcare.png)


## SIF (Servicios financieros y seguros)

El tema de FSI enfatiza un aspecto minimalista y funcional de su formulario. Al aplicar el tema FSI al formulario, puede ver que los componentes del panel son amarillos.

![Tema de FSI](assets/fsi.png)

## Plantillas de referencia {#reference-templates}


[Plantillas](/help/forms/themes.md) permite definir la estructura, el contenido y las acciones iniciales del formulario para los formularios. Puede obtener las siguientes plantillas instalando el [Paquete de contenido de referencia](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Basic
* Blank

La plantilla básica ayuda a crear rápidamente un formulario de inscripción. También puede utilizarla para previsualizar la funcionalidad de los componentes básicos de Adaptive Forms. Proporciona un diseño de asistente para la presentación de datos sección a sección. Utilice la plantilla en blanco para empezar a crear un formulario adaptable desde un lienzo en blanco.


## Modelos de datos de formulario de referencia {#reference-models}

El Forms adaptable puede interactuar con los servidores de Microsoft Dynamics 365 y Salesforce para habilitar los flujos de trabajo empresariales. Por ejemplo:

* Escriba datos en Microsoft Dynamics 365 y Salesforce en el envío del formulario adaptable.
* Escriba datos en Microsoft Dynamics 365 y Salesforce a través de entidades personalizadas definidas en el Modelo de datos de formulario y viceversa.
* Consulte Microsoft Dynamics 365 y el servidor de Salesforce para obtener datos y rellene previamente el Forms adaptable.
* Lea los datos del servidor de Microsoft Dynamics 365 y Salesforce.

Puede obtener los siguientes modelos de datos de formulario instalando el [Paquete de contenido de referencia](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

Para obtener información sobre el uso de estos modelos, consulte [Configuración de los servicios en la nube de Microsoft Dynamics 365 y Salesforce](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)






