---
title: Editor de reglas para Dynamic Forms en el editor universal
description: Cree formularios inteligentes y dinámicos con el Editor de reglas en el Editor universal. Agregue lógica condicional, cálculos y comportamientos interactivos sin codificación.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '3597'
ht-degree: 23%

---


# Editor de reglas para Dynamic Forms en el editor universal

El Editor de reglas del Editor universal permite crear formularios inteligentes y dinámicos que responden a los datos introducidos por el usuario en tiempo real. Puede transformar formularios estáticos en experiencias interactivas con visibilidad de campo condicional, cálculos automatizados y lógica empresarial compleja, todo sin escribir código.

## Lo que aprenderá

Al final de esta guía, deberá hacer lo siguiente:

- Comprender cómo funcionan las reglas y cuándo utilizar diferentes tipos de reglas
- Habilite y acceda al Editor de reglas en el Editor universal
- Crear una lógica condicional para mostrar u ocultar campos de formulario de forma dinámica
- Implementación de cálculos automatizados y validación de datos
- Crear funciones personalizadas para reglas empresariales complejas
- Aplicar las prácticas recomendadas para obtener un rendimiento óptimo de los formularios

## ¿Por qué utilizar el Editor de reglas?

**Transformar Forms estático en experiencias inteligentes:**

- **Lógica condicional**: mostrar campos relevantes basados en las selecciones del usuario
- **Cálculos dinámicos**: calcule automáticamente los valores a medida que escriben los usuarios
- **Validación de datos**: proporciona comentarios en tiempo real y evita errores
- **UX mejorado**: reduce la complejidad del formulario y guía a los usuarios a través de flujos lógicos
- **No se requiere codificación**: la interfaz visual es accesible para quienes no son desarrolladores

**Casos de uso comunes:**

- Formularios de cálculo de impuestos con deducciones condicionales
- Asistentes de varios pasos con rutas ramificadas
- Formularios de seguro con cálculos de tasa
- Formularios de encuesta con preguntas condicionales
- Formularios de comercio electrónico con precios dinámicos

## Cómo funcionan las reglas

Las reglas son instrucciones automatizadas que hacen que los formularios sean inteligentes y adaptables. Especifican lo que debe suceder cuando se cumplen ciertas condiciones.

### **Componentes de regla**

**Condición**: una prueba lógica que se evalúa como verdadera o falsa.

- &quot;¿Es el ingreso del usuario mayor a $50,000?&quot;
- &quot;¿Ha seleccionado el usuario &#39;Sí&#39; para la cobertura de seguro?&quot;
- &quot;¿Está vacío el campo del formulario?&quot;

**Acción**: Resultado que se produce cuando se cumple la condición.

- Mostrar u ocultar campos de formulario
- Calcular valores automáticamente
- Mostrar mensajes de validación
- Habilitar o deshabilitar componentes

### **Patrones de lógica de regla**

**1. Condición-Acción (Cuándo-Entonces)**

```
WHEN gross salary > 50000
THEN show "Additional Deduction" field
```

*Ideal para:* Visibilidad condicional de campo, contenido dinámico

**2. Condición de acción (Set-If)**

```
SET taxable income = gross salary - deductions
IF deductions are applicable
```

*Lo mejor para:* Cálculos, transformaciones de datos

**3. Acción-Condición-Alternativa (If-Then-Else)**

```
IF income > 50000
THEN show "High Income" fields
ELSE show "Standard Income" fields
```

*Lo mejor para:* Lógica de ramificación, opciones mutuamente excluyentes

### **Ejemplo en el mundo real**

**Escenario**: formulario de cálculo de impuestos

- **Condición**: &quot;El salario bruto supera los 50.000 dólares&quot;
- **Acción principal**: mostrar el campo &quot;Deducción adicional&quot;
- **Acción alternativa**: ocultar el campo &quot;Deducción adicional&quot;
- **Resultado**: Los usuarios solo ven los campos relevantes según su nivel de ingresos

## Requisitos previos

Antes de empezar a trabajar con el Editor de reglas, asegúrese de que dispone de lo siguiente:

### **Requisitos de acceso**

- Creando acceso a **AEM as a Cloud Service**
- **Editor universal** con la extensión del Editor de reglas habilitada
- Permisos de edición de formularios en el entorno de AEM

### **Requisitos técnicos**

- **Conocimientos básicos sobre diseño de formularios**: Familiaridad con los componentes de formulario y sus propiedades
- **Familiaridad con la lógica empresarial**: capacidad para definir requisitos condicionales
- **Conocimientos básicos de JavaScript** (solo se requieren para funciones personalizadas)

### **Habilitar extensión del editor de reglas**

