---
title: Numeración dinámica de páginas en el editor de comunicaciones interactivas
description: La numeración de páginas dinámica en el editor de comunicaciones interactivas permite a los autores mostrar automáticamente los números de página en su salida de PDF.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 957944da363b506c34c2630aeedbe984442f34b8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 14%

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

![Buscar documento CI](/help/forms/interactive-communication/assets/dynamic-page.png)

## Utilizar la numeración de páginas dinámica en el editor de comunicaciones interactivas

1. Abra el Editor de comunicaciones interactivas
Abra el proyecto de comunicación interactiva en el editor de CI.

1. Ir a página maestra
La numeración de páginas sólo se puede habilitar en la página maestra. Vaya a la página principal de la comunicación.

1. Habilitar numeración de páginas
En el panel Propiedades, active la opción Habilitar número de página. Esto agrega automáticamente números de página a todas las páginas asociadas.

1. Personalizar ubicación
El componente Número de página se puede colocar en cualquier lugar del lienzo después de soltarlo y personalizarlo libremente mediante propiedades de texto estándar.

1. Vista previa en PDF
Los números de página aparecen únicamente durante la vista previa de PDF y muestran la numeración dinámica en todas las páginas.

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
