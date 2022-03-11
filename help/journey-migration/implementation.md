---
title: Fase de implementación
description: Asegúrese de que el código y el contenido estén listos para la migración a la nube
exl-id: d124f9a5-a754-4ed0-a839-f2968c7c8faa
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 9%

---

# Fase de implementación {#implementation-phase}

En la fase de implementación del recorrido, explorará las herramientas a través de las cuales puede preparar el código y el contenido para que se muevan a AEM as a Cloud Service.

## La historia hasta ahora {#story-so-far}

En las partes anteriores del recorrido, has pasado por [familiarizarse con los cambios en AEM as a Cloud Service](/help/journey-migration/getting-started.md), así como determinar si la implementación está lista para moverse a la nube con la variable [fase de preparación](/help/journey-migration/readiness.md).

Este artículo continúa con consejos sobre cómo utilizar las herramientas proporcionadas por Adobe para asegurarse de que el código y el contenido están listos para moverse a la nube.

## Objetivo {#objective}

El objetivo de este documento es:

* Le presentamos a Cloud Manager, AEM integración continua y el marco de entrega utilizado para implementar código para AEM as a Cloud Service
* Ponga al día con la herramienta de transferencia de contenido
* Describa las herramientas de refactorización de código que debe utilizar para modernizar su código para AEM as a Cloud Service

## Uso de Cloud Manager {#using-cloud-manager}

Antes de comenzar, debe familiarizarse con Cloud Manager, ya que es el único mecanismo para implementar código en AEM as a Cloud Service.

Cloud Manager permite que las organizaciones administren AEM de forma automática en la nube. Incluye un marco de trabajo de integración y entrega continuas (CI/CD) que permite a los equipo de TI y a los asociados de la implementación acelerar la entrega de las personalizaciones o actualizaciones sin poner en riesgo el rendimiento o la seguridad.

Para familiarizarse con el uso de Cloud Manager, consulte los recursos siguientes:

* [Incorporación de Experience Manager as a Cloud Service](/help/onboarding/home.md) para comprender los recursos de autoayuda sobre la integración de Experience Manager as a Cloud Service.

* [Integración de Git con Adobe Cloud Manager](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) para aprender a utilizar un repositorio de Git único para implementar un código.

