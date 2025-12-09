---
title: Gestión del desbordamiento de contenido en el editor de comunicaciones interactivas
description: La administración del desbordamiento de contenido en el Editor de comunicaciones interactivas mejora la forma en que el texto se comporta dentro de los diseños Fluidos y Colocados.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 11%

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

![Buscar documento CI](/help/forms/interactive-communication/assets/content-overflow.png)

## Cómo utilizar la gestión de desbordamiento de contenido en el editor de comunicaciones interactivas

1. Abra el Editor de comunicaciones interactivas
Abra la comunicación en el Editor IC para empezar a editar el diseño y el contenido.

1. Seleccionar el tipo de diseño
Elija el diseño que desee para el subformulario, de posición variable o variable en función de cómo desee que se comporte el contenido.

1. Para diseños de posición variable

   1. Asegúrese de que la jerarquía del subformulario principal está establecida en De posición variable.

   1. En el panel Propiedades, habilite la opción Permitir saltos de página dentro del contenido (visible solo si está habilitada la opción &quot;Permitir saltos de página&quot; del subformulario principal).

   1. Añada o pegue texto, cuando el contenido supera una página, continúa automáticamente en la siguiente página.

1. Para diseños colocados

   1. Agregar o editar texto dentro de un contenedor fijo.

   1. Si el contenido supera la altura del contenedor, aparece un borde rojo en la parte inferior para indicar un desbordamiento.

   1. Cambiar manualmente el tamaño del contenedor para dar cabida al contenido adicional.

1. Previsualizar la comunicación
Utilice la opción Vista previa de PDF para comprobar cómo fluye o desborda el contenido entre páginas para ambos tipos de diseño.

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
