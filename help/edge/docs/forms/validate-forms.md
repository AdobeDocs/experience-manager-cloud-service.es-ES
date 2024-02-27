---
title: 'De hojas de cálculo a Forms: dominio de validaciones de campos de bloque de formulario'
description: Cree formularios potentes más rápido mediante hojas de cálculo y campos de bloque de formularios. Esta guía le ayuda a crear validaciones personalizadas para los campos de bloque Forms de EDS.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Agregar validaciones a campos de formulario

El bloque de formulario tiene una función de validaciones integrada. Estas validaciones se aplican automáticamente en exploradores modernos según el tipo de campo elegido y las propiedades adicionales proporcionadas.

## Explicación de los tipos de campo y validación

El bloque de formulario admite varias opciones [Tipos de entrada de HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), incluidos texto, correo electrónico, número, fecha, etc. También se adapta [área de texto](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select y fieldset, junto con las completas funciones de validación de entrada inherentes a HTML-5.

utiliza tipos de campo de HTML para definir el tipo de datos que puede introducir un usuario. Los distintos tipos de campo tienen diferentes reglas de validación integradas:

Correo electrónico: este tipo de campo valida automáticamente los datos introducidos por el usuario con un formato de dirección de correo electrónico común. Los usuarios que introduzcan un correo electrónico no válido verán un mensaje de error.
Número: Este tipo de campo solo permite la entrada numérica. Los usuarios que introduzcan caracteres no numéricos recibirán un error.
Fecha: este tipo de campo valida los datos introducidos por el usuario con un formato de fecha estándar. Las fechas fuera de un intervalo razonable también pueden marcarse como no válidas.
URL: este tipo de campo valida los datos introducidos por el usuario con un formato de URL válido. Los usuarios que introduzcan una dirección URL no válida verán un mensaje de error.
Tel: Este tipo de campo está diseñado específicamente para números de teléfono y puede almacenar en déclencheur la validación en función de formatos de país específicos (no admitido universalmente).


## Más información

* [Creación y previsualización de un formulario](/help/edge/docs/forms/create-forms.md)
* [Habilitar formulario para enviar datos](/help/edge/docs/forms/submit-forms.md)
* [Publicar un formulario en la página de Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Agregar validaciones a campos de formulario](/help/edge/docs/forms/validate-forms.md)
* [Cambiar temáticas y estilo de formulario](/help/edge/docs/forms/style-theme-forms.md)