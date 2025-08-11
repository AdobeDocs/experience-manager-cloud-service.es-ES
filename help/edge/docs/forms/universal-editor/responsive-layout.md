---
title: Creación de Forms adaptable con editor universal
description: Aprenda a diseñar, probar y optimizar formularios adaptables para todos los dispositivos con el editor universal. Pruebas de dispositivos maestros, patrones de diseño y técnicas de optimización móvil para AEM Forms con Edge Delivery Services.
keywords: formularios adaptables, formularios móviles, prueba de dispositivos, editor universal, diseño adaptable, optimización de formularios, diseño móvil, diseño adaptable, diseños de formulario, emulador de dispositivos
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 0c7fb491-4bad-4202-a472-87e6e6d9ab40
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 1%

---


# Creación de Forms adaptable con editor universal

El panorama web moderno exige formularios que funcionen sin problemas en un espectro cada vez más amplio de dispositivos y tamaños de pantalla. Desde grandes monitores de escritorio hasta pantallas compactas para smartphones, los usuarios esperan experiencias consistentes e intuitivas independientemente del dispositivo que elijan. La creación de formularios adaptables ya no es opcional: es un requisito fundamental para ofrecer experiencias digitales profesionales, accesibles y optimizadas para la conversión.

Universal Editor proporciona herramientas y metodologías completas para desarrollar formularios adaptables que se adaptan de forma inteligente a varias dimensiones de pantalla, métodos de entrada y contextos de usuario. Esta guía explora los fundamentos técnicos, las estrategias de implementación y las técnicas de optimización necesarias para crear formularios que funcionen de forma excepcional en todos los dispositivos, al tiempo que mantienen la facilidad de uso, la accesibilidad y el atractivo visual.

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

El diseño del panel organiza el contenido relacionado en secciones visualmente distintas, lo que permite a los usuarios ver varias secciones a la vez. Este diseño es ideal para los formularios con información clasificada que se beneficia de una presentación simultánea en pantallas más grandes.

![Ejemplo de diseño de panel](/help/edge/docs/forms/universal-editor/assets/panel-layout.png)

**Comportamiento interactivo**

- **Escritorio (1200 px y superior):** paneles se muestran uno al lado del otro o en una cuadrícula para obtener la máxima visibilidad.
- **Tableta (768px-1199px):** Los paneles se apilan verticalmente con el espaciado adecuado para mantener la claridad.
- **Móvil (320px-767px):** Los paneles se presentan en un diseño de una sola columna, con una clara separación entre las secciones para facilitar la navegación.

**Cómo implementar**

1. Agregue el [componente Panel](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel) al formulario.
2. Agrupe los campos relacionados dentro de cada panel para mantener la organización lógica.
3. Asigne encabezados claros y descriptivos a cada sección del panel.
4. Asegúrese de que haya suficiente espacio entre los paneles para evitar el desorden visual.

**Prácticas recomendadas**

- Limite el número de paneles a 3 o 4 en el escritorio para evitar abrumar a los usuarios.
- Utilice títulos concisos y descriptivos para cada panel para ayudar a los usuarios a comprender mejor.
- Organice los campos dentro de los paneles de forma lógica para minimizar la carga cognitiva.
- Pruebe la navegación del panel en dispositivos táctiles para garantizar la facilidad de uso en todas las plataformas.

**Casos de uso comunes**

- **Solicitud de empleo:** secciones de información personal, educación, experiencia y referencias.
- **Registro del producto:** paneles para obtener detalles básicos, especificaciones técnicas e información sobre la garantía.
- **Forms de encuesta:** agrupaciones para datos demográficos, preferencias, comentarios e información de contacto.

### Diseño de asistente

El diseño del asistente guía a los usuarios a través de un proceso de varios pasos, presentando una sección a la vez. Este diseño es especialmente eficaz para formularios complejos, ya que reduce la carga cognitiva y aumenta las tasas de finalización al dividir el proceso en pasos manejables.

