---
title: Componente Línea en el editor de comunicaciones interactivas
description: El componente Línea del Editor de comunicaciones interactivas de AEM Forms permite a los autores insertar líneas horizontales o verticales dentro de un diseño de comunicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 11%

---


# Componente Línea en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Línea del editor de comunicaciones interactivas (IC) permite a los autores insertar líneas horizontales o verticales dentro de un diseño de comunicación. Estas líneas ayudan a segmentar visualmente el contenido, mejorar la legibilidad o resaltar la estructura del formulario. Con estilos personalizables como líneas sólidas o subrayados y una posición flexible, el componente Línea se puede utilizar para fines funcionales y estéticos en el diseño de formularios.

![Buscar documento CI](/help/forms/interactive-communication/assets/line.png)

## &#x200B;2. Propiedades

El componente Línea incluye una serie de propiedades configurables para definir su identidad, apariencia, ubicación y visibilidad dentro del documento.

2.1. Campo básico

- **Nombre:** Identificador único usado internamente para hacer referencia al componente de línea en modelos de datos, reglas o scripts.

- **Tipo de aspecto visual:** Seleccione cómo aparece la línea dentro del formulario.

   - **Ninguna:** No se muestra ninguna línea.

   - **Cuadro sólido:** Procesa la línea como un cuadro sólido, usado normalmente como separador.

   - **Subrayado:** dibuja un subrayado que se suele utilizar debajo de encabezados o campos.

2.2. Posición

- **Descripción:** define la ubicación física de la línea en el diseño del formulario.

- **Configuración:**

   - **Coordenadas X e Y:** Especifica la posición horizontal y vertical.

   - **Altura y anchura:** Establezca la longitud y el grosor de la línea (en mm).

2.3. Margen

- **Descripción:** agrega relleno o espaciado alrededor del componente de línea para controlar la densidad de diseño.

- **Opciones:**

   - Arriba

   - Inferior

   - Izquierda

   - Derecha

2.4. Aspecto

- **Descripción:** permite que el estilo de la línea coincida con el diseño del documento.

- **Opciones:**

   - **Trazo:** Define el color y el grosor del trazo de línea.

   - **Anchura:** Determina el ancho de la línea en el formulario.

   - **Estilo:** Elija entre estilos de línea discontinua, punteada o sólida.

2.5. Presencia

- **Descripción:** controla la visibilidad del componente de línea durante la ejecución.

- **Opciones:**

   - **Visible:** La línea se representa en la salida final.

   - **Oculta:** La línea no se muestra, pero se conserva su espacio de diseño.

## &#x200B;3. Uso

El componente Línea se utiliza a menudo para lo siguiente:

- Dividir visualmente secciones en un formulario largo

- Subrayar encabezados o etiquetas para dar énfasis

- Crear bordes o cuadros alrededor de grupos de campos

- Mejorar la jerarquía visual del diseño de la comunicación

## &#x200B;4. Prácticas recomendadas

- Utilice estilos de línea coherentes en todo el formulario para mantener un aspecto profesional.

- Ajuste los márgenes para evitar el desorden visual y garantizar la alineación.

- Elija los ajustes de trazo y estilo adecuados para que coincidan con la marca o el diseño del documento.

- Oculte las líneas innecesarias para evitar distracciones y conservar el espaciado del diseño.

El componente Línea del editor de comunicaciones interactivas es un elemento de diseño sencillo pero eficaz. Cuando se utiliza de forma estratégica, mejora la estructura visual de los documentos de comunicación, lo que ayuda a los usuarios a navegar por el contenido y garantiza un diseño más limpio y pulido.


