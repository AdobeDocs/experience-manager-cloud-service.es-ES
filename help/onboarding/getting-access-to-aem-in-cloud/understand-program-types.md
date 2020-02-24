---
title: Explicación de los tipos de programas y programas
description: 'Explicación de los tipos de programas y programas: servicios en la nube'
translation-type: tm+mt
source-git-commit: 1129188c06d893bbeb8f8861b6fae25052605f12

---


# Explicación de programas y tipos de programas {#understanding-programs}

En Cloud Manager tiene la entidad Inquilina en la parte superior, que puede tener varios programas dentro de ella.  Cada programa no puede contener más de un entorno de producción y varios entornos sin producción.

## Tipos de programas {#program-types}

Un usuario puede crear un **Simulador para pruebas** o un programa **normal** .

Generalmente, se crea un *Simulador para pruebas* para ofrecer los fines de formación, ejecución de demostraciones, habilitación, puntos de contacto o documentación. No se trata de transportar tráfico en directo y tendrá restricciones que un programa regular no tendrá. Incluirá Sitios y Recursos y se entregará automáticamente con una rama Git que incluye código de muestra, un entorno Dev y una canalización sin producción.

Se crea un programa ** regular para habilitar el tráfico activo en el momento adecuado en el futuro.