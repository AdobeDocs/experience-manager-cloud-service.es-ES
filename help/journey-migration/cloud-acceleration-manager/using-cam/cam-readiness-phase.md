---
title: Fase de preparación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de preparación en Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# Fase de preparación en Cloud Acceleration Manager {#readiness-phase-cam}

AEM Una vez que haya creado un proyecto en Cloud Acceleration Manager, ahora puede iniciar la evaluación de la implementación actual de la en la fase de Preparación.

La fase de preparación incluye:

* [Análisis de las prácticas recomendadas](#best-practices-analysis)
* [Planificación y configuración](#planning-setup)

Siga los pasos a continuación para ir a la fase de preparación:

1. Haga clic en la tarjeta del proyecto para abrir la página de aterrizaje del proyecto.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Vaya a **Preparación** , como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Creación y administración de un proyecto en Cloud Acceleration Manager para obtener más información.

## Tarjeta de análisis de prácticas recomendadas {#best-practices-analysis}

Siga los pasos a continuación para utilizar la tarjeta Análisis de prácticas recomendadas:

1. Haga clic en **Revisar** del menú contextual **Análisis de las prácticas recomendadas** Tarjeta de.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Siga estos pasos para descargar el Analizador de prácticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar un impacto en las instancias críticas para el negocio, se recomienda ejecutar BPA en un entorno de Author lo más cercano posible al entorno de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de Author de producción.

   1. Vaya a [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es-es/aemcloud.html) y descargue el Analizador de prácticas recomendadas como archivo zip.

      >[!NOTE]
      >Revisar [Uso del analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) para aprender a ejecutar BPA.

   1. Exportación del informe en formato CSV

1. Haga clic en **Cargar nuevo informe** para cargar un informe de BPA en CAM.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >El informe no se puede cargar si se encuentra en el modo de incógnito del explorador.

1. Una vez que haya cargado un nuevo informe, verá el informe Análisis de las prácticas recomendadas.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Revise y explore el panel de análisis de las prácticas recomendadas en CAM. Consulte la sección siguiente [Revisión del informe de análisis de prácticas recomendadas](#analysis-report) para obtener más información.

   >[!NOTE]
   >Al cargar un nuevo informe se restablecen todas las evaluaciones.

### Uso de la vista previa {#print-preview-cam}

Puede seleccionar la opción de vista previa de impresión en Cloud Acceleration Manager para obtener una vista previa imprimible de los informes o para imprimir el informe en un formato de PDF para facilitar el uso compartido.

Complete los siguientes pasos:

1. Haga clic en **Vista preliminar** , como se muestra a continuación.

   ![imagen](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. Haciendo clic en **Vista preliminar** abre una nueva pestaña con el informe mostrado en una vista previa imprimible. Haga clic en **Imprimir** para imprimir el informe en formato de PDF.

   >[!IMPORTANT]
   >* La opción **Guardar como PDF** se recomienda y admite para la funcionalidad anterior.
   >* Si se utiliza el botón de impresión del explorador, solo se imprimirá una página.


   ![imagen](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Uso de Ver línea de tendencia {#trendline-view-cam}

Cuando cargue más de un informe de Analizador de prácticas recomendadas (BPA) en un proyecto, podrá seleccionar el **Ver línea de tendencia** para ver y comparar los resultados de los informes históricos de BPA.

Siga los pasos a continuación para ver los informes de la opción de línea de tendencia:

>[!NOTE]
>Cuando cargue más de un informe de BPA en un proyecto, verá el **...** icono.

1. Vaya al proyecto y haga clic en **Revisar** desde el **Análisis de las prácticas recomendadas** Tarjeta de en **Preparación** fase.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Haga clic en **...** para mostrar la lista desplegable.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >El informe que se muestra siempre es el que tiene la fecha del informe más reciente.

1. Haga clic en **Ver línea de tendencia**, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Haciendo clic en **Ver línea de tendencia** abre la vista línea de tendencia del informe, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >El Informe de líneas de tendencia muestra los resultados de los informes de BPA históricos en una representación gráfica.
   >
   >Verá dos gráficos que muestran la tendencia del:
   >1. **Tendencia de conclusiones del informe**
   >1. **Componentes personalizados y tendencia de la plantilla**

   >
   >Puede añadir o cambiar la vista gráfica mediante la lista desplegable, como se muestra en la figura siguiente:
   >![imagen](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Revisar el informe de Best Practices Analyzer {#analysis-report}

Explore las siguientes tarjetas disponibles en la página Informe de análisis de prácticas recomendadas:

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con cada tarjeta, tiene la capacidad de:
>* haga clic en cada tarjeta para abrir su pestaña asociada
>* marcar todas las fichas de informe (incluido el filtrado) para compartirlas o recuperarlas posteriormente
>* utilice el icono de detalles para ver los detalles de cada búsqueda de informe


#### Propiedades del informe {#report-properties}

El **Propiedades del informe** proporciona información sobre las propiedades del informe, como la fecha, la duración, los filtros, la fecha de carga y los detalles de Adobe Experience Manager AEM ().

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Resumen del informe {#report-overview}

Esta **Resumen del informe** AEM La tarjeta de proporciona los resultados del informe y los niveles de gravedad que se aplican al evaluar la preparación para pasar a un estado de preparación as a Cloud Service, tal y como se muestra en la figura siguiente.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Al hacer clic en este informe, se abre **Informe** pestaña.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Puede filtrar el informe en función de la importancia, el subtipo o el recuento.

![imagen](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretación del informe del Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) para conocer las categorías de hallazgos y los niveles de importancia.

#### Evaluación de las prácticas recomendadas {#best-practices-assessment}

AEM AEM La opción de Evaluación de las prácticas recomendadas proporciona una evaluación de su instancia actual de y proporciona orientación sobre los próximos pasos para adoptar las prácticas recomendadas. Puede revisar la siguiente información en esta pestaña:

* AEM Resumen de instancia de
* Componentes y plantillas personalizadas
* Conclusiones adicionales
* Consultas lentas
* Tareas de mantenimiento

#### Evaluación de complejidad de migración {#migration-complexity-assessment}

AEM AEM La opción Evaluación de la complejidad de la migración proporciona una evaluación de la complejidad para migrar la implementación de la existente a la implementación de la migración en as a Cloud Service.

Puede revisar la siguiente información en esta pestaña:

* AEM Resumen de instancia de
* Evaluación
* Consideraciones de migración de contenido

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Uso de la tarjeta de planificación y configuración {#planning-setup}

Siga esta sección para explorar la tarjeta de actividades Planificación y configuración.

1. Haga clic en **Ver** del menú contextual **Planificación y configuración** Tarjeta de. AEM Esta tarjeta proporciona todo el contenido relevante que le ayudará a planificar y configurar su migración a la.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carrusel de contenido muestra toda la información relevante para esta fase del recorrido de migración.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Eliminación de un informe de análisis de prácticas recomendadas {#delete-trendline}

Siga los pasos a continuación para eliminar un informe de la vista Línea de tendencia:

>[!IMPORTANT]
>Un informe solo se puede eliminar cuando se ha cargado más de un informe en un proyecto.

1. Vaya al proyecto y haga clic en **Revisar** desde el **Análisis de las prácticas recomendadas** Tarjeta de en **Preparación** fase.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Haga clic en **...** para mostrar la lista desplegable.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Haga clic en **Ver línea de tendencia**, como se muestra en la figura siguiente.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. Haga clic en el icono Eliminar de la **Informe de tendencias** pantalla.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Haga clic en **Eliminar** para confirmar la eliminación.

   ![imagen](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a iniciar sesión en Cloud Acceleration Manager y a crear un proyecto, ya puede pasar a revisar el siguiente paso en la [Fase de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
