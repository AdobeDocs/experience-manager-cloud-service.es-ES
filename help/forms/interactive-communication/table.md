---
title: Componente Tabla en el editor de comunicaciones interactivas
description: El componente Tabla del Editor de comunicaciones interactivas en AEM Forms permite a los autores insertar tablas personalizables en plantillas de comunicación con facilidad.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 8%

---


# Componente Tabla en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Tabla del editor de comunicaciones interactivas (IC) permite a los autores insertar tablas personalizables en plantillas de comunicación con facilidad. Este componente admite la representación de datos en tablas para casos de uso como resúmenes, listas de elementos, entradas estructuradas o diseños de comparación.

Los autores pueden arrastrar y soltar el componente de tabla en el lienzo, configurar el número de filas y columnas y elegir opciones como incluir filas de encabezado y pie de página o establecer la dirección del diseño. Las tablas se pueden definir como plantillas predeterminadas para mantener la coherencia en varias comunicaciones.

![Buscar documento CI](/help/forms/interactive-communication/assets/table.png)

## &#x200B;2. Propiedades

El componente Tabla incluye varias propiedades configurables para ayudar a los autores a personalizar el comportamiento y el aspecto de la tabla:


2.1 Campo básico

- **Nombre:** Identificador único de la tabla. Este nombre se utiliza internamente para hacer referencia a la tabla en los modelos de datos y la lógica.

- **Filas:** Especifica el número de filas de contenido (sin incluir el encabezado y el pie de página).

- **Columnas:** Define el número de columnas de la tabla.

- **Fila de encabezado:** Opción para incluir una fila de encabezado en la parte superior de la tabla para las etiquetas de columna.

- **Fila de pie de página:** Opción para incluir una fila de pie de página para totales o valores de resumen.

- **Establecer como predeterminado:** Permite a los usuarios guardar la configuración actual como una plantilla de tabla predeterminada para uso futuro.

- **Dirección del diseño:** Define la forma en que se rellenan las filas (normalmente se establece de izquierda a derecha).

Posición 2.2

- **Descripción:** controla la ubicación de la tabla dentro del diseño.

- **Configuración:**

   - **Coordenadas X e Y:** Establece las posiciones horizontal (X) y vertical (Y) de la tabla en el lienzo.

   - **Altura y anchura:** Define el tamaño total de la tabla (en mm), lo que permite una asignación flexible del espacio.

2.3 Aspecto

**Aspecto:** Establece el estilo visual de la tabla. Los autores pueden elegir entre ajustes predefinidos como bordes, planos o elevados.

- **Relleno:** Color de fondo de la tabla o celdas.

- **Trazo:** Color de borde alrededor de la tabla o celdas específicas.

- **Anchura:** Grosor de las líneas de borde.

- **Estilo:** Elija tipos de borde: esquinas redondeadas o esquinas nítidas.

- **Bordes:** configure la visibilidad de los bordes de celda y el radio de esquina.

2.4 Presencia

- **Descripción:** Determina la visibilidad de la tabla durante la ejecución.

- **Opciones:**

   - **Visible:** muestra la tabla normalmente en la salida.

   - **Oculta:** Oculta la tabla pero conserva espacio dentro del diseño.

2.5 Enlace de datos

**Enlace de datos:** Conecte la tabla con un origen de datos (por ejemplo, JSON, esquema XML) para rellenar dinámicamente filas y columnas con valores durante la generación. Esto resulta útil para la facturación desglosada, los registros de transacción o los listados de productos.

## &#x200B;3. Uso

El componente Tabla es ideal para mostrar información estructurada o repetitiva. Los casos de uso habituales incluyen:

- Facturas y facturas con filas de artículos

- Comparaciones de políticas o planes

- Resúmenes de datos de perfil o cuenta

- Catálogos de productos o matrices de características

Los autores pueden configurar el número de filas y columnas, aplicar visibilidad condicional o enlazar datos para mostrar información dinámica.

## &#x200B;4. Prácticas recomendadas

- Utilice filas de encabezado para etiquetar claramente cada columna para mejorar la legibilidad.

- Aplique filas de pie de página para totales o notas importantes cuando corresponda.

- Aproveche el enlace de datos para rellenar filas de forma dinámica en función de la entrada estructurada.

- Mantenga un estilo y un espaciado coherentes mediante la configuración del aspecto y los márgenes.

- Al ocultar una tabla, asegúrese de que el diseño sea continuo eligiendo si desea conservar el espacio o no.

- Utilice plantillas predeterminadas para estandarizar el contenido de tablas en todos los documentos.

El componente Tabla del editor de CI es un componente flexible y fácil de usar diseñado para admitir contenido estructurado en las comunicaciones. Gracias a sus opciones de diseño personalizables, sus características de estilo y su potente enlace de datos, permite a los autores presentar la información de forma clara y eficaz.