La extensión del editor de reglas no está habilitada de forma predeterminada en el editor universal. Puede habilitarlo desde [Extension Manager](/help/implementing/developing/extending/extension-manager.md).

**Después de habilitar la extensión:**
El icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg) aparece en la esquina superior derecha al seleccionar componentes de formulario.

![Editor universal de reglas](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
*Imagen: el icono Editor de reglas aparece al seleccionar componentes de formulario*

**Para tener acceso al Editor de reglas:**

1. Seleccione cualquier componente del formulario en el editor universal.
2. Haga clic en el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg) que aparece.
3. La interfaz del Editor de reglas se abre en un panel nuevo.

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-for-field.png)
*Figura: Interfaz del editor de reglas para editar reglas de componentes*

>[!NOTE]
>
> En este artículo, &quot;componente de formulario&quot; y &quot;objeto de formulario&quot; hacen referencia a los mismos elementos (como campos de entrada, botones, paneles, etc.).

## Resumen de interfaz del Editor de reglas

El Editor de reglas ofrece una interfaz visual fácil de usar para crear y administrar reglas:

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-interface.png)
*Figura: Interfaz completa del Editor de reglas con componentes numerados*

### **Componentes de interfaz**

**1. Título de componente y tipo de regla**

- **Propósito**: muestra el nombre del componente seleccionado y el tipo de regla actual.
- **Ejemplo**: &quot;Ingresar salario bruto&quot; (entrada de texto) con la regla &quot;When&quot; seleccionada.
- **Sugerencia**: Confirme siempre que está editando el componente correcto.

**2. Panel de funciones y objetos de formulario**

- **Ficha Objetos de formulario**: Proporciona una vista jerárquica de todos los componentes de formulario.
   - Se utiliza para: Hacer referencia a otros campos de las reglas.
   - Navegación: expanda o contraiga para localizar componentes específicos.
- **Ficha Funciones**: Contiene funciones matemáticas y lógicas integradas.
   - Se utiliza para: realizar cálculos complejos y manipulaciones de datos.
   - Categorías: Funciones matemáticas, cadena, fecha y validación.

**3. Botón de alternancia del panel**

- **Propósito**: muestra u oculta el panel de funciones y objetos.
- **Sugerencia**: Desactive el panel para aumentar el área de trabajo de edición de reglas.
- **Método abreviado de teclado**: útil cuando se trabaja con reglas complejas.

**4. Generador de reglas visual**

- **Propósito**: El área principal para construir la lógica de regla.
- **Características**: selectores desplegables e interfaz de arrastrar y soltar.
- **Flujo de trabajo**: seleccione el tipo de regla → Definir condiciones → Establecer acciones.

**5. Botones de control**

- **Listo**: guarda la regla y cierra el editor.
- **Cancelar**: descarta los cambios y cierra el editor sin guardarlo.
- **Sugerencia**: Pruebe siempre las reglas antes de hacer clic en Listo.

### **Administración de reglas**

Al abrir el Editor de reglas para un componente que ya tiene reglas:

![mostrar las reglas disponibles del objeto de formulario](/help/edge/docs/forms/assets/rule-editor15.png)
*Figura: Administrar reglas existentes para un componente de formulario*

**Acciones disponibles:**

- **Ver**: revise los resúmenes y la lógica de las reglas.
- **Editar**: modifique las condiciones o acciones de regla existentes.
- **Reordenar**: cambie el orden de ejecución de las reglas (las reglas se ejecutan de arriba abajo).
- **Habilitar/Deshabilitar**: Activar o desactivar temporalmente las reglas para realizar pruebas.
- **Eliminar**: quite las reglas de forma permanente.

>[!TIP]
>
> **Importancia de orden de ejecución de reglas**: las reglas se ejecutan de arriba a abajo. Coloque condiciones más específicas antes de las generales.

## Tipos de reglas disponibles

El Editor de reglas ofrece un conjunto completo de tipos de reglas organizadas por funcionalidad. Seleccione el tipo adecuado en función de su caso de uso específico:

### **Reglas de lógica condicional**

**When**

- **Propósito**: Sirve como regla condicional principal para implementar lógica compleja.
- **Caso de uso**: Por ejemplo, &quot;Cuando el usuario seleccione &#39;Casado&#39;, mostrar campos de información del cónyuge&quot;.
- **Patrón lógico**: condición → acción (con una acción alternativa opcional)

**Ocultar/Mostrar**

- **Propósito**: controla la visibilidad de los campos según las condiciones especificadas.
- **Caso de uso**: oculta secciones irrelevantes o habilita la divulgación progresiva.
- **Práctica recomendada**: Use para crear una experiencia de usuario limpia y centrada.

