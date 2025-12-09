---
title: Componente Botón de opción del editor de comunicaciones interactivas
description: El componente Botón de opción del Editor de comunicaciones interactivas en AEM Forms permite a los autores presentar un conjunto de opciones mutuamente excluyentes a los usuarios, lo que significa que solo se puede seleccionar una opción a la vez.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: e651869132a232db577e94946c082c46eea26bb3
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 9%

---


# Componente Botón de opción del editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El componente **Botón de opción** del editor de comunicaciones interactivas (IC) permite a los autores presentar un conjunto de opciones mutuamente exclusivas a los usuarios, lo que significa que solo se puede seleccionar una opción a la vez. Esto lo hace ideal para casos de uso como preguntas Sí/No, selección de sexo, niveles de clasificación o respuestas categóricas predefinidas.
Los botones de opción son intuitivos, fáciles de configurar y se pueden enlazar a modelos de datos back-end para una captura e integración de datos sin problemas.

![Buscar documento CI](/help/forms/interactive-communication/assets/radio.png)

## &#x200B;2. Propiedades

El componente Botón de opción incluye varias propiedades configurables:

2.1. Campo básico

- **Nombre:** Identificador único del campo. Se utiliza para hacer referencia dentro de modelos de datos, reglas y lógica empresarial.

- **Alternar:** Permite definir cada opción seleccionable en el grupo de botones. Cada alternancia representa un valor posible.

- **Pie de ilustración:** Etiqueta asociada al grupo de botones de opción para guiar al usuario.

- **Reservar:** Valor de reserva opcional si no se realiza ninguna selección o si el enlace de datos está vacío.

2.2. Posición

Descripción: controla la ubicación espacial del grupo de botones de opción en el diseño.

**Configuración:**

- **Coordenadas X e Y**

- **Altura y anchura** (definidas en mm o % para el diseño interactivo)

2.3. Margen

Defina el espaciado alrededor del cuadro de texto:

- Superior (arriba)

- Inferior (abajo)

- Izquierda

- Derecha

2.4. Presencia

- **Descripción:** Determina la visibilidad del componente del botón de radio durante la ejecución.

- **Opciones:**

   - **Visible:** se muestra a los usuarios y ocupa espacio.

   - **Oculto (mantiene el espacio):** No visible pero conserva el espaciado del diseño.



2.5. Enlace de datos

- **Descripción:** conecta el grupo de botones de opción a un modelo de datos para capturar la opción seleccionada.

- **Tipos de enlace:**

   - **Usar nombre:** Usa el nombre de campo asignado como referencia para el enlace.

   - **Usar datos globales:** enlaza el campo a un modelo de datos global o a un elemento de esquema.

   - **Sin enlace de datos:** La selección del botón de opción no está vinculada a ningún origen de datos; se usa para el comportamiento de solo interfaz de usuario.

## &#x200B;3. Uso

El componente Botón de opción es adecuado para escenarios en los que los usuarios deben elegir solo un valor de una lista. Los casos de uso habituales incluyen:

- Selección de un método de comunicación preferido (correo electrónico/teléfono/SMS)

- Confirmación de decisiones binarias (Sí / No)

- Elegir entre opciones limitadas (por ejemplo, Sexo, Estado civil)

- Indicación de niveles de satisfacción o escalas de acuerdo (por ejemplo, No conforme/Neutro/De acuerdo)

Los autores pueden agrupar los botones de opción relacionados y colocarlos dentro de contenedores de diseño para lograr una alineación coherente. Las etiquetas se pueden colocar en línea o encima de los botones según los requisitos de diseño visual.

## &#x200B;4. Prácticas recomendadas

- Limite el número de opciones a 5 o menos para evitar saturar al usuario.

- Utilice subtítulos claros y concisos para describir lo que selecciona el usuario.

- Preseleccione la opción más común o segura, si corresponde.

- Evite utilizar botones de opción cuando los usuarios tengan permiso para elegir más de una opción; en su lugar, utilice casillas de verificación.

- Enlace los botones de opción directamente a los nodos de esquema al integrarse con modelos de datos back-end.

- Aplique un espaciado y una alineación coherentes para una mejor claridad visual, especialmente en diseños aptos para móviles.

El componente Botón de opción del editor de comunicaciones interactivas es un componente de entrada fundamental que ofrece una toma de decisiones limpia y estructurada para los usuarios finales. Cuando se configura con etiquetas claras, espaciado cuidadoso y enlace de datos, garantiza una recopilación de datos confiable y una experiencia de usuario más fluida para formularios, encuestas y flujos de trabajo de incorporación.


