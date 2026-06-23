---
title: Componente de variable independiente en el editor de comunicaciones interactivas
description: El componente Variable no enlazada del Editor de comunicaciones interactivas permite mostrar valores calculados, scripts o configurados de forma independiente con control de formato completo.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: unbound-variable-ic-editor
source-git-commit: ea372529b504ed70b74171e75d1d54f98fef432c
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 2%

---


# Componente de variable independiente en el editor de comunicaciones interactivas


## &#x200B;1. Introducción

El componente **Variable independiente** en el editor de comunicaciones interactivas (IC) le permite colocar un campo cuyo valor no está vinculado a ningún nodo de esquema o modelo de datos externo. En su lugar, el valor se proporciona mediante scripts, cálculo basado en reglas o un valor predeterminado estático, lo que convierte a este componente en la opción correcta siempre que necesite un valor de visualización calculado o intermedio que no provenga directamente de una fuente de datos enlazada.

Dado que una variable no enlazada no está conectada a un modelo de datos de formulario, proporciona control de creación completo sobre el valor en tiempo de diseño y en tiempo de ejecución. Puede utilizarlo para mostrar totales calculados, números de referencia generados dinámicamente, resultados de fórmulas intermedias o cualquier otro valor que produzca el motor de reglas.

El componente admite los cuatro tipos de datos **Texto**, **Numérico**, **Fecha** y **Fecha/Hora**, y el tipo de datos activo determina qué sintaxis de patrón de visualización y símbolos de cláusula de imagen se aplican.

## &#x200B;2. Patrón de visualización

Puede asignar un **patrón de visualización** a un campo de variable independiente desde el panel **Propiedades**, utilizando los mismos controles de patrón de visualización disponibles para los componentes Cuadro de texto, Campo numérico, Campo de fecha y Campo de fecha y hora. Esto permite la presentación con formato de valores calculados o referenciados en la vista previa del lienzo y en la salida generada.

El patrón configurado se refleja inmediatamente en la vista previa del lienzo y se conserva en los ciclos de guardado y recarga.

### Configuración de un patrón de visualización

1. Seleccione el componente Variable independiente en el lienzo de diseño.
2. Abra el panel **Propiedades**.
3. En la sección **Patrón de visualización**, elija un patrón predefinido o escriba una cláusula de imagen personalizada.
4. Previsualice el valor formateado en el lienzo.

### Elección del patrón correcto

Dado que una variable independiente puede contener cualquier tipo de datos, la sintaxis de la cláusula de imagen que utilice debe coincidir con el tipo de datos configurado del campo:

| Tipo de datos de campo | Sintaxis de patrón | Salida de ejemplo | Referencia |
|-----------------|----------------|----------------|-----------|
| Texto | `text{…}` | (555) 123-4567 | [Cuadro De Texto — Patrón De Visualización](/help/forms/interactive-communication/text-box.md#2-display-pattern) |
| Numérica | `num{…}` | $1,234.21 | [Campo numérico — Patrón de visualización](/help/forms/interactive-communication/numeric-field.md#2-display-pattern) |
| Fecha | `date{…}` | 01/04/2007 | [Campo De Fecha — Patrón De Visualización](/help/forms/interactive-communication/date-field.md#2-display-pattern) |
| Fecha/hora | `date{…} time{…}` | 04/01/2007 14:30 | [Campo De Fecha/Hora — Patrón De Visualización](/help/forms/interactive-communication/date-time-field.md#2-display-pattern) |

>[!NOTE]
>
> Si el tipo de datos del campo es Fecha o Fecha/Hora, el valor subyacente debe ajustarse al formato **ISO 8601** (`YYYY-MM-DD` o `YYYY-MM-DDTHH:MM`). Los valores que no siguen este formato se muestran tal cual, sin aplicar el patrón de visualización.

## &#x200B;3. Propiedades

El componente Variable no enlazada comparte un conjunto de propiedades comunes con otros componentes de campo, con una distinción clave: no tiene opciones de enlace de datos externas porque, por definición, su valor es independiente de cualquier origen de datos.

3.1 Campo básico

- **Nombre:** Identificador único de la variable. Se utiliza para hacer referencia a él en reglas, scripts y expresiones dentro de la CI.

- **Tipo de datos:** Especifica el tipo de valor que contiene esta variable **Texto**, **Numérico**, **Fecha** o **Fecha/Hora**. El tipo de datos seleccionado determina qué sintaxis de patrón de visualización se aplica y cómo se valida el valor.

- **Pie de ilustración:** La etiqueta mostrada junto al campo en el lienzo (por ejemplo, &quot;Total calculado&quot; o &quot;Número de referencia&quot;).

- **Valor:** Valor predeterminado o calculado que se muestra en el campo. En la mayoría de los casos, esto se establece mediante programación utilizando el Editor de reglas o una secuencia de comandos, en lugar de escribirse manualmente.

- **Reservar:** Valor de reserva mostrado cuando no hay ningún valor calculado disponible, útil para la salida de sólo impresión o de sólo lectura cuando un campo en blanco es inaceptable.

- **Aspecto:** Un ajuste preestablecido de estilo visual (Ninguno, Cuadro sólido o Subrayado) para el contenedor de campos.

3.2 Tipografía

Controla el estilo del valor mostrado:

- **Variación de fuente:** Elija la familia de fuentes, el grosor (Normal, Negrita) y el estilo (Cursiva) para que coincidan con el contenido circundante.

- **Tamaño de fuente:** Se establece normalmente en 10 pt de forma predeterminada; ajústelo para mantener la coherencia visual con el resto de la comunicación.

Posición 3.3

Define la ubicación del componente en el lienzo:

- **Coordenadas X e Y:** Establezca la posición horizontal y vertical exacta.

- **Anchura y altura:** Especifique dimensiones en milímetros para alinearlas con elementos adyacentes.

Margen 3.4

Define el espaciado alrededor del límite del componente:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

3.5 Aspecto

Estilos en el contenedor de campo:

- **Relleno:** Color de fondo del campo.

- **Trazo:** Borde alrededor del campo, con las siguientes opciones:

   - **Anchura:** Espesor del borde.

   - **Estilo:** sólido, discontinuo o punteado.

   - **Edge:** esquinas redondeadas o nítidas.

3.6 Presencia

Controla la visibilidad durante la ejecución:

- **Visible:** El campo se muestra y ocupa espacio de diseño.

- **Oculto (mantiene el espacio):** El campo es invisible pero su espacio de diseño se conserva, lo que resulta útil cuando se cambia la visibilidad de forma dinámica mediante el Editor de reglas.

## &#x200B;4. Uso

Utilice una variable independiente cuando el valor que desee mostrar sea:

- **Calculado mediante una regla o script**; por ejemplo, un total acumulado, un cálculo de impuestos o un importe de descuento derivado de otros valores de campo.

- **Generado mediante programación**; por ejemplo, un número de referencia o código de seguimiento asignado en tiempo de ejecución por lógica back-end.

- **No disponible en el modelo de datos**; por ejemplo, un resultado intermedio que tiene sentido en pantalla pero no existe como campo de esquema.

- **Visible condicionalmente**: muestra un mensaje o valor calculado solo cuando se cumplen condiciones específicas, usando el Editor de reglas para establecer visibilidad y valor juntos.

Puede colocar una variable independiente dentro de subformularios, contenedores de diseño o directamente en el lienzo de diseño. Combínelo con el Editor de reglas para escribir expresiones que calculen su valor en función de otros campos enlazados en la CI.

## &#x200B;5. Prácticas recomendadas

- **Establezca un valor de reserva significativo** para que las vistas previas de solo lectura y de salida de impresión nunca muestren un campo en blanco cuando el valor calculado no esté disponible.

- **Hacer coincidir el tipo de datos con el resultado**: si está calculando una cantidad de moneda, establezca el tipo de datos en Numérico y aplique un patrón de visualización numérico; si calcula una fecha, establézcalo en Fecha y asegure la entrada ISO 8601.

- **Use un subtítulo sin cifrar**: dado que el valor se calcula y no se puede reconocer directamente a partir de una etiqueta, un subtítulo descriptivo (por ejemplo, &quot;Subtotal (calculado)&quot;) evita confusiones tanto para los revisores como para los usuarios finales.

- **Evite el uso excesivo de variables no enlazadas para los datos que pertenezcan al modelo**; si es razonable agregar un valor al modelo de datos de formulario, prefiera enlazar un campo estándar. Reserve Variables no enlazadas para valores que sean genuinamente transitorios o derivativos.

- **Documente sus expresiones**: agregue un comentario en el Editor de reglas que describa lo que calcula cada variable independiente, de modo que la lógica se mantenga cuando se edite la CI más adelante.

## Ver también

- [Componente Cuadro de texto](/help/forms/interactive-communication/text-box.md) — sintaxis de patrón de visualización para valores de texto
- [Componente de campo numérico](/help/forms/interactive-communication/numeric-field.md) — sintaxis de patrón de visualización para valores numéricos y monetarios
- [Componente de campo de fecha](/help/forms/interactive-communication/date-field.md) — sintaxis de patrón de visualización para fechas
- [Componente de campo de fecha y hora](/help/forms/interactive-communication/date-time-field.md): muestra la sintaxis del patrón para los valores de fecha y hora combinados
- [Usar el Editor de reglas en el Editor de comunicaciones interactivas](/help/forms/interactive-communication/use-the-rule-editor.md): escriba expresiones para calcular y asignar valores a variables independientes
- [Configurar el enlace de datos en el editor de comunicaciones interactivas](/help/forms/interactive-communication/configure-data-binding.md)