**Habilitar/Deshabilitar**

- **Propósito**: controla si se puede interactuar con un campo según las condiciones.
- **Caso de uso**: deshabilite el botón de envío hasta que se completen todos los campos obligatorios.
- **Práctica recomendada**: Proporcione comentarios visuales claros a los usuarios.

### **Reglas de manipulación de datos**

**Establecer Valor De**

- **Propósito**: Rellena automáticamente los valores de los campos.
- **Caso de uso**: establezca la fecha de hoy, calcule los totales o copie los valores entre los campos.
- **Práctica recomendada**: Use para reducir el esfuerzo del usuario y garantizar la precisión.

**Borrar Valor De**

- **Propósito**: quita datos de los campos cuando cambian las condiciones.
- **Caso de uso**: borre los campos dependientes cuando cambie una selección principal.
- **Práctica recomendada**: Mantener la integridad de los datos y evitar valores huérfanos.

**Formato**

- **Propósito**: transforma el modo en que se muestran los valores.
- **Caso de uso**: Aplicar formato a moneda, números de teléfono o fechas.
- **Práctica recomendada**: Mejore la legibilidad sin alterar los datos subyacentes.

### **Reglas de validación**

**Validate**

- **Propósito**: implementa la lógica de validación personalizada.
- **Caso de uso**: Aplicar reglas de negocio complejas o validación entre campos.
- **Práctica recomendada**: Proporcione mensajes de error claros y procesables.

### **Reglas de cálculo**

**Expresión matemática**

- **Propósito**: realiza cálculos automatizados.
- **Caso de uso**: Cálculos de impuestos, totales o porcentajes.
- **Práctica recomendada**: Actualice los cálculos en tiempo real mientras los usuarios escriben.

### **Reglas de interfaz de usuario**

**Definir enfoque**

- **Propósito**: dirige la atención del usuario a campos específicos.
- **Caso de uso**: Céntrese en los campos de error o guíe a los usuarios a través de los pasos del asistente.
- **Práctica recomendada**: Use con moderación para evitar interrumpir el flujo de usuario.

**Set Property**

- **Propósito**: modifica dinámicamente las propiedades de los componentes.
- **Caso de uso**: cambie el texto del marcador de posición o modifique las opciones en un menú desplegable.
- **Práctica recomendada**: Mejore la experiencia del usuario con cambios contextuales.

### **Reglas de control de formularios**

**Enviar formulario**

- **Propósito**: el envío del formulario de Déclencheur se realiza mediante programación.
- **Caso de uso**: Enviar automáticamente después de cumplir ciertas condiciones.
- **Práctica recomendada**: Valide siempre el formulario antes de enviarlo.

**Restablecer formulario**

- **Propósito**: borra todos los datos de formulario y restablece el formulario a su estado inicial.
- **Caso de uso**: Funcionalidad &quot;Comenzar de nuevo&quot;.
- **Práctica recomendada**: Confirme la acción con el usuario antes de restablecer.

**Guardar formulario**

- **Propósito**: guarda el formulario como borrador para completarlo más adelante.
- **Caso de uso**: útil para formularios largos o flujos de trabajo de varias sesiones.
- **Práctica recomendada**: Proporcione comentarios claros sobre el estado de guardado.

### **Reglas avanzadas**

**Invocar servicio**

- **Propósito**: Llama a API o servicios externos.
- **Caso de uso**: búsqueda de direcciones, validación en tiempo real o enriquecimiento de datos.
- **Práctica recomendada**: Controle correctamente los estados de carga y los escenarios de error.

**Agregar/Quitar instancia**

- **Propósito**: administra de forma dinámica secciones repetibles.
- **Caso de uso**: Agregar miembros de la familia o direcciones múltiples.
- **Práctica recomendada**: proporcione controles claros para agregar o quitar instancias.

**Ir A**

- **Propósito**: redirige a los usuarios a otros formularios o páginas.
- **Caso de uso**: Flujos de trabajo de varios formularios o enrutamiento condicional.
- **Práctica recomendada**: Conservar los datos del formulario antes de la navegación.

**Desplazarse Entre Paneles**

- **Propósito**: controla la navegación en formularios de estilo asistente.
- **Caso de uso**: omisión de formularios de varios pasos o de pasos condicionales.
- **Práctica recomendada**: Mostrar indicadores de progreso claros.

**Evento de envío**

- **Propósito**: Almacena en Déclencheur eventos personalizados para integraciones avanzadas.
- **Caso de uso**: Seguimiento de Analytics para integraciones de terceros.
- **Práctica recomendada**: usar solo para acciones que no sean de bloqueo.


