---
title: Fase de preparación
description: AEM Obtenga información acerca de los pasos que debe seguir para asegurarse de que la instalación de la está lista para moverse a la nube.
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: a9aa82c8258e6a5f43680069c65518093c0baf8d
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 6%

---

# Fase de preparación {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Planificación de la transición"
>abstract="Antes de comenzar el recorrido de la transición a Cloud Service, familiarícese con AEM as a Cloud Service. Revise los cambios importantes realizados en él y las funcionalidades reemplazadas u obsoletas."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=es" text="Analizador de prácticas recomendadas"

AEM En esta fase del Recorrido AEM as a Cloud Service de migración as a Cloud Service de la, se familiarizará con la. Puede revisar los cambios más importantes introducidos y comprender lo que se necesita para planificar una migración correcta a la nube.

## La historia hasta ahora {#story-so-far}

El documento anterior, [AEM Introducción a la migración a la as a Cloud Service](/help/journey-migration/getting-started.md)AEM , describe una lista de las fases a las que debe someterse para poder migrar a las fases as a Cloud Service de la. También se describen las ventajas de realizar la migración.

## Objetivo {#objective}

AEM Este documento le ayuda a comprender qué factores debe tener en cuenta para poder asegurarse de que la instalación de la está lista para moverse a la nube:

* Obtenga información acerca de cambios importantes y funciones obsoletas
* AEM Obtenga información sobre cómo planificar la migración a la as a Cloud Service de la

## AEM Revisar los cambios más importantes en la arquitectura as a Cloud Service de la aplicación {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service AEM trae muchas nuevas características y posibilidades para la gestión de sus Proyectos de la.

AEM AEM Junto con estas mejoras, se han introducido varias diferencias entre las instalaciones on-premise de y Adobe Managed Services, en comparación con las instalaciones on-premise de as a Cloud Service.

