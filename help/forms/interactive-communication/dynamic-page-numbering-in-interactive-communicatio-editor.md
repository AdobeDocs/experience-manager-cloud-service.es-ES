---
title: Numeración dinámica de páginas en el editor de comunicaciones interactivas
description: La numeración de páginas dinámica en el editor de comunicaciones interactivas permite a los autores mostrar automáticamente los números de página en su salida de PDF.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: dae482e1f57a3504bf08926b57b89ca9266bd36a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 19%

---


# Numeración dinámica de páginas en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## Introducción

La función Numeración dinámica de páginas de la comunicación interactiva (CI) permite a los autores mostrar automáticamente los números de página en su salida de PDF. La numeración de páginas se puede habilitar en el nivel de página maestra, lo que garantiza una numeración coherente en todas las páginas de diseño asociadas. Esto ayuda a mantener un seguimiento de páginas claro y un diseño profesional a través de las comunicaciones de varias páginas.

## Capacidades clave

- **Configuración de página maestra:**
La numeración de páginas puede habilitarse en el nivel de página maestra. El componente se puede colocar en cualquier lugar del lienzo después de soltarlo y personalizarlo libremente, ya que admite todas las propiedades disponibles en el componente de texto.

- **Ubicación automática:**
Aparece un componente de numeración de páginas en la parte inferior central de cada página con el formato:
&quot;**Número de página de ##**&quot;

   - El primer **#** representa el número de página actual.

   - El segundo **##** representa el número total de páginas en la comunicación.

- **Visualización dinámica en la vista previa de PDF:**
Los números de página se representan de forma dinámica durante la vista previa de PDF y muestran una numeración de página precisa en la salida final.

### Ejemplo

Al obtener una vista previa de una comunicación interactiva de 5 páginas, se mostrará cada página:

Página 1 de 5

Página 2 de 5

... y así sucesivamente, actualizándose dinámicamente durante la generación de PDF.

## Principales ventajas

- Mejora la legibilidad y la profesionalidad de los documentos.

- Automatiza la numeración de páginas sin intervención manual.

- Mantiene la coherencia en todas las páginas vinculadas a una página maestra.