## Tutorial paso a paso: Creación de una calculadora de impuestos inteligente

Esta sección proporciona un ejemplo práctico para mostrar las capacidades del Editor de reglas. El ejemplo le guía a través de la creación de un formulario de cálculo de impuestos que utiliza lógica condicional y cálculos automatizados.

![Captura de pantalla de la interfaz del Editor de reglas que muestra la creación de una regla condicional con lógica When-Then para la visibilidad del campo de formulario](/help/edge/docs/forms/assets/rule-editor-1.png)
*Imagen: formulario de cálculo de impuestos con campos condicionales inteligentes*

### **Información general del tutorial**

En este tutorial, creará un formulario que:

1. **Se adapta a los datos proporcionados por el usuario**: muestra los campos relevantes según el nivel de ingresos.
2. **Calcula automáticamente**: calcula la deuda tributaria en tiempo real.
3. **Valida datos**: garantiza cálculos y entradas de datos precisos.

### **Estructura de formulario**

| Nombre del campo | Tipo | Función | Comportamiento |
|------------|------|---------|----------|
| **Salario bruto** | Entrada de número | El usuario introduce ingresos anuales | Lógica condicional de Déclencheur |
| **Deducción adicional** | Entrada de número | Deducciones adicionales (si procede) | Muestra cuándo salario > 50 000 $ |
| **Ingresos gravables** | Entrada de número | Calculado automáticamente | Actualizaciones de cambios de entrada |
| **Impuestos por pagar** | Entrada de número | Importe final de impuestos | Calcula a una tasa del 10 % |

### **Lógica empresarial para implementar**

**Regla 1: Visualización condicional del campo**

```
WHEN Gross Salary > 50,000
THEN Show "Additional Deduction" field
ELSE Hide "Additional Deduction" field
```

**Regla 2: Cálculo de ingresos gravables**

```
SET Taxable Income = Gross Salary - Additional Deduction
(When Additional Deduction is applicable)
```

**Regla 3: Cálculo de impuestos**

```
SET Tax Payable = Taxable Income × 10%
(Simplified flat rate for demonstration)
```

### **Pasos de implementación**

Siga estos pasos para crear su formulario de impuestos inteligente:



+++ 1: Crear el formulario base

**Objetivo**: cree la estructura básica del formulario con todos los componentes necesarios

Para crear el formulario de cálculo de impuestos en el editor universal:

1. **Abrir editor universal**
   - Vaya a la consola de AEM Sites
   - Seleccione la página donde desea agregar el formulario
   - Haga clic en **Editar** para abrir el Editor universal

2. **Agregar componentes de formulario**

   Añada estos componentes en orden:

   | Componente | Tipo | Etiqueta | Configuración |
   |-----------|------|-------|----------|
   | Título | Título | &quot;Formulario de cálculo de impuestos&quot; | Nivel de encabezado H2 |
   | Entrada de número | Entrada de número | &quot;Salario bruto&quot; | Obligatorio: Sí, Marcador de posición: &quot;Introducir salario anual&quot; |
   | Entrada de número | Entrada de número | &quot;Deducción adicional&quot; | Obligatorio: No, Marcador de posición: &quot;Introducir deducciones adicionales&quot; |
   | Entrada de número | Entrada de número | &quot;Ingresos gravables&quot; | Obligatorio: No, solo lectura: Sí |
   | Entrada de número | Entrada de número | &quot;Impuesto a pagar&quot; | Obligatorio: No, solo lectura: Sí |
   | Botón Enviar | Enviar | &quot;Calcular impuesto&quot; | Tipo: Enviar |

3. **Configurar la configuración inicial**

   - **Ocultar el campo Deducción adicional**:
      - Seleccione el componente &quot;Deducción adicional&quot;
      - En el panel Propiedades, establezca **Visible** en **No**
      - Este campo se muestra de forma condicional según las reglas

   - **Hacer que los campos calculados sean de solo lectura**:
      - Seleccione los campos &quot;Ingresos gravables&quot; e &quot;Impuestos por pagar&quot;
      - Definir **Solo lectura** en **Sí** en las propiedades

     ![Captura de pantalla de un formulario de cálculo de impuestos con campos de entrada para el salario bruto, el estado civil y los hijos a cargo, que muestra la estructura del formulario antes de que se apliquen las reglas](/help/edge/docs/forms/assets/rule-editor2.png)
     *Figura: Estructura del formulario inicial con componentes básicos configurados*

**Punto de comprobación**: ahora debería tener un formulario con todos los campos obligatorios, donde Deducción adicional está oculta y los campos calculados son de sólo lectura.

+++

