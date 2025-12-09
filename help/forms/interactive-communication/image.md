---
title: Componente de imagen en el editor de comunicaciones interactivas
description: Componente de imagen en el editor de comunicaciones interactivas de AEM Forms para permitir a los autores mejorar los diseños de comunicación mediante la inserción de imágenes estáticas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 14%

---


# Componente de imagen en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Imagen del Editor de comunicaciones interactivas permite a los autores mejorar los diseños de comunicación mediante la inserción de imágenes estáticas. Este componente es esencial para crear diseños visualmente atractivos e incorporar elementos de marca como logotipos o iconos visuales. Los autores pueden colocarlo en las páginas maestras y en la vista Diseño para garantizar un aspecto coherente en varios formatos de salida, como PDF.

![Buscar documento CI](/help/forms/interactive-communication/assets/image.1.png)

## 2.Properties

El componente Imagen proporciona varias propiedades para ayudar a configurar su aspecto, aspecto y comportamiento.

2.1. Descripción de la imagen

Nombre:
Actúa como identificador único del componente de imagen, lo que permite hacer referencia fácilmente dentro de la jerarquía del componente o del editor de reglas.

Seleccionar imagen: permite al autor cargar una imagen o hacer referencia a ella, como un logotipo, un icono o cualquier otro elemento visual estático de varias fuentes.


2.2. Posición

Descripción: controla la ubicación espacial de la imagen en el diseño.

Configuración:

Coordenadas X e Y

Altura y anchura (en mm)

Margen de 2,3

Defina el espaciado alrededor del cuadro de texto:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4. Aspecto

Aspecto: define el estilo visual del campo de imagen, elige ajustes preestablecidos como borde, plano o elevado, y personaliza con el color de relleno, el ancho de trazo y el estilo de esquina (redondeado o nítido).

2.5. Presencia

Descripción: Determina la visibilidad del componente de imagen durante la ejecución.

- Opciones:

   - Visible

   - Oculto (mantiene el espacio)

## 3.Usage

El componente Imagen es ideal para lo siguiente:

- Inserción de logotipos en encabezados de documento

- Mostrar imágenes de productos en facturas o presupuestos

- Mejora de la participación visual en las comunicaciones

## 4.Prácticas recomendadas

- Utilice imágenes de una biblioteca compartida para facilitar la reutilización y la coherencia.

- Mantenga la forma de la imagen consistente para evitar estiramientos o pixelados.

- Evite utilizar archivos de imagen muy grandes para mantener el documento rápido y adaptable.

- Configure la imagen para que se muestre u oculte condicionalmente si no siempre es necesaria.

El componente Imagen de la comunicación interactiva de AEM desempeña un papel vital en la creación de comunicaciones de marca, personalizadas y visualmente eficaces. Con propiedades configurables, mejora la experiencia del usuario al tiempo que mantiene la coherencia del diseño en diferentes formatos.
