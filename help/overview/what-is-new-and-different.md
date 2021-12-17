---
title: Novedades y diferencias - Adobe Experience Manager as a Cloud Service
description: 'Novedades y diferencias: Adobe Experience Manager (AEM) as a Cloud Service.'
exl-id: d1ce126e-960c-4367-b741-af709dd81010
source-git-commit: cf688addd731d7a7107a648b40fbbdd149fef503
workflow-type: tm+mt
source-wordcount: '1906'
ht-degree: 10%

---

# Novedades y diferencias {#what-is-new-and-what-is-different}

Durante muchos años AEM ha estado disponible tanto:

* Local

* as a Managed Service

Hay diferencias intrínsecas entre estos enfoques anteriores y AEM as a Cloud Service:

* [Arquitectura](#architecture)
* [Actualizaciones](#upgrades)
* [Cloud Manager](#cloud-manager)
* [Incorporación](#onboarding)
* [Desarrollo de](#developing)
* [Operaciones y rendimiento](#operations-and-performance)
* [Administración de identidades](#identity-management)
* [Interfaz de usuario de creación](#authoring-user-interface)
* [AEM Sites](#aem-sites)
* [AEM Assets](#aem-assets)

>[!NOTE]
>
>Estas descripciones generales no son exhaustivas, pero tienen por objeto proporcionar una introducción.

>[!NOTE]
>
>Para obtener más información sobre las versiones On-Premise y Managed Service, consulte la documentación configurada para [AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es).

## Arquitectura {#architecture}

>[!NOTE]
>
>Para obtener más información, consulte [Arquitectura](/help/overview/architecture.md).

AEM as a Cloud Service ahora tiene:

* Arquitectura dinámica con un número variable de imágenes de AEM.

![Arquitectura dinámica](assets/introduction-03.png "Arquitectura dinámica")

Esta arquitectura:

* Se adapta en función del tráfico *real* y la actividad *real*.

* Tiene instancias individuales que solo se ejecutan cuando es necesario.

* Utiliza aplicaciones modulares.

* Tiene un clúster de creación predeterminado, lo que elimina el tiempo de inactividad durante las tareas de mantenimiento.

Esto permite adaptarse automáticamente a distintos patrones de uso:

![Adaptación automática para patrones de uso variables](assets/introduction-04.png "Adaptación automática para patrones de uso variables")


## Actualizaciones AEM {#aem-updates}

>[!NOTE]
>Para obtener más información, consulte [Actualizaciones en la versión AEM](/help/implementing/deploying/aem-version-updates.md).

AEM as a Cloud Service ahora utiliza la integración continua y la entrega continua (CI/CD) para garantizar que sus proyectos se encuentren en la versión de AEM más actual. Esto significa que las instancias Producción y Fase se actualizan a la última versión de AEM sin interrupciones del servicio para los usuarios.

>[!NOTE]
> Si la actualización al entorno de producción falla, Cloud Manager invertirá automáticamente el entorno de ensayo. Esto se realiza automáticamente para garantizar que, después de completarse una actualización, tanto los entornos de fase como de producción estén en la misma versión AEM.

AEM actualizaciones de versión son de dos tipos:

* **AEM actualizaciones push**

   * Se puede publicar diariamente.
   * Principalmente mantenimiento, incluidas las últimas correcciones de errores y actualizaciones de seguridad.

      Como los cambios se aplican regularmente, el impacto es incremental, lo que reduce el impacto en su servicio.

* **Nuevas actualizaciones de funciones**

   * Publicado mediante un calendario mensual predecible.

## Cloud Manager {#cloud-manager}

Adobe Cloud Manager es una parte integral del enfoque de actualización continua de AEM as a Cloud Service, ya que controla todas las actualizaciones de las instancias. Esto es obligatorio.

Las actualizaciones se pueden activar mediante Adobe cuando hay una nueva versión del servicio en la nube disponible. Como alternativa, puede almacenar en déclencheur las actualizaciones de la aplicación mediante las canalizaciones que Cloud Manager proporciona.

Cloud Manager es:

* se utiliza para administrar AEM programas y entornos,

* un componente esencial de AEM as a Cloud Service; cada nuevo inquilino se aprovisiona primero para el acceso a Cloud Manager,

* el punto de entrada único para su personal de operaciones y desarrollo.

En concreto, el número y el tipo de programas de AEM que se pueden crear desde Cloud Manager se derivan de:

* del contrato de licencia de cliente,

* de agentes impulsados por el interior cuando AEM as a Cloud Service se utiliza para la habilitación o la formación,

* a partir de procesos impulsados por externos como ensayos iniciados desde Adobe.com.

Cloud Manager ha evolucionado como un portal de autoservicio donde se pueden crear y configurar los componentes principales de AEM as a Cloud Service:

* Creación y administración de nuevos programas. Consulte [Explicación de programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) para obtener más información.

* Creación y administración de entornos AEM dentro de estos programas. Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md) para obtener más información.

* Creación y administración de canalizaciones para implementar el código de cliente y la configuración relacionada en un entorno específico. Consulte [Configuración de la canalización de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información.

* Recibir notificaciones de eventos de ciclo vital importantes para estos componentes (por ejemplo, actualizaciones de productos).

Cloud Manager crea entornos en centros de datos en muchas regiones geográficas, lo que proporciona una cobertura global. Los puntos de presencia de CDN (PoPs) garantizan una entrega de contenido con baja latencia para clientes ubicados en todo el mundo.


## Incorporación {#onboarding}

>[!NOTE]
>
>Para obtener más información, consulte [Incorporación](/help/onboarding/home.md).

El inicio y la administración de un proyecto de AEM es sencillo al usar AEM as a Cloud Service como Adobe es responsable de muchos aspectos:

* Las imágenes de AEM de línea de base están optimizadas para casos de uso específicos.

* Muchas de las tareas de configuración manual se han vuelto redundantes.

También es significativamente diferente, ya que ahora lo hay:

* Una fase de evaluación para garantizar que se hayan cumplido todos los requisitos previos; incluido, por ejemplo:

   * Requisitos legales

   * Acuerdos contractuales

   * Requisitos técnicos para cualquier contenido existente o código personalizado por el cliente

* Requisitos de implementación:

   * Actualizaciones de código; cualquier aplicación de cliente desarrollada para una versión anterior de AEM deberá revisarse y posiblemente actualizarse.

   * Migración de contenido

## Desarrollo de {#developing}

>[!NOTE]
>
>Para obtener más información, comience con [Directrices de desarrollo](/help/implementing/developing/introduction/development-guidelines.md) y [Desarrollo: Tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

La nueva arquitectura que admite AEM as a Cloud Service implica algunos cambios clave en la experiencia general del desarrollador. Uno de los principales objetivos de AEM as a Cloud Service es permitir que los clientes con experiencia (que han utilizado AEM local o en el contexto de los servicios administrados de Adobe) migren a AEM as a Cloud Service lo antes posible, sin tener que reescribir la mayor parte de su código personalizado. Sin embargo, es posible que todavía se necesiten algunos ajustes.

### Desarrollo en la nube {#aem-as-a-cloud-service-developing-cloud-development}

Para que las aplicaciones de AEM existentes se ejecuten en AEM as a Cloud Service, se esperan los siguientes pasos:

* El código y la configuración de la aplicación deben almacenarse en el repositorio de código Git del programa Cloud Manager asociado.
* El código y la configuración de la aplicación deben ser compatibles con la última versión de la imagen de AEM de línea de base (que puede estar cambiando diariamente).
   * La aplicación del cliente debe crearse e implementarse mediante la canalización de Cloud Manager asociada al entorno de Cloud Manager.
* La aplicación del cliente debe pasar todas las puertas de calidad, seguridad y rendimiento del código que se aplican en la canalización.
* Las imágenes creadas para la aplicación del cliente deben implementarse mediante la canalización de Cloud Manager.

Este proceso se conoce comúnmente como desarrollo con prioridad en la nube. Dado que se espera que la duración de extremo a extremo tome minutos (de 20 a 50 según la complejidad de la aplicación), es necesario adoptar metodologías de desarrollo rápido antes de que se intenten en la nube los cambios de código y configuración pendientes.

La consola web, en la que se administran los paquetes OSGI y su configuración asociada, y que anteriormente formaba parte de QuickStart de AEM, ya no es directamente accesible para los usuarios de un entorno as a Cloud Service AEM. Se puede acceder a esta interfaz en modo de solo lectura mediante una nueva consola para desarrolladores. Con esta consola, los desarrolladores pueden seleccionar e iniciar sesión directamente en cualquier nodo concreto de un autor o servicio de publicación y, a continuación, acceder a las áreas bloqueadas de forma predeterminada.

>[!NOTE]
>
>Consulte también [Configuración de OSGi](/help/implementing/deploying/overview.md#osgi-configuration)

Otro requisito común para los desarrolladores es el acceso rápido a los archivos de registro de los distintos entornos. Con AEM as a Cloud Service, los archivos de registro de los diferentes nodos de los nodos de autor y publicación están disponibles mediante Cloud Manager, ya sea en forma de archivos que se pueden descargar o a través de API.

Debido a la clara separación de código y contenido, los desarrolladores pueden utilizar un proceso particular para actualizar contenido como parte de una implementación. Los casos de uso habituales del contenido mutable son:

* Estándar *default* contenido que forma parte del proyecto del cliente (por ejemplo, carpetas, plantillas, flujos de trabajo, etc.)

* Definiciones de índices de búsqueda

* ACL y permisos

* Usuarios y grupos de usuarios de servicios

### Desarrollo local {#aem-as-a-cloud-service-developing-local-development}

A fin de apoyar las iteraciones y el desarrollo rápidos, también es posible desarrollar aplicaciones AEM fuera del contexto as a Cloud Service AEM. Con este fin, se ponen a disposición de los desarrolladores los siguientes artefactos:

* Inicio rápido as a Cloud Service AEM: a `.jar` instalador independiente basado en la última base de código de AEM, con la misma superficie funcional y API.

* El SDK de Dispatcher as a Cloud Service AEM: un proceso basado en imágenes para probar y validar configuraciones de Dispatcher localmente

>[!NOTE]
>
>Debe tenerse en cuenta que Cloud QuickStart no permite todas las funcionalidades de AEM Sites y AEM Assets. Consiste en un entorno de creación sencillo en el que la mayoría de las extensiones se pueden desarrollar y probar.

## Operaciones y rendimiento {#operations-and-performance}

>[!NOTE]
>
>Para obtener más información, comience con [Copia de seguridad](/help/operations/backup.md), [Indexación](/help/operations/indexing.md) y [Otras tareas de mantenimiento](/help/operations/maintenance.md).

Con AEM as a Cloud Service, esas operaciones se automatizan para que ya no sea necesaria ninguna interrupción del servicio.

En estas áreas:

* Se han automatizado muchas tareas.

* Las topologías están optimizadas para lograr la máxima resiliencia y eficiencia; por ejemplo, la replicación binaria es la predeterminada.

* Las tareas de carga pesada, como colas, trabajos y tareas de procesamiento masivo, se han movido fuera de la instancia de AEM principal para que se gestionen mediante microservicios compartidos y dedicados.

Las operaciones para AEM as a Cloud Service también están soportadas por una nueva infraestructura de monitoreo, reporting y alertas. Esto permite que los SRE de Adobe (ingenieros de confiabilidad del sitio) mantengan el servicio de forma proactiva en buen estado. Los diferentes elementos de la arquitectura están equipados con una variedad de controles sanitarios. Si, por alguna razón, un nodo particular de la arquitectura se considera no saludable, entonces se elimina del servicio y se reemplaza silenciosamente por uno nuevo y saludable.

## Administración de identidades {#identity-management}

>[!NOTE]
>
>Para obtener más información, consulte [Seguridad: compatibilidad con IMS](/help/security/ims-support.md).

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los ID de Adobe para acceder al nivel de creación.

Esto requiere el uso de la variable [Consola de administración de Adobe](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. Las cuentas de usuario permiten a los usuarios acceder a los productos y servicios de Adobe, ya que la información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS) para compartirse en todos los servicios de nube. Una vez asignado el acceso a AEM, se puede hacer referencia a las cuentas de usuario en AEM as a Cloud Service (como antes); por ejemplo, para definir funciones y permisos desde las interfaces de usuario de seguridad de AEM.

Esto combina las ventajas de:

* Uso del sistema Identity Management de Adobe (IMS) para proporcionar el inicio de sesión único en todas las aplicaciones de nube de Adobe.

* Las preferencias de usuario permanecen locales en cada instancia concreta de AEM as a Cloud Service.

## Interfaz de usuario de creación {#authoring-user-interface}

>[!NOTE]
>
>Para obtener más información, la variable [Gestión básica](/help/sites-cloud/authoring/getting-started/basic-handling.md) es un buen punto de partida.

Los principios básicos de la interfaz de usuario (IU) de creación, tanto para Sites como para Assets, resultarán muy familiares para cualquiera que haya utilizado AEM en el pasado.

La principal diferencia es que la interfaz de usuario solo es táctil; la IU clásica ya no está disponible. De lo contrario, los conceptos básicos permanecen inalterados, con sólo pequeños cambios aparentes.

## AEM Sites {#aem-sites}

Adobe Experience Manager Sites as a Cloud Service le permite ofrecer a sus clientes experiencias personalizadas basadas en contenido, combinando la potencia del sistema de gestión de contenido AEM con la administración de recursos digitales de AEM.

Para obtener más información, consulte la descripción general de [Cambios en Sitios](/help/sites-cloud/sites-cloud-changes.md).

## AEM Assets {#aem-assets}

Adobe Experience Manager Assets as a Cloud Service ofrece una solución PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de activos digitales y Dynamic Media con rapidez e impacto, sino que también utilicen funciones inteligentes de próxima generación, como AI/ML, desde un sistema que siempre esté actualizado, siempre disponible y siempre aprendiendo.

La oferta de recursos incluye el procesamiento de recursos de próxima generación en la nube y la ingesta y búsqueda de recursos de alto rendimiento.

Para obtener más información, consulte [información general e introducción a Assets as a Cloud Service](/help/assets/overview.md).

## Cómo conocer Adobe Experience Manager as a Cloud Service {#getting-to-know-aem-as-cloud-service}

Para obtener más información, consulte:

* [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
* La [arquitectura](/help/overview/architecture.md) de Adobe Experience Manager as a Cloud Service
* [Cambios importantes en AEM as a Cloud Service (Notas de la versión)](/help/release-notes/aem-cloud-changes.md)
* [Cambios importantes en AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
* [Cambios importantes en AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)
* [Presentación de AEM Assets as a Cloud Service](/help/assets/overview.md)
* [Tutoriales de Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=es)

>[!TIP]
>
>Una vez que tenga una descripción general de AEM as a Cloud Service, puede agregarla rápidamente revisando la [Recorrido de incorporación.](/help/journey-onboarding/home.md)
>
>¿Ya está incorporado o listo para sumergirse en las funciones de AEM de prueba? Instale el [Complemento Demostraciones de Referencia de AEM](/help/journey-sites/demos-add-on/overview.md) para explorar AEM potentes funciones con ejemplos enriquecidos.