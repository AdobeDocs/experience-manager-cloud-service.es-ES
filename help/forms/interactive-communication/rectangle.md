---
title: Componente Rectángulo en el editor de comunicaciones interactivas
description: El componente Rectángulo del Editor de comunicaciones interactivas en AEM Forms permite a los autores añadir elementos gráficos con forma que sirven como divisores de diseño, acentos visuales o contenedores de contenido.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 12%

---


# Componente Rectángulo en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Rectángulo del editor de comunicaciones interactivas (IC) permite a los autores añadir elementos gráficos con forma que sirven como divisores de diseño, acentos visuales o contenedores de contenido. Los rectángulos mejoran la jerarquía visual y dirigen la atención del usuario en los diseños de comunicaciones estructuradas.
Este componente no está vinculado a los datos, pero es fundamental para mejorar la claridad del diseño, agrupar los campos relacionados y mejorar la presentación general.

![Buscar documento CI](/help/forms/interactive-communication/assets/rectangle.png)

## &#x200B;2. Propiedades

El componente Rectángulo incluye varias propiedades personalizables:

2.1. Nombre

Nombre: identificador único del rectángulo. Se utiliza principalmente para hacer referencia a en jerarquías de diseño o para aplicar estilos de forma coherente.

2.2. Posición

- **Descripción:** Determina dónde aparece el rectángulo en el diseño del documento.

- **Configuración:**

   - **Coordenadas X e Y:** Definir ubicación horizontal y vertical.

   - **Alto y ancho (en mm):** Controle el tamaño del rectángulo.

2.3. Margen

Define el espacio alrededor del componente rectángulo para separarlo de otros elementos de la interfaz de usuario:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4. Aspecto

- **Descripción:** rige el estilo visual del rectángulo.

- **Opciones de personalización:**

   - **Relleno:** El color interno del rectángulo.

   - **Trazo:** El color del contorno del rectángulo.

   - **Anchura de trazo:** Grosor del borde del rectángulo.

   - **Estilo:** estilos preestablecidos como plano, con borde o elevado.

   - **Bordes:** controla el aspecto de las esquinas (por ejemplo, bordes redondeados o afilados).

2.5. Presencia

- **Descripción:** Especifica si el rectángulo se mostrará cuando se represente la comunicación.

- **Opciones:**

   - **Visible:** Muestra el rectángulo en tiempo de ejecución.

   - **Oculto:** Mantiene el espacio de diseño sin mostrar el rectángulo.

## &#x200B;3. Uso

El componente Rectángulo se utiliza generalmente con fines de diseño y estilo en lugar de entrada de contenido. Los casos de uso comunes incluyen los siguientes:

- Creación de una separación visual entre secciones

- Resaltado de elementos agrupados

- Mejora de la legibilidad y el equilibrio visual

- Encabezados de marcos, pies de página o secciones de llamadas

Los rectángulos se pueden combinar con otros elementos de diseño, como subformularios o contenedores, para estructuras de diseño visuales complejas.

## &#x200B;4. Prácticas recomendadas

- Utilice un estilo coherente para los rectángulos en todo el diseño para garantizar la armonía visual.

- Aplique los márgenes y el espaciado adecuados para evitar el abarrotamiento de los campos adyacentes.

- Elija colores de relleno y de trazo que se alineen con la marca o el tema del documento.

- Utilice los bordes redondeados sutilmente para mejorar la estética en los diseños modernos de la interfaz de usuario.

- Oculte los rectángulos si solo son necesarios con fines de diseño durante la edición, pero no son necesarios en la salida final.

El componente Rectángulo es una herramienta no interactiva pero potente del editor de CI. Cuando se diseña y coloca de forma eficaz, mejora la precisión del diseño, el flujo visual y la experiencia del usuario sin añadir complejidad al enlace de datos ni a la interactividad.