![Ejemplo de diseño del asistente](/help/edge/docs/forms/universal-editor/assets/wizard-layout.png)

**Comportamiento interactivo**

- **Todos los dispositivos:** Mantiene un enfoque de un solo paso, lo cual es óptimo para los usuarios móviles.
- **Contenido del paso:** Cada paso se adapta de forma responsable, apilando campos u organizándolos uno al lado del otro según corresponda para el tamaño de pantalla.
- **Navegación:** Incluye botones táctiles con un espaciado adecuado para facilitar la interacción.
- **Indicador de progreso:** Las barras de progreso o los indicadores de paso se escalan correctamente para diferentes dispositivos, lo que proporciona información clara sobre el estado de finalización.

**Cómo implementar**

1. Inserte el [componente Asistente](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard) en el formulario.
2. Divida el formulario en pasos lógicos, idealmente entre 3 y 7, para mantener cada paso centrado y manejable.
3. Añada indicadores de progreso para ayudar a los usuarios a comprender su posición en el proceso.
4. Proporciona controles de navegación claros, como los botones Siguiente, Atrás y Guardar.

**Consejos de optimización móvil**

- Utilice destinos táctiles grandes (al menos 44 píxeles de altura) para los controles de navegación a fin de mejorar la accesibilidad.
- Asegúrese de que los indicadores de paso sean visibles y legibles en las pantallas pequeñas.
- Limite el número de campos por paso para minimizar el desplazamiento y mejorar el enfoque.
- Habilite la funcionalidad de guardado automático para evitar la pérdida de datos si los usuarios abandonan el formulario.

**Prácticas recomendadas**

- Diseñe pasos para seguir una progresión lógica, con cada paso basándose en el anterior.
- Utilice títulos claros y descriptivos para cada paso a fin de establecer las expectativas del usuario.
- Valide los datos introducidos por el usuario en cada paso para detectar los errores de forma temprana y reducir la frustración.
- Permite a los usuarios retroceder para revisar o editar la información anterior sin perder datos.

**Casos de uso comunes**

- **Reclamos de seguro:** pasos para obtener detalles del incidente, envío de pruebas, información personal y revisión.
- **Configuración de cuenta:** fases para obtener información básica, preferencias, configuración de seguridad y confirmación.
- **Proceso de pedido:** Pasos para la selección de productos, la información de envío, los detalles de pago y el resumen del pedido.

### Diseño de acordeón

El diseño de acordeón ahorra espacio al organizar el contenido en secciones contraíbles, lo que lo hace ideal para información opcional o secundaria. Esta presentación es especialmente eficaz para los formularios con contenido que se puede agrupar lógicamente y no necesita mostrarse todo a la vez.

![Ejemplo de diseño de acordeón](/help/edge/docs/forms/universal-editor/assets/accordion-layout.png)

**Comportamiento interactivo**

- **Rendimiento móvil:** Solo se expande la sección relevante, lo que reduce la necesidad de desplazarse y mejora los tiempos de carga.
- **Encabezados táctiles optimizados:** Los encabezados de sección son fáciles de tocar y expandir y admiten gestos naturales en dispositivos móviles.
- **Animaciones suaves:** Las secciones de expansión y contracción proporcionan comentarios visuales sobre las interacciones del usuario.
- **Eficiencia de espacio:** Las secciones contraídas minimizan el espacio vertical, lo que facilita la navegación del formulario en todos los dispositivos.

**Cómo implementar**

1. Agregue el [componente Acordeón](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion) al formulario.
2. Agrupar contenido opcional o secundario relacionado dentro de cada sección de acordeón.
3. Utilice encabezados claros y descriptivos para cada sección a fin de ayudar a los usuarios a comprender qué información incluye.
4. Establezca los estados predeterminados adecuados de apertura o cierre para cada sección en función de la importancia y las necesidades del usuario.

**Ventajas móviles**

