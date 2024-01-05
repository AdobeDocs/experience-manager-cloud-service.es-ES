---
title: Fase de implementación
description: Asegúrese de que el código y el contenido estén listos para la migración a la nube
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 9%

---

# Fase de implementación {#implementation-phase}

En la fase de implementación del recorrido AEM, explorará las herramientas a través de las cuales puede preparar su código y contenido para trasladarlo a la fase de implementación as a Cloud Service.

## La historia hasta ahora {#story-so-far}

En las partes anteriores del recorrido, ha pasado por [AEM familiarizarse con los cambios en el as a Cloud Service](/help/journey-migration/getting-started.md)y determinan si la implementación está lista para moverse a la nube con el [fase preparación](/help/journey-migration/readiness.md).

Este artículo continúa con consejos sobre cómo utilizar las herramientas proporcionadas por el Adobe para asegurarse de que el código y el contenido están listos para moverse a la nube.

## Objetivo {#objective}

Este documento tiene como objetivo:

* AEM AEM Preséntele Cloud Manager, la integración continua de la y el marco de trabajo de entrega utilizado para implementar código en as a Cloud Service
* Póngase al día con la herramienta de transferencia de contenido
* AEM Describa las herramientas de refactorización de código que tiene que utilizar para modernizar su código para que sea más as a Cloud Service. Para obtener más información, haga lo siguiente:

## Uso de Cloud Manager {#using-cloud-manager}

AEM Antes de empezar, debe familiarizarse con Cloud Manager, ya que es el único mecanismo para implementar código en las versiones as a Cloud Service de los.

Cloud Manager permite que las organizaciones administren AEM de forma automática en la nube. Incluye un marco de trabajo de integración y entrega continuas (CI/CD) que permite a los equipo de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

Puede familiarizarse con el uso de Cloud Manager consultando los siguientes recursos:

* [Recorrido de incorporación](/help/journey-onboarding/overview.md) para comprender los recursos de autoayuda sobre la incorporación de Experience Manager as a Cloud Service.

* [Integración de Git con Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) para aprender a utilizar un repositorio de Git único para implementar un código.

* [Configuración de Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) para obtener información sobre la administración de productos y el acceso de los usuarios en Admin Console.

## Utilice las herramientas proporcionadas por el Adobe para preparar el contenido y la nube de código {#use-tools-to-make-code-and-content-cloud-ready}

Los pasos exactos de la transición a Cloud Service dependen de los sistemas que haya adquirido y de las prácticas de desarrollo de software que siga.

AEM En la siguiente figura se muestran los pasos principales involucrados en la fase que implica convertir el código y el contenido para usarlos con el código as a Cloud Service:

![imagen](/help/journey-migration/assets/exec-image1.png)

Empezaremos a detallar las herramientas que debe utilizar para que pueda conseguirlo en los capítulos siguientes.

## Migración de contenido {#content-migration}

AEM Para migrar contenido de la instancia de actual a la instancia de Cloud Service, puede utilizar la herramienta de transferencia de contenido de Adobe.

Con esta herramienta, puede especificar el subconjunto de contenido que desea transferir de la instancia de AEM de origen a la instancia de AEM de Cloud Service.

La migración de contenido es un proceso de varios pasos que requiere planificación, seguimiento y colaboración entre diferentes equipos.

