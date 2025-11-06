---
title: Panel de control de auditoría de experiencias
description: Descubra cómo la auditoría de experiencias valida el proceso de implementación y garantiza que los cambios cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO. Proporciona una interfaz de panel clara e informativa para rastrear estas métricas.
exl-id: 6d33c3c5-258c-4c9c-90c2-d566eaeb14c0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 8%

---


# Panel de auditoría de experiencias {#experience-audit-dashboard}

<!-- Engineer architect over this feature was Bogdan Anton; scrum master Alexandru Nica -->

Descubra cómo la auditoría de experiencias valida el proceso de implementación y garantiza que los cambios cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO (optimización del motor de búsqueda). Proporciona una interfaz de panel clara e informativa para rastrear estas métricas.

## Información general {#overview}

La auditoría de experiencias valida el proceso de implementación y ayuda a garantizar que se implementen los cambios:

1. Cumplan los estándares de línea de base para el rendimiento, la accesibilidad, las prácticas recomendadas y la SEO.
1. No introduzcan regresiones.

La auditoría de experiencias en Cloud Manager garantiza que la experiencia del usuario en el sitio sea de los más altos estándares.

Los resultados de la auditoría son informativos y permiten al administrador de implementación ver las puntuaciones y el cambio entre las puntuaciones actuales y anteriores. Esta perspectiva es importante para determinar si hay una regresión que se haya introducido con la implementación actual.

