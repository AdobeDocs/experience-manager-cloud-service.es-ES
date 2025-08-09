---
title: Editor de reglas para Dynamic Forms en el editor universal
description: Cree formularios inteligentes y dinámicos con el Editor de reglas en el Editor universal. Agregue lógica condicional, cálculos y comportamientos interactivos sin codificación.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '2598'
ht-degree: 1%

---


# Editor de reglas para Dynamic Forms en el editor universal

El Editor de reglas permite a los autores convertir formularios estáticos en experiencias interactivas e inteligentes, sin necesidad de escribir código. Puede mostrar campos de forma condicional, realizar cálculos, validar datos, guiar a los usuarios a través de flujos e integrar la lógica empresarial que se adapta a medida que las personas escriben.

## Qué va a aprender

Al final de esta guía, deberá ser capaz de:

- Comprender cómo funcionan las reglas y cuándo utilizar diferentes tipos de reglas
- Habilite y acceda al Editor de reglas en el Editor universal
- Crear una lógica condicional para mostrar u ocultar campos dinámicamente
- Implementación de cálculos automatizados y validación de datos
- Crear funciones personalizadas para reglas empresariales complejas
- Aplicar las prácticas recomendadas para el rendimiento, el mantenimiento y la experiencia de usuario

## ¿Por qué utilizar el Editor de reglas?

- **Lógica condicional**: muestra los campos relevantes solo cuando sea necesario para reducir el ruido y la carga cognitiva.
- **Cálculos dinámicos**: Calcule los valores automáticamente (totales, tasas e impuestos) mientras los usuarios escriben.
- **Validación de datos**: Evite errores antes de tiempo con comprobaciones en tiempo real y mensajes claros.
- **Experiencias guiadas**: guíe a los usuarios a través de pasos lógicos (asistentes, ramas).
- **Creación sin código**: configure un comportamiento eficaz mediante una interfaz visual.

Los escenarios comunes incluyen calculadoras de impuestos, estimadores de préstamos y primas, flujos de elegibilidad, aplicaciones de varios pasos y encuestas con preguntas condicionales.

## Funcionamiento de las reglas

Una regla define lo que debe suceder cuando se cumple una condición. Conceptualmente, una regla tiene dos partes:

- **Condición**: Una instrucción que se evalúa como verdadera o falsa.
   - Ejemplos: &quot;Ingresos > 50 000&quot;, &quot;Cobertura = &#39;Sí&#39;&quot;, &quot;El campo está vacío&quot;
- **Acción**: Lo que ocurre cuando la condición es verdadera (y opcionalmente, cuando es falsa).
   - Ejemplos: Mostrar/ocultar un campo, Establecer/borrar un valor, Validar entrada, Habilitar/deshabilitar un botón

+++ Patrones de lógica de reglas

- **Condición → Acción (Cuándo/Entonces)**

  ```text
  WHEN Gross Salary > 50000
  THEN Show "Additional Deduction"
  ```

  Lo mejor para la visibilidad condicional y la revelación progresiva.

- **Condición de ← de acción (establecer si/solo si)**

  ```text
  SET Taxable Income = Gross Salary - Deductions
  IF Deductions are applicable
  ```

  Ideal para cálculos y transformaciones de datos.

- **Si → Entonces → (acción alternativa)**

  ```text
  IF Income > 50000
  THEN Show "High Income" fields
  ELSE Show "Standard Income" fields
  ```

  Es ideal para la lógica de ramificación y los flujos mutuamente excluyentes.

+++

+++ Ejemplo real

- **Condición**: &quot;El salario bruto supera los 50.000 dólares&quot;
- **Acción principal**: mostrar &quot;Deducción adicional&quot;
- **Acción alternativa**: ocultar &quot;Deducción adicional&quot;
- **Resultado**: los usuarios solo ven los campos que se les aplican

+++

## Requisitos previos


+++ Requisitos de acceso

**Permisos y configuración esenciales**:

- **AEM as a Cloud Service**: acceso de creación con permisos de edición de formularios
- **Editor universal**: instalado y configurado en su entorno
- **Extensión del editor de reglas**: Habilitado mediante [Extension Manager](/help/implementing/developing/extending/extension-manager.md)
- **Permisos de edición de formularios**: capacidad para crear y modificar componentes de formulario en el Editor universal

**Pasos de comprobación**:

1. Confirme que puede acceder al editor universal desde la consola de AEM Sites.
2. Compruebe que puede crear y editar componentes de formulario
3. Compruebe que aparece el icono del Editor de reglas ![edit-rules](/help/forms/assets/edit-rules-icon.svg) al seleccionar componentes de formulario

+++

+++ Requisitos técnicos

**Conocimientos y habilidades requeridos**:

- **Competencia del editor universal**: experimente la creación de formularios con entradas de texto, listas desplegables y propiedades de campo básicas
- **Comprensión de la lógica empresarial**: capacidad para definir requisitos condicionales y reglas de validación para su caso de uso específico
- **Familiaridad con los componentes del formulario**: conocimiento de los tipos de campo (texto, número, lista desplegable), propiedades (necesarias, visibles, de solo lectura) y estructura del formulario

**Opcional para uso avanzado**:

- **Aspectos básicos de JavaScript**: Necesario solo para crear funciones personalizadas (tipos de datos, funciones, sintaxis básica)
- **Comprensión de JSON**: útil para la manipulación de datos complejos y las integraciones de API

**Preguntas de evaluación**:

- ¿Puede crear un formulario básico con entradas de texto y un botón de envío en el editor universal?
- ¿Sabe cuándo los campos deben ser obligatorios o opcionales en el contexto empresarial?
- ¿Puede identificar qué elementos de formulario necesitan visibilidad condicional en su caso de uso?

+++

+++ Habilitar la extensión del Editor de reglas

**Importante**: La extensión del Editor de reglas no está habilitada de manera predeterminada en los entornos del Editor universal.

**Pasos de activación**:

1. Vaya a [Extension Manager](/help/implementing/developing/extending/extension-manager.md) en su entorno de AEM
2. Busque la extensión &quot;Editor de reglas&quot; en la lista de extensiones disponibles
3. Haga clic en **Habilitar** y confirme la activación
4. Espere a que se actualice el sistema (puede tardar entre 1 y 2 minutos)

**Verificación**:

- Después de habilitarlo, el icono Editor de reglas aparece al seleccionar un componente de formulario: ![edit-rules](/help/forms/assets/edit-rules-icon.svg)

![Editor universal de reglas](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)
Figura: El icono Editor de reglas aparece al seleccionar componentes de formulario

Para abrir el Editor de reglas:

1. Seleccione un componente de formulario en el Editor universal.
2. Haga clic en el icono Editor de reglas.
3. El Editor de reglas se abrirá en un panel lateral.

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-for-field.png)
Imagen: interfaz del Editor de reglas para editar reglas de componentes

>[!NOTE]
>
> En este artículo, &quot;componente de formulario&quot; y &quot;objeto de formulario&quot; hacen referencia a los mismos elementos (por ejemplo, entradas, botones o paneles).

## Introducción a la interfaz del Editor de reglas

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/assets/rule-editor-interface.png)
Imagen: interfaz completa del editor de reglas con componentes numerados

- **Título del componente y tipo de regla**: confirma el componente seleccionado y el tipo de regla activo.
- **Panel de funciones y objetos de formulario**:
   - Objetos de formulario: vista jerárquica de campos y contenedores para hacer referencia a ellos en las reglas
   - Funciones: ayudantes de validación, fecha, cadena y matemáticas integrados
- **Alternar panel**: muestra u oculta el panel de objetos y funciones para aumentar el espacio de trabajo
- **Generador de reglas visual**: Compositor de reglas desplegable y de arrastrar y soltar
- **Controles**: Listo (guardar), Cancelar (descartar). Pruebe siempre las reglas antes de guardar.

+++

+++ Administración de reglas existentes

Cuando un componente ya tiene reglas, puede:

- **Vista**: ver lógica y resúmenes de reglas
- **Editar**: Modificar condiciones y acciones
- **Reordenar**: cambie el orden de ejecución (de arriba abajo)
- **Habilitar/Deshabilitar**: alternar reglas para pruebas
- **Eliminar**: quite las reglas de forma segura

>[!TIP]
>
> Ponga las reglas específicas antes que las generales. La ejecución es de arriba a abajo.

+++

## Tipos de regla disponibles

Elija el tipo de regla que mejor se adapte a sus intenciones.

+++ Lógica condicional

- **When**: regla principal para comportamiento condicional complejo (condición → acción ± Else)
- **Ocultar/Mostrar**: controla la visibilidad en función de una condición (divulgación progresiva)
- **Habilitar/Deshabilitar**: controla si un campo es interactivo (por ejemplo, deshabilita Enviar hasta que los campos obligatorios sean válidos)