- Reduce el desplazamiento al contraer las secciones no utilizadas, lo que permite a los usuarios centrarse en una sección a la vez.
- La interacción táctil admite gestos de expansión/contracción naturales.
- Carga más rápida, ya que solo está visible el contenido activo.
- Se ha mejorado el enfoque, ya que los usuarios solo ven la información que necesitan en un momento determinado.

**Prácticas recomendadas**

- Utilice encabezados de sección claros para que los usuarios sepan qué esperar antes de expandir una sección.
- Agrupe el contenido relacionado lógicamente dentro de cada sección para ayudar a la comprensión.
- Establecer secciones importantes para que comiencen a expandirse si se requiere atención inmediata.
- Proporcione resúmenes o vistas previas de secciones breves para ayudar a los usuarios a decidir qué secciones expandir.

**Casos de uso comunes**

- **Configuración del producto:** secciones para Opciones básicas, Configuración avanzada, Accesorios y Soporte técnico.
- **Preguntas más frecuentes sobre Forms:** agrupaciones para preguntas de cuenta, facturación, técnicas y generales.
- **Configuración Forms:** secciones para Privacidad, Notificaciones, Apariencia y Opciones avanzadas.


## Parte 3: Prácticas recomendadas de diseño interactivo

### Prácticas recomendadas por tipo de dispositivo

+++Optimización móvil (320px-767px)

**Diseño e interacción:**

- Utilice un diseño de una sola columna para todo el contenido del formulario para maximizar la legibilidad y facilidad de uso.
- Asegúrese de que todos los botones y elementos interactivos tengan al menos 44 píxeles de altura para una interacción táctil fiable.
- Proporciona una navegación clara y sencilla con botones visibles atrás y siguiente.
- Minimice la necesidad de desplazarse dentro de cada sección separando los formularios largos.
- Céntrese automáticamente en el primer campo de entrada para preguntar al teclado móvil.

**Directrices de campo:**

- Los campos de texto deben abarcar el ancho completo de la pantalla con suficiente relleno para la entrada táctil.
- Utilice elementos nativos de lista desplegable/selección para una óptima facilidad de uso móvil.
- Implemente selectores de fechas nativos para obtener una experiencia móvil coherente.
- Ampliar las áreas de carga de archivos y etiquetarlas con claridad para facilitar el acceso.

+++

+++Optimización de tableta (768px-1199px)

**Diseño y uso:**

- Utilice diseños de dos columnas para campos relacionados para aprovechar el mayor espacio en pantalla.
- Pruebe el aspecto y la facilidad de uso del formulario en orientación vertical y horizontal.
- Diseñe tanto para la entrada táctil como para la del ratón, lo que garantiza que todos los controles sean fácilmente accesibles.
- Aumente el tamaño del área de contenido al tiempo que mantiene una jerarquía visual y una legibilidad claras.

+++

+++Optimización de sobremesas (1200 px+)

**Características avanzadas y diseño:**

- Utilice diseños de varias columnas para utilizar de forma eficaz el espacio horizontal y reducir el desplazamiento vertical.
- Proporcione métodos abreviados del teclado para realizar acciones frecuentes con el fin de admitir usuarios avanzados.
- Implementar estados de desplazamiento y comentarios visuales para elementos interactivos.
- Ofrezca validación avanzada con mensajes de error claros y detallados para formularios complejos.

+++

## Resolución de problemas

### Problemas de diseño

+++Saltos de diseño de formulario en dispositivos móviles

**Causas posibles:**

- Elementos de ancho fijo que no se adaptan a pantallas más pequeñas
- CSS con prioridad de escritorio que anula los estilos móviles
- Las imágenes o el contenido desbordan sus contenedores

**Corrección:**

- Asegúrese de que todas las imágenes y contenedores utilizan un tamaño relativo o basado en porcentajes.
- Comience con un enfoque CSS basado en dispositivos móviles y cree capas de mejoras para pantallas más grandes.
- Pruebe formularios utilizando emuladores de dispositivos y dispositivos reales.
- Evite las dimensiones fijas; utilice diseños flexibles.

