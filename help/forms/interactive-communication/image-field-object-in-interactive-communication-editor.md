---
title: Objeto de campo de imagen en el editor de comunicaciones interactivas
description: Objeto de campo de imagen en el editor de comunicaciones interactivas de AEM Forms para permitir a los autores insertar imágenes en un diseño de comunicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 10%

---


# Objeto de campo de imagen en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Campo de imagen del editor de comunicaciones interactivas permite a los autores insertar imágenes en un diseño de comunicación. Es ideal para casos de uso como identificación con fotos, verificación de documentos o validación visual donde es esencial mostrar una imagen al usuario final.

Compatible con formatos comunes como **JPEG** y **PNG**, este componente ofrece opciones de configuración flexibles para definir cómo se muestra, almacena y diseña la imagen. Los autores también pueden **asignar un nombre o una etiqueta** al campo de imagen, lo que mejora la claridad y organización del diseño.

![Buscar documento CI](/help/forms/interactive-communication/assets/imagefield.png)

## &#x200B;2. Propiedades

El objeto Campo de imagen incluye varias propiedades configurables:

2.1. Campo básico

- **Nombre:** Defina un identificador único para el campo, usado para hacer referencia a reglas y modelos de datos.

- **Pie de ilustración:** Muestra la etiqueta mostrada a los usuarios en la interfaz.

- **Seleccionar imagen:** Permita que el autor cargue una imagen mediante esta propiedad, que normalmente se utiliza para logotipos, ID u otros elementos visuales.

- **Reservar imagen:** Defina la alineación de la imagen, izquierda, derecha, superior o inferior, o especifique una **posición personalizada** con unidades como milímetros (por ejemplo, 20 mm).

2.2. Posición

Controla la ubicación espacial de la imagen en el diseño.

- Coordenadas X e Y

- Altura y anchura (en mm)

2.3. Margen

Defina el espaciado alrededor del cuadro de texto:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4. Aspecto

Aspecto: define el estilo visual del campo de imagen, elige ajustes preestablecidos como borde, plano o elevado, y personaliza con el color de relleno, el ancho de trazo y el estilo de esquina (redondeado o nítido).

2.5. Presencia

Determina la visibilidad del objeto de imagen durante la ejecución.

- Visible

- Oculto (mantiene el espacio)

2.6. Enlace de datos

Vincule el campo de imagen a una fuente de datos para recuperar y mostrar el contenido de imagen dinámico dentro de la comunicación.

**Tipo de enlace de datos:** Define la forma en que el campo de imagen se conecta a la estructura o esquema de datos subyacente.

**Nombre de usuario:** Enlaza el campo de imagen con el nombre de campo especificado en el esquema o modelo de datos, lo que permite que la imagen se rellene dinámicamente durante la ejecución.

**Usar datos globales:** Conecta el campo de imagen con los datos globales que se comparten en toda la comunicación, lo que garantiza la coherencia en el contenido visual.

**Sin enlace de datos:** Mantiene el campo desconectado de cualquier dato del servidor, lo cual es ideal en los casos en que se muestra una imagen estática o cuando la imagen se controla exclusivamente a través de la configuración de la interfaz de usuario.

## &#x200B;3. Uso

El campo de imagen es útil en contextos en los que se requiere el envío de contenido visual. Los casos de uso comunes incluyen los siguientes:

- Carga de la prueba de ID (pasaporte, licencia)

- Enviar fotos de perfil o personales

- Adjuntar visualmente documentos de apoyo

Los autores pueden colocar el campo dentro de subformularios o contenedores de diseño para su alineación y utilizar reglas de validación personalizadas para controlar los tipos y tamaños de archivo aceptados.

## &#x200B;4. Prácticas recomendadas

- Utilice etiquetas o instrucciones claras cuando solicite que se carguen imágenes.

- Limite el tamaño y los formatos del archivo mediante la validación del rendimiento.

- Asegúrese de que las imágenes de reserva (reserva) sean accesibles.

- Enlace el campo a una ruta de esquema significativa si la integración con el back-end

El objeto Campo de imagen del editor de comunicaciones interactivas es un componente versátil que mejora la interactividad del formulario al habilitar las cargas de contenido visual. Cuando se diseña con estilo, validación y enlace de datos, admite una experiencia del usuario perfecta y una captura de datos eficiente para los envíos basados en imágenes.




