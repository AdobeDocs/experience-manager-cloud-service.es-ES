---
title: Go-Live
description: Aprenda a realizar la migración una vez que el código y el contenido estén listos para la nube
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
source-git-commit: 75d702cf45e38da4b7259907e7f707b6f18bd428
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 4%

---

# Go-Live {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Preparación para el lanzamiento"
>abstract="Para garantizar un lanzamiento con éxito y sin problemas en AEM as a Cloud Service, debe planificar los periodos de congelación de código y contenido, las iteraciones de prueba, las recargas de contenido, las pruebas de rendimiento, las pruebas de seguridad y mucho más."

En esta parte del recorrido AEM, aprenderá a planificar y realizar la migración una vez que el código y el contenido estén listos para transferirse a la as a Cloud Service. Además, aprenderá cuáles son las prácticas recomendadas y las limitaciones conocidas al realizar la migración.

## La historia hasta ahora {#story-so-far}

En las fases anteriores del recorrido:

* AEM Ha aprendido a empezar con el paso a la as a Cloud Service de la en [Primeros pasos](/help/journey-migration/getting-started.md) página.
* Se ha determinado si la implementación está lista para moverse a la nube mediante la lectura del [Fase de preparación](/help/journey-migration/readiness.md)
* Familiarícese con las herramientas y el proceso mediante los cuales puede preparar su código y nube de contenido con [Fase de implementación](/help/journey-migration/implementation.md).

## Objetivo {#objective}

AEM Este documento le ayuda a comprender cómo realizar la migración a as a Cloud Service una vez que esté familiarizado con los pasos anteriores del recorrido de trabajo. AEM Aprenderá a realizar la migración inicial de la producción y las prácticas recomendadas que debe seguir al migrar a la producción as a Cloud Service de.

## Migración de producción inicial {#initial-migration}