+++ &#x200B;2. Agregar una regla de condición para un campo de formulario

Una vez haya creado el formulario, escriba la primera regla para mostrar el campo `Additional Deduction` solo si el salario bruto supera los 50 000 $. Para añadir una regla de condición:

1. Abra un formulario en el Editor universal para editarlo, seleccione el campo **[!UICONTROL Salario bruto]** en el árbol de contenido y seleccione ![edit-rules](/help/forms/assets/edit-rules-icon.svg). También puede seleccionar el campo **[!UICONTROL salario bruto]** directamente desde el panel **[!UICONTROL Objeto de formularios]**.
   ![Ejemplo1 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor3.png)
Aparecerá la interfaz visual del Editor de reglas.
1. Haga clic en **[!UICONTROL Crear]** para crear reglas.
   ![Ejemplo2 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor4.png)
De forma predeterminada, el tipo de regla `Set Value Of` está seleccionado. Aunque no puede cambiar ni modificar el objeto seleccionado, puede utilizar la lista desplegable de reglas para seleccionar otro tipo de regla. \
   ![Ejemplo3 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor5.png)
1. Abra la lista desplegable de tipo de regla y seleccione el tipo de regla **[!UICONTROL Cuando]**.
   ![Ejemplo4 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor6.png)
1. Seleccione el menú desplegable **[!UICONTROL Seleccionar estado]** y seleccione **[!UICONTROL es superior a]**. Aparece el campo **[!UICONTROL Escribir un número]**.
   ![Ejemplo5 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor7.png)
1. Escriba `50000` en el campo **[!UICONTROL Escribir un número]** en la regla.
   ![Ejemplo6 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor8.png)
Ha definido la condición como `When Gross Salary is greater than 50000`. A continuación, defina la acción que se realizará si esta condición es `True`.
1. En la instrucción `Then`, seleccione **[!UICONTROL Mostrar]** en el menú desplegable **[!UICONTROL Seleccionar acción]**.
   ![Ejemplo7 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor9.png)
1. Arrastre y suelte el campo **[!UICONTROL Deducción adicional]** de la pestaña Objetos de formulario en el campo **[!UICONTROL Soltar objeto o seleccionar aquí]**. Como alternativa, seleccione el campo **[!UICONTROL Soltar objeto o seleccionar aquí]** y seleccione el campo **[!UICONTROL Deducción adicional]** en el menú emergente, que muestra todos los objetos del formulario.
   ![Ejemplo8 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor10.png)
1. Haga clic en **[!UICONTROL Añadir la sección O]** para añadir otra condición para el campo **[!UICONTROL Salario bruto]**, en caso de que especifique un salario inferior a `50000`.
   ![Ejemplo9 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor11.png)
1. Seleccione **[!UICONTROL Ocultar]** del menú desplegable **[!UICONTROL Seleccionar acción]** en la instrucción `Else`.
   ![Ejemplo10 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor12.png)
1. Arrastre y suelte el campo **[!UICONTROL Deducción adicional]** de la pestaña Objetos de formulario en el campo **[!UICONTROL Soltar objeto o seleccionar aquí]**. Como alternativa, seleccione el campo **[!UICONTROL Soltar objeto o seleccionar aquí]** y seleccione el campo **[!UICONTROL Deducción adicional]** en el menú emergente, que muestra todos los objetos del formulario.
   ![Ejemplo11 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor13.png)
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.
La regla aparece de la siguiente manera en el Editor de reglas.
   ![Ejemplo12 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> Como alternativa, puede escribir una regla Show en el campo Deducción adicional, en lugar de una regla When en el campo Salario bruto, para implementar el mismo comportamiento.

+++

+++ &#x200B;3. Añadir reglas de cálculo para los campos de formulario

A continuación, escriba una regla para calcular `Taxable Income`, que es la diferencia entre `Gross Salary` y `Additional Deduction` (si corresponde). Para añadir una regla de cálculo en el campo **[!UICONTROL Ingresos gravables]**, realice los siguientes pasos:

1. En el modo de creación, seleccione el campo **[!UICONTROL Ingresos gravables]** y seleccione el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg). También puede seleccionar el campo **[!UICONTROL Ingresos gravables]** directamente desde el panel **[!UICONTROL Objeto de formularios]**.
1. A continuación, seleccione **[!UICONTROL Crear]** para crear la regla.
   ![Ejemplo13 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor16.png)
1. Seleccione **[!UICONTROL Seleccionar opción]** y seleccione **[!UICONTROL Expresión matemática]**. Se abre un campo para escribir una expresión matemática.
   ![Ejemplo14 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor17.png)

