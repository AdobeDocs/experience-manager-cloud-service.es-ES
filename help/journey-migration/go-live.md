---
title: Go-Live
description: Obtenga información sobre cómo realizar la migración una vez que el código y el contenido estén listos para la nube
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 30acb844ee4021b3e14011b548825c864de8903d
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 4%

---

# Go-Live {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparación para el lanzamiento"
>abstract="Para garantizar un lanzamiento con éxito y sin problemas en AEM as a Cloud Service, debe planificar los periodos de congelación de código y contenido, las iteraciones de prueba, las recargas de contenido, las pruebas de rendimiento, las pruebas de seguridad y mucho más."

En esta parte del recorrido, aprenderá a planificar y realizar la migración una vez que el código y el contenido estén listos para moverse a AEM as a Cloud Service. Además, aprenderá cuáles son las prácticas recomendadas y las limitaciones conocidas al realizar la migración.

## La historia hasta ahora {#story-so-far}

En las fases anteriores del recorrido:

* Aprendió a empezar con el paso a AEM as a Cloud Service en la [Introducción](/help/journey-migration/getting-started.md) página.
* Se determinó si la implementación está lista para moverse a la nube leyendo el informe [Fase de preparación](/help/journey-migration/readiness.md)
* Familiarícese con las herramientas y el proceso a través del cual puede preparar su código y la nube de contenido con el [Fase de implementación](/help/journey-migration/implementation.md).

## Objetivo {#objective}

Este documento le ayudará a comprender cómo realizar la migración a AEM as a Cloud Service una vez que esté familiarizado con los pasos anteriores del recorrido. Aprenderá a realizar la migración inicial de producción, así como las prácticas recomendadas a seguir al migrar a AEM as a Cloud Service.

## Migración de producción inicial {#initial-migration}