* [Configuración de Adobe Experience as a Cloud Service](/help/security/ims-support.md#aem-configuration) para obtener información sobre la administración de productos y el acceso de los usuarios en Admin Console.

## Utilice las herramientas proporcionadas por el Adobe para preparar el contenido y la nube de código {#use-tools-to-make-code-and-content-cloud-ready}

Los pasos exactos de la transición a Cloud Service dependen de los sistemas que haya adquirido y de las prácticas de desarrollo de software que siga.

La siguiente figura muestra los pasos principales involucrados en la fase que implica la conversión del código y el contenido para su uso con AEM as a Cloud Service:

![image](/help/journey-migration/assets/exec-image1.png)

Empezaremos a detallar las herramientas que necesita utilizar para lograrlo en los capítulos siguientes.

## Migración de contenido {#content-migration}

Para migrar contenido de la instancia de AEM actual a la instancia de Cloud Service, puede utilizar la herramienta de transferencia de contenido de Adobe.

Con esta herramienta, puede especificar el subconjunto de contenido que desea transferir de la instancia de AEM de origen a la instancia de AEM de Cloud Service.

La migración de contenido es un proceso de varios pasos que requiere planificación, seguimiento y colaboración entre diferentes equipos.

Para obtener un detalle completo sobre cómo funciona la herramienta y cómo se recomienda usarla, consulte la [Documentación de la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md).

## Refactorización de código {#code-refactor}

### Configuración para desarrollo {#set-up-for-development}

Es hora de empezar a refactorizar las funciones existentes para que sean compatibles con los Cloud Services.

Para ello, debe echar un vistazo a la documentación que detalla las herramientas básicas que tendrá que empezar a refactorizar el código:


* Durante la planificación, es aconsejable disponer de una lista de áreas que deben refactorizarse para ser compatibles con AEM as a Cloud Service. Puede revisar [Directrices de desarrollo](/help/implementing/developing/introduction/development-guidelines.md) para obtener más información sobre cómo refactorizar y optimizar el código para el Cloud Service.
* Más información sobre cómo [Administrar configuraciones](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/configurations.html?lang=en#what-is-a-configuration) en AEM as a Cloud Service.
* Obtenga información sobre cómo configurar un entorno de desarrollo local descargando el [SDK as a Cloud Service AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)
* Por último, familiarícese con el [API de Java as a Cloud Service AEM](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Además, también puede:

* Vea este vídeo para comprender cómo instalar el SDK de Dispatcher localmente:

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* Vea este vídeo para comprender cómo configurar el SDK de Dispatcher:

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

### Un cambio en la mentalidad {#a-change-in-mindset}

El desarrollo y la ejecución del código en AEM as a Cloud Service requieren un cambio de mentalidad. Cabe señalar que el código debe ser flexible, especialmente porque una instancia puede detenerse en cualquier momento. Debe tenerse en cuenta que el código que se ejecuta en Cloud Service siempre se realiza en un clúster. Esto significa que siempre hay más de una instancia en ejecución.

Se requieren ciertos cambios para que AEM proyectos de Maven sean compatibles con la nube. AEM as a Cloud Service requiere una separación de *contenido* y *code* en paquetes distintos para su implementación en AEM:

* `/apps` y `/libs` se consideran áreas inmutables de AEM, ya que no se pueden cambiar después de iniciarse AEM (es decir, durante la ejecución). Esto incluye operaciones de creación, actualización o eliminación. Cualquier intento de cambiar un área inmutable durante la ejecución fallará.

* Todo lo demás en el repositorio (por ejemplo, `/content` , `/conf` , `/var` , `/home` , `/etc` , `/oak:index` , `/system` , `/tmp`) son todas áreas mutables, lo que significa que se pueden cambiar durante la ejecución.

Para obtener más información, consulte la [Estructura del paquete recomendado](/help/implementing/developing/introduction/aem-project-content-package-structure.md#recommended-package-structure) documentación.


### Herramientas de migración de Cloud {#cloud-migration-tools}

Adobe proporciona varias herramientas para acelerar algunas de las tareas de refactorización de código. La comprensión de estas herramientas y los problemas que resuelven reducirán la complejidad y el tiempo de migración.

* [Migración del flujo de trabajo de recursos](/help/journey-migration/moving-to-aem-assets/asset-workflow-migration-tool.md), una herramienta que se utiliza para migrar automáticamente los flujos de trabajo de procesamiento de recursos
* [Dispatcher Converter](/help/journey-migration/refactoring-tools/dispatcher-transformation-utility-tools.md), una herramienta que convierte las configuraciones de Dispatcher existentes en un formato listo para AEM as a Cloud Service.
* [Modernizador de repositorio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/repo-modernizer.html?lang=en), una herramienta que toma un proyecto Multimode AEM como entrada y lo convierte en uno as a Cloud Service AEM
* [Conversor de índices](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/moving/refactoring-tools/index-converter.html?lang=en), una herramienta que convierte índices en un formulario compatible con AEM as a Cloud Service
* [Herramientas de modernización](/help/journey-migration/refactoring-tools/aem-modernization-tools.md), un conjunto de utilidades que se puede utilizar para convertir funciones de AEM heredadas a las funciones modernas y compatibles de AEM as a Cloud Service.

Una vez configurado el entorno de desarrollo local, familiarícese con el SDK as a Cloud Service de AEM consultando al [documentación](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

### Programar una congelación de código {#schedule-a-code-freeze}

Para administrar el desarrollo continuo de código en su AEM activo junto con las tareas de refactorización de código como parte de su recorrido de transición, le recomendamos que programe un período de congelación de código hasta que haya completado la reestructuración del proyecto Maven para que sea compatible con AEM as a Cloud Service.

Una vez que se haya realizado la reestructuración del proyecto, puede reanudar el nuevo desarrollo de código basado en esta nueva estructura. Esto reduce los errores de canalización de Cloud Manager durante la implementación y prueba del código.

>[!NOTE]
>Las tareas Transferencia de contenido y Refactorización de código no tienen que realizarse secuencialmente. Estas tareas se pueden hacer independientemente unas de otras. Sin embargo, se necesita una estructura de proyecto correcta para garantizar que el contenido se procese correctamente en el entorno de Cloud Service.

## Prácticas recomendadas para la implementación y prueba de códigos {#best-practices}

La canalización de Cloud Manager admite la ejecución de pruebas que se ejecutan con el entorno de ensayo.

Siga las prácticas recomendadas en los documentos siguientes en relación con las pruebas de calidad del código:

* [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md), un documento que describe el proceso de escritura de secuencias de comandos de prueba y explica el concepto de cobertura recomendada de al menos un 50 %.
* [Comprender las reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) que tiene como objetivo describir las reglas de calidad de código personalizadas ejecutadas por Cloud Manager creadas en función de las prácticas recomendadas de ingeniería de AEM.

## Preparación para Go-Live {#preparing-for-go-live}

La preparación del sistema de origen para la migración implica tareas de nivel de administrador AEM y del sistema. Para empezar, puede verificar que el repositorio de contenido esté en un estado bien mantenido comprobando la variable [limpieza de revisión](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/revision-cleanup.html) y [colección de residuos del almacén de datos](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/data-store-garbage-collection.html) estado de la tarea. Si está ejecutando AEM versión 6.3 (ya que la herramienta de transferencia de contenido es compatible a partir de la versión 6.3), se recomienda realizar la compactación sin conexión, seguida de la colección de residuos del almacén de datos.

[Comprobación de la coherencia de los datos](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/consistency-check.html) se recomienda en todas las versiones de AEM para garantizar que el repositorio de contenido esté en buen estado para iniciar las actividades de migración.

Se requiere acceso a nivel de administrador del sistema para instalar y configurar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)

También se recomienda revisar los recursos, páginas, proyectos AEM, usuarios y grupos que no se utilicen para ahorrar tiempo al migrar. Consulte la [Estado del repositorio de contenido](#repository-health) para obtener más información.

### Estado del repositorio de contenido {#repository-health}

Una vez que acceda a una [clone de producción](#proof-of-migration) se establece continuar para comprobar el estado del repositorio. Como se mencionó en la sección anterior, el objetivo es limpiar y compactar el repositorio en el origen antes de iniciar la migración. Este paso ahorrará mucho tiempo, de lo contrario, en la resolución de problemas una vez que se inicie la migración.

| Elemento de acción | Principales seguimientos |
|---------|----------|
| Usuarios, grupos y permisos | Debe comprender el volumen de usuarios, grupos y complejidad en torno a las suscripciones. Busque oportunidades para limpiar todos los usuarios no utilizados y grupos del origen antes de la migración. |
| Procesamiento de recursos incompleto | Intente completar el procesamiento de los recursos en el sistema de origen antes de iniciar la migración para evitar posibles problemas en AEM migración posterior as a Cloud Service. |
| Estado del contenido | Se recomienda consultar si hay contenido incorrecto y purgarlo antes de iniciar la migración. Por ejemplo, busque recursos o páginas que no tengan representaciones originales o que estén bloqueadas en el procesamiento del flujo de trabajo. Consulte también [Estado de los recursos](#asset-health). |

## Recopilación de datos {#gathering-data}

>[!NOTE]
> La variable [Estrategia y cronología de migración de contenido](#content-strategy-and-timeline) en esta sección se explica cómo extrapolar los datos recopilados y crear un plan de migración.

La recopilación de datos puede ayudarle a planificar las actividades de migración y las tareas asociadas. Los tiempos de extracción e ingesta son especialmente útiles, ya que los puntos de datos pueden asociarse con un tamaño específico del conjunto de migración. Como tal, estos datos pueden extrapolarse para elaborar un plan:

* Cantidad total de tiempo necesario para [extracción](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md)
* Cantidad total de tiempo necesario para [ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
* Cantidad total de tiempo necesario para realizar la recarga [extracción](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)
* Cantidad total de tiempo necesario para realizar la recarga [ingesta](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)

Otro punto de datos importante es la cantidad de tiempo que se tarda en completar la variable [asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md), si esto va acompañado de la migración de contenido. Puede tener en cuenta este punto de datos para obtener estimaciones más realistas, ya que se agregará a la cronología de extracción general y es posible que no sea necesario ejecutarlo durante las recargas.

Estos puntos de datos también pueden ayudarle [Establecer KPI](/help/journey-migration/readiness.md#establish-kpis) y otras tareas relacionadas con la migración.

### Plan de migración {#migration-plan}

En función de los puntos de datos recopilados (consulte más arriba), puede crear un plan de migración que se pueda integrar en un plan de proyecto de macro. Este paso permitirá que todas las partes interesadas principales visualicen y planifiquen las actividades de migración.

La tabla siguiente ilustra un plan de migración típico:

| Iteración de migración | Fecha de inicio | Fecha final estimada | Dependencias | Duración estimada (en días) | Detalles adicionales/elementos de acción |
|---|---|---|---|---|---|
| PRDCLONE-AUTHOR-INITIAL-USRMAP-CSSTAGE-AUTHOR |  |  |  |  |  |
| PRDCLONE-PUBLISH-TOPUP-CSSTAGE-AUTHOR |  |  |  |  |  |

Como puede ver en la tabla anterior, resulta útil seguir un formato de nombre específico para identificar las iteraciones de migración, por ejemplo: **PRDCLONE** para el entorno de AEM de origen , **AUTOR/PUBLICACIÓN** para el entorno as a Cloud Service AEM, **CSSTAGE-AUTHOR** para la instancia as a Cloud Service de AEM, etc.

Algunos detalles importantes que influyen en el plan de migración:

**El número total de extracciones necesarias**

* Las extracciones de autor y publicación en entornos específicos se consideran dos extracciones paralelas, ya que son independientes entre sí.
* Número de extracciones principales basadas en el crecimiento del repositorio en periodos de tiempo específicos.

**Número total de entradas necesarias**

* Es importante capturar este elemento en el plan, ya que un conjunto extraído se puede ingerir en varios entornos de Cloud Service.
* Número de entradas principales.
* La migración de contenido del autor de origen a la instancia de autor del servicio de nube y de la publicación de origen a publicación del Cloud Service es la práctica recomendada para evitar la ingesta de todo el contenido del autor en la publicación del Cloud Service.

### Rastreador de migración {#migration-tracker}

Puede utilizar el rastreador de migración para anotar los tiempos de las ejecuciones inicial y superior. Estos puntos de datos le ayudarán a formular requisitos realistas de congelación de contenido antes del resumen final.

El rastreador también le ayudará a:

* Identificar las desviaciones con respecto al planificador que requieran ajustes en el plan o en las cronologías de lanzamiento
* Proporcionar un estado realista que se pueda usar en todas las comunicaciones necesarias
* Planificar migraciones iniciales o futuras de recarga

La siguiente tabla ilustra un rastreador de migración funcional:

| Origen (Entorno/Instancia/URL) | Destino (Entorno/Instancia/URL) | Nombre del conjunto de migración, Tipo (inicial o superior) | Tamaño del conjunto de migración (MB) | Asignación de usuarios (sí/no) | Duración de la extracción (inicio, fin, tiempo empleado) | Duración de la ingesta (inicio, fin, tiempo necesario) | Problemas / Resoluciones / Detalles |
|---|---|---|---|---|---|---|---|
|  |  |  |  |  |  |  |  |

## Estrategia y cronología de migración de contenido {#content-strategyand-timeline}

En la siguiente sección se muestran los pasos importantes y las tareas asociadas que se pueden utilizar para formular una estrategia y una cronología de migración de contenido.

![image](/help/journey-migration/assets/content-migration2.png)

### Contratación {#fitment}

* Realice una limpieza de revisión, recopilación de residuos del almacén de datos y comprobaciones de coherencia de los datos. Consulte también [Preparación para Go-Live](#preparing-for-go-live)
* [Recopilar estadísticas](#gathering-data) acerca del repositorio de origen de AEM:
   * Tamaño del almacén de segmentos
   * Tamaño del almacén de índices
   * Número de páginas
   * Número de activos
   * Número de usuarios y grupos
* Sepa si las siguientes funciones están habilitadas en el origen de AEM (también se requiere en AEM as a Cloud Service):
   * Etiquetado inteligente
   * Búsqueda por similitudes
   * Buscar texto que contenga texto en documentos de Word y PDF
* Recopilar el Analizador de prácticas recomendadas [informe](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md)
* Importar en el [Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/introduction/overview-cam.md)
   * Revise la recomendación de autoanálisis para asegurarse de que AEM as a Cloud Service pueda manejar los requerimientos de almacenamiento de información.
* Cree un ticket de soporte de Adobe para cualquier aclaración antes de continuar con el plan de migración.

### Prueba de la migración {#proof-of-migration}

* Solicite un clon de producción que:
   * Está en la misma zona de red
   * Proporcionará contenido de producción como usuarios y grupos
   * Creación y publicación de clones: un nodo cada uno en el caso de un clúster o una granja de servidores de publicación
* Elija un subconjunto del contenido que se migrará para que:
   * Es una mezcla de todos los tipos de contenido disponibles
   * Contiene todos los usuarios y grupos en caso de que [asignación de usuarios](/help/journey-migration/content-transfer-tool/user-mapping-tool/overview-user-mapping-tool.md) es obligatorio
* Incluye el 25% del contenido o hasta 1 TB de contenido, lo que sea menos.
* Ejecute al menos un completo y [arriba](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) migración, desde el clon de producción al entorno de no producción as a Cloud Service AEM
* Resuelva cualquier problema potencial como:
   * Espacio en disco en el origen AEM
   * Conectividad entre la fuente de AEM y AEM as a Cloud Service
   * Cualquiera [limitaciones relacionadas con la ingesta](go-live.md#known-limitations).
* Registrar el tiempo que se tarda en [extracción e ingesta](#gathering-data):
   * Conozca cuánto contenido se añade por semana
   * Extraiga los tiempos medidos a partir de la prueba de migración para crear un [plan de migración](#migration-plan).

## Siguientes pasos {#what-is-next}

Una vez que haya comprendido completamente cómo evaluar si la instalación de AEM está lista para ser trasladada a la nube, a medida que aprendemos a utilizar las herramientas necesarias para prepararla, es hora de pasar al [fase de lanzamiento](/help/journey-migration/go-live.md).