1. En el campo de la expresión matemática:

   - Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Salario bruto]** en el primer campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.

   - Seleccione **[!UICONTROL Menos]** en el campo **[!UICONTROL Seleccionar operador]**.

   - Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Deducción adicional]** en el otro campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.
     ![Ejemplo15 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor18.png)

1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

   Ahora, añada una regla para el campo `Tax Payable `, que se determina multiplicando los ingresos gravables por la tasa de impuestos. Para simplificar, suponga una tasa de impuestos fija de `10%`.

1. En el modo de creación, seleccione el campo **[!UICONTROL Ingresos gravables]** y seleccione el icono ![edit-rules](/help/forms/assets/edit-rules-icon.svg). A continuación, seleccione **[!UICONTROL Crear]** para crear reglas.
   ![Ejemplo16 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor19.png)
1. Seleccione **[!UICONTROL Seleccionar opción]** y seleccione **[!UICONTROL Expresión matemática]**. Se abre un campo para escribir una expresión matemática.
   ![Ejemplo del editor de reglas17](/help/edge/docs/forms/assets/rule-editor20.png)
1. En el campo de la expresión matemática:

   - Seleccione o arrastre y suelte desde la pestaña Objeto de formularios el campo **[!UICONTROL Ingresos gravables]** en el primer campo **[!UICONTROL Soltar objeto o seleccionar aquí]**.

   - Seleccione **[!UICONTROL Multiplicado por]** en el campo **[!UICONTROL Seleccionar operador]**.

   - Seleccione **Número** del campo **[!UICONTROL Seleccionar opción]** e introduzca el valor como `10` en el campo **[!UICONTROL Escribir un número]**.
     ![Ejemplo18 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor21.png)
1. A continuación, seleccione el área resaltada alrededor del campo de expresión y haga clic en **[!UICONTROL Ampliar expresión]**.
   ![Ejemplo19 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor22.png)
1. En el campo para ampliar la expresión, seleccione **[!UICONTROL divided by]** en el campo **[!UICONTROL Seleccionar operador]** y **[!UICONTROL Número]** en el campo **[!UICONTROL Seleccionar opción]**. A continuación, especifique `100` en el campo de número.
   ![Ejemplo20 del Editor de reglas](/help/edge/docs/forms/assets/rule-editor23.png)
1. Seleccione **[!UICONTROL Listo]** para guardar la regla.

+++

+++ &#x200B;4. Previsualizar un formulario

Ahora, al obtener una vista previa del formulario e introducir el **Salario bruto** como `60,000`, aparecerá el campo **Deducción adicional**, y se calcularán en consecuencia los **Ingresos gravables** e **Impuestos por pagar**.

![Seleccionar un formulario](/help/edge/docs/forms/assets/rule-editor-form.png)

+++

Además de las funciones integradas como Suma y Promedio, puede crear funciones personalizadas para implementar una lógica empresarial compleja adaptada a sus necesidades específicas.

## Avanzadas: funciones personalizadas

**Cuándo usar funciones personalizadas:**

- Para cálculos complejos que superan las capacidades de las funciones integradas
- Para implementar reglas de validación específicas de la empresa
- Para transformaciones de datos y formato
- Para integrar con sistemas externos o API

**Beneficios:**

- **Reutilización**: escriba la función una vez y utilícela en varios formularios y reglas
- **Mantenimiento**: lógica centralizada fácil de actualizar
- **Rendimiento**: ejecución de JavaScript optimizada
- **Flexibilidad**: capacidad para controlar escenarios complejos a los que no se aplican reglas estándar

### **Creando funciones personalizadas**

**Ubicación de archivo**: `/blocks/form/functions.js` en su proyecto de AEM

**Flujo de trabajo de desarrollo:**

1. **Declaración de función**
   - Defina parámetros y nombres de función claros y descriptivos.
   - Utilice nombres que indiquen el propósito de la función
   - Parámetros de documento y tipos de valor devuelto

2. **Implementación lógica**
   - Escriba código JavaScript limpio y eficiente
   - Gestión de casos extremos y escenarios de error
   - Siga las prácticas recomendadas de codificación

3. **Exportación de funciones**
   - Exportar funciones para que estén disponibles en el Editor de reglas
   - Uso de exportaciones con nombre para mejorar la organización
   - Prueba de funciones antes de la implementación

4. **Documentación**
   - Agregar comentarios JSDoc para la documentación de funciones
   - Incluir ejemplos de uso
   - Especificar tipos de parámetros y valores devueltos

El ejemplo siguiente muestra dos funciones personalizadas: `getFullName` y `days`.

