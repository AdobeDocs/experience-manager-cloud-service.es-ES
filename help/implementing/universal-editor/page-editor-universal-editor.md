---
title: Editor de páginas y editor universal
description: El editor de páginas sigue siendo compatible con Adobe, pero el editor universal ofrece posibilidades interesantes para sus nuevos proyectos.
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 3%

---

# Editor de páginas y editor universal {#page-editor-universal-editor}

El editor de páginas sigue siendo compatible con Adobe, pero el editor universal ofrece posibilidades interesantes para sus nuevos proyectos.

## Fondo {#background}

Adobe presentó [Universal Editor](/help/implementing/universal-editor/introduction.md) en 2024 como un editor optimizado que adopta un enfoque de desarrollo moderno basado en Javascript. El editor universal es la visión de Adobe para una experiencia de creación de contenido visual fluida y ampliable.

Consciente del conjunto de funciones enriquecidas del [Editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) y de los innumerables proyectos que han invertido en él a lo largo de la larga historia de AEM, Adobe sigue siendo totalmente compatible con el Editor de páginas, aunque la innovación se centrará en el Editor universal.

## Recomendación {#recommendation}

Aunque se está reduciendo rápidamente, sigue habiendo un espacio entre las características Editor universal y Editor de página ([se puede encontrar una comparación de características en la siguiente sección](#feature-comparison)).

Como regla general:

* **Los nuevos proyectos** deben aprovechar de forma predeterminada el Editor universal.
* **Los proyectos existentes** deben seguir usando el Editor de páginas y tener en cuenta el Editor universal al iniciar esfuerzos de Edge Delivery o sin encabezado.

**El editor que elija debe estar totalmente determinado por las necesidades de cada proyecto.**

## Comparación de funciones {#feature-comparison}

Debido a que la brecha entre las características de los dos editores se está reduciendo constantemente, asegúrese de consultar las [notas de la versión del editor universal](/help/release-notes/universal-editor/current.md) para conocer los últimos desarrollos.

### Entrega {#delivery}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| [Entrega de publicación](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponible]{type=Positive} | Se recomienda su uso con los componentes principales y los proyectos tradicionales de AEM | [!BADGE No disponible]{type=Negative} | Las páginas tradicionales de AEM suelen depender de varias funciones específicas del editor de páginas que son difíciles de replicar tal cual con el editor universal. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} |  |
| [Envío sin encabezado](/help/headless/introduction.md) | [!BADGE Disponible parcialmente]{type=Caution} | Solo con [el Editor de SPA,](/help/implementing/developing/hybrid/introduction.md) que estaba [obsoleto](/help/implementing/developing/hybrid/spa-editor-deprecation.md) a favor del Editor universal | [!BADGE Disponible]{type=Positive} | El editor universal permite a los desarrolladores traer su propia aplicación web sin imponer requisitos de marco de trabajo específicos ni restricciones de implementación. |

### Persistencia {#persistence}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Edición de componentes de página | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Editando [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | Incluir la inserción y reordenación de fragmentos |

### Capacidades {#capabilities}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Plantillas de página | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | El editor universal no es independiente del sistema de plantillas utilizado. Sin embargo, el patrón de implementación típico favorece las plantillas definidas por el desarrollador, ya que las herramientas modernas de front-end facilitan en gran medida a los desarrolladores la definición y el mantenimiento de la lógica de plantilla directamente en el código. |
| Edición en WYSIWYG | [!BADGE Disponible]{type=Positive} | Limitado a páginas | [!BADGE Disponible]{type=Positive} | Páginas de soporte y fragmentos de contenido |
| [Generar variaciones](/help/generative-ai/generate-variations.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | [Disponible como extensión](/help/implementing/universal-editor/extending.md) |
| Insertar nuevo bloque | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Reordenar bloque | [!BADGE Disponible]{type=Positive} | Es posible con arrastrar y soltar en contexto, pero no en el panel lateral &quot;vista de árbol&quot; | [!BADGE Disponible]{type=Positive} | Posible mediante arrastrar y soltar en el panel lateral &quot;vista de árbol&quot;, pero aún no en contexto (planificado) |
| Cortar/copiar-pegar bloque | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| Aplicar estilos | [!BADGE Disponible]{type=Positive} | Los estilos se pueden aplicar a los componentes mediante [el sistema de estilos.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponible]{type=Positive} | Los estilos se pueden aplicar mediante propiedades de componente normal (o fragmento de contenido). El mismo selector de estilo no está disponible en el editor universal, pero con un widget de selección múltiple se puede lograr un UX muy similar. |
| Aplicar diseño | [!BADGE Disponible]{type=Positive} | Los sitios deben implementar [AEM Responsive Grid](/help/implementing/developing/introduction/responsive-design.md) para permitir a los autores cambiar el tamaño de los componentes en tres puntos de interrupción predefinidos. | [!BADGE Disponible]{type=Positive} | Los diseños se pueden aplicar mediante propiedades de componente normales (o fragmento de contenido), pero la cuadrícula adaptable no es compatible. |
| Deshacer-Rehacer | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| Publicar (también para previsualizar) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Iniciar flujo de trabajo](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión |
| Comentario | [!BADGE Disponible]{type=Positive} | Usando [anotaciones](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE No disponible]{type=Negative} | Planeado |
| Integración de Workfront | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión |
| [MSM e inicios](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible para páginas como extensión |
| Experimentación y personalización | [!BADGE Disponible]{type=Positive} | Usando [modo de destino](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponible]{type=Positive} | Disponible como extensión para Edge Delivery Services |
| Árbol de contenido | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | También permite la reordenación dentro del árbol |
| Simulación de dispositivo | [!BADGE Disponible]{type=Positive} | [Los dispositivos configurados se pueden simular,](/help/sites-cloud/administering/responsive-layout.md) pero el usuario no puede introducir manualmente ninguna dimensión de pantalla diferente para simular. | [!BADGE Disponible]{type=Positive} | [Se pueden especificar manualmente todas las dimensiones de pantalla que se van a simular,](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator) pero no se pueden configurar los puntos de interrupción predeterminados. |
| [Bloqueo de páginas](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Respeta el estado de bloqueo establecido en la consola Sitios con la extensión disponible para bloquear/desbloquear páginas desde el editor |
| [Propiedades de página](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible desde el Administrador del sitio, con extensión para acceder también a las propiedades de las páginas desde el editor |
| Propiedades de varios campos | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Control de versiones de página](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Deformación de tiempo](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) y [Vista de diferencia](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| Ver en administración | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión para páginas |
| Ver estado de la página | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Disponible en la consola Sitios |
| Extensibilidad | [!BADGE Disponible]{type=Positive} | Como superposiciones de AEM | [!BADGE Disponible]{type=Positive} | Como puntos de extensión claramente definidos, utilizando App Builder y muy pocos conocimientos específicos de AEM. |

## Adopción del editor universal {#adopt-ue}

El editor universal ofrece muchas ventajas, lo que lo convierte en una gran solución para nuevos proyectos.

* **Edición visual:** Al igual que para el Editor de páginas, los autores pueden editar contenido directamente dentro de la vista previa y ver al instante cómo sus cambios afectan la experiencia del visitante.
* **Revisión para el futuro:** La hoja de ruta de AEM da prioridad al Editor universal como editor visual. Su adopción garantiza el acceso a las últimas innovaciones y mejoras.
* **Integración más sencilla:** No se requiere SDK específico de AEM para usar el Editor universal, lo que reduce el bloqueo de pila tecnológica.
* **Traer su propia aplicación:** El editor universal admite cualquier marco web o arquitectura, lo que permite la adopción sin requerir una refactorización compleja.
* **Extensibilidad:** El editor universal se beneficia de un marco de trabajo de [extensión sólido,](/help/implementing/universal-editor/extending.md) que incluye integraciones con GenAI, Workfront y más.

### Migración al editor universal {#migrate-ue}

No hay una ruta de migración directa del Editor de páginas al Editor universal. Esto se debe a diferencias fundamentales entre las dos tecnologías.

* El editor universal no vuelve a introducir funciones como el editor de plantillas, el sistema de estilos o la cuadrícula interactiva.
   * Estos casos de uso ahora se pueden administrar de forma más eficaz con CSS de front-end ligero y Javascript en proyectos Edge Delivery Services o sin encabezado.
* Dado que el editor universal es un editor como servicio, no puede permitir a los implementadores insertar CSS o JS en los cuadros de diálogo de componentes.
   * Esto evita la conversión automática de los cuadros de diálogo de componentes desde el Editor de páginas.
   * Esto afecta a muchas áreas de los cuadros de diálogo, como widgets personalizados, validación de campos, reglas de mostrar/ocultar y personalizaciones basadas en plantillas.
      * Aunque estas funcionalidades aún son posibles, el Editor universal las resuelve mediante la configuración de, en lugar de implementar el JavaScript personalizado en los cuadros de diálogo.

Aunque técnicamente el editor universal puede habilitar la edición de páginas para proyectos tradicionales de AEM (por ejemplo, creados con los componentes principales), estos sitios suelen depender de varias funciones específicas del editor de páginas, como el sistema de estilos, la cuadrícula interactiva, las plantillas editables y el Javascript personalizado dentro de los cuadros de diálogo.

Dado que el editor universal sigue un enfoque más simplificado y moderno que no admite estas funciones heredadas, la migración de estos sitios requeriría una refactorización significativa. Por este motivo, la migración de **sitios del editor de páginas al editor universal solo se recomienda para proyectos en transición a Edge Delivery Services.**
