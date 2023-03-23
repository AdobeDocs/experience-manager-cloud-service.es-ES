---
title: Fase de preparación
description: Obtenga información sobre los pasos que debe seguir para asegurarse de que la instalación de AEM está lista para moverse a la nube
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 7%

---

# Fase de preparación {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planificación de la transición"
>abstract="Antes de comenzar el viaje de transición a Cloud Service, debe familiarizarse con AEM as a Cloud Service, revisar los cambios importantes que se le han realizado y también las funciones que se han sustituido o están en desuso."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Analizador de prácticas recomendadas"

En esta fase del Recorrido as a Cloud Service de Migración de AEM, se familiarizará con AEM as a Cloud Service, revisará los cambios notables que ha introducido y comprenderá lo que se necesita para planificar una migración exitosa a la nube.

## La historia hasta ahora {#story-so-far}

El documento anterior, [Introducción al paso a AEM as a Cloud Service](/help/journey-migration/getting-started.md), describe una lista de las fases que debe pasar para migrar a AEM as a Cloud Service, así como los beneficios de hacerlo.

## Objetivo {#objective}

Este documento le ayuda a comprender qué factores debe tener en cuenta para asegurarse de que la instalación de AEM está lista para moverse a la nube:

* Obtenga información sobre cambios importantes y funciones obsoletas
* Obtenga información sobre cómo planificar la migración a AEM as a Cloud Service

## Revise los cambios más importantes en la arquitectura as a Cloud Service AEM {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service ofrece muchas nuevas funciones y posibilidades para la gestión de sus proyectos AEM.

Junto con estas mejoras, se han introducido varias diferencias entre las instalaciones locales de AEM y Adobe Managed Services, en comparación con AEM as a Cloud Service.