Antes de poder realizar la migración de producción, siga los pasos de ajuste y prueba de la migración que se describen en la sección [Estrategia y cronología de migración de contenido](/help/journey-migration/implementation.md##strategy-timeline) de la sección [Fase de implementación](/help/journey-migration/implementation.md).

* Inicie la migración desde la producción en función de la experiencia adquirida durante la migración de la fase as a Cloud Service AEM realizada en los clones:
   * Autor-Autor
   * Publicación

* Valide el contenido introducido en los niveles de creación y publicación as a Cloud Service de AEM.
* Indica al equipo de creación de contenido que evite mover contenido tanto en el origen como en el destino hasta que se complete la ingesta
* Se puede añadir, editar o eliminar contenido nuevo, pero evite moverlo. Esto se aplica tanto al origen como al destino.
* Registre el [tiempo empleado](/help/journey-migration/implementation.md#gathering-data) para la extracción e ingesta completas con una estimación de futuros cronogramas de migración adicionales.
* Cree un [planificador de migración](/help/journey-migration/implementation.md#migration-plan) tanto para autor como para publicación.

## Ventajas principales incrementales {#top-up}

Después de la migración inicial desde la producción, debe realizar recargas incrementales para asegurarse de que el contenido se actualiza en la instancia de la nube. Por este motivo, se recomienda seguir estas prácticas recomendadas:

* Recopile datos sobre la cantidad de contenido. Por ejemplo: por semana, dos semanas o un mes.
* Asegúrese de planificar las recargas de forma que evite más de 48 horas de extracción e ingesta de contenido. Esto se recomienda para que las recargas de contenido encajen en un lapso de tiempo de fin de semana.
* Planifique el número de recargas necesarias y utilice esas estimaciones para planificar la fecha de lanzamiento.

## Identificar las cronologías de código y congelación de contenido para la migración {#code-content-freeze}

Como se mencionó anteriormente, tendrá que programar un período de congelación de código y contenido. Utilice las siguientes preguntas para ayudarle a planificar el periodo de congelación:

* ¿Cuánto tiempo debo congelar las actividades de creación de contenido?
* ¿Durante cuánto tiempo debo pedir a mi equipo de envío que deje de agregar nuevas funciones?

Para responder a la primera pregunta, debe tener en cuenta el tiempo que se ha tardado en realizar ejecuciones de prueba en entornos que no sean de producción. Para responder a la segunda pregunta, necesita una estrecha colaboración entre el equipo que agrega nuevas funciones y el equipo que refactoriza el código. El objetivo debe ser asegurarse de que todo el código que se agrega a la implementación existente también se agregue, pruebe e implemente en la rama de servicios en la nube. En términos generales, esto significa que la cantidad de congelación de código será menor.

Además, debe planificar un congelamiento de contenido cuando se programe el resumen final del contenido.

## Prácticas recomendadas {#best-practices}

Al planificar o realizar la migración, debe tener en cuenta las siguientes directrices:

* Migrar de autor a autor y publicar para publicación
* Solicite un clon de producción que se pueda utilizar para:
   * Capturar estadísticas del repositorio
   * Prueba de las actividades de migración
   * Preparación del plan de migración
   * Identificar los requisitos de congelación de contenido
   * Identifique cualquier necesidad de ampliación en Producción al realizar la migración desde la producción

**Prácticas recomendadas de la herramienta de transferencia de contenido**

Asegúrese de que, al activarse, ejecute la migración de contenido en producción en lugar de en un clon. Un buen enfoque es usar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) para la migración inicial y luego ejecute las extracciones superiores con frecuencia (incluso diariamente) para extraer trozos más pequeños y para evitar cualquier carga a largo plazo en la AEM de origen.

Al realizar la migración de producción, debe evitar ejecutar la herramienta de transferencia de contenido desde un clon porque:

* Si un cliente requiere que las versiones de contenido se migren durante las migraciones superiores, la ejecución de la herramienta de transferencia de contenido desde un clon no migra las versiones. Incluso si el clon se vuelve a crear con frecuencia desde el autor activo, cada vez que se crea un clon se restablecen los puntos de comprobación que utilizará la herramienta de transferencia de contenido para calcular los deltas.
* Dado que un clon no se puede actualizar como un todo, el paquete ACL Query debe utilizarse para empaquetar e instalar el contenido que se está añadiendo o editando de producción a clon. El problema con este enfoque es que cualquier contenido eliminado en la instancia de origen nunca llegará al clon a menos que se elimine manualmente tanto del origen como del clon. Esto introduce la posibilidad de que el contenido eliminado en la producción no se elimine en el clon y AEM as a Cloud Service.

**Optimización de la carga en el origen de AEM al realizar la migración de contenido**

Recuerde que la carga en el origen de AEM será buena durante la fase de extracción. Debe tener en cuenta que:

* La herramienta de transferencia de contenido es un proceso Java externo que utiliza un JVM Heap de 4 GB
* La versión que no es de AzCopy descarga binarios, los almacena en un espacio temporal en el autor de la AEM de origen, lo que consume E/S de disco y, a continuación, carga en el contenedor de Azure que consume ancho de banda de la red
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) transfiere blobs directamente desde el almacén de blobs al contenedor de Azure, que ahorra E/S de disco y ancho de banda de red. La versión de AzCopy todavía utiliza el disco y el ancho de banda de red para extraer y cargar los datos del almacén de segmentos en el contenedor de Azure
* El proceso de la herramienta de transferencia de contenido es más ligero en los recursos del sistema durante la fase de ingesta, ya que solo transmite registros de ingesta y no hay mucha carga en la instancia de origen en lo que se refiere a E/S de disco o ancho de banda de red.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta que la ingesta completa falla si se encuentra alguna de las siguientes limitaciones como parte del conjunto de migración extraído:

* Nodo JCR con un nombre superior a 150 caracteres
* Nodo JCR mayor de 16 MB
* Cualquier usuario o grupo con `rep:AuthorizableID` ingesta que ya está presente en AEM as a Cloud Service
* Si cualquier recurso extraído e ingerido se mueve a una ruta diferente, ya sea en el origen o en el destino, antes de la siguiente iteración de la migración.

## Estado de los recursos {#asset-health}

Comparado con la sección anterior a la ingesta **no** falla debido a las siguientes preocupaciones sobre los activos. Sin embargo, es muy recomendable que realice los pasos adecuados en estos casos:

* Falta cualquier recurso que tenga la representación original
* Cualquier carpeta que falte `jcr:content` nodo .

Los dos elementos anteriores se identificarán y presentarán informes en la [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) informe.

## Lista de comprobación de Go-Live {#Go-Live-Checklist}

Revise esta lista de actividades para asegurarse de que realiza una migración sin problemas y sin problemas.

* Ejecute una canalización de producción completa con pruebas funcionales y de interfaz de usuario para garantizar un **always current** AEM experiencia del producto. Consulte los siguientes recursos.
   * [Actualizaciones de la versión de AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Prueba funcional personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Pruebas de IU](/help/implementing/cloud-manager/ui-testing.md)
* Migre contenido a producción y asegúrese de que hay un subconjunto relevante disponible en el entorno de ensayo para realizar pruebas.
   * Tenga en cuenta que las prácticas recomendadas de DevOps para AEM implican que el código sube del desarrollo al entorno de producción mientras que el contenido baja de los entornos de producción.
* Programe un período de congelación de contenido y código.
   * Consulte también la sección [Cronologías de bloqueo de código y contenido para la migración](#code-content-freeze)
* Realice el resumen final del contenido.
* Valide las configuraciones de Dispatcher.
   * Utilice un validador de Dispatcher local que facilite la configuración, validación y simulación del Dispatcher localmente
      * [Configure las herramientas de Dispatcher locales.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Revise detenidamente la configuración del host virtual.
      * La solución más sencilla (y predeterminada) es incluir `ServerAlias *` en el archivo host virtual de `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Esto permitirá que funcionen los alias de host utilizados por las pruebas funcionales del producto, la invalidación de la caché de Dispatcher y los clones.
      * Sin embargo, si `ServerAlias *` no es aceptable, como mínimo lo siguiente `ServerAlias` además de los dominios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL y DNS.
   * Si está utilizando su propia CDN, introduzca un ticket de soporte para configurar el enrutamiento adecuado.
      * Consulte la sección [La CDN del cliente apunta a AEM CDN administrada](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) en la documentación de CDN para obtener más información.
      * Deberá configurar SSL y DNS según la documentación de su proveedor de CDN.
   * Si no utiliza una CDN adicional, administre SSL y DNS según la siguiente documentación:
      * Administración de certificados SSL
         * [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Administración del certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Administración de nombres de dominio personalizados (DNS)
         * Para asegurarse de que el cambio de DNS no introduzca problemas inesperados, es mejor crear un subdominio de prueba al que conectar la instancia de producción antes de lanzarse y realizar una ronda de pruebas de UAT. Por lo tanto, si su dominio es ejemplo.com, puede crear un subdominio test.example.com y aplicarlo a la producción. Durante la prueba de UAT del dominio, querrá buscar cosas como la redirección de vínculos adecuada, el almacenamiento en caché y las configuraciones de Dispatcher.
         * [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Recuerde validar el conjunto TTL para su registro DNS.
      * El TTL es la cantidad de tiempo que un registro DNS permanece en una caché antes de solicitar al servidor una actualización.
      * Si tiene un TTL muy alto, las actualizaciones del registro DNS tardarán más en propagarse.
* Ejecute pruebas de rendimiento y seguridad que cumplan con los requisitos y objetivos de su negocio.
* Realice un corte y asegúrese de que el lanzamiento real se realiza sin ninguna implementación nueva o actualización de contenido.
* Crear perfiles de notificación de usuario Admin Console. Consulte [Perfiles de notificación](/help/journey-onboarding/notification-profiles.md)

Siempre puede hacer referencia a la lista en caso de que necesite volver a calibrar las tareas mientras realiza la migración.

## Siguientes pasos {#what-is-next}

Una vez que sepa cómo realizar la migración a AEM as a Cloud Service, puede comprobar la variable [Publicar Go-Live](/help/journey-migration/post-go-live.md) para mantener la instancia funcionando sin problemas.
