---
title: Go-Live
description: Aprenda a realizar la migración una vez que el código y el contenido estén listos para la nube
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 3%

---

# Go-Live {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparación para el lanzamiento"
>abstract="Para garantizar un lanzamiento con éxito y sin problemas en AEM as a Cloud Service, debe planificar los periodos de congelación de código y contenido, las iteraciones de prueba, las recargas de contenido, las pruebas de rendimiento, las pruebas de seguridad y mucho más."

En esta parte del recorrido, aprenderá a planificar y realizar la migración una vez que el código y el contenido estén listos para moverse a AEM as a Cloud Service. Además, aprenderá cuáles son las prácticas recomendadas y las limitaciones conocidas al realizar la migración.

## La historia hasta ahora {#story-so-far}

En las fases anteriores del recorrido:

* Ha aprendido a empezar con el cambio a AEM as a Cloud Service en la página [Introducción](/help/journey-migration/getting-started.md).
* Se determinó si la implementación está lista para moverse a la nube al leer la [fase de preparación](/help/journey-migration/readiness.md)
* Familiarícese con las herramientas y el proceso mediante los cuales puede preparar su nube de contenido y código con la [fase de implementación](/help/journey-migration/implementation.md).

## Objetivo {#objective}

Este documento le ayuda a comprender cómo realizar la migración a AEM as a Cloud Service una vez que esté familiarizado con los pasos anteriores del recorrido. Aprenderá a realizar la migración de producción inicial y las prácticas recomendadas que debe seguir al migrar a AEM as a Cloud Service.

## Migración de producción inicial {#initial-migration}

