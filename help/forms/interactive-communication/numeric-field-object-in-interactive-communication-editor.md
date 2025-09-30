---
title: Objeto de campo numérico en el editor de comunicaciones interactivas
description: El objeto de campo numérico en el editor de comunicaciones interactivas de AEM Forms permite a los autores recopilar entradas numéricas de los usuarios en un formato controlado.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 7%

---


# Objeto de campo numérico en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Campo numérico del editor de comunicaciones interactivas (IC) permite a los autores recopilar entradas numéricas de los usuarios en un formato controlado. Tanto si captura números de teléfono, códigos PIN, ID de política o cifras financieras, este campo garantiza que solo se acepten valores numéricos. El componente también admite el estilo, el formato, la validación y el enlace de datos, lo que lo hace esencial para las comunicaciones estructuradas.

![Buscar documento CI](/help/forms/interactive-communication/assets/numericfield.png)

## &#x200B;2. Propiedades

2.1 Campo básico

- **Nombre:** Defina un identificador único para el campo, que se usará en modelos de datos, reglas y scripts.

- **Pie de ilustración:** Muestra la etiqueta en pantalla a los usuarios (por ejemplo, &quot;Número de contacto&quot; o &quot;Id. de empleado&quot;).

- **Valor:** Permite que los usuarios introduzcan datos numéricos, como números de teléfono, ID, cantidades o valores monetarios.

- **Reservar:** Establezca la alineación del valor numérico (izquierda, derecha, superior o inferior) o especifique una posición personalizada utilizando unidades como milímetros (por ejemplo, 20 mm).

- **Aspecto:** Establezca el aspecto del cuadro de valor como Ninguno, Cuadro sólido o Subrayado en función del diseño visual deseado.

2.2 Tipografía

Controla el estilo visual de los caracteres numéricos introducidos por el usuario:

- **Validación de fuente:** Aplique restricciones para asegurarse de que sólo se aceptan entradas numéricas válidas (como números enteros, decimales o intervalos de números) según el tipo de datos deseado.

- **Tamaño de fuente:** Ajuste el tamaño del texto numérico mediante valores de punto como 10 pt, 12 pt o 20 pt para mantener la coherencia y legibilidad en todo el formulario.

Posición 2.3

Controla la ubicación espacial del campo numérico en el lienzo.

- **Coordenadas X e Y:** Definir la ubicación exacta del campo.

- **Ancho y alto (en mm):** Determina el tamaño del cuadro de entrada.

Margen de 2,4

Define el espaciado alrededor del límite del campo numérico para una alineación limpia.

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.5 Aspecto

Estilos el contenedor del campo de entrada numérico para que coincida con el diseño visual deseado:

- **Relleno:** Establece el color de fondo del campo numérico. Esto ayuda a separarlo visualmente de otros elementos o a hacer coincidir este elemento con la temática general.

- **Trazo:** Agregue bordes alrededor del campo numérico con las siguientes opciones personalizables:

- **Anchura:** Defina el grosor del borde para adaptarlo al énfasis visual.

- **Estilo:** Elija un patrón de borde: sólido, discontinuo o punteado.

- **Edge:** Seleccione entre esquinas redondeadas o nítidas para el borde.

- **Radio:** Ajuste la redondez de la esquina utilizando valores de radio específicos (por ejemplo, 4 píxeles, 10 píxeles) para suavizar o enfocar el aspecto del campo.

2.6 Presencia

Controla la visibilidad del campo numérico durante el tiempo de ejecución.

- **Visible:** Estado predeterminado; el campo se muestra normalmente.

- **Oculto (mantiene el espacio):** El campo es invisible pero el espacio se mantiene en el diseño.

2.7 Enlace de datos

**Tipo de enlace de datos:** Conecta el campo numérico a un origen de datos (XML o JSON) para la integración en tiempo real.

**Nombre de usuario:** enlaza el campo a su nombre único para capturar valores de forma simple.

**Usar datos globales:** vincula el campo a un nodo de datos compartidos en formularios o fragmentos.

**Sin enlace de datos:** Mantiene el campo estático para uso de solo visualización o entrada temporal.

## &#x200B;3. Uso

Los campos numéricos son ideales en situaciones en las que solo los dígitos son entradas válidas. Los casos de uso comunes incluyen los siguientes:

- Capturando **números móviles, OTP y PIN**

- Introduciendo **números de póliza o ID de empleado**

- Recopilando **cantidades numéricas o valores monetarios**

- Habilitar **campos numéricos basados en pasos** (por ejemplo, contadores o entradas de puntuación)

Los autores pueden colocar campos numéricos dentro de contenedores de diseño o subformularios y aplicar validaciones (como restricciones de longitud, mínimo o máximo valor) para mejorar la calidad de los datos.

## &#x200B;4. Prácticas recomendadas

- Etiquete claramente los campos numéricos con las unidades si es necesario (por ejemplo, &quot;Cantidad en ₹&quot;).

- Aplique validación de formato (como límites de 10 dígitos para números de teléfono) para mejorar la precisión.

- Utilice valores de reserva cuando los campos sean obligatorios pero puedan faltar datos dinámicos.

- Enlace los campos numéricos cuidadosamente a las rutas de esquema para admitir el procesamiento back-end.

- Mantenga un aspecto y una tipografía coherentes para que coincidan con las directrices de marca.

El objeto **Campo numérico** del editor de comunicaciones interactivas es una herramienta precisa y confiable para la recopilación de datos basados en dígitos. Gracias a sus sólidas opciones de formato, controles de visibilidad y enlace de datos, garantiza que las entradas numéricas se capturan sin problemas y se integran perfectamente en los formularios digitales. Cuando se diseña y configura correctamente, mejora significativamente la capacidad de uso del formulario y la precisión general de los datos.


