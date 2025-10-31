---
title: Gestión del desbordamiento de contenido en el editor de comunicaciones interactivas
description: La administración del desbordamiento de contenido en el Editor de comunicaciones interactivas mejora la forma en que el texto se comporta dentro de los diseños Fluidos y Colocados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 371838c77beafa8c67259a865b25325632bea0b0
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 17%

---


# Gestión del desbordamiento de contenido en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## Introducción

La función Gestión de desbordamiento de contenido del Editor de comunicaciones interactivas mejora el comportamiento del texto dentro de los diseños de posición y posición variable. Garantiza la continuidad del contenido sin problemas para los diseños fluidos y proporciona alertas visuales para los diseños colocados, lo que proporciona a los autores un mejor control y flexibilidad al diseñar las comunicaciones.

## Capacidades clave

### Diseño de posición variable

- **Nueva opción:**
Agrega una propiedad **permitir saltos de página** dentro del contenido para controlar el comportamiento del desbordamiento. Esta opción solo está visible cuando el subformulario principal está establecido en De posición variable y su propiedad **Permitir saltos de página** está habilitada.

- **Continuación automática de la página:**
Cuando el contenido supera el espacio disponible, se crea automáticamente una nueva página y la edición continúa sin problemas.

- **Compatibilidad con copiar y pegar:**
El texto grande pegado en el editor fluye automáticamente entre páginas, manteniendo la coherencia del diseño.

### Diseño posicionado

- **Indicador de desbordamiento:**
Cuando el contenido supera el contenedor (subformulario o página), el editor de texto se expande para editarlo, pero la altura del elemento permanece fija.

- **Alerta visual:**
Aparece un borde rojo en la parte inferior del contenedor para indicar un desbordamiento.

- **Ajuste manual:**
Los autores cambian manualmente el tamaño del contenedor para adaptarlo al contenido adicional.

>[!NOTE]
>
> Esta función requiere que toda la jerarquía principal (como los subformularios) se establezca en De posición variable. Si se coloca cualquier subformulario principal en la jerarquía, la opción **Permitir saltos de página** dentro del contenido no funcionará como se espera.

## Ventajas

- Mejora la eficacia y el control de la creación de contenido.

- Mantiene un diseño y una legibilidad coherentes en todas las páginas.

- Ayuda a identificar el desbordamiento rápidamente mediante indicadores visuales.

- Mejora la flexibilidad del diseño de la comunicación para ambos tipos de diseño.
