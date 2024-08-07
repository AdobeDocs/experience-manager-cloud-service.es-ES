---
title: Tablero de auditoría de experiencias
description: Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO a través de una interfaz de panel clara e informativa.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c7362a77fd929d812db3cd40bf01763ed3bef02c
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 7%

---


# Tablero de auditoría de experiencias {#experience-audit-dashboard}

Descubra cómo la auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO a través de una interfaz de panel clara e informativa.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para [el programa de clientes pioneros.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)
>
>Para obtener más información sobre la característica de auditoría de experiencias de AEM as a Cloud Service, consulte el documento [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md)

## Información general {#overview}

La auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que los cambios implementados:

1. Cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas, la SEO (optimización de motores de búsqueda) y la PWA (aplicación web progresiva).

1. No introduzcan regresiones.

La auditoría de experiencias en Cloud Manager garantiza que la experiencia del usuario en el sitio sea de los más altos estándares.

Los resultados de la auditoría son informativos y permiten al administrador de implementación ver las puntuaciones y el cambio entre las puntuaciones actuales y anteriores. Esta perspectiva es importante para determinar si hay una regresión que se haya introducido con la implementación actual.

La auditoría de experiencias está equipada con [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), una herramienta de código abierto de Google, y está habilitada en todas las canalizaciones de producción de Cloud Manager.

## Disponibilidad {#availability}

La auditoría de experiencias está disponible para Cloud Manager:

* Canalizaciones de producción de Sites, de forma predeterminada
* Desarrollo de canalizaciones de pila completa, opcionalmente
* Desarrollo de canalizaciones front-end, opcional

