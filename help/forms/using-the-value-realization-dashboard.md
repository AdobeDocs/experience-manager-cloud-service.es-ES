---
title: Uso del panel de realización de valor para analizar las tendencias de uso de formularios y documentos
description: Aprenda a utilizar el panel de información sobre el uso de formularios para monitorizar y comprender el rendimiento de los formularios y los fragmentos de formulario.
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components, Core Components
hide: true
hidefromtoc: true
exl-id: f58aa2df-dfb6-4eb4-b20d-e81bb01be8a7
source-git-commit: 3bc967bc2b6584abbd73e3456e123ed76a8959b6
workflow-type: ht
source-wordcount: '873'
ht-degree: 100%

---

# Uso del panel de realización de valor para analizar las tendencias de uso de formularios y documentos

<span class="preview"> Esta función está disponible a través del programa de acceso rápido. Para solicitar acceso, envíe un correo electrónico desde su dirección oficial a aem-forms-ea@adobe.com. <span>

![Panel de realización del valor](/help/edge/docs/forms/universal-editor/assets/forms-insights-banner.svg)

Al monitorizar regularmente las métricas presentadas en el panel “Información sobre el uso de formularios”, puede obtener información valiosa sobre el rendimiento de los formularios, documentos y fragmentos de formulario. Utilice estos datos para tomar decisiones fundamentadas sobre el diseño del formulario, la administración de fragmentos y la estrategia general del formulario.

En este artículo se proporcionan instrucciones de uso detalladas e interpretación de métricas para el Panel de realización de valor. Para obtener información general conceptual y las ventajas del panel, consulte [Información acerca del panel de realización de valor](/help/forms/aem-forms-value-realization-dashboard.md).


## Acceso al panel de información sobre el uso

Para acceder al panel de información sobre el uso de formularios:

1. Vaya a **Formularios** > **Formularios y documentos**.
1. Haga clic en **Panel InProduct**. El panel se abre en una nueva ventana.

   ![Panel de realización de valor](/help/forms/assets/forms-usage-insights.png)

## Información general

El panel consta de dos secciones principales:

- **Actividad de formularios y documentos a lo largo del tiempo:** esta sección proporciona información sobre el uso y la evolución de los formularios durante un período seleccionado.
- **Uso del fragmento:** esta sección le permite supervisar la adopción y reutilización de fragmentos de formulario.

## Actividad de formularios y documentos a lo largo del tiempo

Esta sección contiene cuatro gráficos, cada uno de los cuales realiza un seguimiento de un aspecto diferente de la actividad del formulario. Todos los gráficos comparten la misma estructura:

- **Tipo de gráfico:** gráfico de líneas y gráfico de barras
- **Eje X:** fecha (que muestra la actividad diaria)
- **Eje Y:** recuento (representa el número de ocurrencias de la actividad rastreada)
- **Período de tiempo:** ajustable mediante un menú desplegable (opciones: “Últimos 30 días”, “Últimos 12 meses”)




### Envío de formularios

- **Finalidad:** este gráfico muestra el número de veces que los formularios se han enviado correctamente durante el período de tiempo seleccionado.

  ![Gráfico de envío de formularios](/help/forms/assets/forms-submissions-vr-dashboard-form-insights.png)
- **Información para extraer:**
   - **Análisis de tendencias:** observe la tendencia general de los envíos de formularios. ¿El número aumenta, disminuye o se mantiene relativamente constante?
   - **Períodos de máxima afluencia:** identifique días o períodos con frecuencias de envío inusualmente altas. Investigue las posibles razones de estos picos (por ejemplo, campañas de marketing o eventos específicos).
   - **Períodos de actividad bajos:** identifique los períodos con frecuencias de envío bajas e investigue las posibles causas (por ejemplo, tiempo de inactividad del formulario, problemas de uso).
   - **Análisis comparativo:** compare las frecuencias de envío en diferentes períodos de tiempo (por ejemplo, los últimos 30 días en comparación con los 30 días anteriores) para evaluar los cambios de rendimiento.

### Representaciones de los documentos

- **Finalidad:** este gráfico rastrea el número de documentos generados como resultado de los envíos de formularios. Es importante si los formularios activan la creación de documentos (por ejemplo, contratos, informes).

  ![Gráfico de representaciones de documentos](/help/forms/assets/document-rendetions-vr-dashboard-form-insights.png)


