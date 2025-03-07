---
title: Uso del panel de realización de valor para analizar las tendencias de uso de formularios y documentos
description: Aprenda a utilizar el panel de perspectivas de uso de Forms para monitorizar y comprender el rendimiento de los formularios y los fragmentos de formulario.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components, Core Components
hide: true
hidefromtoc: true
source-git-commit: 09d383638d6caba596d22a7c6b544768de5245a0
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# Uso del panel de realización de valor para analizar las tendencias de uso de formularios y documentos

<span class="preview"> Esta característica está disponible a través del programa de acceso anticipado. Para solicitar acceso, envíe un correo electrónico desde su dirección oficial a aem-forms-ea@adobe.com. <span>

![Panel de realización de valores](/help/edge/docs/forms/universal-editor/assets/forms-insights-banner.svg)

Al supervisar regularmente las métricas presentadas en el panel &quot;Perspectivas de uso de Forms&quot;, puede obtener información valiosa sobre el rendimiento de los formularios, documentos y fragmentos de formulario. Utilice estos datos para tomar decisiones informadas sobre el diseño del formulario, la administración de fragmentos y la estrategia general del formulario.

Este artículo proporciona instrucciones de uso detalladas e interpretación de métricas para el Tablero de Realización de Valores. Para obtener una descripción general conceptual y las ventajas del tablero, vea [Comprender el tablero de realización de valores](/help/forms/aem-forms-value-realization-dashboard.md).


## Acceso al panel de perspectivas de uso

Para acceder al panel de información de uso de Forms:

1. Vaya a **Forms** > **Forms y documentos**
1. Haga clic en **Tablero de InProduct**. El tablero se abre en una nueva ventana.

   ![Panel de realización de valores](/help/forms/assets/forms-usage-insights.png)

## Información general

El tablero consta de dos secciones principales:

- **Actividad de formularios y documentos a lo largo del tiempo:** Esta sección proporciona información sobre el uso y la evolución de los formularios durante un período seleccionado.
- **Uso del fragmento:** Esta sección le permite supervisar la adopción y reutilización de fragmentos de formulario.

## Actividad de formularios y documentos a lo largo del tiempo

Esta sección contiene cuatro gráficos, cada uno de los cuales realiza un seguimiento de un aspecto diferente de la actividad del formulario. Todos los gráficos comparten la misma estructura:

- **Tipo de gráfico:** Gráfico de líneas y gráfico de barras
- **Eje X:** Fecha (que muestra la actividad diaria)
- **Eje Y:** Recuento (que representa el número de ocurrencias de la actividad rastreada)
- **Período de tiempo:** Ajustable mediante un menú desplegable (opciones: &quot;Últimos 30 días&quot;, &quot;Últimos 12 meses&quot;)




### Envíos de formularios

- **Propósito:** Este gráfico muestra el número de veces que los formularios se han enviado correctamente durante el período de tiempo seleccionado.

  ![Gráfico de envíos de Forms](/help/forms/assets/forms-submissions-vr-dashboard-form-insights.png)
- **Información para extraer:**
   - **Análisis de tendencias:** Observe la tendencia general de los envíos de formularios. ¿Aumenta, disminuye o se mantiene relativamente constante el número?
   - **Períodos punta:** Identifique días o períodos con tasas de envío inusualmente altas. Investigue las posibles razones de estos picos (por ejemplo, campañas de marketing o eventos específicos).
   - **Períodos de actividad bajos:** Identifique los períodos con tasas de envío bajas e investigue las posibles causas (por ejemplo, tiempo de inactividad del formulario, problemas de uso).
   - **Análisis comparativo:** Compare las tasas de envío en diferentes períodos de tiempo (por ejemplo, los últimos 30 días en comparación con los 30 días anteriores) para evaluar los cambios de rendimiento.

### Representaciones de documentos

- **Propósito:** Este gráfico rastrea el número de documentos generados como resultado de los envíos de formularios. Esto es importante si los formularios tienen en déclencheur la creación de documentos (por ejemplo, contratos o informes).

  ![Gráfico de representaciones de documentos](/help/forms/assets/document-rendetions-vr-dashboard-form-insights.png)