Antes de realizar la migración de producción, siga los pasos de ajuste y prueba de la migración descritos en la sección [Estrategia y cronología de la migración de contenido](/help/journey-migration/implementation.md##strategy-timeline) de la [fase de implementación](/help/journey-migration/implementation.md).

* Inicie la migración desde producción en función de la experiencia adquirida durante la migración de fase de AEM as a Cloud Service realizada en clones:
   * Autor-Autor
   * Publish-Publish

* Valide el contenido introducido en los niveles de creación y publicación de AEM as a Cloud Service.
* Indique al equipo de creación de contenido que evite mover contenido tanto en el origen como en el destino hasta que se complete la ingesta
* Se puede añadir, editar o eliminar contenido nuevo, pero evite moverlo. Esto se aplica tanto al origen como al destino.
* Registre el [tiempo que se tarda](/help/journey-migration/implementation.md#gathering-data) en la extracción e ingesta completas para obtener una estimación de los plazos futuros de migración de recarga.
* Crear un [planificador de migración](/help/journey-migration/implementation.md#migration-plan) tanto para autor como para publicación.

## Superiores incrementales {#top-up}

Después de la migración inicial desde producción, debe realizar recargas incrementales para asegurarse de que el contenido esté actualizado en la instancia de la nube. Debido a esto, se recomienda seguir estas prácticas recomendadas:

* Recopilar datos sobre la cantidad de contenido. Por ejemplo: por una semana, dos semanas o un mes.
* Asegúrese de planificar las recargas de forma que se eviten más de 48 horas de extracción e ingesta de contenido. Esto se recomienda para que las recargas de contenido se ajusten a un lapso de tiempo de fin de semana.
* Planifique el número de recargas necesarias y utilice esas estimaciones para planificar en torno a la fecha de lanzamiento.

## Identificación de las escalas de tiempo de congelación de contenido y código para la migración {#code-content-freeze}

Como se mencionó anteriormente, tendrá que programar un período de congelación de código y contenido. Utilice las siguientes preguntas para planificar mejor el período de congelación:

* ¿Cuánto tiempo tengo que congelar las actividades de creación de contenido?
* ¿Durante cuánto tiempo debo pedir a mi equipo de envío que deje de añadir nuevas funciones?

Para responder a la primera pregunta, debe tener en cuenta el tiempo que se ha tardado en realizar ejecuciones de prueba en entornos que no son de producción. Para responder a la segunda pregunta, necesita una estrecha colaboración entre el equipo que está agregando nuevas funciones y el equipo que está refactorizando el código. El objetivo es garantizar que todo el código que se añade a la implementación existente también se añada, pruebe e implemente en la rama de los servicios en la nube. Generalmente, significa que la cantidad de código congelado es menor.

Además, debe planificar la congelación de contenido cuando se programe la recarga de contenido final.

## Prácticas recomendadas {#best-practices}

Al planificar o realizar la migración, debe tener en cuenta las siguientes directrices:

* Migrar de Autor a Autor y de Publish a Publish
* Solicite un clon de producción que se pueda utilizar para lo siguiente:
   * Recopilar estadísticas del repositorio
   * Prueba de actividades de migración
   * Preparación del plan de migración
   * Identificar requisitos de congelación de contenido
   * Identifique cualquier necesidad de ampliación en Producción al realizar la migración desde producción

**Prácticas recomendadas de la herramienta de transferencia de contenido**

Asegúrese de que, al lanzarse, ejecute la migración de contenido en producción en lugar de un clon. AEM Un buen enfoque es usar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para la migración inicial y luego ejecutar extracciones de recarga con frecuencia (incluso diariamente) para extraer fragmentos más pequeños y evitar cualquier carga a largo plazo en la fuente de los datos de origen.

Al realizar la migración de producción, debe evitar ejecutar la herramienta de transferencia de contenido desde un clon porque:

* Si un cliente requiere que se migren las versiones de contenido durante las migraciones superiores, la ejecución de la herramienta de transferencia de contenido desde un clon no migra las versiones. Incluso si el clon se vuelve a crear desde el autor activo con frecuencia, cada vez que se crea un clon, se restablecen los puntos de comprobación utilizados por la herramienta de transferencia de contenido para calcular los deltas.
* Dado que un clon no se puede actualizar como un todo, el paquete de consulta ACL debe utilizarse para empaquetar e instalar el contenido que se agrega o edita de la producción al clon. El problema con este enfoque es que cualquier contenido eliminado en la instancia de origen nunca llegará al clon a menos que se elimine manualmente tanto del origen como del clon. Esto introduce la posibilidad de que el contenido eliminado en la producción no se elimine en el clon y en AEM as a Cloud Service.

AEM **Optimizando la carga en el origen de su al realizar la migración de contenido**

AEM Recuerde, la carga en el origen de la es mayor durante la fase de extracción. Tenga en cuenta lo siguiente:

* La herramienta de transferencia de contenido es un proceso Java externo que utiliza un montón de JVM de 4 GB
* AEM La versión que no es AzCopy descarga binarios, los almacena en un espacio temporal en el autor del origen, consumiendo E/S del disco y, a continuación, los carga en el contenedor de Azure, que consume ancho de banda de red
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) transfiere blobs directamente del almacén de blobs al contenedor de Azure, lo que ahorra ancho de banda de red y E/S de disco. La versión de AzCopy sigue utilizando el ancho de banda del disco y de la red para extraer y cargar los datos del almacén de segmentos en el contenedor de Azure
* El proceso de la herramienta de transferencia de contenido es más ligero en los recursos del sistema durante la fase de ingesta, ya que solo transmite registros de ingesta y no hay mucha carga en la instancia de origen en lo que respecta a E/S de disco o ancho de banda de red.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta que toda la ingesta falla si se encuentra cualquiera de las siguientes limitaciones como parte del conjunto de migración extraída:

* Un nodo JCR que tiene un nombre de más de 150 caracteres
* Un nodo JCR de más de 16 MB
* Cualquier usuario/grupo con `rep:AuthorizableID` en proceso de ingesta que ya esté presente en AEM as a Cloud Service
* Si algún recurso extraído e introducido se mueve a una ruta diferente en origen o destino antes de la siguiente iteración de la migración.

## Estado de recursos {#asset-health}

En comparación con la sección anterior, la ingesta **no** produce errores debido a los siguientes problemas con los recursos. Sin embargo, es muy recomendable que realice los pasos adecuados en estos casos:

* Falta cualquier recurso que tenga la representación original
* Cualquier carpeta que tenga un nodo `jcr:content` ausente.

Ambos de los elementos anteriores se identifican y se incluyen en el informe [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md).

## Lista de comprobación para el lanzamiento {#Go-Live-Checklist}

Para obtener más información, consulte la [Lista de comprobación de lanzamiento](/help/journey-onboarding/go-live-checklist.md).

## Siguientes pasos {#what-is-next}

Una vez que sepa cómo realizar la migración a AEM as a Cloud Service, puede consultar la página [Post-Go-Live](/help/journey-migration/post-go-live.md) para que la instancia se ejecute sin problemas.
