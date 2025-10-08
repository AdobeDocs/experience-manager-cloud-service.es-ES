---
title: Componente de código de barras en el editor de comunicaciones interactivas
description: El componente de código de barras del Editor de comunicaciones interactivas en AEM Forms permite a los autores representar visualmente los datos codificados dentro de las plantillas de comunicación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 7%

---


# Componente de código de barras en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Código de barras del editor de comunicaciones interactivas permite a los autores representar visualmente los datos codificados dentro de las plantillas de comunicación. Esto resulta particularmente útil en aplicaciones que implican seguimiento, identificación, facturación o automatización. Con compatibilidad con varios estándares de código de barras como Código 128, QR y más, este componente ofrece opciones flexibles de estilo, posicionamiento y enlace de datos para adaptarse a una amplia gama de necesidades comerciales.

Tanto si va a crear facturas de clientes, etiquetas de envío o tarjetas de socio, el componente Código de barras simplifica el proceso al incrustar datos legibles por el equipo directamente en el documento.

![Buscar documento CI](/help/forms/interactive-communication/assets/barcode.png)

## &#x200B;2. Propiedades

El componente de código de barras incluye un conjunto completo de opciones configurables para controlar su comportamiento y aspecto:

2.1 Campo básico

**Nombre:** Identificador único del código de barras. Se utiliza para hacer referencia al componente en modelos de datos y conjuntos de reglas.

**Ubicación:** Especifica dónde se muestra el texto del código de barras en relación con el símbolo del código de barras.

**Opciones:**

- **Ninguno:** Oculta el texto.

- **Arriba:** Muestra el texto sobre el código de barras.

- **Debajo:** Muestra el texto debajo del código de barras.

- **Sobre incrustado:** Incrusta el texto en el área superior del código de barras.

- **Incrustado debajo:** Incrusta el texto dentro del área inferior del código de barras.

- **Tipo:** Especifica el estándar de código de barras (por ejemplo, Código 128, Código 39, Código QR, etc.).

- **Valor predeterminado:** Valor predefinido que aparece si no se proporcionan datos.

- **Longitud de datos:** Indica el número esperado o máximo de caracteres que puede contener el código de barras.

- **Suma de comprobación:** Valida la precisión de los datos del código de barras.

   - **Opciones:**

      - **Ninguno:** No hay validación de suma de comprobación.

      - **Automático:** calcula automáticamente la suma de comprobación en función del tipo.

- **Proporción ancha/estrecha:** Define la anchura relativa de las barras anchas respecto a las estrechas (utilizadas en algunos códigos de barras 1D).

2.2 Ubicación

Determina dónde aparece el código de barras en relación con el contenido:

- **Ninguno:** No hay posicionamiento adicional.

- **Arriba:** coloca el código de barras sobre el contenido relacionado.

- **Por debajo:** Coloca el código de barras debajo del contenido.

- **Sobre incrustado:** El código de barras está incrustado y flota sobre el contenido.

- **Incrustado inferior:** Incrustado debajo del contenido.

Posición 2.3

Define la ubicación exacta del código de barras dentro del diseño:

- **Coordenadas X e Y:** Coloque el código de barras dentro del formulario utilizando unidades milimétricas.

- **Altura y anchura:** Defina las dimensiones físicas del código de barras.

Margen de 2,4

Añade espacio alrededor del código de barras para una mejor separación visual:

- Arriba

- Inferior

- Izquierda

- Derecha

Estos márgenes ayudan a mantener la coherencia y legibilidad del diseño.

2.5 Aspecto

Personalice el estilo visual del código de barras:

- **Relleno:** Color de fondo del área de código de barras.

- **Trazo:** Color del borde.

- **Anchura:** Define el grosor de las líneas de código de barras.

- **Estilo:** Elija entre ajustes preestablecidos como plano, con borde o elevado.

- **Bordes:** Decida entre esquinas redondeadas o nítidas para el cuadro de código de barras.

2.6 Presencia

Controla si el código de barras se muestra o se oculta durante la ejecución:

- **Visible:** El código de barras se muestra en la salida final.

- **Oculto:** Espacio reservado, pero no se muestra el código de barras.

2.7 Enlace de datos

Enlace de datos: conecta el código de barras a un modelo de datos back-end (XML o JSON). Esto garantiza que el código de barras refleje dinámicamente los datos únicos por instancia de documento, como un ID de pedido o un número de seguimiento.

## &#x200B;3. Uso

El componente Código de barras es especialmente útil para automatizar procesos que dependen de datos escaneados. Se puede agregar a plantillas de comunicación como:

- Facturas (para referencia del cliente y pagos de exploración rápida)

- Etiquetas de envío (para el seguimiento de paquetes)

- Tarjetas de membresía o fidelización (para identificación basada en escaneo)

- Cupones y cupones (para validación en el punto de venta)

Los autores pueden incrustar el código de barras en contenedores de diseño y aplicarle un estilo según la marca o el tema del documento.

## &#x200B;4. Prácticas recomendadas

- Utilice un tipo de código de barras adecuado para el caso de uso, por ejemplo, Código QR para URL o Código 128 para ID alfanuméricos.

- Valide la legibilidad del código de barras imprimiendo versiones de prueba y escaneándolas.

- Garantice la integridad de los datos mediante la opción de suma de comprobación si el estándar de código de barras lo admite.

- Elija tamaños y anchos de línea legibles para evitar problemas de digitalización.

- Mantenga los márgenes adecuados para evitar el recorte al imprimir.

El componente Código de barras del editor de comunicaciones interactivas permite a los creadores de documentos salvar la distancia entre los sistemas digitales y físicos. Cuando se implementa con eficacia, mejora la automatización, mejora la comodidad del usuario y admite la integración perfecta con dispositivos de digitalización y flujos de trabajo.