La auditoría de experiencias está equipada con [Google Lighthouse](https://developer.chrome.com/docs/lighthouse/overview/), una herramienta de código abierto de Google, y está habilitada en todas las canalizaciones de producción de Cloud Manager.

## Disponibilidad {#availability}

La auditoría de experiencias está disponible para Cloud Manager:

* (Predeterminado) Canalizaciones de producción de sitios.
* (Opcional) Desarrollo de canalizaciones de pila completa.
* (Opcional) Desarrollo de canalizaciones front-end.

Consulte la [sección Configuración](#configuration) para obtener más información sobre cómo configurar la auditoría para los entornos opcionales.

Las auditorías se ejecutan como parte de la canalización. Las auditorías también se pueden [ejecutar bajo demanda](#on-demand) fuera de las canalizaciones.

## Configuración {#configuration}

La auditoría de experiencias está disponible de forma predeterminada para las canalizaciones de producción. Opcionalmente, se puede habilitar para el desarrollo de canalizaciones full-stack y front-end. En todos los casos, debe definir qué rutas de contenido se evalúan durante la ejecución de la canalización.

1. Según el tipo de canalización que desee configurar, realice una de las siguientes acciones:

   * [Agregue una canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) para definir las rutas que desea que evalúe la auditoría.
   * [Agregue una canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md), si desea habilitar la auditoría en una canalización de pila completa de front-end o de desarrollo.
   * [Editar una canalización existente](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) y actualizar las opciones existentes.

1. Para usar la auditoría de experiencias al agregar o editar una canalización que no sea de producción, marque la casilla de verificación **Auditoría de experiencias**. Puede encontrar esta opción en la ficha **Código Source**.

   ![Habilitando auditoría de experiencias](/help/implementing/cloud-manager/reports/assets/experience-audit-enable.jpg)

   * Necesario solo para canalizaciones que no sean de producción.
   * La ficha **Auditoría de experiencias** aparece cuando se selecciona la casilla de verificación.

1. Tanto para las canalizaciones de producción como para las que no son de producción, usted define las rutas que deben incluirse en la auditoría de experiencias en la pestaña **Auditoría de experiencias**.

   * Las rutas de acceso a la página deben comenzar por `/` y son relativas al sitio.
   * Por ejemplo, si el sitio es `wknd.site` y desea incluir a `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, escriba la ruta de acceso `/us/en/about-us.html`.

   ![Definición de una ruta para la auditoría de experiencias](/help/implementing/cloud-manager/reports/assets/experience-audit-add-page.png)

1. Haga clic en **Agregar página** y la ruta se completará de forma automática con la dirección de su entorno, además se agregará a la tabla de rutas.

   ![Guardar ruta de acceso a la tabla](/help/implementing/cloud-manager/reports/assets/experience-audit-page-added.png)

1. Siga agregando rutas según sea necesario repitiendo los dos pasos anteriores.

   * Puede agregar un máximo de 25 rutas.
   * Si no define una ruta, la página principal del sitio se incluye en la auditoría de experiencias de forma predeterminada.

1. Haga clic en **Guardar**.

## Resultados de la auditoría de experiencias {#results}

Los resultados de la auditoría de experiencias se presentan en la fase **Prueba de ensayos** de la canalización de producción a través de la [página de ejecución de la canalización de producción](/help/implementing/cloud-manager/deploy-code.md).

![Panel en la canalización](/help/implementing/cloud-manager/reports/assets/experience-audit-dashboard.png)

La auditoría de experiencias proporciona la mediana de las puntuaciones de Google Lighthouse para las [páginas configuradas](#configuration) y la diferencia de puntuación con respecto al análisis anterior.

Desde esta vista de resumen en la fase **Prueba de ensayo** de la canalización, tiene dos opciones:

* **[Ver las páginas más lentas](#view-slowest-pages)**
* **[Ver el informe completo](#view-full-report)**

Puede acceder a los resultados completos de la auditoría haciendo clic en la pestaña **Informes** del panel de Cloud Manager. Además del resumen que se muestra en los detalles de ejecución de la canalización, puedes ver [el informe completo](#view-full-report) directamente.

>[!TIP]
>
>Las secciones siguientes describen cómo ver los resultados de la auditoría de experiencias.
>
>* Para obtener más información sobre cómo funciona la auditoría, consulte [Detalles de evaluación de auditoría de experiencias](#details).
>* Para saber cómo ejecutar una auditoría de experiencias bajo demanda, consulte [Informes de auditoría bajo demanda](#on-demand).
>* Si tiene problemas con la auditoría, consulte [Problemas de contadores de auditoría de experiencias](#issues).

### Ver las páginas más lentas {#view-slowest-pages}

Haga clic en **Ver páginas más lentas** para abrir el cuadro de diálogo **Más lentas** 5 páginas. Se muestran las cinco páginas de menor rendimiento que [configuró para auditar](#configuration).

![Cinco más lentos](/help/implementing/cloud-manager/reports/assets/experience-audit-slowest-five.png)

Cloud Manager desglosa las puntuaciones por **Rendimiento**, **Accesibilidad**, **Prácticas recomendadas** y **SEO**, mostrando la desviación de cada métrica con respecto a la auditoría anterior.

De forma predeterminada, el cuadro de diálogo se abre con las puntuaciones de los dispositivos móviles. Puede ver las puntuaciones de escritorio mediante el conmutador **Dispositivos** situado cerca de la parte superior del cuadro de diálogo.

El cuadro de diálogo tiene por objeto ofrecerle una descripción general rápida. Para obtener información detallada, haz clic en **Ver informe completo**.

### Ver el informe completo {#view-full-report}

Para ver el informe completo de auditoría de experiencias, haga lo siguiente:

* Haga clic en **`View full report`** en el cuadro de diálogo **[Más lento: 5 páginas](#view-slowest-pages)**.
* Haga clic en **`View full report`** al ver la [ejecución de una canalización](#results).
* Haga clic en la ficha **Informes** de Cloud Manager.

Se abre la pestaña **Informes** de Cloud Manager, donde se muestra **Auditoría de experiencias**.

![Informes de auditoría de experiencias](/help/implementing/cloud-manager/reports/assets/experience-audit-reports.png)

El informe se divide en dos áreas:

* **[Puntuaciones de página — tendencia](#trend)**
* **[Resultados del análisis de auditoría de experiencias](#results)**

#### Puntuaciones de página: tendencia {#trend}

De manera predeterminada, la vista seleccionada para **puntuaciones de página — tendencia** es **puntuaciones medias** para **el año pasado**.

Puede elegir ver las tendencias de categorías específicas de Faro haciendo clic en el nombre de la categoría en la leyenda.

![Tendencia seleccionable](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-selectable.png)

Use la lista desplegable **Seleccionar** de la parte superior del gráfico para seleccionar detalles específicos de la página, y los desplegables **Ver** y **Déclencheur** de la parte inferior para elegir diferentes lapsos de tiempo y el tipo de déclencheur, respectivamente.

La lista desplegable **Vista** ofrece la posibilidad de seleccionar un lapso de tiempo preestablecido o un intervalo personalizado para una vista más específica.

![Vista de tendencia](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-view.png)

Al mover el ratón sobre el gráfico, la información sobre herramientas muestra los valores de las categorías de Google Lighthouse en puntos específicos del tiempo.

![Detalles de tendencia](/help/implementing/cloud-manager/reports/assets/experience-audit-trend-details.png)

Si hace clic en el gráfico en un momento dado, se abrirá una ventana emergente con detalles de ese análisis. Haga clic en **abrir análisis de auditoría de experiencias** para cargar los resultados del análisis en la sección **[resultados del análisis de auditoría de experiencias](#scan-results)**.

![Seleccionar análisis diferente](/help/implementing/cloud-manager/reports/assets/experience-audit-open-scan.png)

#### Resultados del análisis de auditoría de experiencias {#scan-results}

La sección **Resultados del análisis de auditoría de experiencias** proporciona detalles de las puntuaciones de todas las páginas digitalizadas. Use los botones **Anterior** y **Siguiente** para hojear los resultados y elegir cuántos elementos se deben paginar en la pantalla.

![Páginas digitalizadas](/help/implementing/cloud-manager/reports/assets/experience-audit-scanned-pages.png)

Haga clic en el vínculo de una página determinada para actualizar el filtro **Seleccionar** de [**Puntuaciones de página — tendencia** sección](#trend) y mostrar la ficha **Informes sin procesar** que le proporciona puntuaciones para cada auditoría de la página. Haga clic en la fecha del informe en la columna **Informe Lighthouse** para recuperar un archivo JSON de los datos sin procesar.

![Informe sin procesar](/help/implementing/cloud-manager/reports/assets/experience-audit-raw-reports.png)

Se abrirá una nueva pestaña en el explorador, que lo dirigirá a `https://googlechrome.github.io/lighthouse/viewer/`. Carga automáticamente una dirección URL firmada que contiene el informe JSON sin procesar de Lighthouse de la página seleccionada, lo que permite una inspección detallada.

![Visualizando informe sin procesar](/help/implementing/cloud-manager/reports/assets/experience-audit-view-raw-report.png)

## Informes de auditoría de análisis bajo demanda {#on-demand}

Además de ejecutarse durante la ejecución de la canalización, los informes de auditoría de experiencias también se pueden generar bajo demanda. Esta opción es una buena solución para analizar las páginas rápidamente, sin tener que ejecutar una canalización.

Para ejecutar un análisis bajo demanda, vaya a la ficha **Informes** para poder ver el informe de auditoría completo y, a continuación, haga clic en el botón **Ejecutar análisis**.

![Análisis bajo demanda](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand.png)

El botón **Ejecutar análisis** deja de estar disponible y aparece marcado con un icono de reloj cuando ya se está ejecutando un análisis Bajo demanda.

![Análisis bajo demanda en ejecución](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-running.png)

Los análisis bajo demanda almacenan en déclencheur una auditoría de experiencias para las últimas 25 [páginas configuradas](#configuration) y, por lo general, finalizan en unos minutos.

Una vez finalizado, el gráfico de puntuaciones se actualiza automáticamente y puede inspeccionar los resultados exactamente como para un análisis de ejecución de canalización.

Puede filtrar el gráfico de puntuaciones según el tipo de déclencheur usando el selector **Déclencheur**.

![filtro de Déclencheur](/help/implementing/cloud-manager/reports/assets/experience-audit-on-demand-trigger.png)

>[!NOTE]
>
>Un análisis Bajo demanda solo se puede iniciar si el entorno no se elimina y no hay otros análisis pendientes en el mismo entorno.

## La auditoría de experiencias encuentra problemas {#issues}

Si las [páginas que configuró](#configuration) para auditar no estaban disponibles o si había otros errores en la auditoría, la auditoría de experiencias refleja este hecho.

La canalización muestra una sección de errores ampliable para ver las rutas URL relativas a las que no pudo acceder.

![Problemas detectados por la auditoría de experiencias](/help/implementing/cloud-manager/reports/assets/experience-audit-issues.png)

Si visualiza el informe completo, los detalles se muestran en la sección **[Resultados del análisis de auditoría de experiencias](#results)**, que también es ampliable.

![Problemas completos con el informe](/help/implementing/cloud-manager/reports/assets/experience-audit-issues-report.png)

Algunas razones por las que las páginas podrían no estar disponibles son las siguientes:

* La configuración bloquea el acceso.
* La página no existe.
* La página redirige los envíos que requieren una autenticación distinta de la básica.
* Se ha producido un problema interno.

>[!TIP]
>
>[Acceder a los informes sin procesar](#scan-results) de una página puede proporcionar detalles sobre por qué no se pudo auditar la página.

## Detalles de evaluación de auditoría de experiencias {#details}

Los siguientes detalles proporcionan información adicional sobre cómo la auditoría de experiencias evalúa el sitio. No son necesarios para el uso general de la función y se proporcionan aquí para su integridad.

* La auditoría explora el dominio de origen (`.com`) desde las [rutas configuradas de la página Auditoría de experiencias](#configuration) del editor para simular experiencias reales del usuario, lo que le ayuda a tomar mejores decisiones sobre la administración y optimización de sus sitios web.
* En las canalizaciones full-stack de producción, se analiza el entorno de ensayo. Para garantizar que la auditoría proporcione los detalles relevantes durante la auditoría, el contenido del entorno de ensayo debe ser lo más parecido posible al entorno de producción.
* Las páginas mostradas en la lista desplegable **Seleccionar** en la sección [**Puntuaciones de página — tendencia**](#trend) son todas páginas conocidas que la auditoría de experiencias ha analizado anteriormente.
