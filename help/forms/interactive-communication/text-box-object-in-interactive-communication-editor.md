---
title: Objeto de cuadro de texto en el editor de comunicaciones interactivas
description: El objeto de cuadro de texto del Editor de comunicaciones interactivas de AEM Forms permite a los autores introducir y mostrar contenido de texto dentro de una comunicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: acad9e05288a606c54e2059c2381725ac982f7d8
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 11%

---


# Objeto de cuadro de texto en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El objeto **Cuadro de texto** del Editor de comunicaciones interactivas permite a los autores introducir y mostrar contenido de texto dentro de una comunicación. Es uno de los componentes más fundamentales y ampliamente utilizados, que se utilizan comúnmente para recopilar nombres, comentarios, comentarios o datos personalizados al diseñar comunicaciones interactivas o fragmentos de comunicación.

El cuadro de texto admite **enlace de datos**, lo que permite a los autores combinar contenido estático y dinámico sin problemas, por ejemplo: ***&quot;Nombre de usuario: @name&quot;***, donde @name es un campo de datos enlazado que se rellena dinámicamente cuando el documento se guarda como PDF. Además, admite el formato de texto enriquecido y una posición flexible para un control preciso del diseño.

![Buscar documento CI](/help/forms/interactive-communication/assets/textbox.png)

## &#x200B;2. Propiedades

El objeto de cuadro de texto proporciona un amplio conjunto de propiedades que ayudan a configurar su aspecto, presentación y comportamiento.

2.1 Tipografía

**Familia de fuentes:** Permite la selección de estilos de fuente como Arial, Helvetica, Times New Roman, etc.

**Validación de fuente:** Se pueden aplicar restricciones de entrada opcionales para asegurarse de que sólo se aceptan formatos de texto, numéricos o especiales.

**Alineación del texto:** Las opciones incluyen alineación a la izquierda, a la derecha, al centro o justificada.

**Estilo de texto:** Habilite el formato de texto con las características de negrita, cursiva, tachado y subrayado.

**Listas:** Admite la inserción de listas ordenadas (numeradas) y sin ordenar (con viñetas).

Posición 2.2

**Anchura y altura:** Establezca las dimensiones del cuadro de texto en píxeles o porcentaje en relación con el contenedor.

Margen de 2,3

Defina el espaciado alrededor del cuadro de texto:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4 Aspecto

- **Relleno de texto:** Personalizar el color y la transparencia del texto.

- **Relleno:** Establecer el color de fondo del cuadro de texto.

- **Trazo:** Agregue bordes con elementos personalizables:

   - Anchura (grosor)

   - Estilo (sólido, discontinuo, punteado)

   - Edge (esquinas redondeadas o nítidas)

2.5 Presencia

**Visible:** Configuración predeterminada; el cuadro de texto se muestra al usuario.

**Oculto:** El cuadro de texto está incluido en el formulario, pero no se muestra.



## &#x200B;3. Uso

El cuadro de texto se utiliza para:

- Recopilar información del cliente, como nombres, comentarios o comentarios.

- Introducción de valores alfanuméricos.

- Integración de mensajes personalizados con modelos de datos enlazados.

- Incrustar dentro de fragmentos para su uso repetido en todos los documentos.

Los autores pueden arrastrar el cuadro de texto desde la Biblioteca de objetos hasta la vista Diseño o la vista Patrón y configurar su comportamiento mediante el Panel de propiedades.

## &#x200B;4. Prácticas recomendadas

- Asocie siempre los cuadros de texto con etiquetas de campo significativas para mejorar la accesibilidad.

- Utilice las validaciones de entrada adecuadas para evitar errores de entrada de datos.

- Asegúrese de que el diseño sea adaptable al establecer los márgenes y las anchuras en relación con los contenedores principales.

- Evite estilos de fuente excesivos que puedan dificultar la legibilidad.

Al configurar las propiedades del cuadro de texto con cuidado, los autores pueden crear experiencias de comunicación interactivas, interactivas y fáciles de usar dentro del Editor de comunicaciones interactivas de AEM.
