---
title: Fase de preparación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de preparación en Cloud Acceleration Manager.
exl-id: 91a13cae-4934-42e8-9538-896fd72f5acb
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 5%

---

# Fase de preparación en Cloud Acceleration Manager {#readiness-phase-cam}

Una vez que haya creado un proyecto en Cloud Acceleration Manager, ahora puede iniciar la evaluación de su implementación de AEM actual en la fase de preparación.

La fase de preparación incluye:

* [Análisis de prácticas recomendadas](#best-practices-analysis)
* [Planificación y configuración](#planning-setup)

Siga los pasos a continuación para ir a la fase de preparación:

1. Haga clic en la tarjeta del proyecto para abrir la página de aterrizaje del proyecto.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Vaya a la sección **Preparación**, como se muestra en la figura siguiente.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Creación y administración de un proyecto en Cloud Acceleration Manager para obtener más información.

## Uso de la tarjeta de análisis de prácticas recomendadas {#best-practices-analysis}

Siga los pasos a continuación para utilizar la tarjeta de Análisis de prácticas recomendadas:

1. Haga clic en el botón **Review** de la tarjeta **Best Practices Analysis**.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Siga estos pasos para descargar el Analizador de prácticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar BPA en un entorno de Author lo más cercano posible al entorno de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de Author de producción.

   1. Vaya al portal [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/es-ES/aemcloud.html) y descargue el Analizador de prácticas recomendadas como archivo zip.

      >[!NOTE]
      >Revise [Usar el Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) para aprender a ejecutar BPA.

   1. Exportar el informe en formato CSV

1. Haga clic en **Cargar nuevo informe** para cargar el informe de BPA en CAM.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >El informe no se puede cargar si se encuentra en el modo Incognito del explorador.

1. Una vez que haya cargado un nuevo informe, verá el informe Análisis de prácticas recomendadas .

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Revise y explore el tablero de Análisis de prácticas recomendadas en CAM. Consulte la sección siguiente [Revisión del informe de análisis de prácticas recomendadas](#analysis-report) para obtener más información.

   >[!NOTE]
   >Al cargar un nuevo informe, se restablecen todas las evaluaciones.

1. Haga clic en el icono **Vista previa de impresión**, como se muestra a continuación.

   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Al hacer clic en **Vista previa de impresión** se abre una nueva ficha en la que el informe se muestra en una vista previa imprimible. Haga clic en **Imprimir** para imprimir el informe en formato de PDF para facilitar el uso compartido.

   >[!IMPORTANT]
   >* Se recomienda la opción **Guardar como PDF** y se admite para la funcionalidad anterior.
   >* Si se utiliza el botón de impresión del navegador, se imprimirá una sola página.


   ![image](/help/move-to-cloud-service/best-practices-analyzer/assets/bpa-printpreview2.png)

### Revisión del informe de Análisis de prácticas recomendadas {#analysis-report}

Explore las siguientes tarjetas disponibles en la página Informe de análisis de prácticas recomendadas :

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con cada tarjeta, tiene la capacidad de:
>* haga clic en cada tarjeta para abrir su ficha asociada
>* marque todas las fichas del informe (incluido el filtrado) para compartirlas o recuperarlas en el futuro
>* utilice el icono de detalles para ver los detalles de cada búsqueda de informe


#### Propiedades del informe {#report-properties}

La tarjeta **Propiedades del informe** proporciona información sobre las propiedades del informe, como la fecha, la duración, los filtros, la fecha de carga y los detalles de Adobe Experience Manager (AEM).

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Información general del informe {#report-overview}

Esta tarjeta **Información general de informe** proporciona los resultados del informe y los niveles de gravedad que se aplican al evaluar la preparación para pasar a AEM as a Cloud Service, como se muestra en la figura siguiente.

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Al hacer clic en este informe se abre la pestaña **Report**.

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Puede filtrar el informe en función de su importancia, subtipo o recuento.

![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretación del informe de Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) para obtener más información sobre las categorías de hallazgos y los niveles de importancia.

#### Evaluación de prácticas recomendadas {#best-practices-assessment}

La opción Evaluación de prácticas recomendadas proporciona una evaluación de la instancia de AEM actual y proporciona orientación sobre los pasos siguientes para adoptar AEM prácticas recomendadas. Puede revisar la siguiente información desde esta pestaña:

* Información general de la instancia de AEM
* Plantillas y componentes personalizados
* Conclusiones adicionales
* Consultas lentas
* Tareas de mantenimiento

#### Evaluación de la complejidad de la migración {#migration-complexity-assessment}

La opción de evaluación de la complejidad de la migración proporciona una evaluación de la complejidad para migrar la implementación de AEM existente a AEM as a Cloud Service.

Puede revisar la siguiente información desde esta pestaña:

* Información general de la instancia de AEM
* Evaluación
* Consideraciones sobre la migración de contenido

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Uso de la tarjeta de planificación y configuración {#planning-setup}

Siga esta sección para explorar la tarjeta de actividad Planificación y configuración .

1. Haga clic en el botón **View** de la tarjeta **Planning And Setup**. Esta tarjeta proporciona todo el contenido relevante que le ayudará a planificar y configurar su migración AEM.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carrusel de contenido muestra toda la información relevante para esta fase del recorrido de migración.

   ![image](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a iniciar sesión en Cloud Acceleration Manager y a crear un proyecto, ya está listo para pasar a revisar el siguiente paso en la [fase de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
