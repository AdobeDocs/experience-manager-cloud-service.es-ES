---
title: Información general sobre herramientas de refactorización
description: Obtenga información sobre cómo empezar a utilizar las herramientas de refactorización de AEM
source-git-commit: a77dfef8dce9f4ed549135087f7b63f6d46a4ea1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 1%

---


<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=es" text="Guidelines and Best Practices"

-->

# Información general sobre herramientas de refactorización {#refactoring-tools-overview}

**Las herramientas de refactorización** agilizan el proceso de actualización de los proyectos existentes de AEM para que sean compatibles con **AEM as a Cloud Service (AEMaaCS)**. Estas herramientas automatizan tareas comunes de refactorización y modernización, y se integran con **Cloud Acceleration Manager (CAM)** para ofrecer una experiencia perfecta.

Anteriormente disponible solo como utilidades CLI, las herramientas de refactorización ahora proporcionan una interfaz unificada con funciones como inspección automatizada, generación de configuración y ejecución de trabajos, lo que reduce la sobrecarga manual y mejora la visibilidad.

## Flujo de trabajo de inspección {#inspection-workflow}

El **flujo de trabajo de inspección** simplifica el proceso de preparación para ejecutar las herramientas de refactorización.

### Características principales:

* **Déclencheur automático**: al cargar un proyecto, se inicia automáticamente la inspección.
* **Generación de configuración**: las herramientas inspeccionan el código fuente cargado y generan las configuraciones necesarias.
* **Envío de carga útil**: estas configuraciones se pasan directamente a las herramientas seleccionadas para su ejecución.

## Herramientas de refactorización disponibles

### Modernizador de repositorio {#repo-modernizer}

El **Modernizador de repositorio** reestructura el diseño y el contenido del repositorio de su proyecto de AEM para que se ajuste a los estándares y las prácticas recomendadas de AEMaaCS. Sustituye a la herramienta de modernización de repositorios heredada con una automatización y precisión mejoradas.

### Transformador de código {#code-transformer}

El **Transformador de código** usa el reconocimiento inteligente de patrones y el análisis controlado por IA para detectar y actualizar los segmentos de código que son incompatibles con AEMaaCS. Esta herramienta simplifica el esfuerzo de migración y reduce los cambios manuales en el código.

## Fases de flujo de trabajo de refactorización {#phases-in-refactoring-tools}

Las herramientas de refactorización siguen un proceso estructurado en dos fases:

### Fase 1: Cargar el código Source

* Cargue su código fuente (en formato ZIP) utilizando la interfaz CAM.
* Una vez subido, el **Flujo de trabajo de inspección** se activa automáticamente para analizar el proyecto y prepararlo para la ejecución de la herramienta.

>[!NOTE]
>Durante el proceso de inspección, no se permite cargar otro proyecto.

### Fase 2: Déclencheur de un trabajo de refactorización

Después de una inspección correcta, puede ejecutar una o más herramientas de refactorización:

* **Ejecutar Modernizador de repositorio** - Ejecuta la modernización del repositorio.
* **Ejecutar transformador de código**: ejecuta la transformación de código en función de la salida de inspección.
* **Ejecutar todas las herramientas juntas**: ejecuta todas las herramientas disponibles en una sola operación.

>[!NOTE]
>Los trabajos de refactorización solo se pueden iniciar después de que el código fuente se haya cargado e inspeccionado correctamente.

>[!NOTE]
>Los usuarios pueden almacenar en déclencheur varios trabajos de refactorización de forma paralela, pero cada trabajo se ejecutará por separado.