La lista de elementos de la tabla siguiente es el subconjunto de los cambios más relevantes para una migración a AEM as a Cloud Service. Puede consultar la lista completa de cambios importantes [here](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>¿Qué ha cambiado?</th>
    <th>Referencia</th>
    <th>Principales seguimientos</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separe los filtros mutables e inmutables en los paquetes correspondientes</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">AEM cambios importantes as a Cloud Service</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM estructura del proyecto para AEM as a Cloud Service</a></td>
    <td>Un paquete único que se puede implementar en AEM as a Cloud Service puede tener subpaquetes, principalmente para contener contenido mutable e inmutable separado en sus propios paquetes.</td>
  </tr>
  <tr>
    <td>Punto de repo</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentación de Apache Sling RepoInit</a></td>
    <td>Las secuencias de comandos de informe son la práctica recomendada para crear cualquier estructura de nodo inicial, usuario, grupo o usuario de servicio. Dado que estos scripts se pueden dirigir mediante el modo de ejecución y se pueden administrar mediante la implementación del paquete de código, proporcionan mucha flexibilidad para lograr las tareas de inicialización del repositorio.</td>
  </tr>
  <tr>
    <td>No se permiten los modos de ejecución personalizados</td>
    <td></td>
    <td>Solo se admiten los modos de ejecución proporcionados fuera de la caja con AEM as a Cloud Service.<br>Cuando se añaden entornos de desarrollo adicionales, todos se vinculan al modo de ejecución "dev".</td>
  </tr>
  <tr>
    <td>La ejecución de canalización de Cloud Manager es la única forma de implementar</td>
    <td></td>
    <td>En AEM as a Cloud Service, no se permite el acceso a /system/console, por lo que todas las configuraciones de OSGi deben formar parte del código y implementarse como código.<br>Las configuraciones de OSGi están disponibles en modo de solo lectura para su visualización a través de Developer Console a través de Cloud Manager</td>
  </tr>
  <tr>
    <td>Los agentes de replicación se reemplazan con Sling Content Distribution</td>
    <td></td>
    <td>El concepto del agente de replicación se reemplaza por Sing Content Distribution. Si hay personalizaciones que aprovechan los agentes de replicación, deben rediseñarse.<br>No se admite la replicación inversa</td>
  </tr>
  <tr>
    <td>CRX/DE y Administrador de paquetes</td>
    <td></td>
    <td>CRX/DE solo se permite en el entorno de desarrollo.<br>El Administrador de paquetes es accesible en todas las instancias de creación, pero los paquetes que se van a implementar solo deben contener contenido mutable ( por ejemplo: /content o /conf)</td>
  </tr>
  <tr>
    <td>CDN integrada y obtenga su propia CDN</td>
    <td></td>
    <td>AEM as a Cloud Service incluye la CDN para todos los entornos, que está optimizada para la mayoría de los casos de uso.<br>Si desea configurar su propia CDN, debe enviar una solicitud al soporte de Adobe para que sea aprobada.<br>Si se aprueba, la CDN señalará a Finfinito y no a AEM instancias en ningún entorno.</td>
  </tr>
  <tr>
    <td>Trabajos de larga duración</td>
    <td></td>
    <td>Evite ejecutar trabajos de larga duración, como Sling Schedulers o trabajos Cron, ya que las AEM instancias que se ejecutan en los contenedores pueden ir y venir en cualquier momento.<br>Reconsidere estas funcionalidades para descargarlas en Adobe I/O.</td>
  </tr>
  <tr>
    <td>Cambiar a operaciones asincrónicas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">Configuración de operaciones asincrónicas</a></td>
    <td>Para mejorar el rendimiento general de los entornos, determinadas operaciones se ejecutan en modo asíncrono. Los trabajos asincrónicos se pondrán en cola y se ejecutarán cuando los recursos del sistema estén disponibles.</td>
  </tr>
  <tr>
    <td>Estrategias de integración y autenticación basadas en tokens</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">Generación de tokens de acceso para API del lado del servidor</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Tutorial de autenticación basada en tokens</a></td>
    <td>Es habitual que los sistemas externos a AEM intenten realizar operaciones HTTP dentro de AEM.<br>El método recomendado es implementar las estrategias descritas aquí en lugar de depender de la creación de nombres de usuario locales con contraseñas en AEM.</td>
  </tr>
  <tr>
    <td>Uso de E/S de archivo/disco</td>
    <td></td>
    <td>Como no hay garantía de cuánto espacio en disco se asigna y las instancias de los contenedores van y vienen, no es aconsejable utilizar operaciones de E/S de archivo para escribir o leer desde el disco conectado a la instancia de AEM.</td>
  </tr>
  <tr>
    <td>Flujo de trabajo de recursos de actualización de DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Servicio de asset compute</a></td>
    <td>Los pasos de procesamiento de contenido que forman parte del flujo de trabajo de recursos de actualización de DAM ahora se sustituyen por el servicio de Asset compute</td>
  </tr>
  <tr>
    <td>Métodos de carga de recursos y pasos de proceso de flujo de trabajo admitidos en AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">Cargar comparaciones de API y pasos de proceso de WF admitidos</a></td>
    <td>En AEM as a Cloud Service, durante la carga o descarga de un recurso, el recurso se transmite directamente dentro o fuera del almacenamiento binario.</br>No todos los pasos del proceso de flujo de trabajo son compatibles con AEMaaCS.</td>
  </tr>
  <tr>
    <td>Lanzadores de flujo de trabajo</td>
    <td></td>
    <td>Elimine de su código cualquier iniciador de flujo de trabajo que active OOTB o el flujo de trabajo personalizado de recursos de actualización de DAM.</br>Todos los recursos cargados en AEM as a Cloud Service serán procesados por el servicio de procesamiento de recursos. Para ver los pasos personalizados, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> Flujos de trabajo posteriores al procesamiento</a> sobre cómo configurar y configurar flujos de trabajo posteriores al procesamiento.</td>
  </tr>
  <tr>
    <td>Pasos de representación personalizados</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">Perfiles de procesamiento</a></td>
    <td>Cualquier generación de representación personalizada, conversiones de imagen o codificaciones de vídeo debe descargarse en el servicio de procesamiento de recursos creando los perfiles de procesamiento correspondientes.</td>
  </tr>
  <tr>
    <td>Búsqueda de contenido e indexación</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">Búsqueda de contenido e indexación de cambios</a></td>
    <td>Hay cambios considerables en el procesamiento subyacente de los índices y cuando se está iniciando.<br>Comprenda y refactorice completamente los índices Oak antes de administrarlos en el código que implementará.</td>
  </tr>
  <tr>
    <td>No todas las tareas de mantenimiento son configurables</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEM tareas de mantenimiento as a Cloud Service</a></td>
    <td>Solo puede configurar ciertas tareas de mantenimiento con AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>Cambios en el repositorio de publicación</td>
    <td></td>
    <td>No se permiten cambios directos en el repositorio de Publish, excepto en los que se encuentran en /home. Siempre se recomienda realizar los cambios en author y distribuirlos. Todos los cambios de código y configuración deben implementarse a través de la canalización correspondiente de Cloud Manager.</td>
  </tr>
  <tr>
    <td>Configuraciones y almacenamiento en caché de Dispatcher</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">Dispatcher en la nube</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">Administración de caché<br></td>
    <td>Las configuraciones de Dispatcher deben seguir una estructura específica.<br>Las configuraciones deben administrarse como parte del código e implementarse mediante la canalización de Cloud Manager.</td>
  </tr>
  <tr>
    <td>Copia de seguridad y restauración</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">Copia de seguridad y restauración as a Cloud Service AEM</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Cambios en la autenticación</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es">Compatibilidad con IMS para AEM as a Cloud Service</td>
    <td>Si anteriormente estaba utilizando la integración SAML 2.0 tanto en el autor como en la publicación antes de pasar a Cloud Service, el cambio principal es que AEM autor as a Cloud Service solo se integra con Adobe IMS. Sin embargo, AEM nivel de publicación as a Cloud Service aún puede aprovechar SAML u otras integraciones de autenticación. AEM as a Cloud Service ofrece compatibilidad con la autenticación IMS solo para usuarios creadores, administradores y desarrolladores. La autenticación IMS no ofrece compatibilidad con usuarios finales externos de sitios de clientes como visitantes del sitio.</td>
  </tr>
</tbody>
</table>

## Funciones en desuso {#deprecated-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

Le recomendamos que consulte la [Funciones obsoletas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) para familiarizarse con las funciones y capacidades que se han marcado como obsoletas en Experience Manager as a Cloud Service y ver cuál es el impacto para su implementación de AEM.

## Planifique una revisión de la instalación de AEM {#review-planning}

Una vez que se haya acostumbrado a los cambios introducidos con AEM as a Cloud Service, es hora de empezar a planificar una revisión de la instalación existente, para medir el nivel de cambios necesarios para moverla a la nube.

La siguiente figura muestra los pasos clave involucrados durante la fase de revisión:

![imagen](/help/journey-migration/assets/planning-phaseimg1.png)

A continuación, analizaremos en detalle cada uno de estos pasos.

### Evaluación de la preparación de Cloud Service {#assess-cloud-readiness}

El primer paso es evaluar su preparación para pasar de la versión de AEM existente al Cloud Service y determinar las áreas que requerirán refactorización para ser compatibles con AEM as a Cloud Service.

Deberá realizar una evaluación completa del código fuente de AEM actual en relación con los cambios importantes y las funciones obsoletas para determinar el nivel de esfuerzo esperado en el recorrido de transición.

El número de conclusiones influirá directamente en los plazos y el éxito general del proyecto. Por lo tanto, se recomienda descubrir en la medida de lo posible la planificación del envío o iniciar las conversaciones necesarias para rediseñar cualquier personalización necesaria para ajustarse a AEM práctica recomendada as a Cloud Service.

**Analizador de prácticas recomendadas**

Puede acelerar la evaluación ejecutando el Analizador de prácticas recomendadas en su versión AEM actual. Conocer bien cómo funciona es clave para acelerar la planificación de la evaluación.

Puede leer cómo funciona consultando al [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) documentación.

**Crear un informe de evaluación de preparación para la nube**

El siguiente paso es crear un informe basado en todos los conocimientos adquiridos hasta ahora. Para ello, puede generar informes de Best Practices Analyzer desde las instancias de fase y producción. [a continuación, cárguelos en Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) para un informe digestivo de los elementos procesables.

Un informe típico debe contener estas entradas:

* Documentación que detalla el conjunto de funciones de su instalación de AEM particular
* Detalles sobre las configuraciones y el código personalizados AEM
* Configuraciones de Dispatcher de producción
* Configuraciones de CDN (si hay alguna)

**Socializar el informe**

Una vez completados los informes de Best Practices Analyzer, compártalos con los equipos relevantes para confirmar sus conclusiones y planificar los pasos siguientes. Según las preferencias, también puede distribuir una versión impresa del informe utilizando [Vista previa de impresión](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Revisión de la planificación de recursos {#review-resource-planning}

Una vez que haya calculado el nivel de esfuerzo necesario para pasar a Cloud Service, debe identificar los recursos, crear un equipo y asignar funciones y responsabilidades para el proceso de transición.

### Establecimiento de los KPI {#establish-kpis}

Si no ha establecido los indicadores de rendimiento clave (KPI) anteriormente, se recomienda establecer los KPI para la implementación de AEM para ayudar a su equipo a centrarse en lo que más importa.

Consulte [Desarrollo de KPI](https://guided.adobe.com/welcome/aem/part6.html) para aprender a elegir los KPI adecuados para sus objetivos empresariales.

## Siguientes pasos {#what-is-next}

Una vez que entienda el alcance de los cambios necesarios para pasar a AEM as a Cloud Service, es hora de [Preparar el código y la nube de contenido](/help/journey-migration/implementation.md) antes de realizar la migración.

## Recursos adicionales {#additional-resources}

* [Introducción a Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) : Una guía completa sobre cómo utilizar Cloud Acceleration Manager para acelerar su paso a la nube
* [AEM as a Cloud Service: Introducción, arquitectura y pensamiento diferentes](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM de una página principal del Cloud Service](/help/overview/home.md) : para obtener una descripción general de la documentación as a Cloud Service del Experience Manager, comience aquí.
* [Información general as a Cloud Service de AEM](/help/overview/home.md) : Esta guía proporciona información general sobre Experience Manager as a Cloud Service, incluida una introducción, terminología y arquitectura.
* [Recorrido de incorporación](/help/journey-onboarding/overview.md)- Esta guía proporciona un resumen de cómo empezar a trabajar con Experience Manager as a Cloud Service, incluida cómo obtener acceso y configurar su equipo
