---
title: Editor de reglas para formularios de Edge Delivery Services
description: Cree formularios dinámicos e inteligentes con el editor de reglas en el editor universal. Añada lógica condicional, cálculos y comportamientos interactivos sin codificación.
feature: Edge Delivery Services
role: Admin, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 100%

---


# Editor de reglas para formularios de Edge Delivery Services

El editor de reglas permite a los autores convertir formularios estáticos en experiencias adaptables e inteligentes, sin necesidad de escribir código. Puede mostrar campos de forma condicional, realizar cálculos, validar datos, guiar a los usuarios a través de flujos e integrar la lógica empresarial que se adapta a medida que las personas escriben.

## Lo que aprenderá

Al final de esta guía, podrá hacer lo siguiente:

- Comprender cómo funcionan las reglas y cuándo utilizar diferentes tipos de reglas.
- Habilitar el editor de reglas y acceder a él en el editor universal.
- Crear una lógica condicional para mostrar u ocultar campos dinámicamente.
- Implementar cálculos automatizados y validación de datos.
- Crear funciones personalizadas para reglas empresariales complejas.
- Aplicar las prácticas recomendadas para el rendimiento, el mantenimiento y la experiencia de usuario.

## ¿Por qué utilizar el editor de reglas?

- **Lógica condicional**: muestre los campos pertinentes solo cuando es necesario para reducir el ruido y la carga cognitiva.
- **Cálculos dinámicos**: calcule los valores automáticamente (totales, tasas e impuestos) mientras los usuarios escriben.
- **Validación de datos**: evite errores antes de tiempo con comprobaciones en tiempo real y mensajes claros.
- **Experiencias guiadas**: guíe a los usuarios a través de pasos lógicos (asistentes, ramas).
- **Creación sin código**: configure un comportamiento eficaz mediante una interfaz visual.

Los escenarios comunes incluyen calculadoras de impuestos, estimadores de préstamos y primas, flujos de idoneidad, aplicaciones de varios pasos y encuestas con preguntas condicionales.

## Funcionamiento de las reglas

Una regla define lo que debe suceder cuando se cumple una condición. Conceptualmente, una regla tiene dos partes:

- **Condición**: una instrucción que se evalúa como verdadera o falsa.
   - Ejemplos: “Ingresos > 50 000”, “Cobertura = &#39;Sí&#39;”, “El campo está vacío”
- **Acción**: lo que ocurre cuando la condición es verdadera (y opcionalmente, cuando es falsa).
   - Ejemplos: mostrar/ocultar un campo, establecer/borrar un valor, validar entrada, habilitar/deshabilitar un botón

+++ Patrones de lógica de reglas

- **Condición → Acción (Cuándo/Entonces)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Lo mejor para la visibilidad condicional y la revelación progresiva.

- **Acción ← Condición (Establecer si/Solo si)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Ideal para cálculos y transformaciones de datos.

- **Si → Entonces → Si no (acción alternativa)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Es ideal para la lógica de ramificación y los flujos mutuamente excluyentes.

+++

+++ Ejemplo real

- **Condición**: “El salario bruto supera los 50 000 dólares”
- **Acción principal**: mostrar “Deducción adicional”
- **Acción alternativa**: ocultar “Deducción adicional”
- **Resultado**: los usuarios solo ven los campos que se les aplican

+++

## Requisitos previos


+++ Requisitos de acceso

**Permisos y configuración esenciales**:

