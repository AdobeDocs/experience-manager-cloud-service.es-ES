---
title: Componente Cuadro de texto en el editor de comunicaciones interactivas
description: El componente Cuadro de texto del Editor de comunicaciones interactivas en AEM Forms permite a los autores introducir y mostrar contenido de texto dentro de una comunicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: 6bed824c-b959-4882-a5aa-dbb7fbf2f8a0
source-git-commit: ea372529b504ed70b74171e75d1d54f98fef432c
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 4%

---

# Componente Cuadro de texto en el editor de comunicaciones interactivas


## &#x200B;1. Introducción

El componente **Cuadro de texto** del Editor de comunicaciones interactivas permite a los autores introducir y mostrar contenido de texto dentro de una comunicación. Es uno de los componentes más fundamentales y ampliamente utilizados, que se utilizan comúnmente para recopilar nombres, comentarios, comentarios o datos personalizados al diseñar comunicaciones interactivas o fragmentos de comunicación.

El cuadro de texto admite **enlace de datos**, lo que permite a los autores combinar contenido estático y dinámico sin problemas, por ejemplo: ***&quot;Nombre de usuario: @name&quot;***, donde @name es un campo de datos enlazado que se rellena dinámicamente cuando el documento se guarda como PDF. Además, admite el formato de texto enriquecido y una posición flexible para un control preciso del diseño.

![Buscar documento CI](/help/forms/interactive-communication/assets/textbox.png)

## &#x200B;2. Patrón de visualización

Puede asignar un **patrón de visualización** a un campo de cuadro de texto desde el panel **Propiedades**. Los patrones de visualización controlan cómo se presentan los valores de campo a los usuarios finales en la vista previa del lienzo y en la salida generada; por ejemplo, enmascarando una entrada de texto como número de teléfono: **(555) 123-4567**.

El patrón configurado se refleja inmediatamente en la vista previa del lienzo y se conserva en los ciclos de guardado y recarga. Para casos de uso avanzados, puede definir una **cláusula de imagen XFA personalizada** para obtener el formato de salida deseado.

### Configuración de un patrón de visualización

1. Seleccione el componente Cuadro de texto en el lienzo de diseño.
2. Abra el panel **Propiedades**.
3. En la sección **Patrón de visualización**, elija un patrón predefinido o escriba una cláusula de imagen personalizada.
4. Previsualice el valor formateado en el lienzo.

### Ejemplo de patrón personalizado (texto)

| Patrón | Salida de ejemplo | Descripción |
|---------|----------------|-------------|
| `text{(999) 999-9999}` | (555) 123-4567 | Máscara de número de teléfono |

**Símbolos de la cláusula de imagen (texto):**

| Símbolo | Significado |
|--------|---------|
| 9 | Coincide con un dígito |
| A | Coincide con una carta |
| O | Coincide con alfanumérico |
| X | Coincide con cualquier carácter |

### Prácticas recomendadas

- Elija un patrón que coincida con la forma en que los usuarios finales esperan leer el valor (teléfono, ID, código postal).
- Valide los datos de ejemplo en la vista previa del lienzo antes de publicar.
- Utilice cláusulas de imagen personalizadas únicamente cuando los motivos predefinidos no satisfagan sus necesidades de formato.

## &#x200B;3. Propiedades

El componente cuadro de texto proporciona un amplio conjunto de propiedades para ayudar a configurar su aspecto, presentación y comportamiento.

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



## &#x200B;4. Uso

El cuadro de texto se utiliza para:

- Recopilar información del cliente, como nombres, comentarios o comentarios.

- Introducción de valores alfanuméricos.

- Integración de mensajes personalizados con modelos de datos enlazados.

- Incrustar dentro de fragmentos para su uso repetido en todos los documentos.

Los autores pueden arrastrar el cuadro de texto desde la biblioteca de componentes hasta la vista Diseño o la vista Patrón y configurar su comportamiento mediante el panel Propiedades.

## &#x200B;5. Prácticas recomendadas

- Asocie siempre los cuadros de texto con etiquetas de campo significativas para mejorar la accesibilidad.

- Utilice las validaciones de entrada adecuadas para evitar errores de entrada de datos.

- Asegúrese de que el diseño sea adaptable al establecer los márgenes y las anchuras en relación con los contenedores principales.

- Evite estilos de fuente excesivos que puedan dificultar la legibilidad.

Al configurar las propiedades del cuadro de texto con cuidado, los autores pueden crear experiencias de comunicación interactivas, interactivas y fáciles de usar dentro del Editor de comunicaciones interactivas de AEM.

## Ver también

- [Componente de campo numérico](/help/forms/interactive-communication/numeric-field.md)
- [Componente Campo de fecha](/help/forms/interactive-communication/date-field.md)
- [Componente de campo de fecha y hora](/help/forms/interactive-communication/date-time-field.md)
- [Componente de variable independiente](/help/forms/interactive-communication/unbound-variable.md)
- [Configurar el enlace de datos en el editor de comunicaciones interactivas](/help/forms/interactive-communication/configure-data-binding.md)
- [Usar el Editor de reglas en el Editor de comunicaciones interactivas](/help/forms/interactive-communication/use-the-rule-editor.md)
