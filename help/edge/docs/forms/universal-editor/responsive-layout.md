---
title: Crear formularios adaptables con el editor universal
description: Aprenda a diseñar, probar y optimizar formularios adaptables para todos los dispositivos con el editor universal. Pruebas de dispositivos maestros, patrones de diseño y técnicas de optimización móvil para AEM Forms con Edge Delivery Services.
keywords: formularios adaptables, formularios móviles, prueba de dispositivos, editor universal, diseño adaptable, optimización de formularios, diseño móvil, diseño interactivo, diseños de formulario, emulador de dispositivos
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '2382'
ht-degree: 100%

---


# Crear formularios adaptables con el editor universal

El panorama web moderno exige formularios que funcionen sin problemas en un espectro cada vez más amplio de dispositivos y tamaños de pantalla. Desde grandes monitores de escritorio hasta pantallas compactas para teléfonos inteligentes, los usuarios esperan experiencias uniformes e intuitivas independientemente del dispositivo que elijan. La creación de formularios adaptables ya no es opcional: es un requisito fundamental para ofrecer experiencias digitales profesionales, accesibles y optimizadas para la conversión.

El editor universal proporciona herramientas y metodologías completas para desarrollar formularios adaptables que se adaptan de forma inteligente a varias dimensiones de pantalla, métodos de entrada y contextos de usuario. Esta guía explora los fundamentos técnicos, las estrategias de implementación y las técnicas de optimización necesarias para crear formularios que funcionen de forma excepcional en todos los dispositivos, al tiempo que mantienen la facilidad de uso, la accesibilidad y el atractivo visual.

La creación de formularios adaptables implica dos actividades principales:

- **Pruebas adaptables:** obtenga una vista previa y pruebe los formularios en varios tamaños de pantalla mediante emuladores de dispositivo.
- **Diseño interactivo:** seleccione e implemente patrones de diseño que se adapten sin problemas a diferentes dispositivos.

**En esta guía, aprenderá lo siguiente:**

- Probar formularios en equipos de escritorio, tabletas y dispositivos móviles.
- Seleccionar los patrones de diseño adecuados para el contenido.
- Aplicar prácticas recomendadas de diseño interactivo
- Solucionar problemas comunes de formularios adaptables
- Optimizar formularios para el rendimiento móvil

## Por qué son importantes los formularios adaptables

**Impacto en la experiencia del usuario:**

- Más del 60 % de los usuarios acceden a formularios en dispositivos móviles
- Las experiencias móviles deficientes generan una tasa de abandono un 67 % mayor
- Los formularios adaptables pueden aumentar las tasas de finalización hasta en un 25 %

**Ventajas empresariales:**

- Tasas de finalización de formularios más altas
- Mayor satisfacción del usuario
- Mejora en el cumplimiento de accesibilidad
- Menores costes de desarrollo y mantenimiento

>[!TIP]
>
> **Enfoque que prioriza los dispositivos móviles:** empiece a diseñar para dispositivos móviles y, después, aplique mejoras para pantallas más grandes. De este modo, se garantiza que la funcionalidad principal funcione en el entorno más restringido.

## Parte 1: Prueba de los formularios entre dispositivos

Probar los formularios en diferentes dispositivos le ayuda a identificar y resolver los problemas de adaptabilidad antes de que los usuarios los encuentren. El editor universal proporciona un modo emulador para simular varios tamaños y orientaciones de pantalla.

### Cómo probar su formulario

**Paso 1: Abrir el emulador de dispositivos**

1. Abra el formulario en el editor universal.
2. Haga clic en el icono ![Emulador](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%,width=2%} **Emulador** de la barra de herramientas.
3. Aparecerá el menú del selector de dispositivos.