+++

+++ Manipulación de datos

- **Establecer valor de**: Rellene automáticamente valores (por ejemplo, fechas, totales, copias)
- **Borrar valor de**: quite datos cuando cambien las condiciones
- **Formato**: transforme el formato de visualización (moneda, teléfono, fecha) sin alterar los valores almacenados

+++

+++ Validación

- **Validar**: lógica de validación personalizada, que incluye comprobaciones entre campos y reglas empresariales

+++

+++ Cálculo

- **Expresión matemática**: Calcular valores en tiempo real (totales, impuestos, proporciones)

+++

+++ Interfaz de usuario

- **Definir enfoque**: mueva el enfoque a un campo específico (utilícelo con moderación)
- **Establecer propiedad**: modifique las propiedades del componente de forma dinámica (marcador de posición, opciones, etc.)

+++

+++ Control de formulario

- **Enviar formulario**: envíe el formulario mediante programación (solo después de que pasen las validaciones)
- **Restablecer formulario**: Borrar y restablecer al estado inicial (confirmar antes de usar)
- **Guardar formulario**: guardar como borrador para utilizarlo posteriormente (formularios largos, varias sesiones)

+++

+++ Avanzado 

- **Invocar servicio**: llame a API o servicios externos (controle la carga y los errores).
- **Agregar o quitar instancia**: administre secciones repetibles (por ejemplo, dependientes, direcciones)
- **Navegar a**: ruta a otros formularios/páginas (conservar datos antes de la navegación)
- **Navegar entre paneles**: navegación y omisión de la etapa del Asistente para control
- **Evento de envío**: Almacene en Déclencheur eventos personalizados para integraciones o análisis

+++

## Tutorial paso a paso: Creación de una calculadora de impuestos inteligente

+++ Resumen del tutorial

Este ejemplo muestra la visibilidad condicional y los cálculos automáticos.

![Captura de pantalla de la interfaz del Editor de reglas que muestra la creación de una regla condicional con lógica When-Then para la visibilidad del campo de formulario](/help/edge/docs/forms/assets/rule-editor-1.png)
Imagen: formulario de cálculo de impuestos con campos condicionales inteligentes

Se creará un formulario que:

1. Se adapta a los datos introducidos por el usuario mostrando los campos relevantes
2. Calcula valores en tiempo real
3. Valida datos para mejorar la precisión

+++

+++ Estructura del formulario

| Nombre del campo | Tipo | Función | Comportamiento |
|-------------------------|---------------|--------------------------------|-----------------------------------------|
| Salario bruto | Entrada de número | Ingresos anuales del usuario | Lógica condicional de Déclencheur |
| Deducción adicional | Entrada de número | Deducciones adicionales (si procede) | Solo visible cuando el salario es > 50 000 $ |
| Ingresos gravables | Entrada de número | Valor calculado | Sólo lectura, actualizaciones al cambiar |
| Impuestos a pagar | Entrada de número | Valor calculado | Solo lectura, calculado a una tasa fija |

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

- **Regla 3: Cálculo de impuestos a pagar**

  ```text
  SET Tax Payable = Taxable Income × 10%
  (Simplified flat rate)
  ```

+++

+++ Paso 1: Crear el formulario base

**Objetivo**: genera el formulario base con todos los campos y la configuración inicial.

1. **Abrir editor universal**:
   - Vaya a la consola de AEM Sites, seleccione su página y haga clic en **Editar**
   - Asegúrese de que tiene el [Editor universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) configurado correctamente

2. **Agregar componentes de formulario en este orden**:
   - Título (H2): &quot;Formulario de cálculo de impuestos&quot;
   - Entrada de número: &quot;salario bruto&quot; (obligatorio: sí, marcador de posición: &quot;introducir salario anual&quot;)
   - Entrada de número: &quot;Deducción adicional&quot; (obligatorio: No, marcador de posición: &quot;Introducir deducciones adicionales&quot;)
   - Entrada de número: &quot;Ingresos gravables&quot; (solo lectura: sí)
   - Introducción de número: &quot;Impuesto a pagar&quot; (solo lectura: sí)
   - Botón Enviar: &quot;Calcular Impuesto&quot;

3. **Configurar propiedades del campo inicial**:
   - Ocultar &quot;Deducción adicional&quot; (conjunto visible: No en el panel Propiedades)
   - Establezca &quot;Ingresos gravables&quot; e &quot;Impuestos por pagar&quot; en Solo lectura: Sí

