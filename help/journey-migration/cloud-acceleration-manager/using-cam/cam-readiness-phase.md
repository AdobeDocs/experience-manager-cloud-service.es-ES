---
title: Fase de preparación en Cloud Acceleration Manager
description: Esta página proporciona información general sobre la fase de preparación de Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 3a0576e62518240b89290a75752386128b1ab082
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 7%

---

# Fase de preparación en Cloud Acceleration Manager {#readiness-phase-cam}

Una vez que haya creado un proyecto en Cloud Acceleration Manager (CAM), ahora puede iniciar la evaluación de la implementación actual de Adobe Experience Manager AEM () en la fase de Preparación.

La fase de preparación incluye:

* [Análisis de las prácticas recomendadas](#best-practices-analysis)
* [Planificación y configuración](#planning-setup)

Siga los pasos a continuación para ir a la fase de preparación:

1. Haga clic en la tarjeta de proyecto.

   ![Tarjeta de proyecto](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. En la página de aterrizaje del proyecto, vaya a la sección **Preparación**, como se muestra en la figura siguiente.

   ![Preparación](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Consulte Creación y administración de un proyecto en Cloud Acceleration Manager para obtener más información.

## Uso de la tarjeta de análisis de prácticas recomendadas {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="Informe del análisis de prácticas recomendadas"
>abstract="El informe de BPA puede cargarse en CAM para proporcionar un análisis del mismo con respecto a la migración a AEM as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="Uso del analizador de prácticas recomendadas"

1. Haga clic en **Revisar** en la tarjeta **Análisis de prácticas recomendadas**.

   ![Análisis de prácticas recomendadas - Revisar](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Descargue el Analizador de prácticas recomendadas (BPA).

   >[!NOTE]
   >Para evitar un impacto en las instancias críticas para el negocio, Adobe recomienda ejecutar BPA en un entorno de creación. El entorno debe estar lo más cerca posible del entorno de producción en las áreas de personalizaciones, configuraciones, contenido y aplicaciones de usuario. Como alternativa, se puede ejecutar en un clon del entorno de Author de producción.

   1. Vaya al portal [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*) y descargue el Analizador de prácticas recomendadas como archivo zip.

      >[!NOTE]
      >Revise [Cómo usar el Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=es#imp-considerations) para aprender a ejecutar BPA.

1. En CAM, haz clic en **Obtener clave de carga**, para que puedas obtener la clave que se usa para configurar tu sistema de modo que cargue automáticamente los informes de BPA directamente en CAM.

   ![Obtener clave de carga](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >El informe se puede cargar manualmente, pero el uso de la clave de carga optimiza la operación. Tenga en cuenta que el informe no se puede cargar manualmente si su tamaño es de aproximadamente 200 MB o más. El informe tampoco se puede cargar utilizando el modo de incógnito del explorador.

1. Una vez cargado un nuevo informe, puede ver el informe Análisis de las prácticas recomendadas en CAM.

   ![Informe de análisis de prácticas recomendadas](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Si se cargan varios informes diferentes, el informe que se muestra en detalle siempre es el que tiene la fecha de creación más reciente (no la fecha de carga).

1. Revise y explore el panel de análisis de las prácticas recomendadas en CAM. Consulte [Revisión del informe de análisis de prácticas recomendadas](#analysis-report) para obtener más información.

   >[!NOTE]
   >La carga de un nuevo informe restablece todas las evaluaciones si es más reciente que el informe cargado anteriormente.

### Uso de la vista previa {#print-preview-cam}

Puede seleccionar la opción de vista previa de impresión en Cloud Acceleration Manager para obtener una vista previa imprimible de los informes o para imprimir el informe en un formato de PDF para compartirlo fácilmente.

Complete los siguientes pasos:

1. Haga clic en la acción **Vista preliminar**.

   ![Vista preliminar](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. En la nueva ficha con el informe mostrado en una vista previa imprimible, haga clic en **Imprimir** para imprimir el informe en formato de PDF.

   >[!IMPORTANT]
   >
   >* Se recomienda y admite la opción **Guardar como PDF** para la funcionalidad anterior.
   >* Si se utiliza el botón Imprimir del explorador, se imprime sólo una página.

   ![Imprimir](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Uso de Ver línea de tendencia {#trendline-view-cam}

Cuando carga más de un informe de Analizador de prácticas recomendadas (BPA) en un proyecto, puede seleccionar la opción **Ver línea de tendencia** para ver y comparar los resultados de los informes de BPA históricos.

Siga los pasos a continuación para ver los informes de la opción de línea de tendencia:

>[!NOTE]
>Cuando carga más de un informe de BPA distinto en un proyecto, verá el icono **...**. Los informes se consideran iguales (no distintos) si su host y la hora de creación son iguales.

1. Vaya al proyecto y haga clic en **Revisar** desde la tarjeta de **Análisis de prácticas recomendadas** en la fase de **Preparación**.

   ![Análisis de prácticas recomendadas - Revisar](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. En la lista desplegable **Ver**, haga clic en **Informe de líneas de tendencia**, como se muestra en la figura siguiente.

   ![Informe de tendencias](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Al hacer clic en **Informe de línea de tendencia**, se abre la vista de línea de tendencia del informe.

   ![Vista de línea de tendencia](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >El Informe de líneas de tendencia muestra los resultados de los informes de BPA históricos en una representación gráfica.
   >
   >Verá dos gráficos que muestran la tendencia del:
   > 
   >1. **Tendencia de conclusiones de informes**
   >1. **Componentes personalizados y tendencia de la plantilla**
   >
   >Puede añadir o cambiar la vista gráfica mediante la lista desplegable, como se muestra en la figura siguiente:
   >![Seleccione la vista gráfica](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Revisar el informe de Best Practices Analyzer {#analysis-report}

Explore las siguientes tarjetas, disponibles en la página Informe de análisis de prácticas recomendadas:

![Informe de análisis de prácticas recomendadas](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Con cada tarjeta, puede:
>
>* abrir la pestaña asociada
>* marcar todas las fichas de informe (incluido el filtrado) para compartirlas o recuperarlas posteriormente
>* utilice el icono de detalles para ver los detalles de cada búsqueda de informe

#### Propiedades del informe {#report-properties}

La tarjeta **Propiedades del informe** proporciona información sobre las propiedades del informe, como la fecha del informe, la duración, los filtros, la fecha de carga y los detalles de Adobe Experience Manager AEM ().

![Propiedades del informe](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Resumen del informe {#report-overview}

Esta tarjeta **Información general del informe** proporciona los resultados del informe y los niveles de gravedad que se aplican cuando se evalúa la preparación para pasar a AEM as a Cloud Service, como se muestra en la figura siguiente.

![Información general del informe](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Al hacer clic en este informe, se abre la ficha **Informe**.

![Pestaña Informe](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Puede filtrar el informe en función de su importancia, subtipo o recuento.

![Filtros de informes](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Consulte [Interpretación del informe del Analizador de prácticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=es) para obtener más información sobre las categorías de resultados y los niveles de importancia.

#### Evaluación de las prácticas recomendadas {#best-practices-assessment}

AEM AEM La opción de Evaluación de las prácticas recomendadas proporciona una evaluación de su instancia actual de y proporciona orientación sobre los próximos pasos para adoptar las prácticas recomendadas. Puede revisar la siguiente información en esta pestaña:

* Información general de la instancia de AEM
* Componentes y plantillas personalizadas
* Conclusiones adicionales
* Consultas lentas
* Tareas de mantenimiento

#### Evaluación de la complejidad de la migración {#migration-complexity-assessment}

AEM La opción de evaluación de la complejidad de la migración proporciona una evaluación de la complejidad para migrar la implementación de la existente a AEM as a Cloud Service.

Puede revisar la siguiente información en esta pestaña:

* Información general de la instancia de AEM
* Evaluación
* Consideraciones de migración de contenido

  ![Evaluación de la complejidad de la migración](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Uso de la tarjeta de planificación y configuración {#planning-setup}

1. Haga clic en **Ver** en la tarjeta **Planificación y configuración**. AEM Esta tarjeta proporciona todo el contenido relevante que le ayuda a planificar y configurar su migración a la.

   ![Planificación Y Configuración - Vista](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. Un carrusel de contenido muestra toda la información relevante para esta fase del recorrido de migración.

   ![Carrusel De Planificación Y Configuración](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Eliminación de un informe de análisis de prácticas recomendadas de la vista Línea de tendencia {#delete-trendline}

>[!IMPORTANT]
>Un informe solo se puede eliminar cuando se ha cargado más de un informe en un proyecto.

1. Vaya al proyecto y haga clic en **Revisar** desde la tarjeta de **Análisis de prácticas recomendadas** en la fase de **Preparación**.

   ![Análisis de prácticas recomendadas - Revisar](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Haga clic en **...**.

   ![Elipse](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. En la lista desplegable, haga clic en **Ver línea de tendencia**, como se muestra en la figura siguiente.

   ![Ver línea de tendencia](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Haga clic en el icono Eliminar de la pantalla **Informe de líneas de tendencias**.

   ![Informe De Tendencias - Eliminar](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Haga clic en **Eliminar** para confirmar la eliminación.

   ![Eliminar](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## Siguientes pasos {#whats-next}

Una vez que haya aprendido a iniciar sesión en Cloud Acceleration Manager y a crear un proyecto, ya puede pasar a revisar el siguiente paso en la [fase de implementación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=es).
