---
title: Objeto de campo de fecha en el editor de comunicaciones interactivas
description: El objeto de campo de fecha del Editor de comunicaciones interactivas de AEM Forms permite a los autores insertar un campo de selección de fecha basado en calendario en un documento.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 8%

---


# Objeto de campo de fecha en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente **Campo de fecha** del editor de comunicaciones interactivas (IC) permite a los autores insertar un campo de selección de fecha basado en calendario en un documento. Esto permite a los usuarios elegir fácilmente una fecha de un selector de fechas o introducirla manualmente en un formato predefinido.

Ideal para capturar fechas de nacimiento, horarios de citas, fechas de aplicación o fechas de inicio y finalización de directivas, el campo de fecha mejora la precisión y reduce los errores de entrada. Admite formato, estilo y enlace de datos para una integración perfecta con modelos de datos y sistemas back-end.

![Buscar documento CI](/help/forms/interactive-communication/assets/date.png)

## &#x200B;2. Propiedades

El objeto Campo de fecha incluye varias propiedades configurables:

2.1. Campo básico

- **Nombre:** Identificador único usado para hacer referencia al campo en reglas, scripts y modelos de datos.

- **Pie de ilustración:** Etiqueta de visualización mostrada al usuario (por ejemplo, &quot;Fecha de nacimiento&quot;).

- **Fecha:** El valor de fecha real, que puede estar vacío de forma predeterminada o rellenado previamente con datos dinámicos.

- **Reservar:** Una fecha de reserva opcional (mostrada si no se ha seleccionado ninguna fecha o los datos no están disponibles).

- **Aspecto:** Un ajuste preestablecido de estilo rápido (por ejemplo, subrayado, plano, con bordes) para mantener la coherencia visual.

2.2. Tipografía

Controla la forma en que la fecha aparece visualmente dentro del campo:

- **Variación de fuente:** Elija la familia de fuentes, el grosor (por ejemplo, Normal, Negrita) y el estilo (por ejemplo, Cursiva).

- **Tamaño:** Se suele establecer en 10 puntos de forma predeterminada, pero se puede personalizar para mantener la coherencia con el contenido circundante.

2.3. Posición

Define la ubicación espacial dentro del diseño del documento:

- **Coordenadas X e Y:** Determina la ubicación horizontal y vertical.

- **Anchura y altura:** establecida en milímetros o porcentajes para alinearse con otros elementos de formulario.

2.4. Margen

Especifica el espaciado alrededor de los límites del campo:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

Estos valores ayudan a lograr una alineación precisa dentro de los subformularios o las cuadrículas de diseño.

2.5. Aspecto

Define el estilo visual del contenedor de campos:

- **Relleno:** Color de fondo del campo (por ejemplo, blanco, gris claro).

- **Trazo:** Color de borde o contorno.

- **Anchura:** Grosor del borde del campo.

- **Estilo:** Opciones de línea continua, discontinua o de puntos.

- **Bordes:** permite personalizar las esquinas como redondeadas o nítidas para distintas preferencias de diseño.

2.6. Presencia

Determina cómo y cuándo aparece el campo:

- **Visible:** Valor predeterminado donde el campo se muestra durante la ejecución.

- **Oculto (mantiene el espacio):** El campo permanece invisible, pero el espacio de diseño se conserva.

Esto resulta útil al alternar la visibilidad de forma dinámica en función de los datos introducidos por el usuario o las reglas.

2.7. Enlace de datos

Conecta el campo de fecha a estructuras de datos para almacenar o rellenar previamente los valores.

**Tipo de enlace de datos:**

- **Nombre de usuario:** enlaza el campo al esquema mediante su atributo name.

- **Usar datos globales:** Los enlaces utilizan un modelo de datos predefinido o un elemento de esquema.

- **Sin enlace de datos:** El campo permanece estático, no está conectado a ningún origen de datos.

Esto permite recuperar, mostrar o almacenar los valores de fecha dinámicos en función de la lógica de la aplicación.

## &#x200B;3. Uso

El campo Fecha es especialmente útil en los siguientes casos:

- Registrar la fecha de nacimiento o de unión en formularios de incorporación.

- Selección de las fechas de inicio y finalización de los servicios, las suscripciones o los eventos.

- Ingresar fechas límites de solicitud, espacios para citas o fechas de verificación.

Los autores pueden colocar el campo de fecha dentro de contenedores de diseño o subformularios y configurar la validación (por ejemplo, formato de fecha, límites de intervalo) para mejorar la calidad de los datos.

## &#x200B;4. Prácticas recomendadas

- Use subtítulos claros como &quot;Fecha de inicio&quot; o &quot;Seleccionar fecha de cita&quot; para una mejor experiencia de usuario.

- Establezca intervalos de fechas mínimos y máximos para evitar entradas no válidas (por ejemplo, futuros DOB).

- Aplique estilos de fuente coherentes (se recomiendan 10 puntos) para mejorar la legibilidad.

- Enlace los campos al esquema siempre que se necesite la integración de datos back-end.

- Oculte de forma dinámica los campos de fecha no relevantes mediante reglas de visibilidad.

El objeto **Campo de fecha** del editor de comunicaciones interactivas es una potente herramienta para capturar datos con distinción de tiempo de forma precisa y sencilla. Cuando se diseña meticulosamente y se conecta a rutas de datos significativas, admite una experiencia de usuario perfecta y un procesamiento eficiente de entradas basadas en el tiempo.


