---
title: Objeto de campo Fecha/Hora en el Editor de comunicaciones interactivas
description: Objeto de campo Fecha/Hora en el Editor de comunicaciones interactivas de AEM Forms para permitir a los autores insertar campos en los que los usuarios pueden seleccionar o introducir valores de fecha y hora.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 8%

---


# Objeto de campo Fecha/Hora en el Editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente **Campo de fecha y hora** del editor de comunicaciones interactivas (IC) permite a los autores insertar campos en los que los usuarios pueden seleccionar o introducir valores de fecha y hora. Este componente se utiliza comúnmente para recopilar información como la fecha de nacimiento, los horarios de las citas, las franjas horarias de reserva o las fechas de emisión/caducidad del documento.

El campo admite varias opciones de formato (por ejemplo, formatos DD/MM/AAAA, de 24 o 12 horas), restricciones de validación y personalización de la apariencia para que coincida con el diseño de la comunicación. Mejora la experiencia del usuario al reducir los errores de entrada manuales y promover la coherencia en la recopilación de datos.

![Buscar documento CI](/help/forms/interactive-communication/assets/datetime.png)

## &#x200B;2. Propiedades

El objeto Campo de fecha y hora incluye varias propiedades configurables:

2.1. Campo básico

- **Nombre:** Identificador único del campo. Se utiliza como referencia en reglas, expresiones y enlaces de datos.

- **Pie de ilustración:** La etiqueta se muestra junto al campo para indicar su propósito (por ejemplo, &quot;Fecha de nacimiento&quot;).

- **Fecha:** Permite que los usuarios elijan o introduzcan una fecha de calendario.

- **Hora:** habilita la entrada o selección de valores de hora específicos si están configurados.

- **Reservar:** Se muestra un valor de reserva cuando no se proporciona ninguna entrada, lo cual resulta útil en escenarios de sólo lectura o de impresión.

- **Apariencia:** Seleccione un estilo visual como subrayado, borde o plano para obtener una representación uniforme de la interfaz de usuario.

2.2. Tipografía

Controla el estilo del texto dentro del campo de fecha y hora:

- **Variación de fuente:** Las opciones incluyen Normal, Negrita y Cursiva según los requisitos del tema.

- **Tamaño de fuente:** El valor predeterminado es 10 pt para mantener la coherencia con el diseño del formulario.

2.3. Posición

- **Descripción:** define la ubicación del campo de fecha y hora en el diseño del formulario.

- **Configuración:**

   - **Coordenadas X e Y**

   - **Altura y anchura** (medidas en mm o píxeles) para ajustar el tamaño del campo con precisión.

2.4. Margen

Define el espaciado alrededor del campo para una alineación limpia y la flexibilidad del diseño:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.5. Aspecto

Define el estilo del contenedor para mantener la coherencia y la claridad visuales:

- **Relleno:** Color de fondo del campo.

- **Trazo:** Color del borde alrededor del campo.

- **Anchura:** Grosor del borde.

- **Estilo:** Tipos de borde como sólido, discontinuo o ninguno.

- **Bordes:** Elija entre esquinas nítidas o redondeadas según el tema del formulario.

2.6. Presencia

Determina cómo se comporta el campo durante la ejecución:

- **Visible:** El campo se muestra a los usuarios y ocupa espacio de diseño.

- **Oculto (mantiene el espacio):** El campo no está visible, pero aún se reserva espacio para él en el diseño.

2.7. Enlace de datos

Vincula el campo a una fuente de datos para almacenar o recuperar valores.

- **Tipo de enlace de datos:** Especifica cómo se conecta el campo a los datos.

- **Nombre de usuario:** enlaza el campo con el nombre de campo definido en el esquema.

- **Usar datos globales:** Conecta el campo con datos de nivel global compartidos a través de la comunicación.

- **Sin enlace de datos:** El campo no está conectado a ningún dato backend (se usa solo para valores visuales o calculados).

## &#x200B;3. Uso

El campo de fecha y hora es ideal en escenarios donde se requieren datos temporales coherentes. Los casos de uso comunes incluyen los siguientes:

- Captura de la fecha de nacimiento, fecha de cita u hora del evento

- Registrando problema de documento/Fechas de caducidad

- Selección de las ranuras de entrega o recogida

- Registro de Marcas de Hora de Transacciones

Los autores pueden combinar el campo con contenedores de diseño, validaciones o reglas condicionales para controlar el formato, los campos obligatorios y la visibilidad contextual.

## &#x200B;4. Prácticas recomendadas

- Utilice leyendas claras como &quot;Seleccionar una fecha&quot; o &quot;Hora de la cita&quot; para guiar a los usuarios.

- Habilite el selector de fecha y hora para mejorar la experiencia de usuario y reducir los errores de entrada.

- Aplique restricciones de formato (por ejemplo, solo fechas futuras) cuando sea necesario.

- Proporcione un valor de reserva para accesibilidad o para la reserva de impresión.

- Mantenga una tipografía y un aspecto coherentes con el diseño general del formulario.

- Enlace el campo a una ruta de esquema válida para garantizar una captura y un procesamiento de datos adecuados.

El objeto Campo de fecha y hora del editor de comunicaciones interactivas es un componente potente y fácil de usar que optimiza la entrada basada en el tiempo. Con la configuración correcta de estilo, administración de datos y controles de diseño, permite experiencias de formulario limpias, fiables e intuitivas tanto para usuarios como para sistemas back-end.