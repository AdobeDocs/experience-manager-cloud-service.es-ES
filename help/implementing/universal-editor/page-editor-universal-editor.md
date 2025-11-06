---
title: Editor de páginas y editor universal
description: El editor de páginas sigue siendo compatible con Adobe, pero el editor universal ofrece posibilidades interesantes para sus nuevos proyectos.
feature: Developing
role: Admin, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 100%

---

# Editor de páginas y editor universal {#page-editor-universal-editor}

El editor de páginas sigue siendo compatible con Adobe, pero el editor universal ofrece posibilidades interesantes para sus nuevos proyectos.

## Información general {#background}

Adobe presentó el [editor universal](/help/implementing/universal-editor/introduction.md) en 2024 como un editor optimizado que adopta un enfoque de desarrollo moderno basado en JavaScript. El editor universal es la visión de Adobe de una experiencia de creación de contenido visual fluida y ampliable.

Consciente del rico conjunto de funciones del [editor de páginas](/help/sites-cloud/authoring/page-editor/introduction.md) y de los innumerables proyectos que han invertido en él a lo largo de la extensa historia de AEM, Adobe sigue siendo totalmente compatible con el editor de páginas, aunque la innovación se centrará en el editor universal.

## Recomendación {#recommendation}

Aunque se está reduciendo con rapidez, sigue existiendo una diferencia en cuanto a funciones entre el editor universal y el editor de páginas ([se puede encontrar una comparación de funciones en la siguiente sección](#feature-comparison)).

Como regla general:

* **Los nuevos proyectos** deben aprovechar de forma predeterminada el editor universal.
* **Los proyectos existentes** deben seguir usando el editor de páginas y tener en cuenta el editor universal al emprender iniciativas de Edge Delivery o headless.

**El editor que elija debe estar totalmente determinado por las necesidades de cada proyecto.**

## Comparación de funciones {#feature-comparison}

Debido a que la diferencia entre las funciones de los dos editores se está reduciendo de forma constante, asegúrese de consultar las [notas de la versión del editor universal](/help/release-notes/universal-editor/current.md) para conocer los últimos desarrollos.

### Entrega {#delivery}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| [Entrega de publicación](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponible]{type=Positive} | Se recomienda su uso con los componentes principales y los proyectos AEM tradicionales | [!BADGE No disponible]{type=Negative} | Las páginas tradicionales de AEM suelen depender de varias funciones específicas del editor de páginas que son difíciles de replicar tal cual con el editor universal. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} |  |
| [Envío headless](/help/headless/introduction.md) | [!BADGE Disponible parcialmente]{type=Caution} | Solo con [el editor de SPA,](/help/implementing/developing/hybrid/introduction.md) que estaba [obsoleto](/help/implementing/developing/hybrid/spa-editor-deprecation.md) a favor del editor universal | [!BADGE Disponible]{type=Positive} | El editor universal permite a los desarrolladores traer su propia aplicación web sin imponer requisitos de marco de trabajo específicos ni restricciones de implementación. |

### Persistencia {#persistence}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Edición de componentes de página | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Edición de [fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | Incluidas la inserción y reordenación de fragmentos |

### Capacidades {#capabilities}

|  | Editor de páginas | Notas | Editor universal | Notas |
|---|---|---|---|---|
| Plantillas de página | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | El editor universal es independiente del sistema de plantillas utilizado. Sin embargo, el patrón de implementación típico favorece las plantillas definidas por el desarrollador, ya que las herramientas modernas de front-end facilitan en gran medida a los desarrolladores la definición y el mantenimiento de la lógica de plantilla directamente en el código. |
| Edición WYSIWYG | [!BADGE Disponible]{type=Positive} | Limitado a las páginas | [!BADGE Disponible]{type=Positive} | Admite páginas y fragmentos de contenido |
| [Generar variaciones](/help/generative-ai/generate-variations.md) | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | [Disponible como extensión](/help/implementing/universal-editor/extending.md) |
| Insertar nuevo bloque | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Reordenar bloque | [!BADGE Disponible]{type=Positive} | Es posible con arrastrar y soltar en contexto, pero no en el panel lateral de “vista de árbol” | [!BADGE Disponible]{type=Positive} | Es posible mediante arrastrar y soltar en el panel lateral de “vista de árbol”, pero aún no en contexto (planeado) |
| Cortar/copiar-pegar bloque | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Aplicar estilos | [!BADGE Disponible]{type=Positive} | Los estilos se pueden aplicar a los componentes mediante [el sistema de estilos.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponible]{type=Positive} | Los estilos se pueden aplicar mediante propiedades de componente normal (o fragmento de contenido). El mismo selector de estilo no está disponible en el editor universal, pero con un widget de selección múltiple se puede lograr una UX muy similar. |
| Aplicar diseño | [!BADGE Disponible]{type=Positive} | Los sitios deben implementar la [cuadrícula adaptable de AEM](/help/implementing/developing/introduction/responsive-design.md) para permitir a los autores cambiar el tamaño de los componentes en tres puntos de interrupción predefinidos. | [!BADGE Disponible]{type=Positive} | Los diseños se pueden aplicar mediante propiedades de componente normales (o fragmento de contenido), pero la cuadrícula adaptable no es compatible. |
| Deshacer-Rehacer | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| Publicar (también en vista previa) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Iniciar flujo de trabajo](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión |
| Comentarios | [!BADGE Disponible]{type=Positive} | Uso de [anotaciones](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE No disponible]{type=Negative} | Planeado |
| Integración de Workfront | [!BADGE No disponible]{type=Negative} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión |
| [MSM y lanzamientos](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible para páginas como extensión |
| Experimentación y personalización | [!BADGE Disponible]{type=Positive} | Uso del [modo de destino](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponible]{type=Positive} | Disponible como extensión para Edge Delivery Services |
| Árbol de contenido | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | También permite la reordenación dentro del árbol |
| Simulación de dispositivo | [!BADGE Disponible]{type=Positive} | [Los dispositivos configurados se pueden simular,](/help/sites-cloud/administering/responsive-layout.md) pero el usuario no puede introducir manualmente ninguna dimensión de pantalla diferente para simular. | [!BADGE Disponible]{type=Positive} | [Se pueden especificar manualmente todas las dimensiones de pantalla que se van a simular,](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator) pero no se pueden configurar los puntos de interrupción predeterminados. |
| [Bloqueo de páginas](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Respeta el estado de bloqueo establecido en la consola de Sites con la extensión disponible para bloquear/desbloquear páginas desde el editor |
| [Propiedades de página](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible desde el administrador del sitio, con extensión para acceder también a las propiedades de las páginas desde el editor |
| Propiedades de varios campos | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Versiones de página](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} |  |
| [Deformación de tiempo](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) y [Vista de diferencia](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Planeado |
| Ver en administración | [!BADGE Disponible]{type=Positive} |  | [!BADGE Disponible]{type=Positive} | Disponible como extensión para páginas |
| Ver estado de la página | [!BADGE Disponible]{type=Positive} |  | [!BADGE No disponible]{type=Negative} | Disponible en la consola de Sites |
| Extensibilidad | [!BADGE Disponible]{type=Positive} | Como superposiciones de AEM | [!BADGE Disponible]{type=Positive} | Como puntos de extensión claramente definidos, utilizando App Builder y muy pocos conocimientos específicos de AEM |

## Adopción del editor universal {#adopt-ue}

El editor universal ofrece muchas ventajas, lo que lo convierte en una gran solución para nuevos proyectos.

* **Edición visual:** al igual que para el editor de páginas, los autores pueden editar contenido directamente dentro de la vista previa y ver al instante cómo sus cambios afectan la experiencia del visitante.
* **Preparación para el futuro:** la hoja de ruta de AEM da prioridad al editor universal como editor visual. Su adopción garantiza el acceso a las últimas innovaciones y mejoras.
* **Integración más sencilla:** no se requiere un SDK específico de AEM para usar el editor universal, lo que reduce el bloqueo de la pila tecnológica.
* **Traer su propia aplicación:** el editor universal admite cualquier marco web o arquitectura, lo que permite la adopción sin requerir una refactorización compleja.
* **Extensibilidad:** el editor universal se beneficia de un [marco de extensión](/help/implementing/universal-editor/extending.md) sólido, que incluye integraciones con GenAI, Workfront y más.

### Migración al editor universal {#migrate-ue}

No hay una ruta de migración directa del editor de páginas al editor universal. Esto se debe a diferencias fundamentales entre las dos tecnologías.

* El editor universal no vuelve a introducir funciones como el editor de plantillas, el sistema de estilos o la cuadrícula adaptable.
   * Estos casos de uso ahora se pueden administrar de forma más eficaz con front-end ligero CSS y JavaScript en proyectos de Edge Delivery Services o headless.
* Dado que el editor universal es un editor como servicio, no puede permitir a los implementadores insertar CSS o JS en los cuadros de diálogo de componentes.
   * De este modo, evita la conversión automática de los cuadros de diálogo de componentes desde el editor de páginas.
   * Esto afecta a muchas áreas de los cuadros de diálogo, como widgets personalizados, validación de campos, reglas de mostrar/ocultar y personalizaciones basadas en plantillas.
      * Aunque estas capacidades siguen siendo posibles, el editor universal las resuelve mediante la configuración, en lugar de utilizar JavaScript personalizado implementado en los cuadros de diálogo.

Aunque técnicamente el editor universal puede habilitar la edición de páginas para proyectos AEM tradicionales (p. ej., creados con los componentes principales), estos sitios suelen depender de varias funciones específicas del editor de páginas, como el sistema de estilos, la cuadrícula adaptable, las plantillas editables y JavaScript personalizado dentro de los cuadros de diálogo.

Dado que el editor universal sigue un enfoque más simplificado y moderno que no admite estas funciones heredadas, la migración de estos sitios requeriría una refactorización significativa. Por este motivo, la **migración de sitios del editor de páginas al editor universal solo se recomienda para proyectos en transición a Edge Delivery Services.**
