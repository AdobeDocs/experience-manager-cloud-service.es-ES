---
title: Evaluación del estado de los entornos de producción y ensayo
description: Aprenda a utilizar la evaluación de estado de Cloud Manager. Puede analizar entornos de AEM, ejecutar y revisar informes, ver detalles del problema, exportar PDF y administrar ejecuciones anteriores.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 9%

---


# Evaluación del estado {#about-health-assessment}

La evaluación de estado es un análisis automatizado y no intrusivo para entornos de producción y ensayo en Cloud Manager dentro de AEM as a Cloud Service. Evalúa el contenido, el código y las configuraciones para encontrar antipatrones y desviaciones de las prácticas recomendadas, lo que mejora la seguridad y el rendimiento.

El servicio de evaluación médica hace lo siguiente:

* Analiza los entornos y expone los cuellos de botella, las ineficiencias y los riesgos del rendimiento.
* Analiza las estructuras de contenido, como los modelos, las Live Copies y las configuraciones de los clientes.
* Detecta dependencias obsoletas, incluidas bibliotecas de AEM SDK y de terceros.
* Indica problemas de calidad del código, como anotaciones incorrectas y patrones ineficientes.
* Ofrece directrices procesables en los paneles (por ejemplo, el Centro de actividades).
* Impulsa la corrección proactiva para mejorar el rendimiento del sistema.

Cada ejecución enumera los problemas por gravedad, vincula a las directrices y correcciones recomendadas, y admite una exportación PDF del informe. Puede usar la vista **Informe más reciente** del estado actual y **Informes anteriores** para comparar ejecuciones.