Consulte la [sección Configuración](#configuration) para obtener más información sobre cómo configurar la auditoría para los entornos opcionales.

Las auditorías se ejecutan como parte de la canalización. Las auditorías también pueden [ejecutarse bajo demanda](#on-demand) fuera de las canalizaciones.

## Configuración {#configuration}

La auditoría de experiencias está disponible de forma predeterminada para las canalizaciones de producción. Se puede habilitar, opcionalmente, para el desarrollo de canalizaciones full-stack y front-end. En todos los casos, debe definir qué rutas de contenido se evalúan durante la ejecución de la canalización.

1. Según el tipo de canalización que desee configurar, siga las instrucciones para:

   * Agregue una nueva [canalización de producción,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) si desea definir las rutas que evaluará la auditoría.
   * Agregue una nueva canalización [que no sea de producción,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) si desea habilitar la auditoría en una canalización front-end o de desarrollo de pila completa.
   * O puede [editar una canalización existente,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) y actualizar las opciones existentes.

1. Si está agregando o editando una canalización que no es de producción para la que desea usar la auditoría de experiencias, debe seleccionar la casilla de verificación **Auditoría de experiencias** en la pestaña **Código Source**.

   ![Habilitando auditoría de experiencias](assets/experience-audit-enable.jpg)

   * Esto solo es necesario para canalizaciones que no sean de producción.
   * La ficha **Auditoría de experiencias** aparece cuando se selecciona la casilla de verificación.

1. Tanto para las canalizaciones de producción como para las que no son de producción, usted define las rutas que deben incluirse en la auditoría de experiencias en la pestaña **Auditoría de experiencias**.

   * Las rutas de acceso a la página deben comenzar por `/` y son relativas al sitio.
   * Por ejemplo, si el sitio es `wknd.site` y desea incluir a `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, escriba la ruta de acceso `/us/en/about-us.html`.

   ![Definición de una ruta para la auditoría de experiencias](assets/experience-audit-add-page.png)

1. Pulse o haga clic en **Agregar página**, y la ruta se completará automáticamente con la dirección de su entorno y se agregará a la tabla de rutas.

   ![Guardar ruta de acceso a la tabla](assets/experience-audit-page-added.png)

1. Siga agregando rutas según sea necesario repitiendo los dos pasos anteriores.

   * Puede agregar un máximo de 25 rutas.
   * Si no define una ruta, la página principal del sitio se incluye en la auditoría de experiencias de forma predeterminada.

1. Haga clic en **Guardar** para guardar la canalización.

## Resultados de auditoría de experiencias {#results}

Los resultados de la auditoría de experiencias se presentan en la fase **Prueba de fase** de la canalización de producción a través de la página [ejecución de la canalización de producción](/help/implementing/cloud-manager/deploy-code.md).

![Panel en la canalización](assets/experience-audit-dashboard.jpg)

La auditoría de experiencias proporciona la mediana de las puntuaciones de Google Lighthouse para las [páginas configuradas](#configuration) y la diferencia de puntuación con respecto al análisis anterior.

Desde esta vista de resumen en la fase **Prueba de ensayo** de la canalización, tiene dos opciones:

* **[Ver las páginas más lentas](#view-slowest-pages)**
* **[Ver informe completo](#view-full-report)**

Además del resumen presentado en los detalles de la ejecución de una canalización, también puede acceder directamente a los resultados completos de la auditoría utilizando la pestaña **Informes** del panel de Cloud Manager para acceder directamente a [el informe completo](#view-full-report).

>[!TIP]
>
>Las secciones siguientes describen cómo ver los resultados de la auditoría de experiencias.
>
>* Si desea obtener detalles sobre cómo funciona la auditoría, consulte la sección [Detalles de evaluación de auditoría de experiencias.](#details)
>* Si desea saber cómo ejecutar una auditoría de experiencias bajo demanda, consulte la sección [Informes de auditoría bajo demanda.](#on-demand)
>* Si tiene problemas con la auditoría, consulte la sección [Problemas de contadores de auditoría de experiencias.](#issues)
>* Para obtener sugerencias generales de rendimiento, consulte la sección [Sugerencias generales de rendimiento.](#performance-tips)

### Ver páginas más lentas {#view-slowest-pages}

Al tocar o hacer clic en **Ver páginas más lentas**, se abre el cuadro de diálogo **Más lentas 5 páginas**, que muestra las cinco páginas de menor rendimiento que [configuró para auditar.](#configuration)

![Cinco más lentos](assets/experience-audit-slowest-five.png)

Las puntuaciones se desglosan por **Rendimiento**, **Accesibilidad**, **Prácticas recomendadas** y **SEO**, junto con la desviación de cada métrica de la última auditoría.

De forma predeterminada, el cuadro de diálogo se abre con las puntuaciones de los dispositivos móviles. Puede cambiar esto a puntuaciones de escritorio usando el conmutador **Dispositivos** en la parte superior del cuadro de diálogo.

El cuadro de diálogo está diseñado para una descripción general rápida. Para obtener información detallada, pulsa o haz clic en **Ver informe completo**.

### Ver informe completo {#view-full-report}

Para ver el informe completo de auditoría de experiencias, haga lo siguiente:

* Tocando o haciendo clic en **Ver informe completo** en el cuadro de diálogo **[Más lento: 5 páginas](#view-slowest-pages)**.
* Tocando o haciendo clic en **Ver informe completo** al ver la [ejecución de una canalización.](#results)
* Toque o haga clic en la ficha **Informes** en Cloud Manager.

Se abre la pestaña **Informes** de Cloud Manager, donde se muestra **Auditoría de experiencias**.

![Informes de auditoría de experiencias](assets/experience-audit-reports.png)

El informe se divide en dos áreas:

* **[Puntuaciones de página - tendencia](#trend)**
* **[Resultados del análisis de auditoría de experiencias](#results)**

#### Puntuaciones de la página de Lighthouse: tendencia {#trend}

De manera predeterminada, la vista seleccionada para **puntuaciones de página - tendencia** es **puntuaciones medias** para los **últimos 6 meses**.

Utilice los menús desplegables **Seleccionar** y **Ver** de la parte superior e inferior del botón del gráfico para seleccionar detalles específicos de la página y diferentes lapsos de tiempo, respectivamente. Pulse o haga clic en y en el botón **actualizar tendencia** de la parte superior del gráfico para aplicar las selecciones y actualizar el gráfico.

Al mover el ratón sobre el gráfico, la información sobre herramientas muestra los valores de las categorías de Google Lighthouse en puntos específicos del tiempo.

![Detalles de tendencia](assets/experience-audit-trend-details.png)

Si pulsa o hace clic en el gráfico en un momento dado, se abrirá una ventana emergente con detalles de ese análisis. Pulse o haga clic en **abrir análisis de auditoría de experiencias** para cargar los resultados de ese análisis en la sección **[Resultados del análisis de auditoría de experiencias](#scan-results)**.

![Seleccionar análisis diferente](assets/experience-audit-open-scan.png)

#### Resultados del análisis de auditoría de experiencias {#scan-results}

La sección **Resultados del análisis de auditoría de experiencias** proporciona recomendaciones sobre cómo mejorar su puntuación y detalles de todas las páginas digitalizadas. Se divide en dos secciones:

* **[Recommendations](#recommendations)**
* **[Páginas digitalizadas](#scanned-pages)**

##### Recomendaciones {#recommendations}

La sección **Recommendations** muestra un conjunto agregado de datos. De manera predeterminada, se muestran las recomendaciones de **rendimiento**. Utilice la lista desplegable situada junto al encabezado **Recommendations** para cambiar a otra categoría.

![Recommendations](assets/experience-audit-recommendations.png)

Pulse o haga clic en las comillas angulares de cualquier recomendación para mostrar detalles al respecto.

![Detalles de la recomendación](assets/experience-audit-recommendations-details.png)

Cuando están disponibles, los detalles ampliados de la recomendación también contienen el porcentaje de impacto de las recomendaciones, para ayudarle a centrarse en los cambios más impactantes.

Pulse o haga clic en el vínculo **ver páginas** de la vista de detalles para ver las páginas a las que se aplica la recomendación.

![Páginas para los detalles de la recomendación](assets/experience-audit-details-pages.png)

##### Páginas digitalizadas {#scanned-pages}

La sección **Páginas digitalizadas** proporciona puntuaciones de detalles en todas las páginas digitalizadas. Puede usar los botones **Anterior** y **Siguiente** para hojear los resultados y elegir cuántos elementos se mostrarán en la pantalla.

![Páginas digitalizadas](assets/experience-audit-scanned-pages.png)

Al tocar o hacer clic en el vínculo de una página en particular, se actualiza el filtro **Seleccionar** de [**Puntuaciones de página - tendencia** sección](#trend) y se muestra la pestaña **Puntuaciones y recomendaciones** de la página seleccionada.

![Resultados de la página](assets/experience-audit-page-results.png)

La ficha **Informes sin procesar** le proporciona puntuaciones para cada auditoría de la página. Pulse o haga clic en la fecha del informe en la columna **Informe de Lighthouse** para recuperar un archivo JSON de los datos sin procesar.

![Informe sin procesar](assets/experience-audit-raw-reports.png)

Se abrirá una nueva pestaña en su explorador, que apuntará a `https://googlechrome.github.io/lighthouse/viewer/` con una URL firmada del informe Notación de objetos de JavaScript (JSON) sin procesar de Lighthouse para la página seleccionada, el cual se abrirá automáticamente para su inspección detallada

![Visualizando informe sin procesar](assets/experience-audit-view-raw-report.png)

## Informes de auditoría bajo demanda {#on-demand}

Además de ejecutarse durante la ejecución de la canalización, los informes de auditoría de experiencias también se pueden generar bajo demanda. Esta es una buena solución para analizar rápidamente sus páginas, sin tener que ejecutar una canalización.

Para ejecutar un análisis bajo demanda, vaya a la ficha **Informes** para ver el informe de auditoría completo y, a continuación, toque o haga clic en el botón **Ejecutar análisis**.

![Análisis bajo demanda](assets/experience-audit-on-demand.png)

El botón **Ejecutar análisis** deja de estar disponible y aparece marcado con un icono de reloj cuando ya se está ejecutando un análisis bajo demanda.

![Análisis bajo demanda en ejecución](assets/experience-audit-on-demand-running.png)

Los análisis bajo demanda almacenan en déclencheur una auditoría de experiencias para las últimas 25 [páginas configuradas](#configuration) y, por lo general, finalizan en unos minutos.

Una vez finalizado, el gráfico de puntuaciones se actualizará automáticamente y puede inspeccionar los resultados exactamente como para un análisis de ejecución de canalización.

Puede filtrar el gráfico de puntuaciones según el tipo de déclencheur usando el selector **Déclencheur**.

![filtro de Déclencheur](assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>Un análisis bajo demanda solo se puede iniciar si el entorno no se elimina y no hay otros análisis pendientes en el mismo entorno.

## La auditoría de experiencias encuentra problemas {#issues}

Si las [páginas que configuró](#configuration) para auditar no estaban disponibles o si había otros errores en la auditoría, la auditoría de experiencias lo refleja.

La canalización muestra una sección de errores ampliable para ver las rutas URL relativas a las que no pudo acceder.

![Problemas detectados por la auditoría de experiencias](assets/experience-audit-issues.jpg)

Si visualiza el informe completo, los detalles se muestran en la sección **[Resultados del análisis de auditoría de experiencias](#results)**, que también es ampliable.

![Problemas completos con el informe](assets/experience-audit-issues-report.png)

Algunas razones por las que las páginas podrían no estar disponibles son las siguientes:

* La configuración bloquea el acceso.
* La página no existe.
* La página redirige los envíos que requieren una autenticación distinta de la básica.
* Se ha producido un problema interno.
* Etc

>[!TIP]
>
>[Acceder a los informes sin procesar](#scanned-pages) de una página puede proporcionar detalles sobre por qué no se pudo auditar la página.

## Consejos generales de rendimiento {#performance-tips}

Dos de los problemas de impacto más comunes y fáciles de solucionar están relacionados con los Cambios acumulativos de diseño (CLS) y la Pintura de contenido más grande (LCP).

Estas se pueden mejorar mediante:

* No cargar de forma diferida las imágenes por encima del pliegue (el contenido visible en el explorador sin necesidad de desplazarse hacia abajo).
* Priorizar correctamente cómo se cargan los recursos (por ejemplo, cargando asincrónicamente las imágenes debajo del pliegue después de cargar el documento).
* Precarga de archivos JavaScript y CSS que se utilizan para representar contenido sobre el pliegue (si es necesario).
* Reservar el espacio vertical asignando una relación de aspecto a los contenedores que se cargan lentamente o se procesan más adelante.
* Convertir imágenes al formato WebP para reducir su tamaño.
* Usar `<picture>` y la imagen `srcset` con diferentes tamaños de imagen para diferentes tamaños de ventanilla (y asegurarse de que funciona el cambio de tamaño).

## Detalles de evaluación de auditoría de experiencias {#details}

Los siguientes detalles proporcionan información adicional sobre cómo la auditoría de experiencias evalúa el sitio. No son necesarios para el uso general de la función y se proporcionan aquí para su integridad.

* La auditoría analiza el dominio de origen (`.com`) tal como se define en las [rutas configuradas de la página Auditoría de experiencias](#configuration) del editor para simular las experiencias reales del usuario con mayor precisión y le ayuda a tomar decisiones más informadas sobre la administración y la optimización de sus sitios web.
* En las canalizaciones full-stack de producción, se analiza el entorno de ensayo.
   * Para garantizar que la auditoría proporcione los detalles relevantes durante la auditoría, el contenido del entorno de ensayo debe estar lo más cerca posible del entorno de producción.
* Las páginas mostradas en el menú desplegable **Seleccionar** de la sección [**Puntuaciones de página - tendencia**](#trend) son todas páginas conocidas que la auditoría de experiencias analizó anteriormente.
* [Una recomendación](#recommendations) puede tener una ganancia potencial y una diferencia con respecto al análisis anterior.
   * La auditoría de experiencias calcula la ganancia potencial procesando el informe sin procesar de cada página y correlacionando los bytes o milisegundos desperdiciados con una perspectiva que tiene un impacto ponderado en la puntuación de rendimiento.
   * La auditoría proporciona esta información (así como las páginas afectadas) para ayudar a decidir qué recomendación aplicar.
   * Para obtener más información, consulte la sección [Consejos generales de rendimiento](#performance-tips)
* Dado que una canalización de front-end podría implementarse en un entorno existente (o podría haber varias canalizaciones de front-end dirigidas al mismo entorno) y los resultados del análisis se agregan a nivel de entorno, las puntuaciones, tendencias y recomendaciones se muestran en el mismo entorno seleccionado, independientemente de la ejecución de la canalización que activó el análisis.