- **Información para extraer:**
   - **Correlación con los envíos de formularios:** compare la tendencia de las representaciones de documentos con la tendencia de los envíos de formularios. Lo ideal es que estén estrechamente relacionados. Las discrepancias pueden indicar problemas con el proceso de generación de documentos.
   - **Volumen de generación de documentos:** evalúe el volumen total de documentos que se están generando para comprender la carga de trabajo del sistema de generación de documentos.

### Formularios creados


- **Finalidad:** este gráfico muestra el número de formularios nuevos creados dentro del período de tiempo seleccionado.

  ![Gráfico de formularios creados](/help/forms/assets/forms-created-vr-dashboard-form-insights.png)

- **Información para extraer:**
   - **Velocidad de creación de formularios:** realice un seguimiento de la velocidad a la que se crean los nuevos formularios. Proporciona información sobre la demanda de nuevos formularios dentro de la organización.
   - **Picos en la creación:** identifique períodos con una actividad de creación de formularios inusualmente alta. Esto puede indicar proyectos o iniciativas específicos que requieren nuevos formularios.

### Formularios publicados

- **Finalidad:** este gráfico hace un seguimiento del número de formularios que se han publicado (disponibles para el uso) dentro del período de tiempo seleccionado.

  ![Gráfico de formularios publicados](/help/forms/assets/forms-publish-vr-dashboard-form-insights.png)


- **Información para extraer:**
   - **Velocidad de implementación de formularios:** supervise la velocidad a la que implementan los nuevos formularios para los usuarios.
   - **Retardo entre creación y publicación:** analice la diferencia horaria entre el gráfico “Formularios creados” y el gráfico “Formularios publicados”. Un retardo significativo puede indicar cuellos de botella en el proceso de aprobación o implementación del formulario.

## Uso de fragmentos

En esta sección se proporciona información sobre el uso de fragmentos de formulario, que son componentes reutilizables que se pueden incorporar en varios formularios.

![Gráfico de formularios publicados](/help/forms/assets/fragment-usage-vr-dashboard-form-insights.png)

### Número de fragmentos de formulario en uso

- **Tipo de gráfico:** visualización numérica (muestra un solo valor)
- **Finalidad:** muestra el número total de fragmentos de formulario únicos que se están utilizando actualmente en los formularios activos.
- **Información para extraer:**
   - **Adopción de fragmentos:** evalúe la adopción general de fragmentos de formulario dentro de la organización. Un número mayor indica un mayor uso de componentes reutilizables.

### Reutilización de fragmentos de formulario

- **Tipo de gráfico:** visualización numérica (muestra un solo valor)
- **Finalidad:** muestra el número total de veces que los fragmentos de formulario se han reutilizado en diferentes formularios. Esta métrica indica la eficacia con la que se aprovechan los fragmentos para evitar duplicaciones y mantener la coherencia.
- **Información para extraer:**
   - **Índice de reutilización de fragmentos:** monitorice el índice de reutilización de los fragmentos existentes en formularios nuevos. Un número mayor indica un mejor aprovechamiento de los componentes reutilizables y una mayor eficiencia.

## Ejemplos de escenarios

- **Escenario:** observa una caída repentina en los “Envíos de formularios”.
   - **Acción:** investigue las posibles causas, como el tiempo de inactividad del formulario, los problemas de uso o una disminución del tráfico en la página de aterrizaje del formulario.
- **Escenario:** el valor “Reutilización de fragmentos de formulario” es bajo.
   - **Acción:** promocione las ventajas del uso de fragmentos de formulario para su equipo; asegúrese de que los fragmentos estén bien organizados y sean fáciles de encontrar, y ofrezca formación sobre cómo crear y reutilizar fragmentos de forma eficaz.
- **Escenario:** hay un retardo significativo entre los “Formularios creados” y los “Formularios publicados”.
   - **Acción:** revise el proceso de aprobación e implementación de los formularios a identificar para eliminar los cuellos de botella.



## Véase también

- [Información sobre el panel de realización de valor](/help/forms/aem-forms-value-realization-dashboard.md)
