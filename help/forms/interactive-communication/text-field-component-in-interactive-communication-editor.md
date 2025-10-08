---
title: Componente Campo de texto en el editor de comunicaciones interactivas
description: Componente Campo de texto en el editor de comunicaciones interactivas de AEM Forms para permitir a los autores mostrar información como nombres, direcciones, comentarios o ID numéricos.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 7%

---


# Componente Campo de texto en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Campo de texto del editor de comunicaciones interactivas (IC) permite a los autores mostrar información como nombres, direcciones, comentarios o ID numéricos. El valor mostrado en el campo de texto está predefinido (estático) o se rellena dinámicamente mediante el enlace de datos. Admite entradas de una sola línea, reglas de validación y formatos flexibles, lo que lo convierte en uno de los elementos más utilizados y versátiles en las comunicaciones personalizadas.

![Buscar documento CI](/help/forms/interactive-communication/assets/textfield.png)

## &#x200B;2. Propiedades

2.1 Campo básico

- **Nombre:** Defina un identificador único para el campo, que se usará en modelos de datos, reglas y scripts.

- **Pie de ilustración:** Muestra la etiqueta en pantalla a los usuarios (por ejemplo, &quot;Nombre&quot;).

- **Valor:** Muestra texto como nombres, direcciones, comentarios u otros detalles. El valor es estático o se deriva del enlace de datos.

- **Reservar:** Establezca la alineación del valor, izquierda, derecha, superior o inferior, o especifique una posición personalizada utilizando unidades como milímetros (por ejemplo, 20 mm).

- **Aspecto:** Establezca el aspecto del cuadro de valor como Ninguno, Cuadro sólido o Subrayado en función del diseño visual deseado.

2.2 Tipografía

Controla el estilo visual de los caracteres escritos:

- **Validación de fuente:** Aplique restricciones opcionales para validar el formato del valor mostrado, como permitir sólo caracteres alfabéticos, números o motivos personalizados específicos.

- **Tamaño de fuente:** Ajuste el tamaño del texto dentro del campo con valores de punto como 10 pt, 12 pt, 20 pt, etc., para garantizar la legibilidad y la alineación con los estándares de diseño.

Posición 2.3

Define la ubicación del campo dentro del diseño:

- **Coordenadas X / Y**

- **Anchura y altura** (mm, píxeles o %)

Margen de 2,4

Especifica el espacio alrededor del contenedor de campos:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.5 Aspecto

Estila el propio contenedor de campo:

- **Relleno:** Establece el color de fondo del cuadro de texto. Esto ayuda a distinguir las áreas de entrada o alinearlas con los colores de la marca.

- **Trazo:** Agregue bordes alrededor del cuadro de texto con las siguientes propiedades personalizables:

- **Anchura:** Defina el grosor del borde.

- **Estilo:** Elija entre estilos de borde sólido, discontinuo o punteado.

- **Edge:** Seleccione la forma de las esquinas, ya sea redondeada o nítida.

- **Radio:** Ajuste la curvatura de la esquina con valores de radio (por ejemplo, 4 px, 10 px) para obtener un aspecto más suave o más angular.

2.6 Presencia

Determina la visibilidad durante la ejecución:

- **Visible:** se muestra y ocupa espacio

- **Oculto (mantiene el espacio):** Invisible, pero el espacio de diseño está reservado

2.7 Enlace de datos

Vincula el campo de texto a una fuente de datos para mostrar valores de forma dinámica o estática dentro de la comunicación.

- **Tipo de enlace de datos:** Especifica cómo se conecta el campo a un origen de datos o esquema.

- **Usar nombre:** Enlaza el campo de texto usando el nombre de campo definido en el modelo de datos o esquema, permitiendo la visualización de texto dinámico basado en datos externos.

- **Usar datos globales:** Conecta el campo a los datos globales que se comparten en toda la comunicación para obtener una visualización coherente de la información.

- **Sin enlace de datos:** Mantiene el campo desenlazado de cualquier origen backend. Se utiliza para mostrar valores estáticos o texto destinado únicamente a contexto visual.

## &#x200B;3. Uso

Los escenarios comunes incluyen:

- Captura de datos personales (nombres, direcciones, números de teléfono)

- Aceptar comentarios o comentarios (multilínea)

- Introducción de números de política o ID de cuenta

- Recopilación de valores numéricos cortos, como códigos PIN u OTP

Los autores pueden colocar el campo en subformularios o cuadrículas de diseño para su alineación y adjuntar reglas de validación (límites de longitud, patrones regex) para garantizar una entrada limpia.

## &#x200B;4. Prácticas recomendadas

- Aplique la validación (indicadores obligatorios, comprobaciones de patrones) para obtener comentarios inmediatos.

- Proporcionar texto de reserva significativo para vistas impresas o de solo lectura.

- Mantenga la tipografía coherente con las directrices de marca.

- Reduzca la anchura del campo en los diseños móviles para adaptarlo a pantallas más pequeñas.

- Enlace directamente al modelo de datos siempre que sea posible para un mantenimiento más sencillo.

El componente Campo de texto del editor de CI es un bloque de creación versátil que optimiza la captura de datos. Cuando se configura cuidadosamente, con una tipografía bien elegida, etiquetas claras, una validación adecuada y un enlace de datos sólido, ofrece una experiencia fácil de usar y datos fiables para el procesamiento posterior.