Antes de realizar la migración de producción, siga los pasos de ajuste y prueba de migración descritos en la sección [Estrategia y cronología de migración de contenido](/help/journey-migration/implementation.md##strategy-timeline) de la sección [Fase de implementación](/help/journey-migration/implementation.md).

* AEM Inicie la migración desde producción en función de la experiencia adquirida durante la migración en fase as a Cloud Service de la realizada en clones:
   * Autor-Autor
   * Publish-Publish

* AEM Valide el contenido introducido en los niveles de creación y publicación as a Cloud Service de la.
* Indique al equipo de creación de contenido que evite mover contenido tanto en el origen como en el destino hasta que se complete la ingesta
* Se puede añadir, editar o eliminar contenido nuevo, pero evite moverlo. Esto se aplica tanto al origen como al destino.
* Registre el [tiempo empleado](/help/journey-migration/implementation.md#gathering-data) para que la extracción y la ingesta completas tengan una estimación de los plazos de migración adicionales futuros.
* Crear un [planificador de migración](/help/journey-migration/implementation.md#migration-plan) para creación y publicación.

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

* Migrar de Autor a Autor y Publicar para Publicar
* Solicite un clon de producción que se pueda utilizar para lo siguiente:
   * Recopilar estadísticas del repositorio
   * Prueba de actividades de migración
   * Preparación del plan de migración
   * Identificar requisitos de congelación de contenido
   * Identifique cualquier necesidad de ampliación en Producción al realizar la migración desde producción

**Prácticas recomendadas de la herramienta de transferencia de contenido**

Asegúrese de que, al lanzarse, ejecute la migración de contenido en producción en lugar de un clon. Un buen enfoque es utilizar [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) AEM para la migración inicial y, a continuación, ejecute extracciones de recarga con frecuencia (incluso diariamente) para extraer fragmentos más pequeños y evitar cualquier carga a largo plazo en el origen de la.

Al realizar la migración de producción, debe evitar ejecutar la herramienta de transferencia de contenido desde un clon porque:

* Si un cliente requiere que se migren las versiones de contenido durante las migraciones superiores, la ejecución de la herramienta de transferencia de contenido desde un clon no migra las versiones. Incluso si el clon se vuelve a crear desde el autor activo con frecuencia, cada vez que se crea un clon, se restablecen los puntos de comprobación utilizados por la herramienta de transferencia de contenido para calcular los deltas.
* Dado que un clon no se puede actualizar como un todo, el paquete de consulta ACL debe utilizarse para empaquetar e instalar el contenido que se agrega o edita de la producción al clon. El problema con este enfoque es que cualquier contenido eliminado en la instancia de origen nunca llegará al clon a menos que se elimine manualmente tanto del origen como del clon. AEM Esto introduce la posibilidad de que el contenido eliminado en la producción no se elimine en el clon y la as a Cloud Service.

**AEM Optimización de la carga en el origen de la al realizar la migración de contenido**

AEM Recuerde, la carga en el origen de la es mayor durante la fase de extracción. Tenga en cuenta lo siguiente:

* La herramienta de transferencia de contenido es un proceso Java externo que utiliza un montón de JVM de 4 GB
* AEM La versión que no es AzCopy descarga binarios, los almacena en un espacio temporal en el autor del origen, consumiendo E/S del disco y, a continuación, los carga en el contenedor de Azure, que consume ancho de banda de red
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) transfiere blobs directamente desde el almacén de blobs al contenedor de Azure, lo que ahorra ancho de banda de red y E/S de disco. La versión de AzCopy sigue utilizando el ancho de banda del disco y de la red para extraer y cargar los datos del almacén de segmentos en el contenedor de Azure
* El proceso de la herramienta de transferencia de contenido es más ligero en los recursos del sistema durante la fase de ingesta, ya que solo transmite registros de ingesta y no hay mucha carga en la instancia de origen en lo que respecta a E/S de disco o ancho de banda de red.

## Limitaciones conocidas {#known-limitations}

Tenga en cuenta que toda la ingesta falla si se encuentra cualquiera de las siguientes limitaciones como parte del conjunto de migración extraída:

* Un nodo JCR que tiene un nombre de más de 150 caracteres
* Un nodo JCR de más de 16 MB
* Cualquier usuario/grupo con `rep:AuthorizableID` AEM está siendo ingerido que ya está presente en el as a Cloud Service
* Si algún recurso extraído e introducido se mueve a una ruta diferente en origen o destino antes de la siguiente iteración de la migración.

## Estado de recursos {#asset-health}

En comparación con la sección anterior a la ingesta **no tiene** se produce un error debido a los siguientes problemas de recursos. Sin embargo, es muy recomendable que realice los pasos adecuados en estos casos:

* Falta cualquier recurso que tenga la representación original
* Cualquier carpeta que tenga un `jcr:content` nodo.

Ambos elementos se identifican y se comunican en la variable [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) informe.

## Lista de comprobación de lanzamiento {#Go-Live-Checklist}

Revise esta lista de actividades para asegurarse de que la migración se realiza correctamente.

* Ejecute una canalización de producción integral con pruebas funcionales y de interfaz de usuario para garantizar un **siempre actual** AEM Experiencia del producto de la. Consulte los siguientes recursos.
   * [Actualizaciones de la versión de AEM](/help/implementing/deploying/aem-version-updates.md)
   * [Prueba funcional personalizada](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [Pruebas de IU](/help/implementing/cloud-manager/ui-testing.md)
* Migre el contenido a producción y asegúrese de que haya un subconjunto relevante disponible en el ensayo para realizar pruebas.
   * AEM Las prácticas recomendadas de DevOps para los entornos de producción implican que el código asciende desde el desarrollo al entorno de producción, mientras que el contenido baja desde los entornos de producción.
* Programe un período de congelación de contenido y código.
   * Consulte también la sección [Cronología de congelación de código y contenido para la migración](#code-content-freeze)
* Realice la recarga final del contenido.
* Valide las configuraciones de Dispatcher.
   * Utilizar un validador de Dispatcher local que facilite la configuración, validación y simulación del Dispatcher localmente
      * [Configure las herramientas locales de Dispatcher.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)
   * Revise detenidamente la configuración del host virtual.
      * La solución más fácil (y predeterminada) es incluir `ServerAlias *` en el archivo host virtual en el `/dispatcher/src/conf.d/available_vhostsfolder`.
         * Esto permitirá que funcionen los alias de host utilizados por las pruebas funcionales del producto, la invalidación de la caché del despachante y los clones.
      * Sin embargo, si `ServerAlias *` no es aceptable, como mínimo lo siguiente `ServerAlias` se deben permitir las entradas además de los dominios personalizados:
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* Configure CDN, SSL y DNS.
   * Si utiliza su propia CDN, introduzca un ticket de asistencia para configurar el enrutamiento adecuado.
      * Consulte la sección [AEM Los puntos de CDN del cliente a CDN administrada de](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) en la documentación de CDN para obtener más información.
      * Configure SSL y DNS según la documentación de su proveedor de CDN.
   * Si no utiliza una CDN adicional, administre SSL y DNS según la siguiente documentación:
      * Administración de certificados SSL
         * [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * Administración de nombres de dominio personalizados (DNS)
         * Para asegurarse de que la migración a DNS no introducirá problemas inesperados, es mejor crear un subdominio de prueba al que conectar la instancia de producción antes de publicarla y realizar una ronda de pruebas UAT. Por lo tanto, si el dominio es example.com, puede crear un subdominio test.example.com y aplicarlo a la producción. Durante la prueba UAT del dominio, querrá buscar cosas como la redirección de vínculos adecuada, el almacenamiento en caché y las configuraciones de Dispatcher.
         * [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [Administrar el nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * Recuerde validar el TTL establecido para el registro DNS.
      * El TTL es la cantidad de tiempo que un registro DNS permanece en una caché antes de solicitar una actualización al servidor.
      * Si tiene un TTL muy alto, las actualizaciones del registro DNS tardarán más en propagarse.
* Ejecute pruebas de rendimiento y seguridad que cumplan los requisitos y objetivos de su empresa.
   * Realizar pruebas en el entorno de ensayo.  Tiene el mismo tamaño que la producción.
   * Los entornos de desarrollo no tienen el mismo tamaño que los de fase y producción.
* Pase el ratón por encima y asegúrese de que el go-live real se realiza sin ninguna implementación nueva o actualización de contenido.
* Crear perfiles de notificación de usuario Admin Console. Consulte [Perfiles de notificación](/help/journey-onboarding/notification-profiles.md)

Siempre puede hacer referencia a la lista en caso de que necesite volver a calibrar las tareas mientras realiza la migración.

## Siguientes pasos {#what-is-next}

AEM Una vez que sepa cómo llevar a cabo la migración a la as a Cloud Service, puede consultar la sección de [Post-Go-Live](/help/journey-migration/post-go-live.md) para que su instancia se ejecute sin problemas.