![Captura de pantalla de un formulario de cálculo de impuestos con campos de entrada para el salario bruto, el estado civil y los hijos a cargo, que muestra la estructura del formulario antes de que se apliquen las reglas](/help/edge/docs/forms/assets/rule-editor2.png)
Figura: Estructura del formulario inicial con componentes básicos configurados

**Punto de comprobación**: debería tener un formulario con todos los campos obligatorios donde Deducción adicional esté oculta y los campos calculados sean de sólo lectura.

+++

+++ Paso 2: Añadir una regla de visibilidad condicional

**Objetivo**: mostrar el campo &quot;Deducción adicional&quot; solo cuando el salario bruto supere los 50 000 $.

1. **Seleccione el campo Salario bruto** y haga clic en el icono del Editor de reglas ![edit-rules](/help/forms/assets/edit-rules-icon.svg)
2. **Crear nueva regla**:
   - Haga clic en **Crear**
   - Cambiar tipo de regla de &quot;Set Value Of&quot; a **&quot;When&quot;**
3. **Configurar la condición**:
   - Seleccione **&quot;es mayor que&quot;** en el menú desplegable
   - Escriba `50000` en el campo de número
4. **Establecer la acción Then**:
   - Elija **&quot;Mostrar&quot;** de la lista desplegable Seleccionar acción
   - Arrastre o seleccione el campo **&quot;Deducción adicional&quot;** de Objetos de formulario
5. **Agregar la acción Else**:
   - Haga clic en **&quot;Agregar otra sección&quot;**
   - Elija **&quot;Ocultar&quot;** de la lista desplegable Seleccionar acción
   - Seleccione el campo **&quot;Deducción adicional&quot;**
6. **Guardar la regla**: haga clic en **Listo**

>[!NOTE]
>
> Enfoque alternativo: Puede lograr el mismo resultado creando una regla Mostrar/Ocultar directamente en el campo &quot;Deducción adicional&quot; en lugar de una regla When en &quot;Salario bruto&quot;.

+++

+++ Paso 3: Añadir reglas de cálculo

**Objetivo**: Calcular automáticamente &quot;Ingresos gravables&quot; e &quot;Impuestos por pagar&quot; según los datos proporcionados por el usuario.

**Configurar cálculo de ingresos gravables**:

1. **Seleccione el campo &quot;Ingresos gravables&quot;** y abra el Editor de reglas
2. **Crear expresión matemática**:
   - Haga clic en **Crear** → Seleccionar **&quot;Expresión matemática&quot;**
   - Expresión de compilación: **salario bruto − deducción adicional**
   - Arrastre &quot;Salario bruto&quot; al primer campo
   - Seleccionar operador **&quot;Menos&quot;**
   - Arrastre &quot;Deducción adicional&quot; al segundo campo
3. **Guardar**: Haga Clic En **Listo**

**Configurar cálculo de impuestos a pagar**:

1. **Seleccione el campo &quot;Impuesto a pagar&quot;** y abra el Editor de reglas
2. **Crear expresión matemática**:
   - Haga clic en **Crear** → Seleccionar **&quot;Expresión matemática&quot;**
   - Expresión de compilación: **Ingresos gravables × 10 ÷ 100**
   - Arrastre &quot;Ingresos gravables&quot; al primer campo
   - Seleccione el operador **&quot;Multiplied by&quot;**
   - Escriba `10` como número
   - Haga clic en **&quot;Extender expresión&quot;**
   - Seleccionar operador **&quot;dividido por&quot;**
   - Escriba `100` como número
3. **Guardar**: Haga Clic En **Listo**

+++

+++ Paso 4: Probar el formulario

**Compruebe su implementación probando el flujo completo**:

1. **Vista previa del formulario**: haga clic en el modo de vista previa en el editor universal
2. **Probar la lógica condicional**:
   - Ingresar salario bruto = `30000` → &quot;Deducción adicional&quot; debe permanecer oculto
   - Ingresar salario bruto = `60000` → debería aparecer &quot;Deducción adicional&quot;
3. **Cálculos de pruebas**:
   - Con el salario bruto = `60000`, especifique la deducción adicional = `5000`
   - Verificar ingreso gravable = `55000` (60000 - 5000)
   - Verificar Impuesto A Pagar = `5500` (55000 × 10%)

![Vista previa de un formulario](/help/edge/docs/forms/assets/rule-editor-form.png)
Imagen: calculadora de impuestos completada con campos condicionales y cálculos automáticos