AEM La lista de los elementos de la siguiente tabla es el subconjunto de los cambios más relevantes para una migración a as a Cloud Service. Puede consultar la lista completa de cambios importantes [aquí](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>¿Qué ha cambiado?</th>
    <th>Referencia</th>
    <th>Consideraciones clave</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separar filtros mutables e inmutables en paquetes correspondientes</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=es">AEM Cambios importantes as a Cloud Service</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM AEM Estructura del proyecto de para el as a Cloud Service</a></td>
    <td>AEM Un paquete único que se puede implementar en el as a Cloud Service puede tener subpaquetes, principalmente para contener contenido mutable e inmutable separado en sus propios paquetes.</td>
  </tr>
  <tr>
    <td>Inicio de repo</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentación de Apache Sling RepoInit</a></td>
    <td>Los scripts de Repoinit son la práctica recomendada para crear estructuras de nodos iniciales, usuarios, grupos o usuarios de servicios. Dado que estos scripts se pueden dirigir mediante el modo de ejecución y se pueden administrar mediante la implementación de paquetes de código, proporcionan mucha flexibilidad para lograr tareas de inicialización del repositorio.</td>
  </tr>
  <tr>
    <td>No se permiten los modos de ejecución personalizados</td>
    <td></td>
    <td>AEM Solo se admiten los modos de ejecución predeterminados con as a Cloud Service de.<br>Cuando se añaden entornos de desarrollo adicionales, todos ellos se vinculan al modo de ejecución "dev".</td>
  </tr>
  <tr>
    <td>La ejecución de la canalización de Cloud Manager es la única manera de implementar</td>
    <td></td>
    <td>AEM En as a Cloud Service, no se permite el acceso a /system/console, por lo que todas las configuraciones de OSGi deben formar parte del código y deben implementarse como código.<br>Las configuraciones de OSGi están disponibles en modo de solo lectura para su visualización a través de Developer Console mediante Cloud Manager</td>
  </tr>
  <tr>
    <td>Los agentes de replicación se sustituyen por Sling Content Distribution</td>
    <td></td>
    <td>El concepto de agente de replicación se reemplaza por Usar distribución de contenido. Si hay personalizaciones que utilizan agentes de replicación, deben volver a diseñarse.<br>No se admite la replicación inversa</td>
  </tr>
  <tr>
    <td>CRX/DE y Administrador de paquetes</td>
    <td></td>
    <td>CRX/DE solo se permite en el entorno de desarrollo.<br>El Administrador de paquetes es accesible en todas las instancias de autor, pero los paquetes que se van a implementar solo deben contener contenido mutable ( por ejemplo: /content o /conf)</td>
  </tr>
  <tr>
    <td>Creación de una CDN y Obtención de su propia CDN</td>
    <td></td>
    <td>AEM El as a Cloud Service incluye la CDN para todos los entornos, que está optimizada para la mayoría de los casos de uso.<br>Si desea configurar su propia CDN, debe enviar una solicitud al Soporte de Adobe para que se apruebe.<br>AEM Si se aprueba, la CDN apunta a Fastly y no a instancias de en ningún entorno.</td>
  </tr>
  <tr>
    <td>Trabajos de larga duración</td>
    <td></td>
    <td>AEM Evite los trabajos de larga duración, como los Planificadores de Sling o los trabajos de Cron, ya que las instancias de que se ejecutan en los contenedores pueden ir y venir en cualquier momento.<br>Reconsidere estas funcionalidades para poder descargarlas en Adobe Developer.</td>
  </tr>
  <tr>
    <td>Cambiar a operaciones asincrónicas</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">Configuración de operaciones asincrónicas</a></td>
    <td>Para mejorar el rendimiento general de los entornos, ciertas operaciones se ejecutan en modo asincrónico. Los trabajos asincrónicos se ponen en cola y se ejecutan cuando hay recursos del sistema disponibles.</td>
  </tr>
  <tr>
    <td>Estrategias de autenticación e integración basadas en tokens</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">Generación de tokens de acceso para las API del lado del servidor</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Tutorial de autenticación basada en tokens</a></td>
    <td>AEM AEM Es habitual que los sistemas externos a los que se realiza la operación de la conexión estén intentando realizar operaciones HTTP dentro de los sistemas de la conexión de red<br>AEM El enfoque recomendado es implementar las estrategias descritas aquí, en lugar de depender de la creación de nombres de usuario locales con contraseñas en el.</td>
  </tr>
  <tr>
    <td>E/S de archivo/Uso de disco</td>
    <td></td>
    <td>No hay garantía de cuánto espacio en disco se asigna y las instancias en contenedores van y vienen. AEM Por lo tanto, no es aconsejable utilizar las operaciones de E/S de archivo para escribir o leer desde el disco conectado a la instancia de.</td>
  </tr>
  <tr>
    <td>Flujo de trabajo de recursos de actualización DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Servicio de asset compute</a></td>
    <td>Los pasos de procesamiento de medios que forman parte del flujo de trabajo de recursos de actualización de DAM ahora se sustituyen por el servicio de Asset compute</td>
  </tr>
  <tr>
    <td>AEM Métodos de carga de recursos y pasos de proceso de flujo de trabajo admitidos en el as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">Cargar comparaciones de API y pasos de proceso de WF admitidos</a></td>
    <td>AEM En as a Cloud Service, durante la carga o descarga de un recurso, el recurso se transmite directamente dentro o fuera del almacenamiento binario. <br>No todos los pasos del proceso de flujo de trabajo son compatibles con AEMaaCS.</td>
  </tr>
  <tr>
    <td>Lanzadores de flujo de trabajo</td>
    <td></td>
    <td>Elimine del código cualquier lanzador de flujos de trabajo que active el flujo de trabajo de recursos de actualización de DAM predeterminado o personalizado. <br>AEM El servicio de procesamiento de recursos procesará todos los recursos cargados en el recurso as a Cloud Service de la. Para ver los pasos personalizados, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> Flujos de trabajo de posprocesamiento</a> sobre cómo configurar flujos de trabajo posteriores al procesamiento.</td>
  </tr>
  <tr>
    <td>Pasos de representación personalizada</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en">Perfiles de procesamiento</a></td>
    <td>Cualquier generación de representación personalizada, conversión de imágenes o codificaciones de vídeo debe descargarse al servicio de procesamiento de recursos creando los perfiles de procesamiento correspondientes.</td>
  </tr>
  <tr>
    <td>Búsqueda de contenido e indexación</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en">Búsqueda de contenido y cambios de indexación</a></td>
    <td>Hay cambios considerables en el procesamiento subyacente de los índices y en el momento en que comienza a funcionar.<br>Comprenda y refactorice completamente los índices Oak antes de administrarlos en el código que implementa.</td>
  </tr>
  <tr>
    <td>No todas las tareas de mantenimiento se pueden configurar</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html?lang=en">AEM Tareas de mantenimiento as a Cloud Service</a></td>
    <td>AEM Solo se pueden configurar determinadas tareas de mantenimiento con as a Cloud Service de la.</td>
  </tr>
  <tr>
    <td>Cambios en el repositorio de Publish</td>
    <td></td>
    <td>No se permiten cambios directos en el repositorio de Publish, excepto los cambios en /home. Siempre se recomienda distribuir todos los cambios realizados en el autor. Todos los cambios de código y configuración deben implementarse a través de la canalización correspondiente de Cloud Manager.</td>
  </tr>
  <tr>
    <td>Configuraciones y almacenamiento en caché de Dispatcher</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en">Dispatcher en la nube</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html?lang=en#other-content">Administración de caché<br></td>
    <td>Las configuraciones de Dispatcher deben seguir una estructura específica.<br>Las configuraciones deben administrarse como parte del código e implementarse mediante la canalización de Cloud Manager.</td>
  </tr>
  <tr>
    <td>Copia de seguridad y restauración</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en">AEM Copia de seguridad y restauración as a Cloud Service</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Cambios en la autenticación</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=es">Compatibilidad con IMS para AEM as a Cloud Service</td>
    <td>Si anteriormente utilizaba la integración con SAML 2.0 tanto en creación como en publicación antes de pasar a Cloud Service AEM, el cambio principal es que Autor as a Cloud Service solo se integra con Adobe IMS. AEM Sin embargo, el nivel de publicación as a Cloud Service de la todavía puede utilizar SAML u otras integraciones de autenticación. AEM El as a Cloud Service ofrece compatibilidad con la autenticación IMS solo para usuarios creadores, administradores y desarrolladores. La autenticación IMS no ofrece compatibilidad con usuarios finales externos de sitios de clientes como visitantes del sitio.</td>
  </tr>
</tbody>
</table>

## Funciones en desuso {#deprecated-features}

Adobe evalúa constantemente las capacidades de los productos para renovar o sustituir las funciones más antiguas con alternativas modernas que mejoren el valor general del cliente, siempre teniendo en cuenta la compatibilidad con versiones anteriores.

El Adobe recomienda consultar [Funciones obsoletas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html#deprecated-features) para familiarizarse con las funciones y capacidades marcadas como obsoletas en Experience Manager as a Cloud Service. AEM Vea cuál es el impacto para su implementación de la.

## AEM Planifique para una revisión de su instalación de la {#review-planning}

AEM Una vez que se haya acostumbrado a los cambios introducidos con el as a Cloud Service, es hora de empezar a planificar una revisión de la instalación existente. Al hacerlo, puede medir el nivel de cambios necesarios para moverlo a la nube.

La siguiente figura muestra los pasos clave involucrados durante la fase de revisión:

![imagen](/help/journey-migration/assets/planning-phaseimg1.png)

A continuación, explora en detalle qué significa cada uno de estos pasos.

### Evaluación de la preparación de Cloud Service {#assess-cloud-readiness}

AEM El primer paso es evaluar la preparación para pasar de la versión de su existente a la de Cloud Service AEM y determinar las áreas que requieren refactorización para que sean compatibles con las versiones as a Cloud Service de la.

AEM Realice una evaluación completa del código fuente actual de la en relación con los cambios notables y las funciones en desuso para determinar el nivel de esfuerzo esperado en el recorrido de transición.

El número de conclusiones puede influir directamente en los plazos y en el éxito general del proyecto. Por lo tanto, Adobe recomienda que descubra lo más posible para poder planificar la entrega. AEM O bien, inicie las conversaciones para poder rediseñar las personalizaciones necesarias para que estén en consonancia con las prácticas recomendadas as a Cloud Service de la práctica.

**Analizador de prácticas recomendadas**

AEM Puede acelerar la evaluación ejecutando el Analizador de prácticas recomendadas con la versión actual de la versión de la. Tener una buena comprensión de cómo funciona es clave para acelerar la planificación de la evaluación.

Puede leer más sobre cómo funciona consultando el [Analizador de prácticas recomendadas](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) documentación.

**Crear un informe de evaluación de preparación para la nube**

El siguiente paso es crear un informe basado en todos los conocimientos adquiridos hasta el momento. El informe se crea generando informes del Analizador de prácticas recomendadas a partir de las instancias de Ensayo y Producción. [a continuación, cárguelos en Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) para un informe digerible de elementos procesables.

Un informe típico debe contener estas entradas:

* AEM Documentación que detalla el conjunto de funciones de la instalación de su particular
* AEM Detalles sobre las configuraciones y el código personalizados de la
* Configuraciones de Dispatcher de producción
* Configuraciones de CDN (si las hay)

**Socialización del informe**

Una vez completados los informes del Analizador de prácticas recomendadas, compártalos con los equipos relevantes para que pueda confirmar las conclusiones y planificar los pasos siguientes. Según sus preferencias, también puede distribuir una versión impresa del informe utilizando [Vista preliminar](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Revisión de la planificación de recursos {#review-resource-planning}

Una vez que haya calculado el nivel de esfuerzo necesario para pasar a Cloud Service, debe identificar los recursos, crear un equipo y asignar funciones y responsabilidades para el proceso de transición.

### Establecimiento de los KPI {#establish-kpis}

AEM Si no ha establecido los Indicadores clave de rendimiento (KPI) anteriormente, se recomienda establecer los KPI para la implementación de la aplicación de la para ayudar a su equipo a centrarse en lo que más importa.

Consulte [Desarrollo de KPI](https://experienceleague.adobe.com/welcome/aem/part6.html) para que pueda aprender a elegir los KPI adecuados para sus objetivos empresariales.

## Siguientes pasos {#what-is-next}

AEM Una vez que haya comprendido el ámbito de los cambios necesarios para pasar a la fase as a Cloud Service, es hora de hacer lo siguiente: [Preparar el código y la nube de contenido](/help/journey-migration/implementation.md) antes de realizar la migración.

## Recursos adicionales {#additional-resources}

* [Introducción a Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) : Una guía completa sobre cómo utilizar Cloud Acceleration Manager para acelerar el paso a la nube.
* [AEM as a Cloud Service: Introducción, arquitectura y pensamiento diferente](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM Página de inicio de Cloud Service de](/help/overview/home.md) : para obtener una descripción general de la documentación as a Cloud Service del Experience Manager, comience aquí.
* [AEM Resumen as a Cloud Service de](/help/overview/home.md) : Esta guía proporciona información general sobre Experience Manager as a Cloud Service, incluida una introducción, terminología y arquitectura.
* [Recorrido de incorporación](/help/journey-onboarding/overview.md): Esta guía proporciona un resumen de cómo empezar a usar Experience Manager as a Cloud Service, incluido cómo obtener acceso y configurar su equipo.
