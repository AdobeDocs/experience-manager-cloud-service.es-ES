---
title: Creación de Forms adaptable con editor universal
description: Aprenda a diseñar, probar y optimizar formularios adaptables para todos los dispositivos con el editor universal. Pruebas de dispositivos maestros, patrones de diseño y técnicas de optimización móvil para AEM Forms con Edge Delivery Services.
keywords: formularios adaptables, formularios móviles, prueba de dispositivos, editor universal, diseño adaptable, optimización de formularios, diseño móvil, diseño adaptable, diseños de formulario, emulador de dispositivos
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: ccfb85da187e828b5f7e8b1a8bae3f483209368d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 1%

---


# Creación de Forms adaptable con editor universal

Los usuarios acceden a formularios en una amplia gama de dispositivos, incluidos escritorios, tabletas y smartphones. El diseño de formularios adaptables garantiza una experiencia óptima para todos los usuarios, independientemente del dispositivo. En esta guía se explica cómo diseñar, probar y optimizar formularios para cualquier tamaño de pantalla con el Editor universal.


La creación de formularios adaptables implica dos actividades principales:

- **Pruebas adaptables:** Obtenga una vista previa y pruebe los formularios en varios tamaños de pantalla mediante emuladores de dispositivo.
- **Diseño interactivo:** Seleccione e implemente patrones de diseño que se adapten sin problemas a diferentes dispositivos.

**En esta guía, aprenderá a:**

- Probar formularios en equipos de escritorio, tabletas y dispositivos móviles
- Seleccione los patrones de diseño adecuados para el contenido
- Aplicar prácticas recomendadas de diseño interactivo
- Solucionar problemas comunes de formularios adaptables
- Optimización de formularios para el rendimiento móvil

## Por qué es importante Forms interactivo

**Impacto en la experiencia del usuario:**

- Más del 60 % de los usuarios acceden a formularios en dispositivos móviles
- Las experiencias móviles deficientes generan una tasa de abandono un 67 % mayor
- Los formularios adaptables pueden aumentar las tasas de finalización hasta en un 25 %

**Beneficios empresariales:**

- Tasas de finalización de formularios más altas
- Satisfacción del usuario mejorada
- Cumplimiento de accesibilidad mejorado
- Menores costes de desarrollo y mantenimiento

>[!TIP]
>
> **Enfoque Mobile-First:** Empiece a diseñar para dispositivos móviles y, a continuación, mejore para pantallas más grandes. Esto garantiza que la funcionalidad principal funcione en el entorno más restringido.

## Parte 1: Prueba de Forms entre dispositivos

Probar los formularios en diferentes dispositivos le ayuda a identificar y resolver los problemas adaptables antes de que los usuarios los encuentren. El editor universal proporciona un modo de emulador para simular varios tamaños y orientaciones de pantalla.

### Cómo probar su Forms

**Paso 1: Abrir el emulador de dispositivos**