**Criterios de éxito**: el formulario debe mostrar u ocultar campos de forma dinámica y calcular valores en tiempo real a medida que los usuarios escriben.


+++

## Avanzadas: Funciones personalizadas

Para obtener una lógica empresarial compleja que vaya más allá de las capacidades integradas, puede crear funciones de JavaScript personalizadas que se integren a la perfección con el Editor de reglas.

+++ Cuándo utilizar funciones personalizadas

**Escenarios ideales para funciones personalizadas**:

- **Cálculos complejos**: los cálculos de varios pasos no se expresan fácilmente en la regla de expresiones matemáticas
- **Validaciones específicas de la empresa**: lógica de validación personalizada específica de su organización o sector
- **Transformaciones de datos**: Conversiones de formato, manipulaciones de cadenas o análisis de datos
- **Integraciones externas**: llamadas a API internas o servicios de terceros (con limitaciones)

**Ventajas de las funciones personalizadas**:

- **Capacidad de reutilización**: escriba una vez y utilícelo en varios formularios y reglas
- **Mantenimiento**: lógica centralizada más fácil de actualizar y depurar
- **Rendimiento**: ejecución de JavaScript optimizada comparada con cadenas de reglas complejas
- **Flexibilidad**: Administre casos extremos y escenarios complejos no abordados por reglas estándar

+++

+++ Creación e implementación de funciones personalizadas

**Ubicación de archivo**: todas las funciones personalizadas deben definirse en `/blocks/form/functions.js` en su proyecto de Edge Delivery Services.

**Flujo de trabajo de desarrollo**:

1. **Diseño de función**
   - Utilice nombres de funciones descriptivos y orientados a la acción
   - Definir tipos de parámetros claros y valores devueltos
   - Gestión correcta de casos extremos e entradas no válidas

2. **Implementación**
   - Escriba JavaScript limpio y bien comentado
   - Incluir validación de entrada y control de errores
   - Prueba de funciones independiente antes de la integración

3. **Documentación**
   - Añadir comentarios JSDoc completos
   - Incluir ejemplos de uso y descripciones de parámetros
   - Documente cualquier limitación o dependencia

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

![Agregando función personalizada](/help/edge/docs/forms/assets/create-custom-function.png)
Imagen: adición de funciones personalizadas al archivo functions.js

+++

+++ Uso de funciones personalizadas en el Editor de reglas

**Pasos de integración**:

1. **Agregar función al proyecto**
   - Cree o edite `/blocks/form/functions.js` en su proyecto
   - Incluya la función en la instrucción de exportación

2. **Implementar y compilar**
   - Confirmar cambios en el repositorio
   - Asegúrese de que el proceso de compilación se complete correctamente
   - Deje tiempo para actualizaciones de la caché de CDN

3. **Acceso en el editor de reglas**
   - Abra el Editor de reglas para cualquier componente del formulario
   - Seleccione **&quot;Salida de función&quot;** en el menú desplegable **Seleccionar acción**
   - Elija la función personalizada de la lista de funciones disponibles
   - Configurar parámetros de función mediante campos de formulario o valores estáticos

4. **Realizar pruebas exhaustivas**
   - Vista previa del formulario para comprobar el comportamiento de la función
   - Pruebe con varias combinaciones de entrada, incluidos los casos de borde
   - Comprobar el impacto del rendimiento en la carga y la interacción del formulario

![Función personalizada en el editor de reglas](/help/edge/docs/forms/assets/custom-function-rule-editor.png)
Imagen: selección y configuración de funciones personalizadas en la interfaz del Editor de reglas

**Prácticas recomendadas para el uso de funciones**:

- **Control de errores**: Incluya siempre el comportamiento de reserva para los errores de funciones
- **Rendimiento**: funciones de perfil con volúmenes de datos realistas
- **Seguridad**: valide todas las entradas para evitar vulnerabilidades de seguridad
- **Pruebas**: cree casos de prueba que cubran casos normales y extremos

+++

## Prácticas recomendadas para el desarrollo de reglas


+++ Optimización del rendimiento

- Minimice la complejidad de la regla; divida la lógica grande en reglas pequeñas y centradas
- Ordenar reglas por frecuencia (más común primero)
- Mantener manejables los conjuntos de reglas por componente
- Preferir funciones personalizadas reutilizables en lugar de lógica duplicada

+++

+++ Experiencia de usuario