- **Información para extraer:**
   - **Correlación con los envíos de formularios:** Compare la tendencia de las representaciones de documentos con la tendencia de los envíos de formularios. Idealmente, deberían correlacionarse estrechamente. Las discrepancias pueden indicar problemas con el proceso de generación de documentos.
   - **Volumen de generación de documentos:** Evalúe el volumen total de documentos que se están generando para comprender la carga de trabajo del sistema de generación de documentos.

### Formularios creados


- **Propósito:** Este gráfico muestra el número de formularios nuevos creados dentro del período de tiempo seleccionado.

  ![Gráfico creado por Forms](/help/forms/assets/forms-created-vr-dashboard-form-insights.png)

- **Información para extraer:**
   - **Tasa de creación de formularios:** Realice un seguimiento de la velocidad a la que se crean los formularios nuevos. Esto proporciona información sobre la demanda de nuevos formularios dentro de la organización.
   - **Picos en la creación:** Identifique períodos con una actividad de creación de formularios inusualmente alta. Esto puede indicar proyectos o iniciativas específicos que requieren nuevos formularios.

### Forms publicado

- **Propósito:** Este gráfico hace un seguimiento del número de formularios que se han publicado (disponibles para su uso) dentro del período de tiempo seleccionado.

  ![Gráfico publicado de Forms](/help/forms/assets/forms-publish-vr-dashboard-form-insights.png)


- **Información para extraer:**
   - **Tasa de implementación de formularios:** supervise la tasa a la que se implementan nuevos formularios a los usuarios.
   - **Retraso entre la creación y la publicación:** Analice la diferencia horaria entre el gráfico &quot;Forms creado&quot; y el gráfico &quot;Forms publicado&quot;. Un retraso significativo puede indicar cuellos de botella en el proceso de aprobación o implementación del formulario.

## Uso de fragmentos

En esta sección se proporciona información sobre el uso de los fragmentos de formulario, que son componentes reutilizables que se pueden incorporar en varios formularios.

![Gráfico publicado de Forms](/help/forms/assets/fragment-usage-vr-dashboard-form-insights.png)

### Número de fragmentos de formulario en uso

- **Tipo de gráfico:** Visualización numérica (mostrando un solo valor)
- **Propósito:** Muestra el número total de fragmentos de formulario únicos que se están utilizando actualmente en formularios activos.
- **Información para extraer:**
   - **Adopción de fragmentos:** evalúa la adopción general de fragmentos de formulario dentro de la organización. Un número mayor indica un mayor uso de componentes reutilizables.

### Reutilización de fragmentos de formulario

- **Tipo de gráfico:** Visualización numérica (mostrando un solo valor)
- **Propósito:** Esto muestra el número total de veces que los fragmentos de formulario se han reutilizado en diferentes formularios. Esta métrica indica la eficacia con la que se aprovechan los fragmentos para evitar duplicaciones y mantener la coherencia.
- **Información para extraer:**
   - **Tasa de reutilización de fragmentos:** supervise la tasa a la que los fragmentos existentes se están reutilizando en formularios nuevos. Un número mayor indica un mejor aprovechamiento de los componentes reutilizables y una mayor eficiencia.

## Ejemplo de escenarios

- **Escenario:** Observará una caída repentina en &quot;Envíos de formularios&quot;.
   - **Acción:** Investigue posibles causas, como el tiempo de inactividad del formulario, problemas de uso o una disminución del tráfico en la página de aterrizaje del formulario.
- **Escenario:** El valor &quot;Reutilización de fragmentos de formulario&quot; es bajo.
   - **Acción:** Promocione las ventajas de utilizar fragmentos de formulario para su equipo, asegúrese de que los fragmentos estén bien organizados y sean fáciles de encontrar, y proporcione formación sobre cómo crear y reutilizar fragmentos de forma eficaz.
- **Escenario:** Hay un retardo significativo entre &quot;Forms Created&quot; y &quot;Forms Published&quot;.
   - **Acción:** revise el proceso de aprobación e implementación de formularios para identificar y eliminar cuellos de botella.



## Véase también

- [Comprender el panel de realización de valores](/help/forms/aem-forms-value-realization-dashboard.md)