1. Abra el formulario en el Editor universal.
2. Haga clic en el icono ![Emulador](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulador** de la barra de herramientas.
3. Aparecerá el menú del selector de dispositivos.

![Interfaz de prueba adaptable del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Paso 2: Seleccione un dispositivo para realizar pruebas**

- **Escritorio** (anchura superior a 1200 px): vista de edición predeterminada
- **Tablet** (768 px-1199 px de ancho): prueba de pantalla de Medium
- **Móvil** (anchura de 320 px-767 px): prueba de pantalla pequeña
- **Personalizado**: especifique las dimensiones exactas para dispositivos específicos

**Paso 3: Probar las orientaciones del dispositivo**

Utilice el icono **Rotador de pantalla** para probar ambos:

- **Modo vertical**: orientación móvil estándar
- **Modo horizontal**: vista de teléfono o tableta girada

### Resultados de prueba de dispositivo

Cada tipo de dispositivo revela comportamientos adaptables únicos:

| **Tipo de dispositivo** | **Ancho de pantalla** | **Qué comprobar** | **Problemas comunes** |
|-----------------|------------------|-------------------|-------------------|
| **Escritorio** | 1200px+ | Diseño completo, todas las funciones visibles | Espacio en blanco excesivo, diseños demasiado anchos |
| **Tablet** | 768px-1199px | Apilado de componentes, facilidad de uso de navegación | Tamaño incómodo, toque los problemas de destino |
| **Móvil** | 320px-767px | Diseño de una sola columna, navegación con miniatura | Texto pequeño, botones con espacios estrechos |
| **Personalizado** | Definido por el usuario | Requisitos específicos de los dispositivos | Casos extremos de punto de interrupción |

### Ejemplos visuales por dispositivo

**Vista de escritorio (1200px+):**
![Vista de formulario de escritorio](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Diseño de ancho completo con campos de formulario en paralelo.*

**Vista de tableta (768px-1199px):**
![Vista de formulario de tableta](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Diseño de ancho Medium con espaciado de componente ajustado.*

**Vista móvil (320px-767px):**
![Vista de formulario móvil](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Diseño de una sola columna con componentes apilados.*

**Vista de dispositivo personalizado:**
![Vista de dispositivo personalizado](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Dimensiones especificadas por el usuario para pruebas de destino.*

### Probar flujo de trabajo

**Para nuevo Forms:**

1. **Generar en vista de escritorio:** Comience con funcionalidad completa.
2. **Prueba en la tableta:** Comprueba las adaptaciones de las pantallas medianas.
3. **Validar en dispositivos móviles:** Garantizar el uso en pantallas pequeñas.
4. **Solucionar problemas adaptables:** Ajustar diseños según sea necesario.
5. **Volver a probar todos los dispositivos:** Confirmar correcciones en todos los tamaños.

**Para Forms Existente:**

1. **Comprobación rápida del móvil:** ¿Funciona el formulario en los teléfonos?
2. **Identificar áreas problemáticas:** Tenga en cuenta los problemas de uso y diseño.
3. **Pruebas sistemáticas:** Pruebe exhaustivamente cada tamaño de dispositivo.
4. **Problemas del documento:** Realice un seguimiento de lo que debe solucionarse.
5. **Implementar correcciones:** Solucionar problemas metódicamente.

## Parte 2: Selección de patrones de diseño adaptables

Los patrones de diseño determinan la forma en que el contenido del formulario se adapta a diferentes tamaños de pantalla. El patrón correcto mejora tanto la experiencia del usuario como el rendimiento móvil.

### Información general del patrón de diseño

| **Tipo de diseño** | **Es ideal para lo siguiente** | **Rendimiento móvil** | **Complejidad** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Diseño de panel** | Contenido clasificado, formularios estilo panel | Bien | Bajo |
| **Diseño de asistente** | Procesos de varios pasos, flujos de trabajo complejos | Excelente | Media |
| **Diseño de acordeón** | Contenido de estilo FAQ, secciones opcionales | Excelente | Bajo |

### Guía de decisión rápida

**Usar diseño de panel cuando:**

- El contenido se divide en distintas categorías
- Los usuarios deben ver varias secciones a la vez
- El contenido es relativamente sencillo

**Usar diseño de asistente cuando:**

- El formulario tiene varios pasos lógicos
- Desea reducir la carga cognitiva
- Los usuarios móviles son una audiencia principal

**Usar diseño de acordeón al:**

- El formulario tiene contenido opcional o secundario
- La conservación del espacio es importante
- El contenido se puede agrupar lógicamente

### Diseño de panel

**Propósito:** organiza el contenido relacionado en secciones visualmente distintas que se pueden ver simultáneamente.

![Ejemplo de diseño de panel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamiento interactivo:**

- **Escritorio (1200px+):** paneles se muestran uno al lado del otro o en una cuadrícula
- **Tablet (768px-1199px):** paneles apilados verticalmente con espaciado
- **Móvil (320px-767px):** Diseño de una sola columna con saltos de sección claros

**Pasos de implementación:**

1. Usar [componente Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel).
2. Agrupar campos relacionados dentro de cada panel.
3. Agregue encabezados claros para cada sección.
4. Asegúrese de que haya un espacio adecuado entre los paneles.

**Prácticas recomendadas:**

- Limite entre 3 y 4 paneles en el escritorio para evitar abrumar a los usuarios.
- Utilice títulos descriptivos para cada panel.
- Agrupar lógicamente los campos relacionados para reducir la carga cognitiva.
- Pruebe la navegación del panel en dispositivos táctiles.

**Casos de uso de ejemplo:**

- **Solicitud de empleo:** Información personal, educación, experiencia, referencias
- **Registro del producto:** Detalles básicos, especificaciones técnicas, información sobre la garantía
- **Forms de encuesta:** datos demográficos, preferencias, comentarios, contacto

### Diseño de asistente

**Propósito:** guía a los usuarios a través de procesos complejos paso a paso, reduciendo la carga cognitiva y mejorando las tasas de finalización.

![Ejemplo de diseño del asistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamiento interactivo:**

- **Todos los dispositivos:** Mantiene el enfoque de un solo paso para una experiencia móvil óptima.
- **Contenido del paso:** se adapta en cada paso (apilado o en paralelo).
- **Navegación:** Botones táctiles con suficiente espacio.
- **Indicador de progreso:** Escala correctamente el tamaño de la pantalla.

**Pasos de implementación:**

1. Usar el [componente Asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard).
2. Divida los formularios complejos en pasos lógicos (los pasos de 3 a 7 son óptimos).
3. Incluya indicadores de progreso para la orientación del usuario.
4. Proporcione controles de navegación claros (Siguiente, Atrás, Guardar).

**Optimización móvil:**

- Utilice destinos táctiles grandes (mínimo 44 píxeles) para los botones de navegación.
- Asegúrese de que los indicadores de paso sean claros y visibles en las pantallas pequeñas.
- Limite el número de campos por paso para reducir el desplazamiento.
- Habilite el guardado automático para evitar la pérdida de datos.

**Prácticas recomendadas:**

- Asegúrese de la progresión lógica del paso: cada paso debe basarse en el anterior.
- Utilice títulos de pasos claros para que los usuarios sepan qué esperar.
- Valide la entrada en cada paso para detectar los errores de forma temprana.
- Permite a los usuarios navegar hacia atrás para revisar o editar la información.

**Casos de uso de ejemplo:**

- **Reclamos de seguro:** Incidente → Evidencia → Revisión de → personal
- **Configuración de cuenta:** Información básica → Preferencias → Confirmación de → de seguridad
- **Proceso de pedido:** Productos → Envío → Resumen de → de pago

### Diseño de acordeón

**Objetivo:** Ahorra espacio al organizar el contenido en secciones contraíbles, lo que resulta ideal para la información opcional o secundaria.

![Ejemplo de diseño de acordeón](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamiento interactivo:**

- **Excelente rendimiento móvil:** Solo se muestra contenido relevante.
- **Encabezados táctiles:** Fácil de tocar y expandir secciones.
- **Animaciones suaves:** Proporcione comentarios visuales para las interacciones.
- **Espacio eficiente:** minimiza el desplazamiento en todos los dispositivos.

**Pasos de implementación:**

1. Usar el [componente Acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion).
2. Agrupar contenido opcional relacionado en cada sección.
3. Utilice encabezados de sección descriptivos.
4. Establezca los estados abiertos/cerrados predeterminados adecuados.

**Ventajas móviles:**

- Reduce el desplazamiento al contraer las secciones no utilizadas.
- Interacción táctil con gestos naturales de expansión/contracción.
- Carga más rápida: solo está visible el contenido activo.
- Enfoque mejorado: los usuarios solo ven lo que necesitan.

**Prácticas recomendadas:**

- Utilice encabezados de sección claros para que los usuarios sepan qué hay dentro antes de expandirlo.
- Agrupe el contenido relacionado lógicamente dentro de cada sección.
- Configure las secciones importantes para que comiencen a expandirse si es necesario.
- Proporcione vistas previas de sección breves para ayudar a los usuarios a decidir qué expandir.

**Casos de uso de ejemplo:**

- **Configuración del producto:** Accesorios → básicos → avanzados de →
- **Preguntas más frecuentes sobre Forms:** Cuenta → Facturación → Técnico → General
- **Configuración Forms:** Notificaciones de → de privacidad → Apariencia → avanzada

## Parte 3: Prácticas recomendadas de diseño interactivo

### Prácticas recomendadas por tipo de dispositivo

+++Optimización móvil (320px-767px)

**Prácticas esenciales:**

- Utilice un diseño de una sola columna para todo el contenido.
- Proporcionar botones grandes y táctiles (altura mínima de 44 píxeles).
- Simplifique la navegación con opciones claras de atrás/siguiente.
- Minimice el desplazamiento dentro de cada sección.
- Enfoque automático en el primer campo para mostrar el teclado.

**Directrices específicas de campo:**

- **Entradas de texto:** Anchura completa con relleno amplio.
- **desplegables:** Use elementos seleccionados nativos para una mejor experiencia táctil.
- **Selector de fecha:** Use entradas de fecha nativas para la compatibilidad móvil.
- **Cargas de archivos:** Proporciona áreas de carga grandes y claras.

+++

+++Optimización de tableta (768px-1199px)

**Estrategias de diseño:**

- Utilice diseños de dos columnas para los campos relacionados.
- Pruebe las orientaciones vertical y horizontal.
- Admite interacciones táctiles y con el ratón.
- Proporcione áreas de contenido más grandes sin perder la legibilidad.

+++

+++Optimización de sobremesas (1200 px+)

**Características avanzadas:**

- Utilice diseños de varias columnas para un uso eficiente del espacio.
- Ofrezca métodos abreviados del teclado para los usuarios avanzados.
- Implemente estados de desplazamiento para los comentarios interactivos.
- Proporcionar validación avanzada con mensajes de error detallados.

+++

## Solución de problemas completa

### Problemas de diseño

+++Saltos de diseño de formulario en dispositivos móviles

**Causas comunes:**

- Elementos de ancho fijo que no se escalan
- CSS diseñado para diseños que empiezan por el escritorio
- Imágenes o contenido que rebosan sus contenedores

**Soluciones:**

- Asegúrese de que las imágenes y los contenedores se adaptan al tamaño de pantalla.
- Utilice un diseño con prioridad móvil con mejora progresiva.
- Realice pruebas tanto con emuladores de dispositivos como con dispositivos reales.
- Utilice un tamaño flexible en lugar de dimensiones fijas.

+++

+++Tocar destinos demasiado pequeños

**Causas comunes:**

- Botones menores de 44 px × 44 px
- Elementos interactivos colocados demasiado juntos
- CSS personalizado que anula los valores predeterminados táctiles

**Soluciones:**

- Asegúrese de que todos los elementos interactivos tengan al menos 44 px × 44 px.
- Añada espaciado entre botones y vínculos.
- Pruebe la interacción táctil con los dedos reales, no solo con un ratón.
- Aumente las áreas de destino táctiles para facilitar los toques.

+++

+++Problemas de desbordamiento de contenido

**Causas comunes:**

- Texto largo o etiquetas que no se ajustan
- Contenedores de ancho fijo
- Imágenes que no se escalan correctamente

**Soluciones:**

- Habilite el ajuste de texto para el contenido largo.
- Utilice imágenes adaptables que se escalen correctamente.
- Implementar diseños flexibles que se adapten al contenido.
- Realizar pruebas con varias longitudes de contenido.

+++

### Problemas de rendimiento

+++Carga lenta en dispositivos móviles

**Causas comunes:**

- Imágenes grandes no optimizadas para dispositivos móviles
- Ejecución excesiva de JavaScript
- Se están cargando demasiados campos de formulario a la vez

**Soluciones:**

- Optimizar imágenes para diferentes tamaños de pantalla.
- Cargue contenido no crítico solo cuando sea necesario.
- Utilice técnicas para acelerar la carga móvil.
- Minimice los scripts y widgets de terceros.

+++

### Problemas de prueba y validación

+++Diferencias entre emulador y dispositivo real

**Causas comunes:**

- Diferencias de procesamiento específicas del explorador
- Diferencias en la interacción táctil frente al ratón
- Variaciones de velocidad de red

**Soluciones:**

- Realizar pruebas en dispositivos reales siempre que sea posible.
- Utilice varios exploradores para probar el emulador.
- Simule diferentes velocidades de red durante la prueba.
- Valide con usuarios reales en entornos de destino.

+++

## Métricas de éxito para Forms interactivo

+++Indicadores clave de rendimiento

**Métricas de experiencia del usuario:**

- **Tasa de finalización de formularios:** Destino: 85%+ en dispositivos móviles
- **Tiempo para finalizar:** El tiempo de finalización del móvil debe estar dentro del 20% del escritorio
- **Tasa de error:** Menos del 5% de errores de validación
- **Puntos de abandono:** Identificar dónde abandonan los usuarios

**Rendimiento técnico:**

- **Tiempo de carga de la página:** Menos de 3 segundos en redes 3G
- **Datos básicos vitales para la web:** supera todos los puntos de referencia de rendimiento de Google
- **Puntuación de accesibilidad:** Cumplimiento de WCAG 2.1 AA
- **Compatibilidad entre exploradores:** funcionalidad superior al 98 % en los exploradores principales

+++

+++Lista de comprobación de pruebas

**Antes de la publicación:**

- Pruebe el formulario en dispositivos móviles reales.
- Asegúrese de que todos los objetivos táctiles tengan al menos 44 × 44 píxeles.
- Compruebe la legibilidad del texto en todos los tamaños de pantalla.
- Confirmar que la validación del formulario funciona en todos los dispositivos.
- Asegúrese de que el tiempo de carga sea inferior a 3 segundos en el móvil.
- Compruebe que todos los elementos interactivos sean accesibles.
- Probar el envío del formulario en todos los dispositivos compatibles.

+++

## Próximos pasos

**Acciones inmediatas:**

1. **Auditar los formularios actuales:** Probar los formularios existentes mediante el emulador de dispositivos.
2. **Identificar ganancias rápidas:** Corrija primero los problemas obvios de uso móvil.
3. **Priorizar los formularios de alto tráfico:** Céntrese en los formularios que tengan el mayor impacto en el usuario.
4. **Implementar un enfoque que dé prioridad a los dispositivos móviles:** Comience con el diseño de pantalla más pequeño.

**Optimización avanzada:**

- **Supervisión del rendimiento:** Configure Analytics para rastrear las métricas del formulario.
- **Pruebas A/B:** Experimente con diferentes diseños y enfoques.
- **Recopilación de comentarios de usuarios:** Recopilar información de usuarios reales.
- **Mejora continua:** Revise y optimice formularios con regularidad.