+++

+++Tocar destinos demasiado pequeños

**Causas posibles:**

- Botones o vínculos de menos de 44 por 44 píxeles
- Elementos interactivos colocados demasiado juntos
- CSS personalizado que reduce el tamaño de destino táctil predeterminado

**Corrección:**

- Asegúrese de que cada elemento interactivo tenga al menos 44 por 44 píxeles.
- Agregue el espaciado adecuado entre botones, vínculos y otros controles.
- Pruebe con dispositivos táctiles reales, no solo con un ratón.
- Expanda las áreas de destino táctiles según sea necesario para la accesibilidad.

+++

+++Problemas de desbordamiento de contenido

**Causas posibles:**

- Texto largo o etiquetas que no se ajustan
- Contenedores con anchuras fijas
- Imágenes que no se escalan de forma responsable

**Corrección:**

- Habilite el ajuste de texto para todas las etiquetas y el contenido.
- Utilice imágenes adaptables que se escalen con el contenedor.
- Diseñe diseños flexibles que se adapten a distintas longitudes de contenido.
- Realice pruebas con contenido corto y largo para garantizar la adaptabilidad.

+++

### Problemas de rendimiento

+++Carga lenta en dispositivos móviles

**Causas posibles:**

- Imágenes grandes sin optimizar
- JavaScript pesado o excesivo
- Demasiados campos de formulario cargándose simultáneamente

**Corrección:**

- Optimice las imágenes para dispositivos móviles y utilice los formatos de archivo adecuados.
- Aplazar o cargar de forma diferida contenido no crítico.
- Minimice el uso de scripts y widgets de terceros.
- Optimice los campos de formulario para cargar solo lo necesario.

+++

### Problemas de prueba y validación

+++Diferencias entre emulador y dispositivo real

**Causas posibles:**

- Diferencias en los motores de renderización del explorador
- Interacción táctil no simulada con precisión con el ratón
- Discrepancias de velocidad de red

**Corrección:**

- Realice pruebas siempre en dispositivos reales, además de en emuladores.
- Utilice varios exploradores y dispositivos para realizar pruebas exhaustivas.
- Simule varias velocidades de red para identificar cuellos de botella de rendimiento.
- Recopile comentarios de usuarios reales en la audiencia de destino.

+++

## Métricas de éxito para Forms interactivo

+++Indicadores clave de rendimiento

**Experiencia del usuario:**

- **Tasa de finalización de formularios:** El objetivo es alcanzar el 85 % o más en dispositivos móviles.
- **Tiempo para completar:** Los usuarios de dispositivos móviles deben completar los formularios en un plazo del 20 % de las horas de finalización del escritorio.
- **Tasa de error:** Mantener los errores de validación por debajo del 5%.
- **Puntos de abandono:** identifique y solucione los pasos en los que los usuarios abandonan el sitio.

**Rendimiento técnico:**

- **Tiempo de carga de página:** Menos de 3 segundos en una conexión 3G.
- **Elementos Web básicos:** Cumplen o sobrepasan los umbrales recomendados por Google.
- **Accesibilidad:** Consiga el cumplimiento de WCAG 2.1 AA.
- **Compatibilidad de exploradores:** Garantice una funcionalidad superior al 98 % en todos los exploradores principales.

+++

+++Lista de comprobación de pruebas

**Lista de comprobación previa a la publicación:**

- Pruebe el formulario en dispositivos móviles reales (no solo en emuladores).
- Asegúrese de que todos los objetivos táctiles tengan al menos 44 × 44 píxeles.
- Compruebe la legibilidad del texto en todos los tamaños de pantalla admitidos.
- Confirme que la validación del formulario funciona de forma coherente en todos los dispositivos y exploradores.
- Asegúrese de que el tiempo de carga del móvil sea inferior a 3 segundos.
- Compruebe que todos los elementos interactivos sean accesibles mediante el teclado y los lectores de pantalla.
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


