---
title: 'De hojas de cálculo a Formularios: dominio de las validaciones de campos de Bloque de formularios adaptables'
description: Cree formularios potentes más rápido con hojas de cálculo y campos de Bloque de formularios adaptables. Esta guía le ayuda a crear validaciones personalizadas para los campos de bloque de formularios de EDS.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 16e1d42a-42d0-4335-ba81-feedea7ed7d7
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 100%

---

# Agregar validaciones a los campos de formulario

El Bloque de formularios adaptables tiene funciones de validaciones integradas. Estas validaciones se aplican automáticamente en exploradores modernos según el tipo de campo elegido y las propiedades adicionales que proporcione.

## Explicación de los tipos de campo y validación

El Bloque de formularios adaptables admite una variedad de [Tipos de entrada de HTML-5](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/input#input_types), incluidos texto, correo electrónico, número, fecha, etc. También incorpora [textarea](https://developer.mozilla.org/es-es/docs/Web/HTML/Element/textarea), select y fieldset, junto con las completas funciones de validación de entrada inherentes a HTML-5.

utiliza tipos de campo HTML para definir el tipo de datos que puede introducir un usuario. Los distintos tipos de campo tienen diferentes reglas de validación integradas:

Correo electrónico: este tipo de campo valida automáticamente la entrada del usuario con un formato común de dirección de correo electrónico. Los usuarios que introduzcan un correo electrónico no válido verán un mensaje de error.
Número: este tipo de campo solo permite la entrada numérica. Los usuarios que introduzcan caracteres no numéricos recibirán un error.
Fecha: este tipo de campo valida la entrada del usuario con un formato de fecha estándar. Las fechas fuera de un intervalo razonable también pueden marcarse como no válidas.
URL: este tipo de campo valida la entrada del usuario con un formato de URL válido. Los usuarios que introduzcan una dirección URL no válida ven un mensaje de error.
Tel: este tipo de campo está diseñado específicamente para números de teléfono y puede activar la validación en función de formatos de país específicos (no admitidos universalmente).