- Proporcionar una validación clara y comentarios en línea
- Evite los cambios visuales molestos; utilice mostrar/ocultar cuidadosamente
- Pruebas entre dispositivos y diseños

+++

+++ Higiene del desarrollo

- Prueba con casos extremos y valores conocidos
- Verificar en los distintos navegadores
- Documentar la intención detrás de reglas complejas, no solo la mecánica
- Mantener un inventario de reglas para formularios grandes
- Utilice una nomenclatura uniforme para los componentes y las reglas
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
- Fragmentos de expresión de prueba individualmente
- Confirmar tipos de datos (números o cadenas)

+++

+++ Problemas de rendimiento

- Simplificación de las condiciones profundamente anidadas
- Funciones personalizadas de perfil
- Minimizar las llamadas externas dentro de las reglas
- Uso de selectores y referencias específicos

+++

+++ Problemas de funciones personalizadas

- Confirmar ruta de archivo: `/blocks/form/functions.js`
- Asegúrese de que las exportaciones con nombre sean correctas
- Confirme que la compilación incluye los cambios.
- Borrar la caché del explorador después de la implementación
- Validar tipos de parámetros y gestión de errores

+++

+++ Integración del editor universal

- Confirme que la extensión del Editor de reglas esté habilitada.
- Seleccione un componente compatible
- Utilice un navegador compatible (Chrome, Firefox, Safari)
- Compruebe que tiene los permisos necesarios

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
> - Monitorización del rendimiento después de la implementación
> - Tener un plan de reversión para los problemas de reglas
> - Considere las redes lentas y los dispositivos de baja especificación

## Resumen

El editor de reglas del editor universal transforma los formularios estáticos en experiencias inteligentes y adaptables que se adaptan a los datos introducidos por el usuario en tiempo real. Al aprovechar la lógica condicional, los cálculos automatizados y las reglas empresariales personalizadas, puede crear flujos de trabajo de formulario sofisticados sin escribir código de aplicación.

**Funciones clave que ha aprendido**:

- **Lógica condicional**: muestra y oculta campos basados en los datos proporcionados por el usuario para crear experiencias relevantes y enfocadas
- **Cálculos dinámicos**: Calcule automáticamente valores (impuestos, totales, tasas) a medida que los usuarios interactúen con el formulario
- **Validación de datos**: implementa la validación en tiempo real con mensajes de comentarios claros y procesables
- **Funciones personalizadas**: amplíe las capacidades con JavaScript para integraciones y lógica empresarial compleja
- **Optimización del rendimiento**: aplique las prácticas recomendadas para un desarrollo de reglas eficiente y que se pueda mantener

**Valor entregado**:

- **Experiencia del usuario mejorada**: Reduzca la carga cognitiva con revelación progresiva y flujos de formularios inteligentes
- **Errores reducidos**: Impida los envíos no válidos mediante validación en tiempo real y entrada guiada
- **Mayor eficiencia**: Automatice los cálculos y la entrada de datos para minimizar el esfuerzo del usuario
- **Soluciones que se pueden mantener**: Cree reglas reutilizables y bien documentadas que se escalen en toda la organización

**Impacto empresarial**:

Forms se convierte en potentes herramientas para la recopilación de datos, la calificación de posibles clientes y la participación del usuario. El Editor de reglas permite a los autores no técnicos implementar una lógica empresarial sofisticada, reducir los costes de desarrollo y mejorar las tasas de finalización de los formularios y la calidad de los datos.

+++

+++ Próximos pasos

**Ruta de aprendizaje recomendada**:

1. **Empiece con lo básico**: cree reglas sencillas de mostrar y ocultar para comprender los conceptos principales
2. **Práctica con tutoriales**: Utiliza el ejemplo de la calculadora de impuestos como base para tus propios formularios
3. **Expandir gradualmente**: Agregue expresiones matemáticas y reglas de validación a medida que aumente su confianza
4. **Implementar funciones personalizadas**: Desarrolle funciones de JavaScript para los requisitos empresariales especializados
5. **Optimizar y escalar**: aplique las prácticas recomendadas de rendimiento y mantenga la documentación de reglas

**Recursos adicionales**:

- [Documentación del editor universal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction.html) para un contexto más amplio
- [Guía de Extension Manager](/help/implementing/developing/extending/extension-manager.md) para habilitar funciones adicionales
- [Formularios Edge Delivery Services](/help/edge/docs/forms/overview.md) para obtener instrucciones completas de desarrollo de formularios

+++
