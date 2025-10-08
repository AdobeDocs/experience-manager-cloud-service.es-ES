---
title: Componente Casilla de verificación en el editor de comunicaciones interactivas
description: El componente Casilla de verificación del Editor de comunicaciones interactivas en AEM Forms permite a los usuarios realizar selecciones binarias únicas o múltiples (sí/no, true/false).
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: bd8992792afddb2243736578acd24bc47efad842
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 8%

---


# Componente Casilla de verificación en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente Casilla de verificación del editor de comunicaciones interactivas (IC) permite a los usuarios realizar selecciones binarias únicas o múltiples (sí/no, true/false). Se utiliza comúnmente para términos y condiciones, preferencias, campos de consentimiento y opciones de inclusión, y proporciona una forma rápida de capturar la entrada booleana dentro de un formulario de comunicación.

La casilla de verificación admite estilos flexibles, opciones de enlace de datos y reglas de visibilidad, lo que la convierte en una herramienta ligera pero potente para diseñar formularios interactivos y fáciles de usar.

![Buscar documento CI](/help/forms/interactive-communication/assets/checkbox.png)

## &#x200B;2. Propiedades

2.1 Campo básico

- **Nombre:** Identificador único usado para hacer referencia a la casilla de verificación en modelos de datos, reglas o scripts.

- **Alternar:** Permite activar o desactivar la casilla de verificación al hacer clic. Se puede utilizar en modo individual o agrupado.

- **Pie de ilustración:** Etiqueta descriptiva que se muestra al lado de la casilla de verificación, que guía a los usuarios sobre lo que están aceptando o seleccionando.

- **Reservar:** texto o símbolo de marcador de posición opcional que se muestra en los modos de sólo lectura o de reserva cuando no se realiza ninguna interacción.

Posición 2.2

Define dónde se coloca la casilla de verificación en el diseño:

- **Coordenadas X e Y:** Establezca la ubicación de la casilla de verificación dentro de la cuadrícula de diseño.

- **Altura y anchura:** define las dimensiones de la casilla de verificación (en mm o píxeles), lo que es especialmente importante cuando se utilizan iconos o estilos visuales personalizados.

Margen de 2,3

Permite espaciar la casilla de verificación para realizar ajustes de diseño:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4 Aspecto

Controla el estilo visual de la casilla de verificación y su marco:

- **Relleno:** Color de fondo de la casilla de verificación (cuando está seleccionada o no seleccionada).

- **Trazo:** El color del contorno del borde de la casilla de verificación.

- **Anchura de trazo:** Grosor de la línea de borde.

- **Estilo:** Patrón de esquema sólido, discontinuo o personalizado.

- **Bordes:** Define el estilo de esquina de la casilla de verificación: bordes redondeados o afilados según las preferencias de diseño.

2.5 Presencia

Determina cómo y cuándo aparece la casilla de verificación durante la ejecución:

- **Visible:** se muestra normalmente y ocupa espacio.

- **Oculto (mantiene el espacio):** Oculto de la interfaz de usuario, pero se conserva el espacio de diseño. Útil para la visibilidad condicional sin interrupciones en el diseño.

2.6 Enlace de datos

Activa la casilla de verificación para interactuar con fuentes de datos externas o internas:

**Tipo de enlace de datos:**

**Nombre de usuario:** enlaza el valor mediante el nombre de campo del componente.

**Usar datos globales:** Se conecta a un modelo de datos globales compartido en la comunicación.

**Sin enlace de datos:** La casilla de verificación permanece independiente y no está almacenada en el modelo de datos.

&#x200B;3. Uso

Las casillas de verificación se utilizan comúnmente en escenarios como:

- **Campos de consentimiento:** p. ej., &quot;Acepto los términos y condiciones&quot;

- **Preferencias de usuario:** p. ej., &quot;Suscribirse a la newsletter&quot;

- **Selecciones de varias opciones:** p. ej., &quot;Seleccionar todas las opciones aplicables&quot;

- **Confirmaciones de formulario:** Por ejemplo: &quot;Confirmo que los detalles anteriores son correctos&quot;

Las casillas de verificación se pueden colocar dentro de cuadrículas o paneles de diseño y agruparse para mejorar la organización en los formularios.

&#x200B;4. Prácticas recomendadas

- Utilice subtítulos claros y concisos para ayudar a los usuarios a comprender lo que están seleccionando.

- Evite el desorden utilizando casillas de verificación solo para entradas binarias: utilice botones de opción para opciones exclusivas.

- Asegúrese de que el espaciado sea el adecuado mediante la configuración de margen y diseño para una interfaz de usuario limpia.

- Enlace las casillas de verificación a una referencia de modelo de datos significativa cuando sea necesario almacenar o procesar la opción capturada.

- Utilice reglas de visibilidad cuando las casillas de verificación dependan de entradas o condiciones anteriores.

El componente Casilla de verificación del editor de comunicaciones interactivas es un componente simple pero esencial para las entradas binarias. Gracias a su compatibilidad con el estilo, la presencia condicional y el enlace de datos flexible, desempeña un papel clave en la mejora de la interactividad y el control de usuario en los formularios digitales inteligentes. Cuando se implementan con etiquetas reflexivas, un estilo coherente y una integración de datos significativa, las casillas de verificación contribuyen de manera significativa a una experiencia de formulario sencilla e intuitiva.