- **AEM as a Cloud Service**: acceso de creación con permisos de edición de formularios
- **Editor universal**: instalado y configurado en su entorno
- **Extensión del editor de reglas**: habilitado mediante [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Permisos de edición de formularios**: capacidad para crear y modificar componentes de formulario en el editor universal

**Pasos de verificación**:

1. Confirmar que puede acceder al editor universal desde la consola de AEM Sites.
2. Comprobar que puede crear y editar componentes de formulario
3. Comprobar que aparece el icono del Editor de reglas ![edit-rules](/help/forms/assets/edit-rules-icon.svg) al seleccionar componentes de formulario

+++

+++ Requisitos técnicos

**Conocimientos y habilidades requeridos**:

- **Competencia del editor universal**: experimente la creación de formularios con entradas de texto, listas desplegables y propiedades de campo básicas
- **Comprensión de la lógica empresarial**: capacidad para definir requisitos condicionales y reglas de validación para su caso de uso específico
- **Familiaridad con los componentes del formulario**: conocimiento de los tipos de campo (texto, número, lista desplegable), propiedades (necesarias, visibles, de solo lectura) y estructura del formulario

**Opcional para uso avanzado**:

- **Aspectos básicos de JavaScript**: necesario solamente para crear funciones personalizadas (tipos de datos, funciones, sintaxis básica)
- **Comprensión de JSON**: útil para la manipulación de datos complejos y las integraciones de API

**Preguntas de evaluación**:

- ¿Puede crear un formulario básico con entradas de texto y un botón de envío en el editor universal?
- ¿Sabe cuándo los campos deben ser obligatorios u opcionales en el contexto empresarial?
- ¿Puede identificar qué elementos de formulario necesitan visibilidad condicional en su caso de uso?

+++

+++ Habilitar la extensión del Editor de reglas

**Importante**: la extensión del Editor de reglas no está habilitada de forma predeterminada en entornos del editor universal. 

**Pasos de activación**:

1. Ir a [Extension Manager](/help/implementing/developing/extending/extension-manager.md) en su entorno de AEM
2. Buscar la extensión “Editor de reglas” en la lista de extensiones disponibles
3. Hacer clic en **Habilitar** y confirmar la activación
4. Esperar a que se actualice el sistema (puede tardar entre 1 y 2 minutos)

**Verificación**:

- Después de habilitarlo, el icono del Editor de reglas aparece al seleccionar un componente de formulario: ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![Editor universal de reglas](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Figura: El icono del Editor de reglas aparece al seleccionar componentes de formulario

Para abrir el Editor de reglas:

1. Seleccione un componente de formulario en el editor universal.
2. Haga clic en el icono del Editor de reglas.
3. El Editor de reglas se abre en un panel lateral. 

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Imagen: Interfaz del Editor de reglas para editar reglas de componentes

>[!NOTE]
>
> En este artículo, “componente de formulario” y “objeto de formulario” hacen referencia a los mismos elementos (por ejemplo, entradas, botones o paneles).

## Introducción a la interfaz del Editor de reglas

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-interface.png)
Imagen: Interfaz completa del editor de reglas con componentes numerados

1. **Título del componente y tipo de regla**: confirma el componente seleccionado y el tipo de regla activo.
2. **Objetos de formulario y panel Funciones**:

   - Objetos de formulario: vista jerárquica de campos y contenedores para hacer referencia a ellos en las reglas
   - Funciones: ayudantes matemáticas, cadena, fecha y validación integrados

3. **Alternar panel**: muestra u oculta el panel de objetos y funciones para aumentar el espacio de trabajo
4. **Generador de reglas visual**: compositor de reglas de arrastrar y soltar y desplegable
5. **Controles**: Listo (guardar), Cancelar (descartar). Pruebe siempre las reglas antes de guardar.

+++

+++ Administración de reglas existentes

Cuando un componente ya tiene reglas, puede:

- **Ver**: ver resúmenes y lógica de reglas
- **Editar**: modificar condiciones y acciones
- **Reordenar**: cambiar el orden de ejecución (de arriba abajo)
- **Habilitar/Deshabilitar**: alternar reglas para pruebas
- **Eliminar**: quitar las reglas de forma segura

>[!TIP]
>
> Ponga las reglas específicas antes que las generales. La ejecución es de arriba a abajo.

+++

## Tipos de regla disponibles

Elija el tipo de regla que mejor se adapte a sus intenciones.

+++ Lógica condicional

- **Cuando**: regla principal para comportamiento condicional complejo (Condición → Acción ± Si no)
- **Ocultar/Mostrar**: controla la visibilidad en función de una condición (divulgación progresiva)
- **Habilitar/Deshabilitar**: controla si un campo es interactivo (por ejemplo, deshabilitar Enviar hasta que los campos obligatorios sean válidos)

+++

+++ Manipulación de datos

- **Establecer valor de**: rellenar automáticamente valores (por ejemplo, fechas, totales, copias)
- **Borrar valor de**: quitar datos cuando cambien las condiciones
- **Formato**: transformar el formato de visualización (moneda, teléfono, fecha) sin alterar los valores almacenados

+++

+++ Validación

- **Validar**: lógica de validación personalizada, que incluye comprobaciones entre campos y reglas empresariales

+++

+++ Cálculo

- **Expresión matemática**: calcular valores en tiempo real (totales, impuestos, proporciones)

+++

+++ Interfaz de usuario

- **Definir enfoque**: mover el enfoque a un campo específico (utilícelo con moderación)
- **Establecer propiedad**: modificar las propiedades del componente de forma dinámica (marcador de posición, opciones, etc.)

+++

+++ Control de formulario

- **Enviar formulario**: envíear el formulario mediante programación (solo después de que se superen las validaciones)
- **Restablecer formulario**: borrar y restablecer al estado inicial (confirmar antes de usar)
- **Guardar formulario**: guardar como borrador para utilizarlo posteriormente (formularios largos, varias sesiones)

+++

+++ Avanzado 

- **Invocar servicio**: llamar a API o servicios externos (controle la carga y los errores)
- **Añadir o quitar instancia**: administrar secciones repetibles (por ejemplo, dependientes, direcciones)
- **Navegar a**: ruta a otros formularios/páginas (conservar datos antes de la navegación)
- **Navegar entre paneles**: controlar la navegación por los pasos del asistente y la omisión de estos
- **Evento de envío**: desencadenar eventos personalizados para integraciones o análisis

+++

## Tutorial paso a paso: Creación de una calculadora de impuestos inteligente

+++ Información general del tutorial

En este ejemplo se muestra la visibilidad condicional y los cálculos automáticos.

![Captura de pantalla de la interfaz del Editor de reglas que muestra la creación de una regla condicional con la lógica Cuando-Entonces para la visibilidad del campo de formulario](/help/edge/docs/forms/assets/rule-editor-1.png)
Figura: Formulario de cálculo de impuestos con campos condicionales inteligentes

Creará un formulario que:

1. Se adapta a los datos introducidos por el usuario mostrando los campos pertinentes
2. Calcula valores en tiempo real
3. Valida datos para mejorar la precisión

+++

+++ Estructura del formulario

| Nombre del campo | Tipo | Función | Comportamiento |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Salario bruto | Entrada de número | Ingresos anuales del usuario | Lógica condicional de desencadenadores |
| Deducción adicional | Entrada de número | Deducciones adicionales (si procede) | Solo visible cuando el salario es > 50 000 USD |
| Ingresos gravables | Entrada de número | Valor calculado | Sólo lectura, actualizaciones al cambiar |
| Impuestos que se deben pagar | Entrada de número | Valor calculado | Solo lectura, calculado a una tasa fija |

+++

+++ Lógica empresarial

- **Regla 1: Visualización condicional**

  ```text
  WHEN Gross Salary > 50,000
  THEN Show "Additional Deduction"
  ELSE Hide "Additional Deduction"
  ```

- **Regla 2: Cálculo de ingresos gravables**

  ```text
  SET Taxable Income = Gross Salary - Additional Deduction
  (Only when Additional Deduction applies)
  ```

- **Regla 3: Cálculo de impuestos que se deben pagar**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ Paso 1: Creación del formulario

**Objetivo**: generar el formulario base con todos los campos y la configuración inicial.

1. **Abrir editor universal**:
   - Vaya a la consola de AEM Sites, seleccione su página y haga clic en **Editar**
   - Asegúrese de que tiene el [editor universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=es) configurado correctamente

2. **Añadir componentes de formulario en este orden**:
   - Título (H2): “Formulario de cálculo de impuestos”
   - Entrada de número: &quot;Salario bruto&quot; (obligatorio: sí, marcador de posición: &quot;Introducir salario anual&quot;)
   - Entrada de número: &quot;Deducción adicional&quot; (obligatorio: no, marcador de posición: &quot;Introducir deducciones adicionales&quot;)
   - Entrada de número: &quot;Ingresos gravables&quot; (solo lectura: sí)
   - Introducción de número: &quot;Impuestos que se deben pagar&quot; (solo lectura: sí)
   - Botón Enviar: &quot;Calcular Impuesto&quot;

3. **Configurar propiedades del campo inicial**:
   - Ocultar &quot;Deducción adicional&quot; (establecer Visible: No en el panel Propiedades)
   - Establecer &quot;Ingresos gravables&quot; e &quot;Impuestos que se deben pagar&quot; en Solo lectura: Sí

![Captura de pantalla de un formulario de cálculo de impuestos con campos de entrada para el salario bruto, el estado civil y los hijos a cargo, que muestra la estructura del formulario antes de que se apliquen las reglas](/help/edge/docs/forms/assets/rule-editor2.png)
Figura: Estructura inicial del formulario con los componentes básicos configurados.

**Punto de comprobación**: debería tener un formulario con todos los campos obligatorios donde el campo “Deducción adicional” esté oculto y los campos calculados sean de solo lectura.

+++

+++ Paso 2: Añadir una regla de visibilidad condicional

**Objetivo**: mostrar el campo &quot;Deducción adicional&quot; solo cuando el salario bruto supere los 50 000 USD.

1. **Seleccione el campo Salario bruto** y haga clic en el icono del Editor de reglas ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **Crear una nueva función**:
   - Haga clic en **Crear**
   - Cambiar tipo de regla de &quot;Establecer valor de&quot; a **&quot;Cuando&quot;**
3. **Configurar la condición**:
   - Seleccione **&quot;es mayor que&quot;** en la lista desplegable
   - Escriba `50000` en el campo de número
4. **Establecer la acción Entonces**:
   - Elija **“Mostrar”** en la lista desplagable Seleccionar acción
   - Arrastre o seleccione el campo **“Deducción adicional”** en Objetos de formulario
5. **Añadir la acción Si no**:
   - Haga clic en **”Añadir acción Si no”**
   - Elija **“Ocultar”** ene la lista desplegable Seleccionar acción
   - Seleccione el campo **“Deducción adicional”**
6. **Guardar la regla**: haga clic en **Listo**

>[!NOTE]
>
> Enfoque alternativo: puede lograr el mismo resultado creando una regla Mostrar/Ocultar directamente en el campo “Deducción adicional” en lugar de una regla Cuando en “Salario bruto”.

+++

+++ Paso 3: Añadir reglas de cálculo

**Objetivo**: calcular automáticamente “Ingresos gravables” e “Impuestos que se deben pagar” según los datos proporcionados por el usuario.

**Configurar cálculo de ingresos gravables**:

1. **Seleccione el campo “Ingresos gravables”** y abra el Editor de reglas
2. **Crear la expresión matemática**:
   - Haga clic en **Crear** → Seleccionar **&quot;Expresión matemática&quot;**
   - Crear expresión: **Salario bruto − Deducción adicional**
   - Arrastre “Salario bruto” al primer campo
   - Seleccione el operador **“Menos”**
   - Arrastre “Deducción adicional” al segundo campo
3. **Guardar**: haga clic cn **Listo**

**Configurar el cálculo de impuestos que se deben pagar**:

1. **Seleccione el campo “Impuesto que se deben pagar”** y abra el Editor de reglas
2. **Crear la expresión matemática**:
   - Haga clic en **Crear** → Seleccionar **“Expresión matemática”**
   - Crear expresión: **Ingresos gravables × 10 ÷ 100**
   - Arrastrar &quot;Ingresos gravables&quot; al primer campo
   - Seleccione el operador **“Multiplicado por”**
   - Introducir `10` como número
   - Haga clic en **“Extender expresión”**
   - Seleccione el operador **“Dividido por”**
   - Introducir `100` como número
3. **Guardar**: haga clic en **Listo**

+++

+++ Paso 4: Probar el formulario

**Compruebe su implementación probando el flujo completo**:

1. **Previsualizar el formulario**: haga clic en el modo Previsualización en el editor universal
2. **Probar la lógica condicional**:
   - Introduzca Salario bruto = `30000` → “Deducción adicional” debe permanecer oculto
   - Introduzca Salario bruto = `60000` → “Deducción adicional” debe aparecer
3. **Probar los cálculos**:
   - Con Salario bruto = `60000`, introduzca Deducción adicional = `5000`
   - Verificar Ingresos gravables = `55000` (60 000 - 5000)
   - Verificar Impuestos que se deben pagar = `5500` (55 000 × 10 %)

![Previsualizar un formulario](/help/edge/docs/forms/assets/rule-editor-form.png)
Imagen: Calculadora de impuestos completada con campos condicionales y cálculos automáticos

**Criterios de éxito**: el formulario debe mostrar u ocultar campos de forma dinámica y calcular valores en tiempo real a medida que los usuarios escriben.


+++

## Avanzado: funciones personalizadas

Para obtener una lógica empresarial compleja que vaya más allá de las capacidades integradas, puede crear funciones de JavaScript personalizadas que se integren a la perfección con el Editor de reglas.

+++ Cuándo se deben utilizar las funciones personalizadas

**Escenarios ideales para funciones personalizadas**:

- **Cálculos complejos**: los cálculos de varios pasos no se expresan fácilmente en la regla Expresión matemática
- **Validaciones específicas de la empresa**: lógica de validación personalizada específica de su organización o sector
- **Transformaciones de datos**: conversiones de formato, manipulaciones de cadenas o análisis de datos
- **Integraciones externas**: llamadas a API internas o servicios de terceros (con limitaciones)

**Ventajas de las funciones personalizadas**:

- **Capacidad de reutilización**: escriba una vez y utilícelo en varios formularios y reglas
- **Mantenimiento**: lógica centralizada más fácil de actualizar y depurar
- **Rendimiento**: ejecución de JavaScript optimizada comparada con cadenas de reglas complejas
- **Flexibilidad**: administre casos extremos y escenarios complejos no abordados por reglas estándar

+++

+++ Creación e implementación de funciones personalizadas

**Ubicación de archivos**: todas las funciones personalizadas deben definirse en `/blocks/form/functions.js` en el proyecto de Edge Delivery Services.

**Flujo de trabajo de desarrollo**:

1. **Diseño de funciones**
   - Utilizar nombres de funciones descriptivos y orientados a la acción
   - Definir tipos de parámetros claros y valores devueltos
   - Gestionar correctamente casos extremos y entradas no válidas

2. **Implementation**
   - Escribir JavaScript limpio y bien comentado
   - Incluir validación de entrada y control de errores
   - Probar funciones independientemente antes de la integración

3. **Documentación**
   - Añadir comentarios JSDoc completos
   - Incluir ejemplos de uso y descripciones de parámetros
   - Documentar cualquier limitación o dependencia

4. **Implementación**
   - Exportar funciones mediante exportaciones con nombre
   - Implementar en el repositorio del proyecto
   - Verificar la finalización de la compilación antes de probar

**Implementación de ejemplo**:

```javascript
/**
 * Concatenates first and last name with proper formatting
 * @name getFullName
 * @description Combines first and last name, handles edge cases like missing values
 * @param {string} firstName - The person's first name
 * @param {string} lastName - The person's last name  
 * @returns {string} Formatted full name or empty string if both inputs are invalid
 */
function getFullName(firstName, lastName) {
  // Handle null, undefined, or empty string inputs
  const first = (firstName || '').toString().trim();
  const last = (lastName || '').toString().trim();
  
  return `${first} ${last}`.trim();
}

/**
 * Calculates the number of days between two dates
 * @name days
 * @description Computes absolute difference in days, handles various date input formats
 * @param {Date|string} endDate - End date (Date object or ISO string)
 * @param {Date|string} startDate - Start date (Date object or ISO string)
 * @returns {number} Number of days between dates, 0 if inputs are invalid
 */
function days(endDate, startDate) {
  // Convert string inputs to Date objects
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // Validate date objects
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  // Calculate absolute difference in milliseconds, then convert to days
  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// Export functions for use in Rule Editor
export { getFullName, days };
```

![Adición de función personalizada](/help/edge/docs/forms/assets/create-custom-function.png)
Imagen: Adición de funciones personalizadas al archivo functions.js

+++

+++ Uso de funciones personalizadas en el Editor de reglas

**Pasos de integración**:

1. **Añadir función a proyecto**
   - Crear o editar `/blocks/form/functions.js` en el proyecto
   - Incluir la función en la instrucción de exportación

2. **Implementar y compilar**
   - Confirmar cambios en el repositorio
   - Asegurarse de que el proceso de compilación se complete correctamente
   - Dejar tiempo para actualizaciones de la caché de CDN

3. **Acceso en el Editor de reglas**
   - Abrir el Editor de reglas para cualquier componente de formulario
   - Seleccionar **“Salida de función”** en el menú desplegable **Seleccionar acción**
   - Elegir la función personalizada en la lista de funciones disponibles
   - Configurar parámetros de función mediante campos de formulario o valores estáticos

4. **Realizar pruebas exhaustivas**
   - Previsualizar el formulario para verificar el comportamiento de la función
   - Probar con varias combinaciones de entrada, incluidos los casos extremos
   - Verificar el impacto del rendimiento en la carga y la interacción del formulario

![Función personalizada en el Editor de reglas](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Imagen: Selección y configuración de funciones personalizadas en la interfaz del Editor de reglas

>[!NOTE]
>
> Las mejoras realizadas en el editor de reglas, incluidas las reglas personalizadas basadas en eventos, la compatibilidad con variables dinámicas y la integración de API, también están disponibles para los formularios de Edge Delivery Services. Para obtener más información sobre estas mejoras y cómo utilizarlas, consulte el artículo [Mejoras y casos de uso del editor de reglas](/help/forms/rule-editor-enhancements-use-cases.md).

**Prácticas recomendadas para el uso de funciones**:

- **Control de errores**: incluir siempre el comportamiento de reserva para los errores de funciones
- **Rendimiento**: funciones de perfil con volúmenes de datos realistas
- **Seguridad**: validar todas las entradas para evitar vulnerabilidades de seguridad
- **Pruebas**: crear casos de prueba que cubran casos normales y extremos

+++


### Importaciones estáticas para funciones personalizadas

El editor de reglas del editor universal admite importaciones estáticas, lo que permite organizar la lógica reutilizable en varios archivos y formularios. En lugar de mantener todas las funciones personalizadas en un solo archivo (/blocks/form/functions.js), puede importar funciones de otros módulos.
Por ejemplo: Importar funciones desde un archivo externo
Tenga en cuenta la siguiente estructura de carpetas:

```
      form
      ┣ commonLib
      ┃ ┗ functions.js
      ┣ rules
      ┃ ┗ _form.json
      ┣ form.js
      ┗ functions.js
```

Puede importar funciones de `commonLib/functions.js` a su archivo principal `functions.js`, como se muestra a continuación:

```
`import {days} from './commonLib/functions';
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in String format
 * @param {string} lastname in String format
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

// Export multiple functions for use in Rule Editor
export { getFullName, days};
```

### Organización de funciones personalizadas en diferentes formularios

Puede crear diferentes conjuntos de funciones en archivos o carpetas independientes y exportarlos según sea necesario:

- Si desea que determinadas funciones estén disponibles únicamente en formularios específicos, puede proporcionar la ruta al archivo de funciones en la configuración del formulario.

- Si el cuadro de texto de la ruta se deja en blanco, el editor de reglas cargará de forma predeterminada las funciones de `/blocks/form/functions.js`

![Función personalizada en el editor universal (UE)](/help/forms/assets/custom-function-in-ue.png){width=50%}

En la captura de pantalla anterior, la ruta de la función personalizada se añade en el cuadro de texto Ruta de la función personalizada. Las funciones personalizadas de este formulario se cargan desde el archivo especificado (`cc_function.js`).

Esto aporta flexibilidad al compartir funciones en varios formularios o mantenerlos aislados por formulario.

## Prácticas recomendadas para el desarrollo de reglas


+++ Optimización de rendimiento

- Minimice la complejidad de la regla; divida la lógica grande en reglas pequeñas y centradas
- Ordenar reglas por frecuencia (más común primero)
- Mantener manejables los conjuntos de reglas por componente
- Preferir funciones personalizadas reutilizables en lugar de lógica duplicada

+++

+++ Experiencia del usuario

- Proporcionar una validación clara y comentarios en línea
- Evitar los cambios visuales molestos; utilizar la función de mostrar/ocultar cuidadosamente
- Probar entre dispositivos y diseños

+++

+++ Higiene del desarrollo

- Probar con casos extremos y valores conocidos
- Verificar en los distintos navegadores
- Documentar la intención detrás de reglas complejas, no solo la mecánica
- Mantener un inventario de reglas para formularios grandes
- Utilizar una nomenclatura uniforme para los componentes y las reglas
- Funciones personalizadas de versión y pruebas en entornos que no son de producción

+++

## Solución de problemas comunes


+++ Reglas que no se activan

- Comprobar nombres y referencias de componentes
- Comprobar orden de ejecución (de arriba a abajo)
- Validar condiciones con valores conocidos
- Inspeccionar la consola del explorador para detectar errores de bloqueo

+++

+++ Comportamiento incorrecto

- Revisar operadores y agrupación (Y/O)
- Probar fragmentos de expresión individualmente
- Confirmar tipos de datos (números o cadenas)

+++

+++ Problemas de rendimiento

- Simplificar las condiciones profundamente anidadas
- Crear perfiles de funciones personalizadas
- Minimizar las llamadas externas dentro de las reglas
- Usar selectores y referencias específicos

+++

+++ Problemas de funciones personalizadas

- Confirmar la ruta del archivo: `/blocks/form/functions.js`
- Asegurarse de que las exportaciones con nombre son correctas
- Confirmar que la compilación incluye los cambios.
- Borrar la caché del explorador después de la implementación
- Validar tipos de parámetros y gestión de errores

+++

+++ Integración del editor universal

- Confirmar que la extensión del Editor de reglas está habilitada.
- Seleccionar un componente compatible
- Utilizar un explorador compatible (Chrome, Firefox, Safari)
- Comprobar que tiene los permisos necesarios

## Limitaciones importantes

>[!IMPORTANT]
>
> Restricciones de función personalizadas:
>
> - No se admiten importaciones estáticas/dinámicas
> - Toda la lógica debe residir en `/blocks/form/functions.js`
> - Las funciones deben ser sincrónicas (no asincrónicas/en espera o Promesas)
> - El acceso a la API del explorador es limitado

>[!WARNING]
>
> Consideraciones sobre la producción:
>
> - Realizar pruebas exhaustivas en el ensayo
> - Monitorizar el rendimiento después de la implementación
> - Tener un plan de reversión para los problemas de reglas
> - Considerar las redes lentas y los dispositivos de baja especificación

## Resumen

El Editor de reglas del editor universal transforma los formularios estáticos en experiencias inteligentes y adaptables que se adaptan a los datos introducidos por el usuario en tiempo real. Al aprovechar la lógica condicional, los cálculos automatizados y las reglas empresariales personalizadas, puede crear flujos de trabajo de formulario sofisticados sin escribir código de aplicación.

**Funciones clave que ha aprendido**:

- **Lógica condicional**: mostrar y ocultar campos basados en los datos proporcionados por el usuario para crear experiencias relevantes y enfocadas
- **Cálculos dinámicos**: calcular automáticamente valores (impuestos, totales, tasas) a medida que los usuarios interactúan con el formulario
- **Validación de datos**: implementar la validación en tiempo real con mensajes de comentarios claros y procesables
- **Funciones personalizadas**: ampliar las capacidades con JavaScript para integraciones y lógica empresarial compleja
- **Optimización del rendimiento**: aplicar las prácticas recomendadas para un desarrollo de reglas eficiente y que se pueda mantener

**Valor entregado**:

- **Experiencia del usuario mejorada**: reducir la carga cognitiva con revelación progresiva y flujos de formularios inteligentes
- **Errores reducidos**: impedir los envíos no válidos mediante validación en tiempo real y entrada guiada
- **Mayor eficiencia**: automatice los cálculos y la entrada de datos para minimizar el esfuerzo del usuario
- **Soluciones que se pueden mantener**: crear reglas reutilizables y bien documentadas que se escalen en toda la organización

**Impacto empresarial**:

Los formularios se convierten en potentes herramientas para la recopilación de datos, la calificación de posibles clientes y la participación del usuario. El Editor de reglas permite a los autores no técnicos implementar una lógica empresarial sofisticada, reducir los costes de desarrollo y mejorar las tasas de finalización de los formularios y la calidad de los datos.

+++

## Próximos pasos

**Ruta de aprendizaje recomendada**:

1. **Empezar con lo básico**: crear reglas sencillas de mostrar y ocultar para comprender los conceptos principales
2. **Practicar con tutoriales**: utilizar el ejemplo de la calculadora de impuestos como base para sus propios formularios
3. **Expandir gradualmente**: añadir expresiones matemáticas y reglas de validación a medida que aumente la confianza
4. **Implementar funciones personalizadas**: desarrollar funciones de JavaScript para los requisitos empresariales especializados
5. **Optimizar y escalar**: aplicar las prácticas recomendadas de rendimiento y mantener la documentación de reglas

**Recursos adicionales**:

- [Documentación del editor universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html?lang=es) para un contexto más amplio
- [Guía de Extension Manager](/help/implementing/developing/extending/extension-manager.md) para habilitar funciones adicionales
- [Formularios de Edge Delivery Services](/help/edge/docs/forms/overview.md) para obtener instrucciones completas de desarrollo de formularios