Consulte también [Patrones de evaluación de estado](#ha-patterns) para ver las definiciones de reglas y los detalles de corrección.

## Acceso a la página Evaluación de estado {#access-health-assessment}

1. Inicie sesión en Cloud Manager en [experiece.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee. La siguiente imagen es para ilustrarla. Seleccione su propio nombre de organización.

   ![Selección de una organización en Cloud Manager](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. En la consola **Mis programas**, haga clic en el programa para el que desea ver su informe.

1. Realice una de las siguientes acciones:
   * En la tarjeta **Entornos**, a la derecha del nombre de un entorno, haga clic en ![Icono de puntos suspensivos o en Más](https://spectrum.adobe.com/static/icons/ui_18/More.svg) y, a continuación, elija **Evaluación del estado** en el menú.

     ![Seleccionar la evaluación de estado en el menú de los tres puntos de la tarjeta Entornos](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**. En la página Entornos, a la derecha del nombre de un entorno, haga clic en ![Icono de puntos suspensivos o en Más icono](https://spectrum.adobe.com/static/icons/ui_18/More.svg) y, a continuación, elija **Evaluación de estado** en el menú.

     ![Seleccionar la evaluación de estado en el menú de los tres puntos de la página Entornos](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## Ejecutar un nuevo informe para un entorno seleccionado {#run-report}

1. [Acceda a la página de evaluación de estado](#access-health-assessment).
1. En la esquina superior derecha de la página **Evaluación del estado**, confirme el entorno de destino que está a punto de evaluar.

   Si el entorno es incorrecto, haga clic en ![Comilla o menú desplegable para seleccionar un entorno diferente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y elegir el entorno correcto de la lista.

1. Haga clic en **Ejecutar informe**.

   ![Haga clic en el botón Generar nuevo informe en la página Evaluación de estado](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   Mientras se ejecuta un informe para el entorno seleccionado, **Ejecutar informe** permanece deshabilitado hasta que finalice.

   ![Informe en plena ejecución](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   Cuando se complete el informe, este aparecerá en la página **Evaluación del estado**, en la sección **Último informe**.

## Ver el informe más reciente {#view-latest-report}

* En la página **Evaluación del estado**, revise la sección **Último informe** para obtener la siguiente información:

   * Resultados de la ejecución más reciente.
   * Fecha y hora de ejecución.
   * Recuento total de problemas.
   * Aspectos destacados de los problemas más importantes.
   * Acciones: **[Ver detalles](#view-report-details)** o **[Descargar PDF](#download-pdf-report)** de todos los problemas.

  ![Página de la última evaluación después de la generación de un nuevo informe para un entorno seleccionado](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### Ver los detalles del informe más reciente {#view-report-details}

* En la página **Evaluación del estado**, a la derecha del título de **Último informe**, haga clic en ![Icono de puntos suspensivos o en Más icono](https://spectrum.adobe.com/static/icons/ui_18/More.svg) y, a continuación, haga clic en **Ver detalles** o **Descargar**.

  La opción **Ver detalles** le muestra lo siguiente:

   * Una lista completa de cuestiones.
   * Capacidad para ver conclusiones y descripciones de problemas.
   * Capacidad para ver documentación con posibles correcciones.

     ![Descripciones y búsqueda de problemas](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * La opción **Descargar** permite descargar informes de problemas individuales en PDF.

     ![Descargar PDF de informes de problemas individuales](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### Descargar PDF de todo el informe {#download-pdf-report}

* Cerca de la esquina superior derecha de la página del informe, haga clic en **Descargar**.

  Se genera un archivo ZIP que contiene los PDF de todos los problemas detectados en ese informe.

  ![Descargar PDF de todos los problemas encontrados en un informe](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## Revisar informes anteriores {#review-past-reports}

En la página **Evaluación de estado**, revise la sección **Informes anteriores** para obtener la siguiente información:

* Ver los detalles de cualquier informe anterior.
* Ver la fecha de cada ejecución.
* Descargue un PDF para cualquier informe.
* Ordene por fecha, recuento de problemas o entorno.

![Revisar informes anteriores](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* A la derecha del encabezado de **Informes anteriores**, haga clic en ![Comilla o menú desplegable para seleccionar un entorno diferente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) para ordenar los informes pasados por fecha.
* En el extremo derecho de un informe, haga clic en ![icono de puntos suspensivos o en Más icono](https://spectrum.adobe.com/static/icons/ui_18/More.svg) y, a continuación, haga clic en **Ver detalles** o **Descargar**.


## Patrones de evaluación de estado {#ha-patterns}

A continuación se muestra la lista completa de antipatrones y problemas que la evaluación de estado detecta en AEM as a Cloud Service. La tabla agrupa los elementos en tres tipos: análisis de contenido, análisis de código y antipatrones de Cloud Service Optimizer, con una explicación para cada uno.

| Nombre del patrón | Categoría | Tipo | Descripción | Impacto | ¿Auto-arreglado? |
| --- | --- | --- | --- | --- | --- |
| Grupos de AEM personalizados con adiciones de usuarios directos | Seguridad | Análisis de contenido | Los usuarios se agregan directamente a los grupos de AEM en lugar de agregar grupos de IMS como miembros. | La administración de permisos y la gobernanza de seguridad pueden complicarse. [Compatibilidad con IMS](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/ims-support) | No |
| Falta el nodo de contenido JCR en las páginas | Estructura del repositorio | Análisis de contenido | Falta el nodo `jcr:content` en la página. | Limitaciones funcionales en Experience Manager as a Cloud Service. [Detección de patrones - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | No |
| Falta el tipo de medio de Sling en las páginas | Estructura del repositorio | Análisis de contenido | Falta `sling:resourceType` en la página. | Limitaciones funcionales en Experience Manager as a Cloud Service. [Detección de patrones - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | No |
| Páginas con recuento excesivo de nodos | Rendimiento | Análisis de contenido | Las páginas contienen un gran número de nodos en su estructura. | Tiempos de carga de la página lentos y mala experiencia del usuario. [Detección de patrones - PCX](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | No |
| Demasiadas instancias de flujo de trabajo en ejecución | Rendimiento | Análisis de contenido | Se están ejecutando demasiadas instancias de flujo de trabajo. | Degradación general del rendimiento del sistema. [Tareas de mantenimiento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) | No |
| Instancias de flujo de trabajo completadas sin depurar | Rendimiento | Análisis de contenido | Las instancias de flujo de trabajo completadas anteriores no se depuran. | Reducción de la eficacia del sistema y aumento de los costes de almacenamiento. [Tareas de mantenimiento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) | No |
| Estadísticas de uso de fragmentos de contenido | Estadísticas | Análisis de contenido | Registra el número de fragmentos de contenido en uso. | N/D | N/D |
| Estadísticas de uso del modelo de fragmento de contenido | Estadísticas | Análisis de contenido | Registra el número de modelos de fragmento de contenido en uso. | N/D | N/D |
| MSM: gran cantidad de modelos | Estadísticas | Análisis de contenido | Registra el número de modelos. | Puede aumentar la complejidad de la administración y dificultar la gobernanza del contenido. | N/A |
| Páginas MSM por modelo | Estadísticas | Análisis de contenido | Registra el número de páginas por modelo. | Puede aumentar la complejidad de la administración y dificultar la gobernanza del contenido. | N/A |
| Demasiadas Live Copies de MSM | Estadísticas | Análisis de contenido | Registra el número de Live Copies. | Puede provocar problemas de rendimiento durante las implementaciones y complicar la sincronización de contenido. | N/A |
| Demasiadas Live Copies de MSM por modelo | Estadísticas | Análisis de contenido | Registra el número de copias activas por modelo. | Puede provocar problemas de rendimiento durante las implementaciones y complicar la sincronización de contenido. | N/A |
| Número de Assets | Estadísticas | Análisis de contenido | Registra el número de recursos. | N/D | N/D |
| Número de sitios | Estadísticas | Análisis de contenido | Registra el número de sitios. | N/D | N/D |
| Número de Forms | Estadísticas | Análisis de contenido | Registra el número de formularios. | N/D | N/D |
| Fragmentos de formulario | Estadísticas | Análisis de contenido | Registra el número de fragmentos de formulario. | N/D | N/D |
| Comunicaciones de interacción | Estadísticas | Análisis de contenido | Registra el número de interacciones de comunicación del formulario. | N/D | N/D |
| FDM | Estadísticas | Análisis de contenido | Registra el número de modelos de datos de formulario. | N/D | N/D |
| Dependencias obsoletas | Dependencias | Análisis de código | Resalta las dependencias obsoletas en el repositorio del cliente. | Incompatibilidad con versiones más recientes de AEM; posibles vulnerabilidades de seguridad. | No |
| La versión de AEM SDK no coincide | Dependencias | Análisis de código | Versiones anteriores a (n-2) en comparación con la versión del entorno de Cloud Manager. | Puede provocar errores de compilación en Cloud Manager y problemas en entornos de desarrollo locales. | No |
| Dependencia principal de Mockito obsoleta | Dependencias | Análisis de código | Las versiones anteriores a 4.x.x se consideran obsoletas para AEM as a Cloud Service. | Puede provocar errores de compilación en Cloud Manager y problemas en entornos de desarrollo locales. | No |
| Anotaciones no admitidas | Dependencias | Análisis de código | Anotaciones no admitidas en el repositorio de Cloud Manager del cliente. | Posibles errores de la aplicación y disminución del rendimiento. | No |
| Anotación @Inject en modelos Sling | Dependencias | Análisis de código | Anotación `@Inject` obsoleta. | Rendimiento de aplicación reducido debido a la sobrecarga de resolución de inyección. | No |
| Solicitudes HTTP salientes | Rendimiento | Antipatrones de Cloud Service Optimizer | Uso problemático en el contexto de la solicitud, tiempos de espera altos o no cerrar conexiones. | Degradación general del rendimiento del sistema y posibles interrupciones. | Sí |
| Consultas lentas | Rendimiento | Antipatrones de Cloud Service Optimizer | Consultas lentas en el código de cliente. | Rendimiento del sistema degradado y tiempos de espera potenciales. | Sí |

### Categorías {#ha-patterns-categories}

| Categoría | Descripción |
| --- | --- |
| Seguridad | Patrones relacionados con las prácticas de seguridad, la administración de usuarios y el control de acceso. |
| Rendimiento | Patrones que afectan al rendimiento de la aplicación y del sistema. |
| Estructura del repositorio | Patrones relacionados con la organización y estructura del repositorio JCR. |
| Dependencias | Patrones relacionados con las dependencias de código y la administración de versiones. |
| Estadísticas | Patrones que representan estadísticas y métricas de uso. |



