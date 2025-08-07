---
title: Las expresiones regex que Edge Delivery Services para AEM Forms suele utilizar para validar campos de formulario
description: Las expresiones regex que Edge Delivery Services para AEM Forms suele utilizar para validar campos de formulario
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 5cfe23bb-155f-4639-b7b7-5edc172ba92a
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 94%

---

# Expresiones regex comúnmente utilizadas para las validaciones

Estas son algunas expresiones regulares que puede utilizar para mejorar la validación del formulario más allá de lo que ofrecen los exploradores modernos:

## Contraseña segura

```regex
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

Garantiza al menos ocho caracteres con lo siguiente:

- Letras minúsculas (a-z)
- Letras mayúsculas (A-Z)
- Dígitos (0-9)
- Caracteres especiales (@$!%*?&amp;)


## Dirección de correo electrónico


```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Permite letras, números y caracteres especiales en el nombre de usuario y de dominio.


## Número de teléfono (formato de los EE. UU.)

```regex
^\(?([0-9]{3})\)?[-. ]([0-9]{3})[-. ]([0-9]{4})$
```

Valida los números de teléfono con el formato (XXX) XXX-XXXX.



## URL

```regex
^(http|https)://.*$
```

Garantiza una dirección URL válida que empiece por HTTP o HTTPS.



## Fecha (AAAA-MM-DD)

```regex
^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$
```

Valida las fechas con el formato AAAA-MM-DD.


## Hora (HH:MM)

```regex
^([01][0-9]|2[0-3]):[0-5][0-9]$
```

Valida las horas con el formato HH:MM (formato de 24 horas).


## Código postal (formato de los EE. UU.)

```regex
^\d{5}(?:[-\ ]\d{4})?$
```

Valida códigos postales de cinco dígitos de los EE. UU. con un guion opcional y una extensión de cuatro dígitos.


## Nombre de usuario (alfanumérico y guion bajo)

```regex
^[a-zA-Z0-9_]+$
```

Permite letras, números y guiones bajos.


## Código hexadecimal de color

```regex
^#[0-9a-fA-F]{6}$
```

Valida los códigos de color hexadecimal de seis dígitos. Por ejemplo, #FFFFFF.


## Dirección IP

```regex
^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})$
```

Valida direcciones IPv4.



## Número del Seguro Social (formato de los EE. UU.)

```regex
^\d{3}-\d{2}-\d{4}$
```



## Número de la tarjeta de crédito

```regex
^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}$
```

Valida los números de teléfono con el formato (XXX) XXX-XXXX.



## Número de teléfono (formato de los EE. UU.)

```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Valida los números de teléfono con el formato (XXX) XXX-XXXX.