![Interfaz de prueba de adaptabilidad del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

**Paso 2: Seleccione un dispositivo para realizar las pruebas**

- **Escritorio** (anchura superior a 1200 px): vista de edición predeterminada
- **Tableta** (768 px-1199 px de ancho): prueba de pantalla media
- **Móvil** (anchura de 320 px-767 px): prueba de pantalla pequeña
- **Personalizado**: especifique las dimensiones exactas para dispositivos específicos

**Paso 3: Pruebe las orientaciones del dispositivo**

Utilice el icono **Rotador de pantalla** para probar ambos:

- **Modo vertical**: orientación móvil estándar
- **Modo horizontal**: vista girada de teléfono o tableta

### Resultados de prueba de dispositivo

Cada tipo de dispositivo revela comportamientos adaptables únicos:

| **Tipo de dispositivo** | **Ancho de pantalla** | **Qué comprobar** | **Problemas comunes** |
|-----------------|------------------|-------------------|-------------------|
| **Escritorio** | 1200px+ | Diseño completo, todas las funciones visibles | Espacio en blanco excesivo, diseños demasiado anchos |
| **Tableta** | 768 px–1199 px | Apilado de componentes, facilidad de uso de navegación | Tamaño incómodo, problemas con los destinos táctiles |
| **Móvil** | 320 px-767 px | Diseño de una sola columna, navegación con miniaturas | Texto pequeño, botones con espacios estrechos |
| **Personalizado** | Definido por el usuario | Requisitos específicos de los dispositivos | Casos extremos de punto de interrupción |

### Ejemplos visuales por dispositivo

**Vista de escritorio (1200 px+):**
![Vista de formulario de escritorio](/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png)
*Diseño de ancho completo con campos de formulario en paralelo.*

**Vista de tableta (768 px-1199 px):**
![Vista de formulario de tableta](/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png)
*Diseño de ancho medio con espaciado de componentes ajustado.*

**Vista móvil (320 px-767 px):**
![Vista de formulario móvil](/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png)
*Diseño de una sola columna con componentes apilados.*

**Vista de dispositivo personalizado:**
![Vista de dispositivo personalizado](/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png)
*Dimensiones especificadas por el usuario para pruebas de destino.*

### Prueba del flujo de trabajo

**Para nuevos formularios:**

1. **Generar en vista de escritorio:** comience con funcionalidad completa.
2. **Probar en la tableta:** compruebe las adaptaciones de las pantallas medianas.
3. **Validar en dispositivos móviles:** garantizar el uso en pantallas pequeñas.
4. **Solucionar problemas adaptables:** ajustar diseños según sea necesario.
5. **Volver a probar todos los dispositivos:** confirmar correcciones en todos los tamaños.

**Para los formularios existentes:**

1. **Comprobación rápida en el móvil:** ¿funciona el formulario en los teléfonos?
2. **Identificar áreas problemáticas:** tenga en cuenta los problemas de diseño y capacidad de uso.
3. **Pruebas sistemáticas:** pruebe exhaustivamente cada tamaño de dispositivo.
4. **Problemas del documento:** realice un seguimiento de lo que debe solucionarse.
5. **Implementar correcciones:** abordar los problemas metódicamente.

## Parte 2: Selección de patrones de diseño adaptables

Los patrones de diseño determinan la forma en que el contenido del formulario se adapta a diferentes tamaños de pantalla. El patrón correcto mejora tanto la experiencia del usuario como el rendimiento en el móvil.

### Información general del patrón de diseño

| **Tipo de diseño** | **Es ideal para lo siguiente** | **Rendimiento en el móvil** | **Complejidad** |
|---------------------|-------------------------------------------|------------------------|----------------|
| **Diseño de panel** | Contenido clasificado, formularios estilo panel | Bien | Bajo |
| **Diseño del asistente** | Procesos de varios pasos, flujos de trabajo complejos | Excelente | Media |
| **Diseño de acordeón** | Contenido de estilo FAQ, secciones opcionales | Excelente | Bajo |

### Guía de decisión rápida

**Usar diseño de panel cuando:**

- El contenido se divida en distintas categorías
- Los usuarios deban ver varias secciones a la vez
- El contenido sea relativamente simple

**Usar diseño de asistente cuando:**

- El formulario tiene varios pasos lógicos
- Desee reducir la carga cognitiva
- Los usuarios móviles sean la audiencia principal

**Usar diseño de acordeón cuando:**

- El formulario tenga contenido opcional o secundario
- La conservación del espacio sea importante
- El contenido se pueda agrupar lógicamente

### Diseño del panel

El diseño del panel organiza el contenido relacionado en secciones visualmente distintas, lo que permite a los usuarios ver varias secciones a la vez. Este diseño es ideal para los formularios con información en categorías que se beneficia de una presentación simultánea en pantallas más grandes.

![Ejemplo de diseño de panel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamiento adaptable**

- **Escritorio (1200 px y superior):** los paneles se muestran uno al lado del otro o en una cuadrícula para obtener la máxima visibilidad.
- **Tableta (768px-1199px):** los paneles se apilan verticalmente con el espacio adecuado para mantener la claridad.
- **Móvil (320px-767px):** los paneles se presentan en un diseño de una sola columna, con una clara separación entre las secciones para facilitar la navegación.

**Cómo implementarlo**

1. Agregue el [componente Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) al formulario.
2. Agrupe los campos relacionados dentro de cada panel para mantener la organización lógica.
3. Asigne encabezados claros y descriptivos a cada sección del panel.
4. Asegúrese de que haya suficiente espacio entre los paneles para evitar el desorden visual.

**Prácticas recomendadas**

- Limite el número de paneles a 3 o 4 en el escritorio para no abrumar a los usuarios.
- Utilice títulos concisos y descriptivos en cada panel para mejorar la comprensión de los usuarios.
- Organice los campos dentro de los paneles de forma lógica para minimizar la carga cognitiva.
- Pruebe la navegación del panel en dispositivos táctiles para garantizar la facilidad de uso en todas las plataformas.

**Casos de uso comunes**

- **Solicitud de empleo:** secciones de información personal, educación, experiencia y referencias.
- **Registro del producto:** paneles para obtener detalles básicos, especificaciones técnicas e información sobre la garantía.
- **Formularios tipo encuesta:** agrupaciones para datos demográficos, preferencias, comentarios e información de contacto.

### Diseño del asistente

El diseño del asistente guía a los usuarios a través de un proceso de varios pasos, presentando una sección a la vez. Este diseño es especialmente eficaz para formularios complejos, ya que reduce la carga cognitiva y aumenta las tasas de finalización al dividir el proceso en pasos asequibles.

![Ejemplo de diseño del asistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamiento adaptable**

- **Todos los dispositivos:** mantiene un enfoque de un solo paso, lo cual es óptimo para los usuarios móviles.
- **Contenido del paso:** cada paso se adapta de forma responsable, apilando campos u organizándolos uno al lado del otro según corresponda para el tamaño de pantalla.
- **Navegación:** incluye botones táctiles con un espaciado adecuado para facilitar la interacción.
- **Indicador de progreso:** las barras de progreso o los indicadores de paso se escalan correctamente para diferentes dispositivos, lo que proporciona información clara sobre el estado de finalización.

**Implementación**

1. Inserte el [componente de asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) en el formulario.
2. Divida el formulario en pasos lógicos (lo ideal es entre 3 y 7) para que cada paso sea específico y fácil de administrar.
3. Añada indicadores de progreso para ayudar a los usuarios a comprender su posición en el proceso.
4. Proporcione controles de navegación claros, como los botones Siguiente, Atrás y Guardar.

**Consejos de optimización móvil**

- Utilice destinos táctiles grandes (al menos 44 píxeles de altura) para los controles de navegación a fin de mejorar la accesibilidad.
- Asegúrese de que los indicadores de paso sean visibles y legibles en pantallas pequeñas.
- Limite el número de campos por paso para minimizar el desplazamiento y mejorar el enfoque.
- Habilite la funcionalidad de guardado automático para evitar la pérdida de datos si los usuarios salen del formulario.

**Prácticas recomendadas**

- Diseñe pasos para seguir una progresión lógica, de manera que cada paso se base en el anterior.
- Utilice títulos claros y descriptivos para cada paso a fin de establecer las expectativas del usuario.
- Valide los datos introducidos por el usuario en cada paso para detectar los errores de forma temprana y reducir la frustración.
- Permita a los usuarios retroceder en los pasos de navegación para revisar o editar la información anterior sin perder datos.

**Casos de uso comunes**

- **Reclamaciones de seguro:** pasos para obtener detalles del incidente, envío de pruebas, información personal y revisión.
- **Configuración de cuenta:** fases para obtener información básica, preferencias, configuración de seguridad y confirmación.
- **Proceso de pedido:** pasos para la selección de productos, la información de envío, los detalles de pago y el resumen del pedido.

### Diseño de acordeón

El diseño de acordeón ahorra espacio al organizar el contenido en secciones contraíbles, lo que lo hace ideal para información opcional o secundaria. Este diseño es especialmente eficaz para los formularios con contenido que se puede agrupar lógicamente y no necesita mostrarse todo a la vez.

![Ejemplo de diseño de acordeón](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamiento adaptable**

- **Rendimiento móvil:** solo se expande la sección relevante, lo que reduce la necesidad de desplazarse y mejora los tiempos de carga.
- **Encabezados táctiles optimizados:** los encabezados de sección son fáciles de pulsar y expandir y admiten gestos naturales en dispositivos móviles.
- **Animaciones fluidas:** las secciones de expansión y contracción proporcionan comentarios visuales para las interacciones del usuario.
- **Eficiencia del espacio:** las secciones contraídas minimizan el espacio vertical, lo que facilita la navegación por el formulario en todos los dispositivos.

**Implementación**

1. Añada el [componente de acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) al formulario.
2. Agrupe contenido opcional o secundario relacionado dentro de cada sección de acordeón.
3. Utilice encabezados claros y descriptivos para cada sección a fin de ayudar a los usuarios a comprender qué información incluye.
4. Establezca los estados predeterminados adecuados de apertura o cierre para cada sección en función de la importancia y las necesidades del usuario.

**Ventajas móviles**

- Reduce el desplazamiento mediante la contracción de las secciones no utilizadas, lo que permite a los usuarios centrarse en una sección a la vez.
- La interacción táctil admite gestos de expansión o contracción naturales.
- Carga más rápida, ya que solo está visible el contenido activo.
- Se ha mejorado el enfoque, ya que los usuarios solo ven la información que necesitan en un momento determinado.

**Prácticas recomendadas**

- Utilice encabezados de sección claros para que los usuarios sepan qué esperar antes de expandir una sección.
- Agrupe el contenido relacionado lógicamente dentro de cada sección para ayudar a la comprensión.
- Establezca secciones importantes para que comiencen a expandirse si se requiere atención inmediata.
- Proporcione resúmenes o vistas previas de secciones breves para ayudar a los usuarios a decidir qué secciones expandir.

**Casos de uso comunes**

- **Configuración del producto:** secciones para Opciones básicas, Configuración avanzada, Accesorios y Soporte técnico.
- **Preguntas más frecuentes sobre formularios:** agrupaciones para preguntas sobre la cuenta, facturación, aspectos técnicos y generales.
- **Configuración de formularios:** secciones de Privacidad, Notificaciones, Apariencia y Opciones avanzadas.


## Parte 3: Prácticas recomendadas de diseño interactivo

### Prácticas recomendadas por tipo de dispositivo

+++Optimización móvil (320 px - 767 px)

**Diseño e interacción:**

- Utilice un diseño de una sola columna para todo el contenido del formulario para maximizar la legibilidad y facilidad de uso.
- Asegúrese de que todos los botones y elementos interactivos tengan al menos 44 píxeles de altura para una interacción táctil fiable.
- Proporciona una navegación clara y sencilla con botones visibles para retroceder y continuar.
- Minimice la necesidad de desplazarse dentro de cada sección separando los formularios largos.
- Céntrese automáticamente en el primer campo de entrada para enviar la solicitud al teclado móvil.

**Directrices de campo:**

- Los campos de texto deben abarcar el ancho completo de la pantalla con suficiente relleno para la entrada táctil.
- Utilice elementos nativos de lista desplegable/selección para una óptima facilidad de uso móvil.
- Implemente selectores de fechas nativos para obtener una experiencia móvil coherente.
- Amplie las áreas de carga de archivos y etiquételas con claridad para facilitar el acceso.

+++

+++Optimización de tableta (768 px - 1199 px)

**Diseño y uso:**

- Utilice diseños de dos columnas para campos relacionados para aprovechar el mayor espacio en pantalla.
- Pruebe el aspecto y la facilidad de uso del formulario en orientación vertical y horizontal.
- Diseñe tanto para la entrada táctil como para la del ratón, lo que garantiza que todos los controles sean fácilmente accesibles.
- Aumente el tamaño del área de contenido al tiempo que mantiene una jerarquía visual y una legibilidad claras.

+++

+++Optimización para sobremesa (+1200 px)

**Características avanzadas y diseño:**

- Utilice diseños de varias columnas para utilizar de forma eficaz el espacio horizontal y reducir el desplazamiento vertical.
- Proporcione métodos abreviados de teclado para realizar acciones frecuentes con el fin de admitir usuarios avanzados.
- Implemente estados de desplazamiento y comentarios visuales para elementos interactivos.
- Ofrezca validación avanzada con mensajes de error claros y detallados para formularios complejos.

+++

## Resolución de problemas

### Problemas de diseño

+++Saltos de diseño de formulario en dispositivos móviles

**Posibles causas:**

- Elementos de ancho fijo que no se adaptan a pantallas más pequeñas
- CSS con prioridad de escritorio que anula los estilos móviles
- Las imágenes o el contenido desbordan sus contenedores

**Cómo solucionarlo:**

- Asegúrese de que todas las imágenes y contenedores utilizan un tamaño relativo o basado en porcentajes.
- Comience con un enfoque CSS basado en dispositivos móviles y cree capas de mejoras para pantallas más grandes.
- Pruebe los formularios utilizando emuladores de dispositivos y dispositivos reales.
- Evite las dimensiones fijas y utilice diseños flexibles.

+++

+++Destinos táctiles demasiado pequeños

**Posibles causas:**

- Botones o vínculos de menos de 44 px por 44 px
- Elementos interactivos colocados demasiado juntos
- CSS personalizado que reduce el tamaño de destino táctil predeterminado

**Cómo solucionarlo:**

- Asegúrese de que cada elemento interactivo tenga al menos 44 px por 44 px.
- Agregue el espacio adecuado entre botones, vínculos y otros controles.
- Pruebe con dispositivos táctiles reales, no solo con un ratón.
- Expanda las áreas de destino táctiles según sea necesario para la accesibilidad.

+++

+++Problemas de desbordamiento de contenido

**Posibles causas:**

- Texto largo o etiquetas que no se ajustan
- Contenedores con anchuras fijas
- Imágenes que no se escalan de manera adaptable

**Cómo solucionarlo:**

- Habilite el ajuste de texto para todas las etiquetas y el contenido.
- Utilice imágenes adaptables que se escalen con el contenedor.
- Cree diseños flexibles que se adapten a distintas longitudes de contenido.
- Realice pruebas con contenido corto y largo para garantizar la adaptabilidad.

+++

### Problemas de rendimiento

+++Carga lenta en dispositivos móviles

**Posibles causas:**

- Imágenes grandes sin optimizar
- JavaScript pesado o excesivo
- Demasiados campos de formulario cargándose simultáneamente

**Cómo solucionarlo:**

- Optimice las imágenes para dispositivos móviles y utilice los formatos de archivo adecuados.
- Aplace o cargue de forma diferida contenido no crítico.
- Minimice el uso de scripts y widgets de terceros.
- Optimice los campos de formulario para cargar solo lo necesario.

+++

### Problemas de prueba y validación

+++Diferencias entre emulador y dispositivo real

**Posibles causas:**

- Diferencias en los motores de renderización del explorador
- Interacción táctil no simulada con precisión con el ratón
- Discrepancias de velocidad de red

**Cómo solucionarlo:**

- Realice pruebas siempre en dispositivos reales, además de en emuladores.
- Utilice varios exploradores y dispositivos para realizar pruebas exhaustivas.
- Simule varias velocidades de red para identificar cuellos de botella de rendimiento.
- Recopile comentarios de usuarios reales en la audiencia de destino.

+++

## Métricas de éxito de formularios adaptables

+++Indicadores de rendimiento clave

**Experiencia del usuario:**

- **Tasa de finalización de formularios:** el objetivo es alcanzar el 85 % o más en dispositivos móviles.
- **Tiempo para completar:** los usuarios de dispositivos móviles deben completar los formularios en un plazo del 20 % con respecto las horas necesarias para finalizar en la versión de escritorio.
- **Tasa de error:** mantener los errores de validación por debajo del 5 %.
- **Puntos de abandono:** identifique y solucione los pasos en los que los usuarios abandonan el sitio.

**Rendimiento técnico:**

- **Tiempo de carga de la página:** menos de 3 segundos con una conexión 3G.
- **Elementos web básicos:** cumplen o sobrepasan los umbrales recomendados por Google.
- **Accesibilidad:** consiga el cumplimiento con WCAG 2.1 AA.
- **Compatibilidad de exploradores:** garantice una funcionalidad superior al 98 % en todos los exploradores principales.

+++

+++Lista de comprobación de prueba

**Lista de comprobación previa a la publicación:**

- Pruebe el formulario en dispositivos móviles reales (no solo en emuladores).
- Asegúrese de que todos los destinos táctiles tengan al menos 44 px x 44 px.
- Compruebe la legibilidad del texto en todos los tamaños de pantalla admitidos.
- Confirme que la validación del formulario funciona de forma coherente en todos los dispositivos y exploradores.
- Asegúrese de que el tiempo de carga en el móvil sea inferior a 3 segundos.
- Compruebe que todos los elementos interactivos sean accesibles mediante el teclado y los lectores de pantalla.
- Pruebe el envío del formulario en todos los dispositivos compatibles.


+++

## Próximos pasos

**Acciones inmediatas:**

1. **Auditar los formularios actuales:** probar los formularios existentes mediante el emulador de dispositivos.
2. **Identificar ganancias rápidas:** corrija primero los problemas obvios de uso móvil.
3. **Priorizar los formularios de alto tráfico:** céntrese en los formularios que tengan el mayor impacto en el usuario.
4. **Implementar un enfoque que dé prioridad a los dispositivos móviles:** comience con el diseño de pantalla más pequeño.

**Optimización avanzada:**

- **Supervisión del rendimiento:** configure Analytics para controlar las métricas del formulario.
- **Pruebas A/B:** experimente con diferentes diseños y enfoques.
- **Recopilación de comentarios de usuarios:** recopile información de usuarios reales.
- **Mejora continua:** revise y optimice los formularios con regularidad.


