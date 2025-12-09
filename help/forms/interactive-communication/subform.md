---
title: Componente Subformulario en el editor de comunicaciones interactivas
description: El componente Subformulario del Editor de comunicaciones interactivas en AEM Forms permite organizar varios elementos de formulario de forma flexible y estructurada.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 10%

---


# Componente Subformulario en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente **Subformulario** del editor de comunicaciones interactivas (IC) actúa como un contenedor de diseño dinámico que le permite organizar varios elementos de formulario de forma flexible y estructurada. Normalmente se utiliza para agrupar campos relacionados, crear secciones de repetición o definir estructuras de datos anidadas para mejorar la experiencia del usuario y el enlace de datos.

Los subformularios se pueden configurar para que fluyan en diferentes diseños, como de arriba a abajo o de izquierda a derecha, lo que los hace ideales para diseños de formulario complejos y secciones reutilizables.

![Buscar documento CI](/help/forms/interactive-communication/assets/subform.png)

## &#x200B;2. Propiedades

2.1 Propiedades básicas

- **Nombre:** Identificador único del subformulario utilizado en las referencias, modelos de datos y reglas de negocio.

- **Contenido:** Define cómo se organizan los elementos dentro del subformulario.

   - **Colocado:** Colocación absoluta de elementos secundarios utilizando las coordenadas X e Y.

   - **De posición variable (de arriba a abajo):** Organiza los elementos verticalmente.

   - **De posición variable (de izquierda a derecha):** Organiza los elementos horizontalmente.

Posición 2.2

- **Descripción:** Determina la ubicación del subformulario dentro del diseño de comunicación.

- **Configuración:**

   - Coordenadas X e Y (en mm)

   - Anchura y altura (en mm)

2.3 Aspecto

- **Relleno:** Especifica el color de fondo del área del subformulario.

- **Trazo:** Define el color del borde.

- **Anchura:** Establece el grosor del borde.

- **Estilo:** Elija entre ajustes preestablecidos visuales como plano, con borde o elevado.

- **Bordes:** Determina el estilo de las esquinas: redondeado o nítido.

2.4 Presencia

- **Descripción:** controla la visibilidad del subformulario durante la ejecución.

- **Opciones:**

   - **Visible:** Siempre mostrado.

   - **Oculto:** No se muestra, pero el espacio se conserva en el diseño.

2.5 Enlace de datos

- **Tipo de enlace de datos:** Vincula el subformulario a una estructura de datos (normalmente XML o JSON).

- **Nombre de usuario:** enlaza los datos con el nombre asignado del subformulario.

- **Usar datos globales:** Conecta el subformulario a una ruta de acceso de esquema global para el uso compartido de datos.

- **Sin enlace de datos:** El subformulario no almacena ni interactúa con ningún modelo de datos externo.

## &#x200B;3. Uso

Los subformularios son esenciales en los casos en los que sea necesario agrupar, anidar o repetir conjuntos de campos. Las aplicaciones habituales incluyen:

- Organización de bloques de direcciones (por ejemplo, calle, ciudad, código postal)

- Secciones repetidas para elementos de línea o entradas múltiples

- Estructurar la lógica del formulario condicional mediante la visibilidad y las reglas
Los subformularios también se pueden utilizar como contenedores para la alineación de diseño de arrastrar y soltar en diseños estáticos y dinámicos.

## &#x200B;4. Prácticas recomendadas

- Elija el diseño adecuado (de posición y posición variable) según el diseño y las necesidades de datos.

- Utilice nombres significativos para facilitar la integración de datos y las referencias a reglas.

- Aplicar estilo a subformularios para distinguir visualmente secciones agrupadas.

- Cuando utilice subformularios repetibles, asegúrese de que el enlace de datos a las estructuras de la matriz sea correcto.

- Aplique reglas de visibilidad condicionales para optimizar la experiencia del usuario en formularios complejos.

El componente **Subformulario** del editor de comunicaciones interactivas proporciona una forma eficaz de estructurar y controlar diseños de formulario complejos. Tanto si se organizan los campos de entrada como si se administra el contenido dinámico o se habilita el diseño modular, los subformularios mejoran tanto la facilidad de uso como el mantenimiento en todas las plantillas de documento.


