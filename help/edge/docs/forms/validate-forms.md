---
title: 'De hojas de cálculo a Forms: dominio de validaciones de campos de bloques de Forms adaptables'
description: Cree formularios potentes más rápido con hojas de cálculo y campos de bloque de Forms adaptables. Esta guía le ayuda a crear validaciones personalizadas para los campos de bloque Forms de EDS.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
source-git-commit: 2aa70e78764616f41fe64e324c017873cfba1d5b
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Agregar validaciones a campos de formulario

El bloque de Forms adaptable tiene funciones de validaciones integradas. Estas validaciones se aplican automáticamente en exploradores modernos según el tipo de campo elegido y las propiedades adicionales proporcionadas.

## Explicación de los tipos de campo y validación

El bloque de Forms adaptable admite diversas funciones [Tipos de entrada de HTML-5](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), incluidos texto, correo electrónico, número, fecha, etc. También se adapta [área de texto](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), select y fieldset, junto con las completas funciones de validación de entrada inherentes a HTML-5.

utiliza tipos de campo de HTML para definir el tipo de datos que puede introducir un usuario. Los distintos tipos de campo tienen diferentes reglas de validación integradas:

Correo electrónico: este tipo de campo valida automáticamente los datos introducidos por el usuario con un formato de dirección de correo electrónico común. Los usuarios que introduzcan un correo electrónico no válido verán un mensaje de error.
Número: Este tipo de campo solo permite la entrada numérica. Los usuarios que introduzcan caracteres no numéricos recibirán un error.
Fecha: este tipo de campo valida los datos introducidos por el usuario con un formato de fecha estándar. Las fechas fuera de un intervalo razonable también pueden marcarse como no válidas.
URL: este tipo de campo valida los datos introducidos por el usuario con un formato de URL válido. Los usuarios que introduzcan una dirección URL no válida verán un mensaje de error.
Tel: Este tipo de campo está diseñado específicamente para números de teléfono y puede almacenar en déclencheur la validación en función de formatos de país específicos (no admitido universalmente).