Para obtener información detallada completa sobre cómo funciona la herramienta y cómo recomienda Adobe que la utilice, consulte la [Documentación de Content Transfer Tool](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refactorización de código {#code-refactor}

### Configurar para desarrollo {#set-up-for-development}

Es hora de empezar a refactorizar las funciones existentes para que sean compatibles con los Cloud Service.

En primer lugar, observe la documentación que detalla las herramientas básicas y comience a refactorizar el código:


* AEM Durante la planificación, es una buena idea tener una lista de áreas que deben refactorizarse para ser compatibles con las áreas as a Cloud Service de la. Puede revisar [Directrices de desarrollo](/help/implementing/developing/introduction/development-guidelines.md) para obtener más información sobre cómo refactorizar y optimizar el código para Cloud Service.
* Obtenga más información sobre cómo [Administrar configuraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html#what-is-a-configuration) AEM en as a Cloud Service.
* Obtenga información sobre cómo configurar un entorno de desarrollo local descargando el [AEM SDK as a Cloud Service de](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html)
* Por último, familiarícese con el [AEM API de Java as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Además, también puede:

* Vea este vídeo para comprender cómo instalar el SDK de Dispatcher localmente:

  >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Vea este vídeo para comprender cómo configurar el SDK de Dispatcher:

  >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Un cambio de mentalidad {#a-change-in-mindset}

AEM Desarrollar y ejecutar código en as a Cloud Service requiere un cambio en la mentalidad. Cabe señalar que el código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento. Debe tenerse en cuenta que el código que se ejecuta en Cloud Service siempre se realiza en un clúster. Esto significa que siempre hay más de una instancia en ejecución.

AEM Es necesario realizar ciertos cambios para que los proyectos de Maven sean compatibles con la nube en la mayoría de los casos. AEM El as a Cloud Service requiere una separación de *content* y *código* AEM en paquetes distintos para su implementación en el entorno de trabajo de la:

* `/apps` y `/libs` AEM AEM se consideran áreas inmutables de la, ya que no se pueden cambiar después de iniciar la administración de la (es decir, durante la ejecución). Esto incluye operaciones de creación, actualización o eliminación. Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

* Todo lo demás en el repositorio (por ejemplo, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) son todas áreas mutables, lo que significa que se pueden cambiar durante la ejecución.

Para obtener más información, consulte la [Estructura del paquete recomendado](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) documentación.


### Herramientas de migración de nube {#cloud-migration-tools}

Adobe proporciona varias herramientas para acelerar algunas de las tareas de refactorización de código. Comprender estas herramientas y los problemas que resuelven reducirá la complejidad y el tiempo de la migración.

* [Migración de flujo de trabajo de recursos](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), una herramienta que se utiliza para migrar automáticamente los flujos de trabajo de procesamiento de recursos
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md)AEM , una herramienta que convierte las configuraciones existentes de Dispatcher en un formato listo para su uso en el as a Cloud Service de la.
* [Modernizador de repositorio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html)AEM AEM , una herramienta que toma un proyecto de modo múltiple de la manera más rápida y que lo convierte en un proyecto de modo múltiple de la manera más as a Cloud Service y más rápida de usar
* [Conversor de índices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html)AEM , una herramienta que convierte los índices en un formulario compatible con el as a Cloud Service de la
* [Herramientas de modernización](/help/journey-migration/refactoring-tools/aem-modernization-tools.md)AEM AEM , un conjunto de utilidades que se pueden utilizar para convertir las funciones heredadas de los usuarios a las funcionalidades modernas y compatibles de los servicios de as a Cloud Service.

AEM Una vez que haya configurado el entorno de desarrollo local, familiarícese con el SDK as a Cloud Service de la consultando el [documentación](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Programar una congelación de código {#schedule-a-code-freeze}

AEM Para administrar el desarrollo continuo de código en su proyecto activo junto con las tareas de refactorización de código como parte de su recorrido de transición, Adobe AEM recomienda que programe un período de congelación de código hasta que haya completado la reestructuración del proyecto Maven para que sea compatible con el as a Cloud Service de la.

Una vez que se haya realizado la reestructuración del proyecto, puede reanudar el nuevo desarrollo de código basado en esta nueva estructura. Esto reduce los errores de canalización de Cloud Manager durante la implementación y la prueba del código.

>[!NOTE]
>Las tareas de Transferencia de contenido y Refactorización de código no tienen que realizarse secuencialmente. Estas tareas se pueden hacer independientemente unas de otras. Sin embargo, se necesita una estructura de proyecto correcta para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

## Prácticas recomendadas para la implementación y prueba de código {#best-practices}

La canalización de Cloud Manager admite la ejecución de pruebas que se ejecutan en el entorno de ensayo.

Siga las prácticas recomendadas en los documentos siguientes con respecto a las pruebas de calidad del código:

* [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md), un documento que describe el proceso de escritura de scripts de prueba y explica el concepto de cobertura recomendada de al menos el 50 %.
* [Comprender las reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) AEM que tiene como objetivo describir las reglas de calidad del código personalizadas ejecutadas por Cloud Manager y creadas en función de las prácticas recomendadas de ingeniería de.

## Preparación para el lanzamiento {#preparing-for-go-live}

AEM La preparación del sistema de origen para la migración implica tareas a nivel del sistema y del administrador de la. Puede empezar comprobando que el repositorio de contenido está en un estado bien mantenido comprobando el [limpieza de revisión](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html?lang=es) y el [recolección de basura del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html?lang=es) estado de la tarea. AEM Si está ejecutando la versión 6.3 de la aplicación (ya que la herramienta de transferencia de contenido es compatible a partir de la versión 6.3), se recomienda realizar la compactación sin conexión, seguida de la recolección de basura del almacén de datos.

[Comprobación de coherencia de datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) AEM se recomienda en todas las versiones de la aplicación para garantizar que el repositorio de contenido esté en buen estado para iniciar las actividades de migración.

Se requiere acceso de administrador del sistema para instalar y configurar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

AEM También se recomienda revisar los recursos, las páginas, los proyectos, los usuarios y los grupos que no se utilicen para ahorrar tiempo durante la migración. Consulte la [Estado del repositorio de contenido](#repository-health) sección.

### Estado del repositorio de contenido {#repository-health}

Una vez acceda a un [clon de producción](#proof-of-migration) se ha establecido. continúe para comprobar el estado del repositorio. Como se mencionó en la sección anterior, el objetivo es limpiar y compactar el repositorio en el origen antes de iniciar la migración. Este paso podría ahorrar mucho tiempo, de lo contrario, se gasta en solucionar problemas una vez que comience la migración.

| Elemento de acción | Consideraciones clave |
|---------|----------|
| Usuarios, grupos y permisos | Debe comprender el volumen de usuarios, grupos y la complejidad de las suscripciones. Busque oportunidades para limpiar cualquier usuario o grupo no utilizado en el origen antes de la migración. |
| Procesamiento de recursos incompleto | AEM Intente completar el procesamiento de los recursos en el sistema de origen antes de iniciar la migración para evitar posibles problemas en la migración as a Cloud Service posterior a la migración. |
| Estado del contenido | Se recomienda consultar el contenido incorrecto y purgarlo antes de iniciar la migración. Por ejemplo, busque recursos o páginas que no tengan representaciones originales o que estén atascados en el procesamiento del flujo de trabajo. Consulte también [Estado de recursos](#asset-health). |

## Recopilando datos {#gathering-data}

>[!NOTE]
> El [Estrategia y cronología de migración de contenido](#content-strategy-and-timeline) Esta sección detalla cómo extrapolar los datos recopilados y crear un plan de migración.

La recopilación de datos puede ayudarle a planificar las actividades de migración y las tareas asociadas. Los tiempos de extracción y de ingesta son especialmente útiles porque los puntos de datos se pueden asociar con un tamaño específico del conjunto de migración. Como tal, se pueden extrapolar estos puntos de datos para llegar a un plan:

* Cantidad total de tiempo empleado para [extracción](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Cantidad total de tiempo empleado para [ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Cantidad total de tiempo necesario para la recarga [extracción](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Cantidad total de tiempo necesario para la recarga [ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)


<!-- Alexandru: hiding this for now

One more important datapoint is the amount of time it takes to complete the [user mapping](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), if this is coupled with the content migration. You can take this data point into consideration for more realistic estimates, because it is added to the overall extraction timeline and it may not be required to run it during top-ups.

-->

Estos puntos de datos también pueden ayudarle [Establezca los KPI](/help/journey-migration/readiness.md#establish-kpis) y otras tareas relacionadas con la migración.

### Plan de migración {#migration-plan}

En función de los puntos de datos recopilados (ver arriba), puede crear un plan de migración que se puede integrar en un plan de proyecto de macro. Este paso permitirá a todas las partes interesadas clave visualizar y planificar las actividades de migración.

La siguiente tabla ilustra un plan de migración típico:

| Iteración de migración | Fecha inicial | Fecha de finalización estimada | Dependencias | Duración estimada (en días) | Detalles adicionales / Elementos de acción |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |   |   |   |   |   |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |   |   |   |   |   |

Como puede ver en la tabla anterior, resulta útil seguir un formato de nombre específico para identificar las iteraciones de migración, por ejemplo: **PRECLONAR** AEM para el entorno de origen de la, **AUTOR/PUBLICACIÓN** AEM para el entorno as a Cloud Service de la, **CSSTAGE-AUTHOR** AEM para la instancia as a Cloud Service de la, etc.

Algunos detalles importantes que influyen en el plan de migración:

**Número total de extracciones necesarias**

* Las extracciones de autor y publicación en entornos específicos se consideran dos extracciones paralelas, ya que son independientes entre sí.
* Número de extracciones superiores basadas en el crecimiento del repositorio en períodos de tiempo específicos.

**Número total de ingestas requeridas**

* Es importante capturar este elemento en el plan, ya que un conjunto extraído se puede ingerir en varios entornos de Cloud Service.
* Número de ingestas superiores.
* La migración de contenido del Autor de origen a la instancia de Autor del servicio en la nube y de la Publicación de origen a Publicación de Cloud Service es la práctica recomendada para evitar la ingesta de todo el contenido del Autor en la Publicación de Cloud Service.

### Rastreador de migración {#migration-tracker}

Puede utilizar el rastreador de migración para anotar los tiempos tanto de la ejecución inicial como de la superior. Estos puntos de datos le ayudarán a formular requisitos realistas de congelación de contenido antes de la recarga final.

El rastreador también le ayudará a lo siguiente:

* Identifique cualquier desviación del planificador que requiera ajustes en el plan o en las escalas de tiempo de lanzamiento
* Proporcionar un estado realista que se pueda utilizar en todas las comunicaciones necesarias
* Planifique migraciones iniciales o futuras de recarga

La siguiente tabla ilustra un rastreador de migración funcional:

| Origen (Entorno/Instancia/URL) | Destino (entorno/instancia/URL) | Nombre, tipo del conjunto de migración (inicial o superior) | Tamaño del conjunto de migración (MB) | Asignación de usuarios (Sí/No) | Duración de la extracción (inicio, fin, tiempo necesario) | Duración de la ingesta (inicio, final, tiempo necesario) | Problemas / Resoluciones / Detalles |
|---|---|---|---|---|---|---|---|
|   |   |   |   |   |   |   |   |

## Estrategia y cronología de migración de contenido {#content-strategyand-timeline}

En la siguiente sección se muestran los pasos importantes y las tareas asociadas que se pueden utilizar para formular una estrategia de migración de contenido y una cronología.

![imagen](/help/journey-migration/assets/content-migration2.png)

### Montaje {#fitment}

* Realice una limpieza de revisión, una recopilación de residuos del almacén de datos y comprobaciones de coherencia de datos. Consulte también [Preparación para el lanzamiento](#preparing-for-go-live)
* [Recopilar estadísticas](#gathering-data) AEM acerca del repositorio de origen de la:
   * Tamaño del almacén de segmentos
   * Tamaño del almacén de índice
   * Número de páginas
   * Número de recursos
   * Número de usuarios y grupos
* AEM AEM Saber si las siguientes funciones están habilitadas en la fuente de la (también es necesario en el as a Cloud Service de la):
   * Etiquetado inteligente
   * Búsqueda por similitud
   * Buscar texto en documentos de Word y PDF
* Recopilar el Analizador de prácticas recomendadas [informe](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importe en el [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * AEM Revise la recomendación de autoanálisis para asegurarse de que los as a Cloud Service puedan gestionar los requisitos de almacenamiento.
* Cree un ticket de asistencia de Adobe para cualquier aclaración antes de continuar con el plan de migración.

### Prueba de migración {#proof-of-migration}

* Solicite un clon de producción que:
   * Está en la misma zona de red
   * Proporciona contenido de producción como usuarios y grupos
   * Clones para creación y publicación: un nodo para cada clúster o granja de servidores de publicación
* Elija un subconjunto del contenido que se migra para que:
   * Es una combinación de todos los tipos de contenido disponibles
   * Contiene todos los usuarios y grupos
* Incluye el 25 % del contenido o hasta 1 TB de contenido, el valor que sea menor.
* Ejecutar al menos un y [recargar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) AEM migración, desde el clon de producción al entorno de no producción as a Cloud Service
* Resuelva cualquier problema potencial como:
   * AEM Espacio en disco en el origen de la
   * AEM AEM Conectividad entre la fuente de la y la as a Cloud Service de la
   * Cualquiera [limitaciones relacionadas con la ingesta](go-live.md#known-limitations).
* Registrar el tiempo empleado para [extracción e ingesta](#gathering-data):
   * Saber cuánto contenido se añade por semana
   * Extrapolar los tiempos medidos a partir de la prueba de migración para crear una [plan de migración](#migration-plan).

## Siguientes pasos {#what-is-next}

AEM Después de haber comprendido completamente cómo evaluar si su instalación de la está lista para ser trasladada a la nube, a medida que aprendemos a utilizar las herramientas necesarias para prepararla, es hora de pasar al [fase de lanzamiento](/help/journey-migration/go-live.md).