```JavaScript
/**
 - Get Full Name
 - @name getFullName Concats first name and last name
 - @param {string} firstname in Stringformat
 - @param {string} lastname in Stringformat
 - @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 - Calculate the number of days between two dates.
 - @param {*} endDate
 - @param {*} startDate
 - @name days Calculates the numebr of days between two dates
 - @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```

![Añadir una función personalizada](/help/edge/docs/forms/assets/create-custom-function.png)

### Uso de una función personalizada en el Editor de reglas

Para utilizar una función personalizada en el Editor de reglas:

1. **Agregar la función**: Agregue su función personalizada al archivo `../[blocks]/form/functions.js`. Asegúrese de incluirlo en la instrucción `export` dentro del archivo.
2. **Implementar el archivo**: Implemente el archivo `functions.js` actualizado en su proyecto de GitHub y confirme que la compilación se completa correctamente.
3. **Uso de funciones**: en el editor de reglas del formulario, para obtener acceso a la función, seleccione la opción `Function Output` en el campo **[!UICONTROL Seleccionar acción]**.

   ![Funciones personalizadas en el Editor de reglas](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

4. **Vista previa del formulario**: obtenga una vista previa del formulario para comprobar que la función recién implementada funciona según lo esperado.

## Prácticas recomendadas para el desarrollo de reglas

### **Optimización del rendimiento**

**Minimizar complejidad de reglas**

- Mantenga las reglas individuales simples y centradas.
- Divida la lógica compleja en varias reglas más pequeñas.
- Evite las condiciones profundamente anidadas cuando sea posible.

**Optimizar la ejecución de reglas**

- Coloque primero las reglas activadas con más frecuencia.
- Utilice condiciones específicas para reducir las evaluaciones innecesarias.
- Tenga en cuenta el impacto de las reglas en el tiempo de carga del formulario.

**Administración de recursos**

- Limite el número de reglas por componente de formulario.
- Utilice funciones personalizadas para lógica repetida en lugar de duplicar reglas.
- Pruebe el rendimiento con volúmenes de datos realistas.

### **Directrices para la experiencia del usuario**

**Proporcionar comentarios claros**

- Utilice mensajes de validación que guíen a los usuarios hacia la entrada correcta.
- Mostrar indicadores de carga de reglas que implican servicios externos.
- Implementar revelación progresiva para reducir la carga cognitiva.

**Mantener la capacidad de respuesta del formulario**

- Evite las reglas que causan cambios visuales abruptos.
- Implementar transiciones suaves para operaciones de mostrar/ocultar.
- Probar reglas en diferentes dispositivos y tamaños de pantalla.

**Control de errores**

- Proporcionar comportamiento de reserva cuando fallan las reglas.
- Mostrar mensajes de error descriptivos.
- Registre errores para depurar mientras mantiene una experiencia de usuario positiva.

### **Prácticas recomendadas de desarrollo**

**Estrategia de prueba**

- Probar reglas con casos de borde y valores de límite.
- Verifique el comportamiento de las reglas en distintos exploradores.
- Pruebe la funcionalidad del formulario con y sin JavaScript habilitado.

**Documentación**

- Documente la lógica empresarial detrás de reglas complejas.
- Mantenga un inventario de reglas para formularios grandes.
- Utilice convenciones de nomenclatura coherentes para los componentes y las reglas.

**Control de versiones**

- Rastrear cambios en funciones personalizadas en el control de versiones.
- Prueba de reglas en un entorno de desarrollo antes de la producción.
- Mantener copias de seguridad de las configuraciones de reglas en funcionamiento.

## Solución de problemas comunes

### **Problemas De Ejecución De Reglas**

**No se activan las reglas**

- **Comprobar nombres de componentes**: Compruebe que los componentes a los que se hace referencia existen y tienen nombres correctos.
- **Comprobar orden de reglas**: las reglas se ejecutan de arriba abajo; vuelva a ordenarlas si es necesario.
- **Validar condiciones**: Pruebe condiciones con valores conocidos para comprobar la lógica.
- **Consola del explorador**: Compruebe si hay errores de JavaScript que puedan bloquear la ejecución.

**Comportamiento de regla incorrecto**

- **Operadores de lógica de revisión**: confirme que las condiciones AND/OR están correctamente estructuradas.
- **Prueba con datos de ejemplo**: utiliza valores conocidos para aislar problemas.
- **Comprobar tipos de datos**: Asegúrese de que las comparaciones numéricas utilicen números, no cadenas.
- **Validar expresiones**: pruebe las expresiones matemáticas por separado.

### **Problemas de rendimiento**

**Respuesta lenta del formulario**

- **Reducir la complejidad de las reglas**: Simplifique la lógica condicional compleja.
- **Optimizar funciones personalizadas**: Perfil y optimizar código JavaScript.
- **Limitar llamadas externas**: Minimice las invocaciones al servicio en las reglas.
- **Use selectores eficientes**: Asegúrese de que las referencias de objetos de formulario sean específicas.

**Uso de memoria**

- **Limpiar detectores de eventos**: quite enlaces de reglas que no se usen.
- **Optimizar funciones personalizadas**: evite pérdidas de memoria en el código JavaScript.
- **Ámbito de regla de límite**: use reglas de destino en lugar de condiciones globales.

### **Problemas de funciones personalizadas**

**Funciones no disponibles**

- **Comprobar ruta de acceso de archivo**: compruebe que `functions.js` se encuentra en la ubicación correcta: `/blocks/form/functions.js`.
- **Verificar exportaciones**: Asegúrese de que las funciones se exportan correctamente.
- **Proceso de compilación**: Confirme que la compilación del proyecto incluye el archivo de funciones actualizado.
- **Borrado de caché**: borre la caché del explorador después de implementar nuevas funciones.

**Errores de función**

- **Validación de parámetros**: compruebe que los parámetros de función coinciden con los tipos esperados.
- **Control de errores**: Agregue bloques try-catch para controlar las excepciones correctamente.
- **Registro de consola**: use console.log para depurar la ejecución de funciones.
- **Validación de JSDoc**: Asegúrese de que la documentación de la función coincida con la implementación.

### **Integración de editor universal**

**El Editor De Reglas No Aparece**

- **Extensión habilitada**: Compruebe que la extensión del Editor de reglas esté activada.
- **Selección de componentes**: Asegúrese de haber seleccionado un componente de formulario compatible.
- **Compatibilidad con exploradores**: realice pruebas en exploradores compatibles (Chrome, Firefox, Safari).
- **Permisos de acceso**: confirme que el usuario tiene los permisos de AEM necesarios.

**Problemas de interfaz**

- **Visibilidad del panel**: utilice el botón de alternancia para mostrar u ocultar el panel de objetos de formulario.
- **Guardado de reglas**: Asegúrese de que las reglas se guarden antes de cerrar el editor.
- **Zoom del explorador**: restablece el zoom del explorador al 100% para obtener una visualización óptima de la interfaz.

## Limitaciones importantes

>[!IMPORTANT]
>
> **Restricciones de funciones personalizadas**:
>
> - Las importaciones estáticas y dinámicas no son compatibles con los scripts de funciones personalizadas.
> - Todo el código debe incluirse directamente en el archivo `/blocks/form/functions.js`.
> - Las funciones deben ser sincrónicas (no asincrónicas/en espera o Promesas).
> - El acceso a las API de explorador es limitado por motivos de seguridad.

>[!WARNING]
>
> **Consideraciones sobre la producción**:
>
> - Pruebe todas las reglas a fondo en un entorno de ensayo.
> - Supervise el rendimiento del formulario después de implementar reglas complejas.
> - Tenga un plan de reversión para los problemas relacionados con las reglas.
> - Tenga en cuenta el impacto en los usuarios con conexiones de red lentas.

## Resumen

El Editor de reglas del Editor universal permite crear formularios inteligentes y dinámicos que proporcionan experiencias de usuario excepcionales. Al implementar la lógica condicional, los cálculos automatizados y las reglas de negocio personalizadas, puede:

**Transformar Forms estático**:

- Añada visibilidad de campo condicional para interfaces más limpias y centradas.
- Implemente cálculos en tiempo real y validación de datos.
- Cree una lógica empresarial sofisticada sin codificación.

**Mejorar la experiencia del usuario**:

- Guía a los usuarios a través de flujos de formularios lógicos.
- Reduzca los errores con una validación inteligente.
- Proporcione comentarios y asistencia inmediatos.

**Mejorar la eficiencia**:

- Automatice los cálculos repetitivos y la entrada de datos.
- Optimice los flujos de trabajo complejos con enrutamiento inteligente.
- Reduzca la carga de asistencia con funciones de autoservicio.

### **Pasos siguientes**

Ahora que comprende los aspectos básicos del Editor de reglas:

1. **Iniciar simple**: Comience con las reglas básicas de mostrar u ocultar antes de avanzar a cálculos complejos.
1. **Práctica con ejemplos**: Utiliza el tutorial de la calculadora de impuestos como base.
1. **Explorar características avanzadas**: Experimente con funciones personalizadas para requisitos especializados.
1. **Realizar pruebas exhaustivas**: validar siempre las reglas en diferentes escenarios y dispositivos.
1. **Supervisar el rendimiento**: Asegúrese de que las reglas mejoren la experiencia del usuario en lugar de dificultarla.
